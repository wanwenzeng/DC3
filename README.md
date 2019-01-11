# dcHiChIP

## Introduction
With the rapid development of single-cell genomics technology, researchers are now able to study heterogeneous mixtures of cell populations. 
For example, scRNA-seq enables single cell gene expression profiling and scATAC-seq identifies accessible chromatin regions in single cells. 
If these two types of sc-genomics experiments are performed on different samples from the same cell population, then both samples are informative on the same constituent subpopulations, and the analysis of one sample should be informed by the result of the analysis on the other sample. 
Recently Duren et al. proposed a coupled NMF (coupled non-negative matrix factorization) method to cluster cells in each sample and to infer both the expression profile and accessibility profile of each subpopulation. 
These two profiles reveal a great deal about the subpopulation of cells: the accessible regions identify the active regulatory elements (RE) while the expression profiles identify actively transcribed genes. 
However, to infer gene regulatory relations, it is necessary to link an accessible RE to the set of target genes that it regulates. 
While combinatorial indexing has been used for three-dimensional (3D) contact measurement in single cells, it is currently still difficult to perform and not widely used. 
On the other hand, in bulk sample it is easy to establish linkage of active enhancers to their target genes by H3K27ac HiChIP experiments. 
Therefore, it is of considerable scientific significance to be able to deconvolve the bulk sample HiChIP signal (i.e., bulk sample loop counts) into subpopulation-specific HiChIP signals, based on the joint analysis of the following three types of data from separate samples from the same cell population: scRNA-seq, scATAC-seq, bulk H3K27ac HiChIP. 
Here, we introduce dcHiChIP (for deconvolution of HiChIP) for the solution of this problem. 
Based on simulation experiments and biological experiments, it is shown that this method can decompose bulk HiChIP loop counts into subpopulation-specific loop counts. At the same time, the subpopulation-specific loop counts in turn lead to improved clustering results in the scRNA-seq and scATAC-seq data.
