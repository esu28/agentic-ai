# Multi-Modal CCC Inference and Niche Identification Pipeline

## Workflow

<p align="center">
  <img src="docs/workflow.png" alt="Pipeline Workflow" width="80%"/>
</p>

<details>
<summary><strong>Mermaid Source (for supported renderers)</strong></summary>

```mermaid
flowchart LR
  %%================ Inputs ====================
  subgraph Inputs
    style Inputs fill:#f0f8ff,stroke:#666,stroke-width:2px
    A1([Histology Image])
    A2([ST Gene Matrix])
    A3([LRP Database])
    A4([TF Activity Scores])
  end

  %%============= Preprocessing ================
  subgraph Preprocessing
    style Preprocessing fill:#fff8dc,stroke:#666,stroke-width:2px
    B1([Map Spots → Patches])
    B2([Filter & Normalize])
    B3([Standardize Patches])
  end

  %%========== Feature Extraction ============
  subgraph FeatureExtraction
    style FeatureExtraction fill:#e6ffe6,stroke:#666,stroke-width:2px
    C1([DWT Wavelet Features])
    C2([Mutual Info & Coexpression])
    C3([Primary CCC Scores])
  end

  %%======== Graph Construction ===========
  subgraph GraphConstruction
    style GraphConstruction fill:#fff0f5,stroke:#666,stroke-width:2px
    D1([Build Radius Graph])
    D2([Edge Gating Layer])
  end

  %%============ Encoder ==============
  subgraph Encoder
    style Encoder fill:#f5f5dc,stroke:#666,stroke-width:2px
    E1([Graph Transformer w/ Attention])
    E2([Learn Embeddings & γ Weights])
  end

  %%=========== Clustering ===========
  subgraph Clustering
    style Clustering fill:#e0ffff,stroke:#666,stroke-width:2px
    F1([Select Top LRPs (Kneedle)])
    F2([Cluster Embeddings → Niches])
    F1 --> F2
  end

  %%============ Analysis =============
  subgraph Analysis
    style Analysis fill:#d4edda,stroke:#155724,stroke-width:2px
    G1([Marker-Gene Enrichment])
    G2([Niche-Specific CCC Tests])
    G3([Morphology Validation])
    G1 --> G2 --> G3
  end

  %%========== Connections ==========
  A1 & A2 & A3 & A4 --> B1
  B1 --> B2 --> B3 --> C1 --> C2 --> C3 --> D1 --> D2 --> E1 --> E2 --> F1 --> G1
