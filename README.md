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

## Preprocessing
For preprocessing the scRNA-seq data, please following the standard processing pipline to get the expression matrix, where each row represents a gene, each column represents a cell.

For preprocessing the scATAC-seq data, please first put all the .bam files for each cell into a folder. Then run the preprossing script we provided to get the the openness matrix, O and enhancer name. 

For preprocessing the HiChIP data, please restrict HiChIP enhancer-promoter interactions in the genes in scRNA-seq data and enhancers in scATAC-seq data. The first column indicates the index of gene, the second column indicates the index of enhancer, the third column indicates the HiChIP loop counts. We recommend use HiC-pro and hichipper to preprocess the HiChIP data. 


## Running dcHiChIP
**dcHiChIP receives 8 parameters:**

* -k         the clustering numbers

* -O         the location of O matrix

* -E         the location of E matrix

* -G_symbol  the location of gene symbol file

* -E_symbol  the location of enhancer symbol file

* -hichip    the location of HiChIP enhancer-promoter interactions file 

* -lambda1   the hyper-paramters lambda1 to control term of the NMF for E 

* -lamdba2   the hyper-paramters lambda2 to control coupled term

Note:-k, -O, -E, -G_symbol, -E_symbol, -hichip are the must-have parameters; 
-lambda1, -lamdba2 are optional parameters. If dcHiChIP does not receive -lambda1 and -lambda2, it will choose the best parameters automatically.

**dcHiChIP outputs 4 files:**

* scATAC-result.txt                       the clustering results for scATAC-seq

* scRNA-result.txt                        the clustering results for scRNA-seq

* cluster-hichip.txt                      the cluster-specific hichip

* cluster-specific-peaks-genes-pairs.txt  the cluster-specific peak-gene pairs. First column is the gene name, second column is the peak name, the third column is the p-value for gene and last column is the p-value for peak. 



### Example

```
python dcHiChIP.py -k 2 -E exampledata/E.txt -O exampledata/O.txt -G_symbol exampledata/gene.txt -E_symbol exampledata/enhancer.txt -hichip exampledata/hichip.txt  -lambda1 0.04 -lambda2 25

```


## Requirements
* sklearn
* pandas
* scipy
* itertools
* argparse 
* itertools
* MACS



**For any questions about the algorithm, please contact <zengww14@mails.tsinghua.edu.cn> or <zduren@stanford.edu>.**
