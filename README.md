# Wholesale Customer Segmentation using Clustering

![Python](https://img.shields.io/badge/Python-3.8+-blue?logo=python)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-orange?logo=scikit-learn)
![KMeans](https://img.shields.io/badge/Best%20Model-KMeans-brightgreen)
![Type](https://img.shields.io/badge/Type-Unsupervised%20Learning-blueviolet)
![Status](https://img.shields.io/badge/Status-Completed-green)

## Project Overview

This project segments wholesale customers based on their **annual spending behavior** across 6 product categories. Using **unsupervised learning** techniques, customers are grouped into meaningful clusters — enabling targeted marketing strategies and smarter resource allocation.

Three clustering algorithms were compared: **KMeans**, **Hierarchical (Agglomerative)**, and **DBSCAN**.

---

## Dataset

- **Source:** [UCI Machine Learning Repository — Wholesale Customers](https://archive.ics.uci.edu/ml/datasets/wholesale+customers)
- **Samples:** 440 customers × 8 columns
- **No missing values, no duplicates**

| Feature | Description |
|---------|-------------|
| `Channel` | Customer type: 1 = HoReCa, 2 = Retail |
| `Region` | 1 = Lisbon, 2 = Oporto, 3 = Other |
| `Fresh` | Annual spend on fresh products |
| `Milk` | Annual spend on milk products |
| `Grocery` | Annual spend on grocery products |
| `Frozen` | Annual spend on frozen products |
| `Detergents_Paper` | Annual spend on detergents & paper |
| `Delicassen` | Annual spend on delicatessen products |

---

## Data Preprocessing

- Dropped `Channel` and `Region` (categorical identifiers, not spending features)
- Verified zero missing values and no duplicates
- Applied **StandardScaler** for feature normalization (required for distance-based clustering)

---

## Exploratory Data Analysis

- **Histograms** — spending distributions for all 6 product categories (right-skewed)
- **Boxplots** — outlier detection across all expense features
- All features showed significant outliers → justified use of StandardScaler

---

## Models & Results

### Finding Optimal K
- **Elbow Method** (Inertia) → used to narrow down k range
- **Silhouette Score** → best k = **3**

### Clustering Algorithms Compared

| Algorithm | Silhouette Score | Clusters Found | Notes |
|-----------|-----------------|----------------|-------|
| **KMeans** | **0.5483 🏆** | 3 | Best performance |
| Hierarchical | 0.2646 | 3 | Ward linkage |
| DBSCAN | ❌ | 1 + 13 noise | Could not form meaningful clusters |

### Best Model: KMeans (k=3)

---

## Customer Segments (KMeans)

| Cluster | Fresh | Milk | Grocery | Frozen | Detergents | Delicassen | Segment Type |
|---------|-------|------|---------|--------|------------|------------|--------------|
| **0** | 10,441 | 19,386 | 28,656 | 2,190 | 13,328 | 2,374 | 🏪 Retail |
| **1** | 12,063 | 4,115 | 5,535 | 2,941 | 1,696 | 1,299 | 💰 Low Spenders |
| **2** | 34,782 | 30,367 | 16,898 | 48,702 | 756 | 26,776 | 🍽️ HoReCa |

**Segment Descriptions:**
- **Cluster 0 — Retail Customers:** High spending on Grocery, Milk, and Detergents → typical retail store buyers
- **Cluster 1 — Low Spenders:** Below-average spending across all categories → small or infrequent buyers
- **Cluster 2 — HoReCa Customers:** Very high Fresh, Frozen, and Delicassen → Hotels, Restaurants, Cafes

---

## Visualizations

- **Elbow Curve** — Inertia vs K
- **Silhouette Score Curve** — to select best k
- **Dendrogram** — Hierarchical clustering tree
- **PCA Scatter Plots** — All 3 algorithms compared side-by-side (2D projection)
- **Pairplot** — KMeans clusters across all feature pairs
- **Bar Chart** — Average spending per cluster per product category

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| `Python` | Core language |
| `Pandas / NumPy` | Data manipulation |
| `Matplotlib / Seaborn` | Visualization |
| `Scikit-learn` | KMeans, Hierarchical, DBSCAN, PCA, Silhouette |
| `SciPy` | Dendrogram (linkage) |

---

## How to Run

```bash
# Clone the repository
git clone https://github.com/husan-ai/wholesale-customer-segmentation.git
cd wholesale-customer-segmentation

# Install dependencies
pip install -r requirements.txt

# Launch the notebook
jupyter notebook Ulgurji_savdo_ML_Unsupervised.ipynb
```

---

## Requirements

```
numpy
pandas
matplotlib
seaborn
scikit-learn
scipy
jupyter
```

---

## Business Insights

- **Retail segment** should receive promotions on Grocery and Household products
- **HoReCa segment** needs bulk Fresh and Frozen product deals
- **Low spenders** can be targeted with loyalty programs to increase engagement
- DBSCAN revealed **13 outlier customers** — potential VIP or anomalous accounts worth investigating

---

## Future Improvements

- [ ] Try **RobustScaler** instead of StandardScaler to handle outliers better
- [ ] Apply **UMAP** for better dimensionality reduction visualization
- [ ] Tune DBSCAN `eps` using k-distance graph
- [ ] Add **cluster profiling dashboard** with Streamlit
- [ ] Combine with supervised model to predict cluster for new customers

---

## Author

**Husan**  
ML | DL | NLP  
GitHub: [@husan-ai](https://github.com/husan-ai)
