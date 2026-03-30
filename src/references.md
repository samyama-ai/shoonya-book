# Research References

## Foundational Papers

- **Attention Is All You Need** (Vaswani et al., 2017) — The original transformer architecture
- **BERT: Pre-training of Deep Bidirectional Transformers** (Devlin et al., 2018) — Encoder-only transformers for NLU

## Model Architecture

- **FlashAttention: Fast and Memory-Efficient Exact Attention** (Dao et al., 2022)
- **FlashAttention-2** (Dao, 2023)
- **GQA: Training Generalized Multi-Query Transformer Models** (Ainslie et al., 2023)
- **Mixtral of Experts** (Jiang et al., 2024) — MoE for language models
- **Mamba: Linear-Time Sequence Modeling with Selective State Spaces** (Gu & Dao, 2023)
- **SwiGLU Activation Function** (Shazeer, 2020)

## Positional Encodings

- **RoFormer: Enhanced Transformer with Rotary Position Embedding** (Su et al., 2021)
- **YaRN: Efficient Context Window Extension** (Peng et al., 2023)
- **ALiBi: Train Short, Test Long** (Press et al., 2022)

## Inference & Serving

- **Medusa: Simple LLM Inference Acceleration Framework** (Cai et al., 2024)
- **vLLM: Easy, Fast, and Cheap LLM Serving with PagedAttention** (Kwon et al., 2023)
- **GPTQ: Accurate Post-Training Quantization** (Frantar et al., 2023)
- **AWQ: Activation-aware Weight Quantization** (Lin et al., 2024)

## Embeddings

- **NV-Embed v2**: [arxiv.org/abs/2405.17428](https://arxiv.org/abs/2405.17428) — ICLR 2025, latent attention pooling
- **Qwen3-Embedding**: [arxiv.org/pdf/2506.05176](https://arxiv.org/pdf/2506.05176) — Synthetic data + SLERP merging
- **BGE-M3**: [arxiv.org/abs/2402.03216](https://arxiv.org/abs/2402.03216) — Dense+sparse+multi-vector
- **Matryoshka Representation Learning**: [arxiv.org/abs/2205.13147](https://arxiv.org/abs/2205.13147) — Flexible dimensionality
- **Theoretical Limits of Embedding Retrieval**: [arxiv.org/abs/2508.21038](https://arxiv.org/abs/2508.21038)
- **Numeracy Gap in Text Embeddings**: [arxiv.org/abs/2509.05691](https://arxiv.org/abs/2509.05691)

## Graph + Embeddings

- **BioMedKG** (2025) — Multimodal contrastive learning for biomedical KGs: [frontiersin.org](https://www.frontiersin.org/journals/systems-biology/articles/10.3389/fsysb.2025.1651930)
- **BioGraphFusion** (2025) — Graph knowledge embedding: [academic.oup.com/bioinformatics](https://academic.oup.com/bioinformatics/article/41/7/btaf408)
- **GraphFormers** — GNN-nested transformers: [arxiv.org/abs/2105.02605](https://arxiv.org/abs/2105.02605)
- **Text Embeddings in Labeled Property Graphs**: [arxiv.org/html/2507.10772](https://arxiv.org/html/2507.10772)
- **Text2Cypher**: [aclanthology.org/2025.genaik-1.11.pdf](https://aclanthology.org/2025.genaik-1.11.pdf)
- **TigerVector — Vector Search in Graph DBs**: [arxiv.org/html/2501.11216v3](https://arxiv.org/html/2501.11216v3)
- **Neo4j RAG Text Embedding Limitations**: [neo4j.com/blog/developer/rag-text-embeddings-limitations/](https://neo4j.com/blog/developer/rag-text-embeddings-limitations/)

## Benchmarks

- **MTEB Leaderboard**: [huggingface.co/spaces/mteb/leaderboard](https://huggingface.co/spaces/mteb/leaderboard)
