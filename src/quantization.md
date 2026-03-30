# Quantization (GPTQ, AWQ, GGUF)

> This chapter is a work in progress.

## Topics to Cover

- Why quantize: 7B model at FP16 = 14GB, at 4-bit = 3.5GB
- GPTQ: post-training quantization using Hessian information
- AWQ: activation-aware weight quantization — protects salient weights
- GGUF: llama.cpp format for CPU inference
- Quality vs compression tradeoffs
- Shoonya's quantization implementations
