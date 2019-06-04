---
title: "Single-cell RNA-seq: Generation of count matrix"
author: "Mary Piper, Lorena Pantano, Meeta Mistry, Radhika Khetani, Rory Kirchner"
---

*NOTE: This lesson was adapted from [Dr. Mary Piper's presentation](https://github.com/marypiper/WIB_scRNA-seq#wib_scrna-seq) for the [Boston-area Women's Bioinformatics Meetup](https://www.meetup.com/boston-area-womens-bioinformatics/).*

# Single-cell RNA-seq analysis workflow

<img src="../img/sc_workflow.png" width="800">

## Count matrix generation

The scRNA-seq method will determine how to generate the count matrix using technology-specific methods to parse the barcodes and UMIs from the sequencing reads so as to delineate the cells and the transcripts. 

'[**umis**](https://github.com/vals/umis) provides tools for estimating expression in RNA-seq data which performs
sequencing of end tags of transcript, and incorporate molecular tags to
correct for amplification bias.' The steps in this process include the following:

 1. Formatting reads and filtering noisy cellular barcodes
 2. Demultiplexing the samples
 3. Pseudo-mapping to cDNAs
 4. Counting molecular identifiers 
 
<img src="../img/sc_collapsing_umis.png" width="400">

The generation of the count matrix from the raw sequencing data follow the steps in the schematic below for many of the scRNA-seq methods. 

<img src="../img/sc_pre-QC_workflow.png" width="800">

***

Following the generation of count matrix, the remaining steps can be performed using [Seurat](https://satijalab.org/seurat/#about-seurat), the R toolkit for single cell genomics. A tutorial for the remaining steps can be [found here](https://satijalab.org/seurat/v3.0/pbmc3k_tutorial.html), and requires a good working knowledge of R.

## Filtering

Poor quality cells can be filtered out of the count matrix data before moving forward. Poor quality cells often have the following characteristics: 
* a low number of genes or UMIs
* high mitochondrial gene expression indicative of dying cells
* low number of genes per UMI. 

## Clustering

After removing the poor quality cells, the cells can now be clustered based on similarities in transcriptional activity, with the idea that the different cell types separate into the different clusters. The following steps can be followed to perform clustering:

1. **Normalization and transformation** of the raw gene counts per cell to account for **differences in sequencing depth** per cell.
2. Identification of high variance genes.
3. **Regression of sources of unwanted variation** (e.g. number of UMIs per cell, mitochondrial transcript abundance, cell cycle phase).
4. **Identification of the primary sources of heterogeneity** using principal component (PC) analysis and heatmaps.
5. **Clustering cells** based on significant PCs.

To visualize the clusters, there are a few different options that can be helpful, including t-distributed stochastic neighbor embedding (t-SNE), Uniform Manifold Approximation and Projection (UMAP), and PCA. The goals of these methods is to have similar cells closer together in low-dimensional space.

<img src="../img/tSNE.png" width="600">

## Marker identification

After clustering, genes that are markers for different clusters can be used to help identify the cell type of each cluster. Finally, after identification of cell types, there are various types of analyses that can be performed depending on the goal of the experiment.

<img src="../img/tSNE-labelled3.png" width="600">

***

*This lesson was adapted from [Dr. Mary Piper's presentation](https://github.com/marypiper/WIB_scRNA-seq#wib_scrna-seq) for the [Boston-area Women's Bioinformatics Meetup](https://www.meetup.com/boston-area-womens-bioinformatics/).*

*This lesson has been developed by members of the teaching team at the [Harvard Chan Bioinformatics Core (HBC)](http://bioinformatics.sph.harvard.edu/). These are open access materials distributed under the terms of the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0), which permits unrestricted use, distribution, and reproduction in any medium, provided the original author and source are credited.*
