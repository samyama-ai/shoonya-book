# vLLM & Production Serving

> This chapter is a work in progress.

## Topics to Cover

- The serving challenge: maximizing throughput for concurrent users
- PagedAttention: virtual memory for KV cache — 10-24x throughput
- Continuous batching: dynamic batch scheduling
- OpenAI-compatible API: /v1/completions, /v1/chat/completions
- Streaming responses via Server-Sent Events (SSE)
- Shoonya's vLLM compatibility layer
- Deployment: Mac Mini (MPS), Linux (CUDA), Docker
