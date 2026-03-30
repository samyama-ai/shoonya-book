# Feed-Forward Networks (SwiGLU)

> This chapter is a work in progress.

## Topics to Cover

- Role of the FFN in transformer blocks
- Standard FFN: Linear → ReLU → Linear
- SwiGLU: Swish-Gated Linear Unit — why it outperforms ReLU/GELU
- Gating mechanism: element-wise product with sigmoid
- Shoonya's SwiGLU implementation
- Hidden dimension sizing (typically 8/3 × model dim)
