# Standard Operating Procedure for Next-Generation Sequencing (NGS)-Based Translatome Analysis

## Introduction to Translatome


Transcriptomics and proteomics analyses provide more accurate information about the biological factors of microorganisms within an ecosystem. In microbiome research, both metatranscriptomics and translatome analysis help in the precise functional analysis of microbial communities that form clusters.
While metatranscriptomic data offer insights into the expression and activity of genes in the environment, translatome information includes protein synthesis levels and translational regulation data. As a result, translatome data can differ from metatranscriptomic data.
In translatome analysis, ribosome profiling and related sequencing techniques are used to study protein synthesis within microbial communities. This involves the analysis of ribosome-protected mRNA fragments to determine which genes are actively being translated, providing direct measurements of protein synthesis rates.
While translatome analysis provides a functional perspective complementary to metagenomics, it captures the translational state of microbial communities at a specific point in time. This snapshot reveals which genes are actively being translated, providing insights into the functional phenotype of the community under specific environmental conditions.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_0_1.png?raw=true" style="width:90%">
  <figcaption><b>Multi-omics information-based microbiome functional analysis</b></figcaption>  
</figure>

## Ribosome Profiling: Ribo-seq in Translatome Analysis

Ribo-seq is a powerful technique for translatome analysis that applies sequencing technology to study ribosome-protected mRNA sequences.
In this method, cells are treated with chloramphenicol to arrest ribosomes in their translational positions, and MNase (micrococcal nuclease) is used to digest RNA that is not protected by ribosomes.
The sequencing is then performed on the mRNA sequences actively involved in protein synthesis, providing a direct measurement of translation rates across the genome.
Ribo-seq was originally developed by [](doi:10.1126/science.1168978) and has since become the gold standard technique for profiling translation genome-wide. A comprehensive review of ribosome profiling methods is provided by [](doi:10.1038/nrg3645).
The technique has been employed to investigate how protein synthesis changes across diverse organisms and conditions. Ribo-seq allows the quantification of translation rates by measuring ribosome occupancy at each mRNA position.
This technique provides direct insights into which genes are actively being synthesized and at what rates, allowing for accurate quantification of protein synthesis.
Furthermore, an extension of this approach called MetaRibo-seq has been developed to apply ribosome profiling to complex microbial communities [](doi:10.1038/s41564-020-0714-2), making it a valuable tool for translatome analysis in environmental and clinical samples preserved in RNALater.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_0_2.jpg?raw=true" style="width:90%">
  <figcaption><b>Translatome analysis workflow including MetaRibo-seq ; <a href="https://doi.org/10.1038/s41467-020-17081-z">[ref]</a></b></figcaption>  
</figure>

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_0_3.jpg?raw=true" style="width:90%">
  <figcaption><b>Ribosome profiling workflow ; <a href="https://doi.org/10.1073/pnas.1614788113">[ref]</a></b></figcaption>
</figure>

