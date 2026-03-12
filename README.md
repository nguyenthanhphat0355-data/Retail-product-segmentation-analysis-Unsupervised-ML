# Retail Product Segmentation
### RMIT Business Analytics Champion — Season 6 (Round 1)

> **Competition:** RMIT Business Analytics Champion Season 6  
> **Round:** Round 1 — October 11, 2025  
> **Time Constraint:** 120 minutes  
> **Dataset Size:** 9,173 records across 7 columns. The dataset used in this project originates from the RBAC Season 6 competition.
Due to competition confidentiality rules, the dataset cannot be publicly shared.
---

## Overview

This project was completed as part of RMIT Business Analytics Champion Season 6, a competitive analytics case competition organized by the RMIT Analytics Club. Given a fashion retail inventory dataset, our team was tasked with performing data profiling, applying machine learning-based segmentation, and delivering actionable business recommendations — all within a 120-minute window.

My role covered the entire technical pipeline: data cleaning, exploratory analysis, clustering model, dimensionality reduction, and segment profiling. My teammate handled the business strategy and recommendations write-up based on the model outputs.

---

## Problem Statement

The dataset represented a fashion retailer's inventory across thousands of SKUs. The business questions were:

1. **Profiling** — Perform calculation and visualization analysis across the dataset
2. **Segmentation** — Find natural product segments using machine learning
3. **Recommendations** — Provide actionable next steps based on segment findings

---

## Technical Pipeline

### 1. Data Cleaning
- Replaced `#REF!` errors, dash placeholders (`-`), and blank strings with `NaN`
- Dropped all rows with missing values after replacement
- Converted `Stock` column from object to numeric (`float64`)
- Exported cleaned dataset to Excel for reproducibility

### 2. Exploratory Data Analysis
- Profiled all categorical columns: Category (21 unique), Size (11), Color (60), Design No. (1,591)
- Identified heavy right-skew in Stock distribution with significant outliers (max: 1,234 units vs. median: 8)
- Visualized distributions via boxplot, histogram, heatmap (Category × Size), and pie chart (top 5 categories)
- KURTA dominates the catalog at 40.4% of all SKUs

### 3. Feature Engineering & Preprocessing
- Selected features: `Stock`, `Category`, `Size`, `Color`
- Label-encoded all categorical features for clustering compatibility
- Applied `StandardScaler` to normalize feature ranges before K-Means

### 4. Optimal Cluster Selection
- Tested k = 2 to 10 using both **Elbow Method** (inertia) and **Silhouette Score**
- Optimal k = **9** selected based on silhouette score peak
- Silhouette score at k=9: ~0.315

### 5. K-Means Clustering
- Fit K-Means (k=9, random_state=42, n_init=10) on scaled features
- Assigned cluster labels back to full dataset

### 6. Dimensionality Reduction & Visualization
- **PCA** (2 components) for fast 2D cluster scatter plot
- **t-SNE** (2 components, perplexity=30) for non-linear structure visualization
- **3D PCA** (3 components) for additional spatial perspective

### 7. Segment Profiling
Each cluster profiled by:
- Dominant category, size, color
- Average and median stock levels
- Business label assigned: `{DominantCategory}_{DominantSize}_{StockLevel}`

---

## Results

| Cluster | Label | Products | Avg Stock | Dominant Category | Dominant Size |
|---------|-------|----------|-----------|-------------------|---------------|
| 0 | KURTA_XXL_Low_Stock | 1,430 | 17.1 | KURTA | XXL |
| 1 | KURTA_XXL_Low_Stock | 2,074 | 18.9 | KURTA | XXL |
| 2 | KURTA_S_High_Stock | 253 | 209.9 | KURTA | S |
| 3 | SET_XXL_Low_Stock | 756 | 20.9 | SET | XXL |
| 4 | KURTA_L_Low_Stock | 1,284 | 18.3 | KURTA | L |
| 5 | SET_L_Low_Stock | 748 | 20.8 | SET | L |
| 6 | KURTA_XS_High_Stock | 25 | 778.7 | KURTA | XS |
| 7 | SET_XL_Low_Stock | 860 | 18.9 | SET | XL |
| 8 | KURTA_L_Low_Stock | 1,743 | 20.2 | KURTA | L |

**Key findings:**
- KURTA dominates 6 of 9 segments — it is the anchor product of the catalog
- Clusters 2 and 6 are high-stock outliers requiring immediate promotional action (avg. 210–779 units)
- 7 segments are undersupplied relative to demand signals — restocking priority
- All customers with 2+ services have internet — internet is the anchor product for retention

---

## Business Recommendations

*(Business strategy section written by teammate — see report PDF for full recommendations)*

**Promote:** KURTA in S and XS sizes — clear excess inventory via flash sales and BOGO campaigns  
**Restock:** XXL and L size segments across KURTA and SET categories  
**Target:** Size-based customer segmentation for email and ad campaigns  
**Strategy:** Differentiate by color patterns within same-size segments to reduce cannibalization

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| Python | Core language |
| Pandas, NumPy | Data manipulation and cleaning |
| Scikit-learn | K-Means, StandardScaler, PCA, Silhouette Score |
| Matplotlib, Seaborn | Static visualizations |
| t-SNE (sklearn.manifold) | Non-linear dimensionality reduction |

---

## Team & Credits

This project was completed as a team effort for RMIT Business Analytics Champion Season 6.

| Contributor | Role |
|-------------|------|
| Nguyễn Thành Phát | Full technical pipeline — data cleaning, EDA, K-Means clustering, PCA/t-SNE, segment profiling |
| Phạm Nguyễn Minh Khoa| Cross statistical results verification and report business implication for later strategies |
| Đặng Khánh Ngọc, Lê Anh Khoa | Sales and Marketing strategies covering inventory management and promotions |

> *Note: Code and technical analysis by Nguyễn Thành Phát. Business recommendations section co-developed with teammates based on model outputs.*

---

## Competition Context

**Organizer:** RMIT Analytics Club  
**Competition:** RMIT Business Analytics Champion (RBAC) Season 6  
**Round:** Round 1 — Calculation, Visualization & Segmentation  
**Case Sponsor:** Colgate-Palmolive  
**Date:** October 11, 2025
