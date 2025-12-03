# Single-cell RNA-seq Data Analysis and Cell Type Annotation

This notebook performs a comprehensive analysis of single-cell RNA-sequencing data, focusing on quality control, dimensionality reduction, clustering, and automated cell type annotation using `scanpy` and `decoupler`.

## Overview

The goal of this notebook is to process raw single-cell RNA-seq data from bone marrow, identify distinct cell populations, and annotate them based on known cell type markers.

## Libraries Used

- `scanpy`: For single-cell data manipulation, quality control, normalization, dimensionality reduction, and clustering.
- `anndata`: Data structure for single-cell genomics data.
- `pandas`: For data manipulation and handling data frames.
- `decoupler`: For gene set enrichment analysis and automated cell type annotation.
- `igraph`: Graph-based clustering backend for `leiden`.

## Analysis Steps

1.  **Installation of Required Packages**: Installs `scanpy`, `anndata`, `igraph`, `celltypist`, and `decoupler`.
2.  **Data Loading**: Loads the `bone_marrow.h5ad` dataset, an AnnData object containing single-cell expression data.
3.  **Gene Name Standardization**: Converts Ensembl gene IDs to gene symbols to ensure compatibility with annotation resources.
4.  **Quality Control (QC)**: Calculates QC metrics, including mitochondrial, ribosomal, and hemoglobin gene percentages, and visualizes distributions to assess data quality.
5.  **Normalization and Logarithmization**: Normalizes cell counts to adjust for sequencing depth and applies a log1p transformation.
6.  **Feature Selection**: Identifies highly variable genes, which are essential for downstream analysis.
7.  **Dimensionality Reduction (PCA)**: Applies Principal Component Analysis to reduce the high-dimensional gene expression data into a smaller set of principal components.
8.  **Clustering**: Computes cell neighborhoods and performs Leiden clustering to group cells into distinct populations.
9.  **Automated Cell Type Annotation**: Utilizes `decoupler` with the PanglaoDB marker gene set to infer cell type identities for each cluster. This involves:
    -   Reloading PanglaoDB markers.
    -   Running ULM (Unbiased Logistic Regression Model) to calculate cell type activity scores.
    -   Ranking cell types within each cluster to assign the most prominent cell identity.
    -   Mapping cluster IDs to annotated cell types.
10. **Visualization**: Generates UMAP plots with cell type annotations and dot plots to visualize marker gene expression across annotated cell types.
