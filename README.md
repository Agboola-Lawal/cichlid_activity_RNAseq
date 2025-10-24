# cichlid_activity_RNAseq
Comparative RNA-seq analysis of diurnal and nocturnal cichlid species to identify brain gene expression patterns linked to activity cycles using DESeq2 and enrichment analysis.

## Project Overview

This repository contains the full RNA-seq workflow used to perform **differential gene expression (DGE)** analysis in *cichlid* brain samples.  
The project investigates the **molecular basis of diurnal and nocturnal activity patterns** across four species of African cichlids.

| Species | Abbreviation | Activity Pattern |
|----------|---------------|------------------|
| *Tropheops kumwera* | Tk | Diurnal |
| *Astatotilapia calliptera* | Ac | Diurnal |
| *Astatotilapia labrosus* | Al | Nocturnal |
| *Aulonocara stuartgranti* | As | Nocturnal |

RNA-seq data were processed and analyzed to identify differentially expressed genes (DEGs) and enriched biological pathways distinguishing diurnal and nocturnal species.

---

## Research Objectives

- Identify genes with significant expression differences between **diurnal** and **nocturnal** cichlids.  
- Discover **biological processes** and **molecular pathways** associated with circadian activity patterns.  
- Generate **visualizations and enrichment plots** suitable for publication and comparative genomics studies.

---

## Methods Summary

### 1. **Data Generation and Alignment**
- RNA was extracted from brain tissues of the four cichlid species.
- Raw reads were **quality-checked using [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/)**.
- Reads were aligned to the ***Maylandia zebra* reference genome (Ensembl)** using **[STAR aligner](https://github.com/alexdobin/STAR)**.
- Gene-level counts were obtained using **featureCounts**.

### 2. **Differential Expression Analysis**
- Conducted using **[DESeq2](https://bioconductor.org/packages/release/bioc/html/DESeq2.html)** in R.
- Design formula: 

comparing *diurnal* vs *nocturnal* species.
- Adjusted p-values were computed using the Benjamini–Hochberg method (FDR ≤ 0.05).

### 3. **Functional Enrichment**
- Gene Ontology (GO) and KEGG pathway analyses were performed with **[clusterProfiler](https://bioconductor.org/packages/release/bioc/html/clusterProfiler.html)**.
- Gene annotation was based on *Danio rerio* orthologs (via `org.Dr.eg.db`).

### 4. **Visualization**
- Data visualizations generated using:
- **ggplot2** → Volcano plots and summary plots  
- **pheatmap** → Expression clustering  
- **clusterProfiler** → Dot plots for GO and KEGG enrichment  

---

## Outputs

### Key Results
| Output Type | Description | Example Files |
|--------------|--------------|----------------|
| Differential Expression Tables | Significant genes for diurnal vs nocturnal | `results/up_diurnal.csv`, `results/down_diurnal.csv` |
| GO/KEGG Enrichment | Enriched biological processes and pathways | `results/GO_Enrichment_Results_up_diurnal.csv` |
| Visualization Plots | Publication-ready figures | `plots/GO_Enrichment_diurnal_up.png`, `plots/KEGG_pathway_enrichment_diurnal_up.png` |

---

## Repository Structure

cichlid_rnaseq/
│
├── README.md <- This file
├── cichlids_rnaseq.Rmd <- Main reproducible analysis script
│
├── data/
│ ├── cichlids_counts_data.csv <- Precomputed count matrix
│ ├── M_zebra_gene_info.csv <- Gene annotations
│
├── results/
│ ├── DESeq2_results.csv
│ ├── up_diurnal.csv
│ ├── down_diurnal.csv
│ ├── GO_Enrichment_Results_up_diurnal.csv
│ ├── KEGG_Enrichment_Results_up_diurnal.csv
│ ├── GO_Enrichment_Results_down_diurnal.csv
│ ├── KEGG_Enrichment_Results_down_diurnal.csv
│
├── plots/
│ ├── GO_Enrichment_diurnal_up.png
│ ├── KEGG_pathway_enrichment_diurnal_up.png
│ ├── GO_Enrichment_diurnal_down.png
│ ├── KEGG_pathway_enrichment_diurnal_down.png



---

## Reproducibility Instructions

### Install Required Packages
Run the following commands in R to install dependencies:
```r
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install(c("DESeq2", "clusterProfiler", "org.Dr.eg.db", "pheatmap"))
install.packages(c("tidyverse", "ggplot2", "RColorBrewer", "ggrepel"))
```
