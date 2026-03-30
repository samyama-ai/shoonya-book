# KV Cache & Quantization

> This chapter is a work in progress.

## Topics to Cover

- What is the KV cache and why it's the inference memory bottleneck
- KV cache quantization: 4-bit and 8-bit — 50-75% memory reduction
- Priority-based cache management
- Paged attention (vLLM's innovation)
- Shoonya's `kv_cache.py` implementation
- Impact on generation quality vs memory savings
