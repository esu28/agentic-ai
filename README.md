```mermaid
flowchart TD
  A[Histology + ST inputs] --> B[Preprocessing]
  B --> C[DWT texture extraction]
  C --> D[Build radius graph]
  D --> E[Edge gating]
  E --> F[Graph Transformer 👑]
  F --> G[Embeddings → Clustering]
  G --> H[Downstream analyses]
