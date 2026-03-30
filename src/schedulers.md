# Learning Rate Schedulers

> This chapter is a work in progress.

## Topics to Cover

- Why scheduling matters: too high → divergence, too low → slow convergence
- Warmup-Stable-Decay (WSD) — Shoonya's primary scheduler
- Cosine annealing with warm restarts
- OneCycle policy
- Comparison of scheduler shapes and training dynamics
- Implementation in Shoonya's `schedulers.py`
