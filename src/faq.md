# Frequently Asked Questions

## Foundations

### What does "transformer" mean? Why that name?

The 2017 Google paper "Attention Is All You Need" introduced the architecture. It's called a "Transformer" because it **transforms** one sequence of representations into another through **self-attention** — a mechanism where every token looks at every other token to decide what's important.

Before transformers, we had RNNs/LSTMs that processed tokens **one at a time**, sequentially. The transformer's breakthrough was processing **all tokens simultaneously**, making it massively parallelizable on GPUs while capturing long-range dependencies far better.

### Why were encoder-only transformers (like BERT) needed?

The original transformer had both an encoder and decoder — designed for translation (encode English → decode to French). But researchers realized **not every task needs text generation**. Many tasks are about understanding:

- Sentiment classification ("Is this review positive?")
- Semantic similarity ("Are these sentences related?")
- Entity recognition ("What does 'he' refer to?")
- Document retrieval ("Find relevant documents")

For these, you only need the **encoder** — the part that reads the full input bidirectionally and produces a rich representation. The decoder (generation) is unnecessary overhead. So BERT (2018) threw away the decoder and trained just the encoder, producing models perfect for classification, similarity, search, and embeddings.

### What are the three transformer families?

| Architecture | What It Sees | Good At | Examples |
|---|---|---|---|
| **Encoder-only** | All tokens (bidirectional) | Understanding, classification, embeddings | BERT, RoBERTa, BGE-M3 |
| **Decoder-only** | Past tokens only (causal) | Text generation | GPT, Llama, Shoonya |
| **Encoder-Decoder** | Both | Translation, summarization | T5, BART, original Transformer |

---

## Embeddings

### Is an embedding model essentially an LLM / a neural network with transformers, or just a neural network?

An embedding model is a **neural network** — but not necessarily a full LLM. It's a spectrum:

- **Simplest**: Word2Vec (2013) — a shallow 2-layer network. No transformers at all.
- **Middle**: BERT, BGE-M3 — transformer-based but **not generative**. Can't produce text. Trained to output dense vectors.
- **Current SOTA**: Take a full LLM (Mistral-7B, Qwen3-8B), **strip the generation head**, flip to bidirectional attention, add pooling, fine-tune with contrastive loss. These are literally LLMs repurposed as embedding models.

So modern SOTA embedding models **are** transformers, and the best ones **are** LLMs with the generation head removed. But conceptually, an embedding model is any neural network that produces a meaningful vector representation.

### What's the difference between an LLM and an embedding model?

| | LLM | Embedding Model |
|---|---|---|
| **Output** | Next token (probability distribution over vocabulary) | Single fixed-size vector (e.g., 4096 floats) |
| **Use** | Generate text | Compare similarity between inputs |
| **Attention** | Causal (sees only past tokens) | Bidirectional (sees full input) |
| **Training** | Next-token prediction | Contrastive learning (similar pairs close, dissimilar far) |

### Should we build our own embedding model?

**Yes — but scope it narrowly.** Don't try to top the general-purpose MTEB leaderboard. Build a **graph-aware, domain-specialized** model that:

1. **Understands Cypher query semantics** — no existing model does this
2. **Captures graph topology** (node relationships, edge types) alongside text
3. **Is optimized for Samyama's HNSW index**
4. **Covers our verticals** (biomedical, clinical trials, cricket, industrial)

Use an existing open model (Qwen3-Embedding-8B, Apache 2.0) as a baseline for general text, and build the graph-aware layer on top. This gives us unique value without reinventing the wheel.

### What is the path to creating an embedding model?

The modern recipe is **two-stage fine-tuning** of a decoder-only LLM:

1. **Pick a backbone** — Shoonya or an open base (Qwen3-8B, Llama-3.1-8B)
2. **Remove the causal attention mask** → bidirectional attention
3. **Add latent attention pooling** (NV-Embed-v2's innovation)
4. **Stage 1**: Contrastive pre-training on ~50-150M synthetic pairs using MNRL
5. **Stage 2**: Fine-tune on curated domain-specific data with hard negatives
6. **Train with Matryoshka Representation Learning** for flexible dimensionality (128-4096 dims)
7. Evaluate on MTEB + domain-specific benchmarks

### What are the biggest unsolved gaps in embedding models?

| Gap | Why It Matters |
|-----|---------------|
| **Graph structure** | No model captures node-edge-node relationships or typed edges |
| **Cypher understanding** | Zero research on embedding Cypher queries into semantic space |
| **Numeracy** | Models can't encode numbers accurately (critical for clinical trials, cricket stats) |
| **Negation** | "Did NOT respond" ≈ "responded" in embedding space |
| **Compositional queries** | Multi-hop reasoning collapses in single-vector space |
| **Retrieval limits** | Mathematically proven fundamental recall bounds tied to dimensionality |

### Is there a need for a unique embedding model for graph databases?

**Yes — this is the biggest opportunity.** No existing embedding model combines text understanding + graph structure + Cypher query semantics. Specifically:

- **Current approach**: Embed node text properties independently → lose all relational structure
- **Neo4j**: Relies on external embedding APIs — no native embedding model
- **No model understands Cypher**: An embedding that maps natural language questions AND Cypher patterns into the same space would be a first

A Samyama-native embedding model with a Shoonya backbone + GraphSAGE for structural encoding would give us a genuine competitive moat: a database that **natively generates embeddings understanding both content and structure**.

### What is the SOTA in embedding models (March 2026)?

The top models on MTEB:

| Rank | Model | Params | Open? | Key Innovation |
|------|-------|--------|-------|----------------|
| 1 | Gemini Embedding 001 | ? | No | MRL, proprietary distillation |
| 2 | NV-Embed-v2 | 7B | Yes (CC-BY-NC) | Latent attention pooling |
| 3 | Qwen3-Embedding-8B | 8B | Yes (Apache 2.0) | 150M synthetic pairs, SLERP merging |
| 4 | BGE-en-ICL | 7B | Yes | In-context learning for embeddings |
| 5 | Llama-Embed-Nemotron-8B | 8B | Yes | Full open recipe |

**Best open option for commercial use**: Qwen3-Embedding-8B (Apache 2.0).

All top-5 models follow the same recipe: take a 7-8B decoder-only LLM, remove causal mask, add latent attention pooling, two-stage contrastive training with MRL. The differentiator is now **training data quality** and **domain specialization**.

---

## Architecture & Training

### Why does Shoonya use MoE (Mixture of Experts)?

MoE achieves **4-8x model capacity** while keeping compute sparse — each token only activates 1-2 experts out of many. This means you get a much larger model (more knowledge capacity) without proportionally increasing inference cost. It's the same approach used by Mixtral, GPT-4, and other frontier models.

### Why use Mamba/SSM alongside transformers?

Attention is **quadratic** in sequence length — doubling the input quadruples the computation. Mamba (Selective State Space Models) processes sequences in **linear time**, making it 5x faster for long sequences. Shoonya uses a hybrid approach: transformer blocks for tasks needing full attention, Mamba blocks for efficient long-range processing.

### What is speculative decoding and why does it help?

LLMs generate tokens **one at a time** — each token requires a full forward pass. Speculative decoding (Medusa) adds multiple small "draft heads" that predict several future tokens simultaneously. The main model then **verifies** these predictions in parallel. When predictions are correct (which they often are for common patterns), you get 2.2-3.6x speedup with no quality loss.

### Why quantize models?

A 7B parameter model at FP16 needs ~14GB of memory. At 4-bit quantization, that drops to ~3.5GB — fitting on a single consumer GPU or even Apple Silicon. The three methods Shoonya supports:

- **GPTQ**: Uses Hessian information for minimal quality loss
- **AWQ**: Protects the most important weights based on activation patterns
- **GGUF**: Format for llama.cpp CPU inference — run on any machine
