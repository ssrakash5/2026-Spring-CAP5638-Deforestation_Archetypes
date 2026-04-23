# 🌿 Deforestation Archetype Discovery

Unsupervised discovery of deforestation archetypes using event-level spatial morphology and clustering.

---

## Overview

Global forest monitoring systems (e.g., Hansen GFC) detect **where** and **when** forest loss occurs, but not **what kind** of loss it is.

This project reframes deforestation as an **event-level pattern discovery problem**.  
Instead of pixel-wise detection, we analyze connected deforestation events and uncover recurring **geometric archetypes** using unsupervised learning.

---

## 📂 Dataset

### Data Sources

- **Hansen Global Forest Change (GFC)**
  - Annual forest loss maps from Landsat imagery  
  - Spatial resolution: **30 meters**

- **Sentinel-2 (optional refinement)**
  - Higher resolution imagery (**10–20 meters**)

---

### Unit of Analysis

We convert pixel-level forest loss into **event-level patches**:

1. Forest loss map → binary raster  
2. Connected components → group neighboring pixels  
3. Event patch → one deforestation event  

---

### Feature Dataset

Each event is represented using:

- Area  
- Compactness  
- Eccentricity  
- Aspect Ratio  
- Edge Density  
- Mask Fraction  

---

### Dataset Scale

- Thousands of event patches  
- Extended evaluation: **~15,000 global events**

---

### Access

Full datasets and outputs:  
https://drive.google.com/drive/folders/1JmSbuaztQJrZbZ-y1q3aQ5b4uqqN-6eX?usp=drive_link

---

## 💡 Key Idea

> Event shape encodes the underlying deforestation process.

Different drivers (e.g., agriculture, roads, logging) produce distinct spatial patterns.

---

## 🧠 Method

### 1. Event Extraction
- Hansen GFC → connected components  

### 2. Feature Engineering
- Compute geometric features per event  

### 3. Clustering
- **HDBSCAN**
- No predefined cluster count  
- Handles noise  

---

## 📊 Results

- **14 clusters discovered**  
- **5.6% noise**  
- Clear separation (UMAP)

### Stability
- ARI ≈ **0.658**

### Learnability
- kNN accuracy: **98.24%**

---

### Interpretation

| Archetype   | Likely Process          |
|------------|------------------------|
| Linear     | Roads & infrastructure |
| Blocky     | Agriculture            |
| Fragmented | Logging                |

> ⚠️ Interpretations, not ground truth.

---

## 🌍 Generalization

- Tested on **15,000-event global dataset**
- Structure persists with noise

---

## ⚠️ Risk Model (Exploratory)

- ROC-AUC: **0.994**

> ⚠️ Not independent validation (same feature space)

---

## 📁 Repository Structure

This repository is organized into three main components: pipeline code (`src/`), outputs (`outputs/`), and experiment notebook.

```
.
├── Deforestation_archetypes_clean.ipynb
├── download_data.py
├── sn7_imagepair_manifest.csv
├── README.md

├── src/
│   ├── build_manifest_sn7.py
│   ├── extract_events.py
│   ├── step2_tile_pairs.py
│   ├── step3_build_change_masks_from_geojson.py
│   ├── step4_extract_events.py
│   ├── step5_extract_event_features.py
│   ├── step6_cluster_events.py
│   └── step7_interpret_clusters.py

├── outputs/
│   ├── archetypes/
│   │   ├── cluster_XX_gallery.png
│   │   ├── cluster_XX_meanmask.png
│   │   ├── cluster_stats.csv
│   │   └── event_clusters_shapeonly.csv
│   └── gallery/
```

---

## ⚙️ Tech Stack

- Python  
- NumPy, Pandas  
- scikit-learn  
- HDBSCAN  
- UMAP  
- Matplotlib  

---

## 🚀 Key Takeaway

> Deforestation is not random — it has structure that can be discovered and interpreted.

---

## 👤 Authors

- Akash Sagi  
- Sakethram Naidu  
