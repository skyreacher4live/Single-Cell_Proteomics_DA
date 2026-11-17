# Methods notes

All data are simulated. Planted effects exist only to test whether the workflow recovers known signals.

## Synthetic design
8,124 cells x 3,217 protein features; 8 donors (4 Control, 4 FTD); five cerebellar cell classes. Log2-like abundance = baseline + cell-type effect + donor effect + planted FTD effects + cell-level noise. Missingness is abundance-dependent (low abundance, higher dropout).

## Quality control
Cells are kept if they quantify at least 70% of the median observed protein count. Proteins are kept if detected in at least 50% of retained cells.

## Normalisation
Per-cell median centring on the log2 scale. Assumes most proteins do not shift globally in one direction.

## Embedding
Remaining missing values are median-imputed per protein for embedding only (never for testing). The 1,500 most variable proteins are scaled, then PCA (30 components), neighbourhood graph (15 neighbours, 25 PCs), UMAP and Leiden clustering (resolution 0.6).

## Annotation
Clusters are labelled by mean abundance of marker panels and compared with simulated truth (ARI, accuracy).

## Differential abundance
Donor-level pseudobulk (mean observed normalised abundance per donor x cell type), Welch t-test between FTD and Control donors, Benjamini-Hochberg FDR within each cell type. Cells are not treated as independent replicates.

## Benchmark
Planted effects are compared with results (direction recovered, FDR < 0.05).

## Reference
Davis, S., Scott, C., Ansorge, O., & Fischer, R. (2019). Development of a Sensitive, Scalable Method for Spatial, Cell-Type-Resolved Proteomics of the Human Brain. Journal of Proteome Research, 18(4), 1787–1795. https://doi.org/10.1021/acs.jproteome.8b00981.
