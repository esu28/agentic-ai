# Multi-Modal CCC Inference and Niche Identification Pipeline

<p align="center">
  <img src="docs/logo.png" alt="Project Logo" width="150"/>
</p>

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)  
[![Python](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org)

---

## Table of Contents
1. [Overview](#overview)  
2. [Workflow](#workflow)  
3. [Installation](#installation)  
4. [Usage](#usage)  
5. [Pipeline Stages](#pipeline-stages)  
6. [Testing & Benchmarking](#testing--benchmarking)  
7. [Contributing](#contributing)  
8. [License](#license)  

---

## Overview
A **multi-modal, multi-view graph-transformer** framework to decode spatial cell–cell communication by integrating:
- **Histology** (image patches)  
- **Spatial transcriptomics** (ST)  
- **Ligand–receptor biology**  
- **Wavelet texture features**  
- **TF activity scores**  

---

## Workflow

<p align="center">
  <img src="docs/workflow.png" alt="Pipeline Workflow" width="80%"/>
</p>

<details>
<summary><strong>Mermaid Source (for supported renderers)</strong></summary>

```mermaid
flowchart LR
  subgraph Inputs
    style Inputs fill:#f0f8ff,stroke:#666,stroke-width:2px
    A1([Histology Image])
    A2([ST Gene Matrix])
    A3([LRP Database])
    A4([TF Activity Scores])
  end

  subgraph Preprocessing
    style Preprocessing fill:#fff8dc,stroke:#666,stroke-width:2px
    B1([Map Spots → Patches])
    B2([Filter & Normalize])
    B3([Standardize Patches])
  end

  subgraph FeatureExtraction
    style FeatureExtraction fill:#e6ffe6,stroke:#666,stroke-width:2px
    C1([DWT Wavelet Features])
    C2([Mutual Info & Coexpression])
    C3([Primary CCC Scores])
  end

  subgraph GraphConstruction
    style GraphConstruction fill:#fff0f5,stroke:#666,stroke-width:2px
    D1([Build Radius Graph])
    D2([Edge Gating Layer])
  end

  subgraph Encoder
    style Encoder fill:#f5f5dc,stroke:#666,stroke-width:2px
    E1([Graph Transformer w/ Attention])
    E2([Learn Embeddings & γ Weights])
  end

  subgraph Clustering
    style Clustering fill:#e0ffff,stroke:#666,stroke-width:2px
    F1([Select Top LRPs (Kneedle)])
    F2([Cluster Embeddings → Niches])
  end

  subgraph Analysis
    style Analysis fill:#d4edda,stroke:#155724,stroke-width:2px
    G1([Marker-Gene Enrichment])
    G2([Niche-Specific CCC Tests])
    G3([Morphology Validation])
    G4([Spatial Coherence Tests])
  end

  A1 & A2 & A3 & A4 --> B1 --> B2 --> B3 --> C1 --> C2 --> C3 --> D1 --> D2 --> E1 --> E2 --> F1 --> F2 --> G1 --> G2 --> G3 --> G4
