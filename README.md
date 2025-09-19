# RNA-Seq Differential Expression Analysis (DESeq2-based)

This repository contains a complete RNA-seq analysis pipeline using the human reference genome (hg38), from raw FASTQ files to differential expression results, annotation, and visualization.


## 🧬 Pipeline Overview

1. **Reference Genome Preparation**
   - Extract main chromosomes from `BSgenome.Hsapiens.UCSC.hg38`
   - Write to FASTA and index using `Rsubread::buildindex`

2. **Annotation File Preparation**
   - Extract exons from `TxDb.Hsapiens.UCSC.hg38.knownGene`
   - Generate a SAF-format annotation file

3. **Read Alignment**
   - Align paired-end FASTQ reads using `Rsubread::align`
   - Sort and index BAM files using `Rsamtools`

4. **Counting Reads**
   - Use `GenomicAlignments::summarizeOverlaps` to count reads over gene exons

5. **Differential Expression Analysis**
   - Create `DESeqDataSet` object
   - Perform normalization and DE analysis using `DESeq2`
   - Run pairwise contrasts (e.g., 24H_ROSA vs 24H_DMSO)

6. **Gene Annotation**
   - Map ENTREZ IDs to gene symbols using `org.Hs.eg.db`

7. **Visualization**
   - PCA plot of samples using `plotPCA()` and `prcomp()`
   - Volcano plot with `EnhancedVolcano`
   - Expression scatterplot of top 50 DE genes using `ggplot2`

8. **Export**
   - Annotated count matrices and DE results exported as `.xlsx`

## 📦 R Packages Used

- `BSgenome.Hsapiens.UCSC.hg38`
- `TxDb.Hsapiens.UCSC.hg38.knownGene`
- `Rsubread`
- `GenomicAlignments`
- `Rsamtools`
- `DESeq2`
- `org.Hs.eg.db`
- `AnnotationDbi`
- `EnhancedVolcano`
- `ggplot2`
- `openxlsx`
- `BiocParallel`

## 🧪 Sample Contrasts

- `24H_ROSA` vs `24H_DMSO`
- `48H_ROSA` vs `48H_DMSO`

## 📊 Outputs

- Differential expression tables (`.xlsx`)
- Volcano plots and PCA plots (`.png`, `.pdf`)
- Count matrix (`Genecount.xlsx`)
- Normalized expression matrix (`rlog`)

## 🔧 Requirements

- R ≥ 4.2
- Bioconductor ≥ 3.16
- ~8–16 GB RAM for alignment and counting
- Reference genome installed: `BSgenome.Hsapiens.UCSC.hg38`

## 📑 Notes
- Ensure paired-end FASTQ files follow standard naming convention (`*_1.fastq.gz`, `*_2.fastq.gz`)
- Perform QC of the sample files prior to analysis, using FastQC in Python
- SAF file is built from single-exon genes; modify if working with alternative splicing
- To improve volcano and heatmap labeling, consider customizing with significant gene names




