# 🌿 Deforestation Archetype Discovery

Unsupervised discovery of deforestation archetypes using event-level spatial morphology and clustering.



## Overview

Global forest monitoring systems (e.g., Hansen GFC) detect **where** and **when** forest loss occurs, but not **what kind** of loss it is.

This project reframes deforestation as an **event-level pattern discovery problem**.  
Instead of pixel-wise detection, we analyze **connected deforestation events** and uncover recurring **geometric archetypes** using unsupervised learning.



## Key Idea

> Event shape encodes the underlying deforestation process.

Different drivers (e.g., agriculture, roads, logging) produce distinct spatial patterns.  
These patterns can be discovered **without labels** using morphology alone.



## Method

### 1. Event Extraction
- Input: Hansen Global Forest Change (30m)
- Group connected pixels → **event patches**
- Each patch = one deforestation event

### 2. Feature Engineering
Compute geometric features for each event:

- Area  
- Compactness  
- Eccentricity  
- Aspect Ratio  
- Edge Density  
- Mask Fraction  

### 3. Clustering
- Algorithm: **HDBSCAN**
- No predefined number of clusters
- Outliers handled as noise



## Results

- **14 clusters discovered**
- **5.6% events classified as noise**
- Clear separation in feature space (UMAP)

### Stability
- Adjusted Rand Index (ARI): ~0.658  
- Clusters consistent across runs

### Learnability
- kNN classification accuracy: **98.24%**
- Archetypes are well-separated and predictable

### Interpretation (qualitative)

| Archetype   | Likely Process              |
|------------|---------------------------|
| Linear     | Roads & infrastructure     |
| Blocky     | Agricultural clearing      |
| Fragmented | Selective logging          |

> Note: These are interpretations, not labeled ground truth.



## Generalization

- Tested on **15,000-event global dataset**
- Structure persists (with increased noise)
- Suggests archetypes are not dataset-specific



## Exploratory Risk Model

- ROC-AUC: **0.994**
- Some archetypes align with higher-risk signals

> ⚠️ Proxy labels derived from same feature space — not independent validation.




## Tech Stack

- Python  
- NumPy, Pandas  
- scikit-learn  
- HDBSCAN  
- UMAP  
- Matplotlib  

---

## Authors

- Akash Sagi  
- Sakethram Naidu  
