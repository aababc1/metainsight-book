# Differential (transcriptional) expression analysis 

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_9_1.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>  
</figure>

*To perform the following analysis, you should have the same gene set.

By using metatranscriptomic data from different environmental conditions, you can analyze the differences in gene expression based on the specific environmental conditions and obtain information on which genes are up- or down-regulated in each condition. To achieve this, DESeq2 is run using count information generated from the alignment results and functional annotation locus tags.
However, for DESeq2 to work, you need count information and input files for each sample's metadata.
The metadata information can be used in DEG (Differentially Expressed Gene) analysis and various visualization steps.

```bash
#Download FormatDESeqInput.py
$wget https://raw.githubusercontent.com/sujin9819/ngs/main/R_scripts/coverage.R
#make DESeq2 input file
$Rscript coverage.R –r $sample 
#Outputs a result corresponding to the sample keyword
```
`make design sheet(text파일 생성)`  
`File name: Design_Sheet.txt  `  
| Sample | Condition |
| --- | --- |
| cov1 | Control group |
| cov2 | Control group |
| cov3 | Experimental group |
| cov4 | Experimental group |
 

The following DESeq2 code allows you to obtain normalized count values for each gene and DESeq results from comparisons between groups. Genes with a Log2 Fold Change > 1 or < -1 and a p-value < 0.05 are selected. This information enables you to assess differences in gene expression between different environments and explore the similarity between samples, such as PCoA and α-diversity based on each RNA sample. You can visualize this data through clustering, PCoA plots, and other visual representations.
```R
#install DESeq2 package
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("DESeq2")
```

```bash
#DESeq2 running
#R script download
$wget https://raw.githubusercontent.com/sujin9819/ngs/main/R_scripts/RunDESeq_flow.R
$ Rscript RunDESeq_flow.R –i $sample.count –d Design_sheet.txt –o output_directory     
```

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_9_2.png?raw=true" style="width:90%">
  <figcaption><b>Example of output file using RunDESeq_flow.R</b></figcaption>  
</figure>

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_9_3.png?raw=true" style="width:90%">
  <figcaption><b>Example of results using RunDESeq_flow.R</b></figcaption>  
</figure>

Moreover, you can utilize R packages to visualize information related to gene expression, including normalized count data, Log2 Fold Change, and p-values, through visualizations like heatmaps and volcano plots.

### References

Love MI, Huber W, Anders S. Moderated estimation of fold change and dispersion for RNA-seq data with DESeq2. *Genome Biol*. 2014;15(12):550. doi:10.1186/s13059-014-0550-8

Ingolia NT, Ghaemmaghami S, Newman JR, Weissman JS. Genome-wide analysis in vivo of translation with nucleotide resolution using ribosome profiling. *Science*. 2009;324(5924):218-223. doi:10.1126/science.1168978

Ingolia NT. Ribosome profiling: new views of translation, from single codons to genome scale. *Nat Rev Genet*. 2014;15(3):205-213. doi:10.1038/nrg3645

Li H, Handsaker B, Wysoker A, Fennell T, Ruan J, Homer N, Marth G, Abecasis G, Durbin R. The Sequence Alignment/Map format and SAMtools. *Bioinformatics*. 2009;25(16):2078-2079. doi:10.1093/bioinformatics/btp352

Huerta-Cepas J, Szklarczyk D, Forslund K, Hedges LM, Lehmann G, Sasson O, Moreno-Escamilla V, Damashash R, Forslund SJ, Petersen TN, von Mering C, Bork P, Huerta-Cepas J. eggNOG 4.5: a hierarchical orthology framework with improved functional annotations for eukaryotic, archaeal and bacterial proteins. *Nucleic Acids Res*. 2016;44(D1):D286-D293. doi:10.1093/nar/gkv1248
