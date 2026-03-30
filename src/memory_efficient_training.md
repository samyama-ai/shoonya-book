# Memory-Efficient Training

> This chapter is a work in progress.

## Topics to Cover

- The memory challenge: model weights + gradients + optimizer state + activations
- Gradient checkpointing: 50-70% memory reduction by recomputing activations
- Mixed precision training: FP16/BF16/TF32 — halve memory, accelerate compute
- Activation offloading to CPU
- Shoonya's memory-efficient trainer implementation
- Practical memory budgets for different GPU sizes
