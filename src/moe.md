# Mixture of Experts (MoE)

> This chapter is a work in progress.

## Topics to Cover

- What is MoE and why it achieves 4-8x capacity with sparse activation
- Router network: how tokens are assigned to experts
- Top-k gating: selecting 1-2 experts per token
- Load balancing loss: preventing expert collapse
- Shoonya's MoE implementation
- Comparison with dense models at equivalent compute
