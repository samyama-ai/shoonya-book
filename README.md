# Building Shoonya: The Architecture of a Research-Driven Language Model

This repository contains the source code for the "Book as Code" project describing the internal architecture of **Shoonya** — a state-of-the-art, research-driven transformer language model.

It is written using `mdBook`.

## Building the Book

1.  **Install mdBook**:
    ```bash
    cargo install mdbook
    ```

2.  **Build**:
    ```bash
    mdbook build
    ```

3.  **Serve locally**:
    ```bash
    mdbook serve --open
    ```

## Content Structure

*   **Part I**: Foundations — transformers, attention, embeddings
*   **Part II**: Model Architecture — MoE, Mamba, positional encodings
*   **Part III**: Training — schedulers, memory optimization, data pipelines
*   **Part IV**: Inference — speculative decoding, quantization, vLLM serving
*   **Part V**: Embeddings — SOTA, graph-aware models, Samyama integration

## License

This book content is licensed under CC-BY-4.0.
The Shoonya code is licensed under Apache 2.0.
