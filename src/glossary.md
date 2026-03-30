# Glossary

**Attention**
: The mechanism by which each token in a sequence computes relevance scores with all other tokens, producing a weighted combination of their representations.

**AWQ (Activation-Aware Weight Quantization)**
: A 4-bit quantization method that preserves accuracy by identifying and protecting weights that are critical based on activation patterns.

**BPE (Byte Pair Encoding)**
: A tokenization algorithm that iteratively merges the most frequent byte/character pairs to build a vocabulary of subword tokens.

**Causal Attention**
: Attention where each token can only attend to tokens before it (and itself). Used in decoder-only models for text generation.

**Contrastive Learning**
: Training technique where the model learns to place similar items close together and dissimilar items far apart in embedding space. MNRL is the dominant loss function.

**Embedding**
: A fixed-size vector representation of an input (text, node, image) in a continuous vector space, where similar inputs are close together.

**FlashAttention**
: An IO-aware attention algorithm that computes exact attention with reduced memory reads/writes, achieving 1.6-2x speedup.

**GGUF**
: A file format for quantized models designed for llama.cpp, enabling efficient CPU inference.

**GNN (Graph Neural Network)**
: Neural network that operates on graph-structured data, passing messages between connected nodes to learn structural representations.

**GPTQ**
: A post-training quantization method that uses second-order (Hessian) information to minimize quantization error.

**GQA (Grouped Query Attention)**
: Attention variant where multiple query heads share a single key-value head, reducing memory with minimal quality loss.

**GraphSAGE**
: A GNN architecture that generates embeddings by sampling and aggregating features from a node's local neighborhood. Inductive: works on unseen nodes.

**HNSW (Hierarchical Navigable Small World)**
: An approximate nearest neighbor search algorithm. Samyama Graph uses HNSW for vector similarity search.

**KGE (Knowledge Graph Embedding)**
: Models like TransE, RotatE, ComplEx that embed entities and relations from a knowledge graph into continuous vector space.

**KV Cache**
: Cached key and value tensors from previous tokens during autoregressive generation, avoiding redundant computation.

**Mamba**
: A selective state space model that processes sequences in linear time (vs quadratic attention), particularly efficient for long sequences.

**Matryoshka Representation Learning (MRL)**
: Training technique that produces embeddings useful at multiple truncation points (e.g., 128, 256, 512, 1024, 4096 dims).

**MNRL (Multiple Negatives Ranking Loss)**
: Contrastive loss function where all non-paired items in a batch serve as negatives. Larger batch = more negatives = better signal.

**MoE (Mixture of Experts)**
: Architecture where each input token is routed to a subset of "expert" sub-networks, achieving larger model capacity with sparse computation.

**MTEB (Massive Text Embedding Benchmark)**
: The standard evaluation suite for embedding models, covering retrieval, classification, clustering, STS, and more.

**PagedAttention**
: vLLM's innovation: managing KV cache as virtual memory pages, enabling efficient memory sharing across requests.

**RoPE (Rotary Position Embedding)**
: Positional encoding that applies rotation matrices to encode position information, naturally supporting relative position relationships.

**Speculative Decoding**
: Inference acceleration where a draft model proposes multiple tokens, and the main model verifies them in parallel.

**SwiGLU**
: A feed-forward network variant using Swish activation with gating. Standard in modern LLMs.

**Transformer**
: Neural network architecture based on self-attention, processing all tokens simultaneously. The foundation of modern LLMs and embedding models.

**vLLM**
: High-throughput LLM serving engine using PagedAttention for efficient KV cache management. Supports continuous batching and OpenAI-compatible API.

**WSD (Warmup-Stable-Decay)**
: Learning rate scheduler that warms up linearly, holds steady, then decays. Used in Shoonya's training.

**YaRN (Yet another RoPE extensioN)**
: Technique for extending RoPE-based models to longer contexts without full fine-tuning.
