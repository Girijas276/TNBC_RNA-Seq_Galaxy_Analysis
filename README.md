## Differential Gene Expression Analysis in TNBC through RNA-Seq

RNA-seq differential expression analysis of Triple-Negative Breast Cancer using Galaxy (GSE267442)

## Background

Breast cancer is the most common cancer among Indian women, and triple-negative breast cancer (TNBC) the most aggressive subtype. It is disproportionately prevalent in India, accounting for 20–31% of cases compared to 12–15% in Western populations. Because TNBC lacks the ER, PR, and HER2 receptors that current targeted therapies rely on, treatment options remain limited. Differential expression studies like this one help identify the genes driving TNBC, which is a first step toward finding new therapeutic targets.

## Dataset

This analysis uses the publicly available RNA-seq dataset **GSE267442** from the Gene Expression Omnibus (GEO), consisting of 16 samples: tumor and adjacent normal tissue from 4 TNBC and 4 non-TNBC patients. The dataset is linked to a published study ([PMID: 41299328](https://www.ncbi.nlm.nih.gov/pubmed/41299328)) that used multi-omics analysis (RNA-seq + whole-exome sequencing) to identify "CLIC3" as a TNBC-specific prognostic biomarker and therapeutic target. This dataset was used here independently for practice and skill-building in RNA-seq differential expression analysis, using a DESeq2-based pipeline rather than the original study's approach.

## Pipeline / Methods

- **FastQC** - checked quality of raw sequencing reads
- **Trimmomatic** - trimmed adapters and low-quality bases
- **FastQC** - re-checked quality of trimmed reads
- **MultiQC** - consolidated FastQC reports across all samples into one summary
- **HISAT2** - aligned reads to the reference genome (**hg38**)
- **featureCounts** - counted aligned reads per gene using the BAM files and gene annotation (GTF)
- **DESeq2** - identified differentially expressed genes between TNBC and normal conditions
- **g:Profiler** - performed functional enrichment analysis and annotated gene IDs with gene names
- **STRING** - built a protein-protein interaction network from the DEGs
- **cytoHubba** - ranked network genes by connectivity (MCC method) to identify top hub genes
- **cBioPortal** - performed survival analysis on the identified hub genes/proteins

## Key Results

Differential expression analysis using DESeq2 identified **3,319 DEGs** between TNBC and normal tissue**1,757 upregulated** and **1,563 downregulated**. The top 200 genes from each group were used to build a protein-protein interaction network in STRING, and cytoHubba (MCC method) identified the top 10 hub genes in each direction:

- **Upregulated hub genes:** NEK2, CDCA8, CDK1, KIF2C, CENPF, BUB1, KIF20A, CCNA2, KIF11, KIF4A
- **Downregulated hub genes:** ESR1, KIT, MME, GATA3, KRT14, FGF2, ABCG2, GPC3, PTN, AGTR1

Survival analysis in cBioPortal (TCGA BRCA cohort) showed that high expression of **NEK2, BUB1, CCNA2, and KIF4A** was associated with poorer overall survival among the upregulated hub genes, while **ESR1, GATA3, and KIT** showed a similar poor-survival trend among the downregulated genes. These findings suggest these hub genes may serve as potential prognostic markers or therapeutic targets in TNBC.

## Files in this Repo

| File | Description |
| `FastQC_report.zip` | Raw read quality report (FastQC), one representative sample |
| `MultiQC_report.html` | Consolidated QC summary across all samples (post-trimming) |
| `HISAT2_alignment_summary.txt` | Alignment summary, one representative sample |
| `featureCounts_summary.tabular` | Read-counting summary |
| `DESeq2_results.txt` | Full DEG results table (3,319 genes: gene ID, log2FC, p-value) |
| `DESeq2_plots.pdf` | DESeq2 diagnostic plots (e.g. MA-plot/PCA) |
| `normalized_counts.tabular` | Normalized expression counts across samples |
| `pathway_upregulated.tabular` | Pathway enrichment results, upregulated genes |
| `pathway_downregulated.tabular` | Pathway enrichment results, downregulated genes |
| `annotated_gene_IDs.tabular` | Gene ID to gene name annotation |
| `hub_upregulated_gene_network.png` | Hub gene protein-protein interaction network (upregulated genes) |
| `hub_upregulated_gene_rankings.csv` | Hub gene rankings, upregulated (cytoHubba/Cytoscape export) |
| `hub_downregulated_gene_network.png` | Hub gene protein-protein interaction network (downregulated genes) |
| `hub_downregulated_gene_rankings.csv` | Hub gene rankings, downregulated (cytoHubba/Cytoscape export) |
| `volcano_plot.pdf` | Volcano plot of DEGs (up/down/not significant) |

## Tools & Skills Demonstrated

- RNA-seq data analysis (Galaxy platform)
- Quality control: FastQC, MultiQC
- Read trimming and alignment: Trimmomatic, HISAT2
- Gene quantification: featureCounts
- Differential expression analysis: DESeq2
- Functional enrichment analysis: g:Profiler
- Protein-protein interaction network analysis: STRING, Cytoscape, cytoHubba
- Survival analysis: cBioPortal (TCGA BRCA cohort)
- Working with public genomics data: NCBI GEODifferential Gene Expression Analysis in TNBC through RNA-Seq
   
