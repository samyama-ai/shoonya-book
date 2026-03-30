# Unsolved Problems & Gaps

Despite rapid progress, embedding models face fundamental limitations that no current model has overcome. These gaps represent both challenges and opportunities.

## Theoretical Limits of Embedding-Based Retrieval

A 2025 paper (arxiv 2508.21038) proved a sobering result: **the number of distinct top-k result sets that can be returned is fundamentally bounded by embedding dimensionality**. Even with 4096-dim embeddings, there exist realistic queries where the best embedding models achieve recall@2 below 60%, while a long-context reranker (Gemini-2.5-Pro) solves 100% in one forward pass.

**Implication**: Embeddings are necessary for efficiency (you can't run a full LLM on every document in a corpus), but they mathematically cannot solve all retrieval problems. Hybrid approaches (embedding retrieval → LLM reranking) will always be needed.

## The Numeracy Gap

A 2025 paper (arxiv 2509.05691) revealed that **current embedding models cannot accurately encode numerical content**. This is critical for:

- **Clinical trials**: Dosages (500mg vs 50mg), p-values (0.001 vs 0.05), patient counts
- **Industrial data**: Sensor thresholds, operating temperatures, pressure ratings
- **Finance**: Revenue figures, stock prices, ratios
- **Cricket statistics**: Batting averages, strike rates, overs

No model on MTEB has solved this. Numbers are tokenized as arbitrary subword sequences, losing their mathematical meaning.

## Compositional Reasoning and Negation

Embedding models fundamentally struggle with several linguistic constructs:

### Negation
"Patients who did **NOT** respond to treatment" and "Patients who responded to treatment" produce near-identical embeddings. The negation is a small perturbation in token space but a complete semantic inversion.

### Temporal Ordering
"A happened before B" vs "B happened before A" — embeddings capture the presence of A and B but not the directional relationship.

### Compositional Queries
Multi-hop reasoning like "drugs that treat diseases caused by gene X" collapses in a single-vector space. The composition of "treats" → "caused by" → specific gene cannot be captured in one point in vector space.

### Asymmetric Relationships
Hierarchy ("dog is an animal"), containment ("Paris is in France"), and causation ("smoking causes cancer") are inherently directional. Symmetric similarity measures (cosine distance) cannot properly encode them.

## Structured Data and Operations

As Neo4j's research team documented, text embeddings are inadequate for **filtering, sorting, aggregation, and counting operations**. Queries like:

- "Find all clinical trials with >500 patients that started after 2023"
- "List drugs sorted by number of adverse effects"
- "Count the number of matches where Sachin scored a century"

These require structured query execution (SQL, Cypher), not similarity search. Embeddings can find semantically related content but cannot perform computation.

## Benchmark Overfitting

MTEB scores are increasingly gamed. Models are trained to maximize benchmark performance, which may diverge from real-world utility:

- Training data contamination (benchmark test sets leaking into pretraining)
- Overfitting to benchmark distribution patterns
- Domain-specific performance can be dramatically worse than headline MTEB scores
- The 2025 MTEB expansion to 100+ tasks helped but didn't eliminate this

## Long-Context Degradation

While models claim 32K-128K context windows, actual embedding quality degrades significantly beyond ~4K tokens. The "lost in the middle" phenomenon — where information in the middle of long documents is underweighted — affects embeddings just as it affects generation.

## Graph Structure Understanding

**This is the biggest gap relevant to our work.** No current embedding model captures:

- **Node-edge-node relational structure**: The triple (Aspirin)-[TREATS]->(Headache) is more than the sum of its text parts
- **Multi-hop graph paths**: The meaning of a node depends on its neighbors, their neighbors, etc.
- **Graph isomorphism / subgraph patterns**: Structural patterns independent of node labels
- **Property graph schemas**: Typed relationships with properties
- **Cypher/SPARQL query semantics**: No embedding model understands query languages

This gap is precisely what motivates the [Samyama embedding model proposal](./samyama_embedding.md).

## Summary of Gaps and Opportunities

| Gap | Severity | Opportunity for Us |
|-----|----------|-------------------|
| Graph structure | Critical | Direct differentiation — no one else is solving this |
| Cypher understanding | Critical | First-of-its-kind capability |
| Numeracy | High | Important for clinical trials, cricket, industrial KGs |
| Negation/composition | Medium | Partially addressable with graph context |
| Retrieval limits | Fundamental | Accept and design hybrid retrieval + graph traversal |
| Long context | Medium | Graph neighborhoods provide focused context |
