# Data-driven guidelines for high-quality CUT&Tag experiments


Analysis code associated with the manuscript:

**Data-driven guidelines for high-quality CUT&Tag experiments**

This repository contains the computational scripts used to benchmark CUT&Tag and ChIP-seq datasets across transcription factors and histone modifications. The study evaluates how sequencing depth, peak-calling strategy, assay technology, and data representation influence chromatin profiling results.

## Repository contents

Analysis scripts are provided in:

`02152024_CUTnTagQC/`

The repository preserves the code used for the analyses reported in the manuscript, including preprocessing, peak calling, sequencing-depth benchmarking, peak-level quality assessment, motif analysis, cross-assay comparisons, and statistical analyses.

Major analyses include:

- read alignment and filtering
- fragment generation for paired-end sequencing data
- peak calling with MACS2, SICER2, and SEACR
- repeated sequencing-depth downsampling
- FRiP score calculation
- peak number and genomic coverage analysis
- peak-length analysis
- CTCF motif enrichment and summit-to-motif distance analysis
- comparison of shared and assay-specific genomic regions
- CTCF peak recurrence and occupancy analysis
- genomic annotation of peak groups
- PCA of binary peak distributions and quantitative signal profiles
- pairwise Jaccard similarity analysis
- pairwise Pearson correlation analysis
- multivariable modeling of factors affecting sample similarity
- leave-one-sample-out jackknife estimation of confidence intervals

## Data

All CUT&Tag and ChIP-seq datasets analyzed in this study were obtained from public repositories, including the **Gene Expression Omnibus (GEO)** and **Sequence Read Archive (SRA)**.

The complete list of datasets, accession numbers, cell types, targets, and experimental metadata is provided in **Supplementary Table S1** of the associated manuscript.

Raw sequencing data are not redistributed in this repository.

## Analysis overview

### Sequencing-depth benchmarking

CUT&Tag and ChIP-seq datasets were randomly downsampled to multiple sequencing depths. Repeated subsampling was used to evaluate the effects of sequencing depth on metrics including FRiP score, peak number, genomic coverage, and motif-associated peak recovery.

Analyses were performed for CTCF and multiple histone modifications, including H3K4me3, H3K27ac, H3K4me1, H3K27me3, H3K36me3, and H3K9me3.

### Peak calling

Peak-calling performance was evaluated using:

- MACS2
- SICER2
- SEACR

The analyses examine how peak-calling strategy influences peak recovery and downstream quality metrics.

### CTCF peak-distribution similarity

CTCF peaks across datasets and peak callers were merged and divided into 300-bp genomic intervals. A binary peak-by-sample matrix was generated based on the presence or absence of peaks within each interval.

Pairwise peak-distribution similarity was quantified using the Jaccard index:

\[
J(A,B)=\frac{|A\cap B|}{|A\cup B|}
\]

Jaccard similarities were logit-transformed and analyzed using multivariable linear models to estimate the independent contributions of cell type, assay technology, peak caller, and treatment group.

### Quantitative CTCF signal similarity

Quantitative CTCF signal was compared across merged peak regions. Pairwise Pearson correlations were calculated using the 50,000 most variable regions and transformed using the Fisher z transformation:

\[
z=\operatorname{atanh}(r)
\]

Multivariable linear models were used to evaluate the effects of cell type, assay technology, and treatment on quantitative signal similarity.

For pairwise similarity analyses, uncertainty was estimated using a **leave-one-sample-out jackknife** procedure to account for the repeated contribution of individual samples to multiple sample pairs.

## Software

Major command-line tools used in the analyses include:

- Bowtie2
- SAMtools
- BEDTools
- MACS2
- SICER2
- SEACR
- featureCounts
- deepTools

Major R packages include:

- tidyverse
- dplyr
- tidyr
- ggplot2
- Matrix
- FactoMineR
- factoextra
- pheatmap
- broom
- forcats
- stringr

## Reproducibility

The scripts in this repository correspond to the analyses used to generate the results and figures in the associated manuscript.

Many scripts contain file paths and computational settings specific to the original high-performance computing environment. Users reproducing the analyses should modify input paths, reference genome locations, sample metadata, and computational resource settings as appropriate.

The human reference genome assembly used in this study was **hg38**.

## Citation

If you use the code or analytical workflow from this repository, please cite:

**Tian M, Chen Q, Hu SS, Zang C. Data-driven guidelines for high-quality CUT&Tag experiments.**

Citation details will be updated following publication.

## License

This repository is released under the **MIT License**.

## Contact

For questions regarding the code or analysis, please open an issue in this repository.
