# 🧬 Unveiling Regulatory Genes in Pancreatic Cancer Through Single-Cell RNA Sequencing

This repository contains the analysis pipeline and documentation for my **Minor Project**:  
**Unveiling Regulatory Genes in Pancreatic Cancer Through Single-Cell RNA Sequencing (scRNA‑seq)**  
---

## 📖 Project Overview
Pancreatic ductal adenocarcinoma (PDAC) is one of the most lethal cancers, with poor survival rates due to late detection and therapy resistance.  
This project leverages **single‑cell RNA sequencing (scRNA‑seq)** to dissect the **tumor immune microenvironment (TIME)** and identify **regulatory genes** driving PDAC progression.

- **Dataset:** GSE212966 (GEO) and PRJNA878527 (ENA/SRA: SRP396295)  
- **Cells analyzed:** 80,682 (42,573 PDAC vs 38,109 normal)  
- **Clusters identified:** 16 distinct cell populations via UMAP  
- **Key findings:** Dysregulated immune landscape, enrichment of NF‑κB, AGE‑RAGE, collagen metabolism, osteoclast differentiation pathways.

---

## 📂 Repository Structure
```
├── data/                # Raw FASTQ or matrix files (not included here, download from SRA/GEO)
├── scripts/             # R scripts for preprocessing, QC, clustering, DEG, enrichment
├── results/             # Figures, plots, tables generated during analysis
├── README.md            # Documentation (this file)
└── /               
```

---

## ⚙️ Step‑wise Workflow

### 1. 📥 Data Collection
- Download raw scRNA‑seq data from **ENA (PRJNA878527)** or **SRA (SRP396295)**.
- 20 paired‑end samples:  
  - 10 PDAC tumor samples  
  - 10 adjacent normal pancreatic tissue samples  

### 2. 🧩 Alignment & Mapping
- Tool: **Cell Ranger v8.0.1**
- Reference genome: **GRCh38‑2024‑A (10X Genomics)**
- Steps:
  - Demultiplex FASTQ files  
  - Filter low‑quality reads  
  - Extract cell barcodes & UMIs  
  - Align reads using **STAR**  
  - Generate raw & filtered gene‑cell matrices  

### 3. ✅ Quality Control
- Tool: **Seurat v4.3.0**
- Filters applied:
  - <500 genes/cell removed  
  - >25% mitochondrial genes removed  
  - <1000 UMIs/cell removed  
  - Genes detected in <10 cells removed  
- Doublet removal: **scDblFinder**  
- Ambient RNA correction: **SoupX**

### 4. 🔄 Normalization
- Method: **SCTransform (sct)** in Seurat  
- Corrects for sequencing depth & technical noise.

### 5. 🔗 Integration
- Integrate datasets across conditions (PDAC vs normal) to minimize batch effects.  
- Seurat integration pipeline used.

### 6. 🧭 Clustering & Annotation
- Dimensionality reduction: **PCA → UMAP**  
- 16 clusters identified.  
- Annotation via **FindConservedMarkers** + literature references.  
- Cell types: macrophages, CD8 T cells, fibroblasts, neutrophils, epithelial cells, etc.

### 7. 📊 Differential Gene Expression (DEG)
- Tool: **Seurat FindMarkers**  
- Compared PDAC vs normal within each cluster.  
- Top 20 DEGs per cluster identified.

### 8. 📈 Enrichment Analysis
- Tool: **clusterProfiler (R)**  
- Analyses performed:
  - **GO enrichment** → ECM organization, collagen biosynthesis, digestion.  
  - **KEGG pathways** → NF‑κB, AGE‑RAGE, IL‑17 signaling, osteoclast differentiation.  

### 9. 🧾 Results Summary
- **Immune dysregulation:** ↑ macrophages, CD8 T cells, fibroblasts, neutrophils in PDAC.  
- **Loss of exocrine function:** ↓ pancreatic secretion pathways.  
- **Inflammatory signaling:** NF‑κB & AGE‑RAGE activation.  
- **Structural remodeling:** Collagen metabolism, cytoskeleton changes.  
- **Potential therapeutic insights:** TIME profiling may guide immunotherapy combinations.

---

## 📊 Key Figures
- **UMAP plots:** 16 clusters annotated (PDAC vs normal).  
- **Violin plots:** Marker gene expression per cluster.  
- **Bar plots:** DEGs & enriched pathways.  
- **Tables:** Cell counts per type (PDAC vs normal).

---

## 🛠️ Tools & Dependencies
- **Cell Ranger v8.0.1**  
- **R v4.3.0**  
  - Seurat  
  - scDblFinder  
  - SoupX  
  - clusterProfiler  
- **STAR aligner** (via Cell Ranger)

---
---
<img width="1583" height="794" alt="image" src="https://github.com/user-attachments/assets/3172485f-f742-4c11-a67d-53fb906449ed" />

## Data
https://drive.google.com/drive/folders/1FfARQs2JpvkAPfkEPHmyhWxOK9rz-hI8?usp=sharing
