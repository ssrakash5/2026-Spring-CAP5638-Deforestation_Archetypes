# deforestation-archetypes
Moving beyond binary forest loss detection to uncover interpretable deforestation archetypes through unsupervised learning on event-level spatial morphology.

🌿 Deforestation Archetype Discovery

Unsupervised discovery of deforestation archetypes using event-level spatial morphology and clustering.

📌 Overview

Most global forest monitoring systems detect where and when forest loss occurs, but not what kind of loss it is.

This project moves beyond binary detection by modeling deforestation events as geometric objects and discovering recurring archetypes using unsupervised learning.

We show that deforestation is not random — it exhibits consistent, interpretable spatial patterns that can be uncovered without labels.

🚀 Key Idea

Event shape encodes the underlying deforestation process.

Instead of analyzing individual pixels:

We extract event-level patches
Compute morphological features
Discover archetypes via clustering

These archetypes align with real-world processes such as:

🌲 Agricultural clearing
🛣️ Roads & infrastructure
🌿 Selective logging
🧠 Methodology
1. Event Extraction
Input: Hansen Global Forest Change (30m)
Group connected loss pixels → event patches
Each patch = one deforestation event
2. Feature Engineering

For each event, compute geometric features:

Feature	Description
Area	Size of event
Compactness	Density vs spread
Eccentricity	Elongation
Aspect Ratio	Shape stretch
Edge Density	Boundary complexity
Mask Fraction	Internal density
3. Clustering
Algorithm: HDBSCAN
No predefined cluster count
Outliers handled as noise
📊 Results
🔹 Archetypes Discovered
14 distinct clusters
5.6% noise (unassigned outliers)
🔹 Feature Space Separation
Clear separation in UMAP visualization
Clusters form distinct regions → not random
🔹 Stability
Adjusted Rand Index (ARI): ~0.658
Consistent clusters across multiple runs
🔹 Learnability
kNN classification accuracy: 98.24%
Archetypes are well-separated and predictable
🔹 Interpretation (Examples)
Archetype	Likely Process
Linear	Roads & infrastructure
Blocky	Agricultural clearing
Fragmented	Selective logging

⚠️ These are interpretations, not labeled ground truth.

🔹 Generalization
Tested on 15,000-event global dataset
Structure persists (with increased noise)
Suggests archetypes are not dataset-specific
🔹 Exploratory Risk Signal
ROC-AUC: 0.994 (proxy model)
Some archetypes consistently align with higher-risk signals
⚠️ Not independent validation (same feature space)
📈 Example Visualizations
UMAP projection of archetypes
Feature distribution boxplots
Cluster stability heatmap
Confusion matrix (kNN)

(See /results or notebook outputs for visuals)

⚠️ Limitations
No ground-truth driver labels
Risk model uses proxy labels (not independent)
Limited geographic diversity in development set
🔮 Future Work
Align archetypes with labeled deforestation drivers
Evaluate across regions, biomes, and time
Build a benchmark dataset for validation
Integrate into real-time monitoring pipelines
🛠️ Tech Stack
Python
NumPy / Pandas
scikit-learn
HDBSCAN
UMAP
Matplotlib / Seaborn
