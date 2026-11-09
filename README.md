# 🧬 Spatial Transcriptomics Analysis of Murine Knee Joint Aging and Osteoarthritis

**Author:** David Carro Vázquez, PhD  
**Affiliation:** Department of Orthopedic Surgery, University of California, San Francisco (UCSF)  
**Initial development:** April 2025  
**Programming language:** R

---

## 📖 Overview

This repository contains an R-based computational pipeline developed to investigate spatially resolved gene expression patterns in murine knee joint tissues, with particular emphasis on aging, sex-associated differences, and osteoarthritis-related joint injury.

The workflow integrates spatial transcriptomics datasets across experimental conditions and anatomical regions, combining quality control, normalization, dimensionality reduction, differential expression analysis, and functional interpretation.

The pipeline supports tissue-specific investigations of transcriptomic heterogeneity and the identification of molecular signatures associated with musculoskeletal aging and osteoarthritis.

## 🎯 Research Objectives

- Characterize gene expression patterns across anatomically distinct knee joint tissues.
- Identify aging-associated transcriptomic signatures.
- Investigate injury-associated gene expression alterations.
- Evaluate transcriptional variation associated with biological and experimental factors.
- Identify molecular pathways potentially involved in joint aging and osteoarthritis.
- Provide a documented computational framework for analyzing spatial transcriptomics datasets.

## 🔬 Biological Samples and Tissue Regions

The pipeline was developed for murine knee joint spatial transcriptomics datasets spanning different ages, sexes, and experimental injury conditions.

The code includes 16 sample identifiers and supports analysis of the following anatomical subregions:

- Femoral and tibial cartilage
- Femoral and tibial subchondral bone
- Synovium
- Infrapatellar fat pad
- Meniscus
- Femoral and tibial growth plate
- Femoral and tibial bone marrow

## ⚙️ Computational Workflow

### 1. Data Import and Barcode Quality Control

- Import 10x Genomics HDF5 gene expression matrices.
- Integrate spatial barcode annotations with sample metadata.
- Construct tissue-specific Seurat objects.
- Evaluate detected genes, total UMIs, mitochondrial transcript fraction, expression complexity, and highly abundant genes.
- Apply quality-control thresholds and generate diagnostic visualizations.
- Assess barcode consistency and expression matrix integrity.

### 2. Tissue-Specific Data Integration

- Organize samples by anatomical tissue region.
- Merge sample-level Seurat objects into tissue-specific datasets.
- Preserve raw expression counts and associated metadata.
- Validate assay layers, barcode identifiers, and merged expression matrices.

### 3. Normalization and Dimensionality Reduction

- Apply SCTransform normalization using Seurat.
- Adjust for specified technical covariates where configured.
- Perform principal component analysis (PCA).
- Generate UMAP embeddings for transcriptomic visualization.
- Examine principal component variance explained and highly variable genes.

### 4. Clustering and Transcriptomic Characterization

- Construct gene expression-based neighborhood graphs.
- Perform unsupervised clustering using Seurat.
- Visualize transcriptional heterogeneity across samples and tissue regions.
- Compare clustering patterns in relation to experimental metadata.

### 5. Pseudobulk Differential Expression Analysis

- Aggregate raw transcript counts by biological sample and tissue.
- Perform differential expression analysis using DESeq2.
- Evaluate experimental contrasts involving aging and injury.
- Generate differential expression statistics and gene expression visualizations.

### 6. Barcode-Level Differential Expression Analysis

- Apply MAST within Seurat to investigate gene expression differences at the spatial barcode level.
- Account for differences in gene detection rates using the configured statistical model.
- Identify candidate aging- and injury-associated genes.
- Compare expression signatures across anatomical regions.

Spatial barcodes are treated as spatial transcriptomic observations and do not necessarily correspond to individual cells.

### 7. Gene Set Enrichment Analysis

- Perform GSEA using `fgsea`.
- Retrieve curated mouse gene sets through `msigdbr`.
- Evaluate enrichment of biological pathways using ranked gene signatures.
- Integrate functional enrichment results with differential expression analyses.

### 8. Aging-Associated Transcriptomic Signatures

- Evaluate principal component loadings and their relationship to experimental metadata.
- Identify genes contributing to age-associated transcriptomic variation.
- Investigate tissue-specific molecular patterns associated with aging.
- Compare aging-related signatures across musculoskeletal compartments.

### 9. Quality Control and Variance Analysis

- Generate barcode- and gene-level QC summaries.
- Visualize expression distributions and sample-level variation.
- Quantify variance explained by principal components.
- Evaluate the contribution of experimental and technical variables to observed transcriptomic patterns.

---

## 📂 Input Data Structure

The workflow requires two principal input types.

**1. Gene expression matrices**

10x Genomics HDF5 files:

`{SampleID}_filtered_feature_bc_matrix.h5`

These files contain gene expression count matrices indexed by spatial barcodes.

**2. Tissue-specific barcode annotations**

Excel files:

`{SampleID}_{Subregion}.xlsx`

The first column contains spatial barcode identifiers, while additional columns provide sample and tissue metadata.

The R workflow matches barcode identifiers between the expression matrices and annotation tables to construct tissue-specific Seurat objects.

## 🧰 Software Requirements

**Language:** R

**Core packages:**

- Seurat
- SeuratObject
- sctransform
- Matrix
- readxl
- dplyr
- data.table
- ggplot2
- patchwork
- DESeq2
- MAST
- fgsea
- msigdbr
- knitr
- kableExtra
- htmltools

The pipeline uses R Markdown to organize analytical steps and generate reports containing tables and figures.

## ▶️ Running the Pipeline

1. Install the required R and Bioconductor packages.
2. Obtain compatible 10x Genomics expression matrices and spatial barcode annotation files.
3. Configure the input data directory in the R Markdown script.
4. Define sample identifiers and anatomical subregions.
5. Execute the analytical sections in their documented order.
6. Review generated quality-control summaries, differential expression results, and downstream visualizations.

**Note:** The workflow contains dataset-specific configuration parameters and may require adaptation before use with independent datasets.

## 📊 Data Availability

Raw sequencing data, spatial barcode annotation files, and sample-level expression matrices are not distributed through this repository.

The repository is intended to document the computational methods and analytical implementation. Reproduction of the original analyses requires access to the corresponding research datasets.

## 👨‍🔬 Author and Computational Contributions

**David Carro Vázquez, PhD**  
Department of Orthopedic Surgery  
University of California, San Francisco

The repository documents the development and implementation of computational workflows for:

- Spatial transcriptomics preprocessing and quality control.
- Integration of multi-sample and tissue-specific datasets.
- Normalization, clustering, and dimensionality reduction.
- Pseudobulk and barcode-level differential expression analysis.
- Gene set enrichment and functional interpretation.
- Identification of aging-associated transcriptomic signatures.
- Statistical visualization and reproducible analytical reporting.

## 📜 License

See the repository's `LICENSE` file for applicable licensing terms.

## 📬 Contact

**David Carro Vázquez, PhD**  
GitHub: https://github.com/davicarro

For questions about the computational workflow or potential scientific collaborations, please contact the repository author through GitHub.
