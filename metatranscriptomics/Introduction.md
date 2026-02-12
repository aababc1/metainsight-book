# Standard Operating Procedure for Next-Generation Sequencing (NGS)-Based Metatranscriptome Analysis

## Introduction to Metatranscriptome

The term microbiome refers to the concept encompassing a community of microorganisms (microbiota) residing in a particular environment, along with their complete genetic information. Microbiome research traditionally involves the amplification and sequencing of conserved regions of marker genes, such as ribosomal genes, from environmental DNA using PCR, allowing for the identification of the types of microorganisms present in the environment. In contrast, microbiome research utilizes whole DNA sequence analysis, known as metagenome sequencing, which not only identifies the types of microorganisms present in the environment but also enables the exploration of the genetic diversity and functions possessed by these microorganisms. However, metagenomic (metagenome) data can inform about the presence or absence of specific species or genes but cannot determine whether they are active within the microbiome ecosystem, posing limitations.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_0_1.png?raw=true" style="width:90%">
  <figcaption><b> Multi-omics information-based microbiome functional analysis</b></figcaption>  
</figure>

To investigate how microbial communities respond to environmental changes, metatranscriptome analysis has been initiated, and metatranscriptomic information will play a crucial role in understanding the ecology of the microbiome. Even before the advent of high-throughput DNA sequencing methods, research has been conducted to measure the expression levels of genes of interest using qPCR and to study the expression patterns of known transcripts from specific organisms using microarray technology. With the widespread adoption of Next-Generation Sequencing (NGS) technology, RNA sequencing (RNA-seq) has not only allowed for the measurement of the expression levels of known transcript targets but has also made it possible to obtain information on the entire transcriptome, including previously unknown transcripts and transcript variants, such as non-coding RNAs, in a specific environment. For these reasons, RNA-seq is increasingly prevalent in microbiome research and finds applications in various fields, including gene expression analysis, identification of highly active microbial community members, discovery of regulatory factors, investigation of microbial interactions, and studies on interactions with hosts.

Based on these requirements, RNA-seq is being increasingly utilized in microbiome research. In this Standard Operating Procedure (SOP), we aim to describe reference-guided metatranscriptome analysis and reference-independent metatranscriptome analysis methods based on mapping RNA-seq reads to de novo assembled contigs and metagenome-assembled genomes (MAGs) obtained from metagenomes.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_0_2.png?raw=true" style="width:65%">
  <figcaption><b>Reference-guided and reference-independent metatranscriptome analysis methods</b></figcaption>  
</figure>

Before diving into this comprehensive SOP, various tools that can be utilized for metatranscriptome analysis are introduced. In addition to the tools presented in this SOP, other tools listed in Table 1 or similar tools with similar purposes can be selectively applied at each step.

**Table 1. List of available RNA-seq analysis tools**
<table>
<thead>
  <tr>
    <th>Category</th>
    <th>Tools</th>
    <th>Description</th>
    <th>Year</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="3">Trimming</td>
    <td><a href="https://cutadapt.readthedocs.io/en/stable/">cutadapt</a></td>
    <td>5' adaptor trimming</td>
    <td>2011</td>
  </tr>
  <tr>
    <td><a href="https://github.com/FelixKrueger/TrimGalore">TrimGalore</a></td>
    <td>Wrapper around Cutadapt and FastQC<br>paired-end trimming</td>
    <td>2013</td>
  </tr>
  <tr>
    <td><a href="http://www.usadellab.org/cms/?page=trimmomatic">trimmomatic</a></td>
    <td>Paired-end trimming</td>
    <td>2014</td>
  </tr>
  <tr>
    <td rowspan="5">Alignment</td>
    <td><a href="https://bowtie-bio.sourceforge.net/bowtie2/manual.shtml">bowtie2</a></td>
    <td>Short read mapping, local alignment, use FM-index algorithm</td>
    <td>2012</td>
  </tr>
  <tr>
    <td><a href="https://github.com/lh3/bwa">BWA</a></td>
    <td>Low-divergent sequences mapping, need genome reference, use BWT and FM index algorithm</td>
    <td>2009</td>
  </tr>
  <tr>
    <td><a href="https://daehwankimlab.github.io/hisat2/manual/">HiSat2</a></td>
    <td>Highly useful for human data analysis. Utilized in tasks like Human Leukocyte Antigen (HLA) typing and DNA fingerprinting. Use the FM index.</td>
    <td>2019</td>
  </tr>
  <tr>
    <td><a href="https://github.com/alexdobin/STAR">STAR</a></td>
    <td>Improve <em>de novo</em> RNA-seq analysis and allow for the mapping of long-read mRNA data.</td>
    <td>2013</td>
  </tr>
  <tr>
    <td><a href="https://ccb.jhu.edu/software/tophat/manual.shtml">TopHat2</a></td>
    <td>Bowtie-based short read mapping</td>
    <td>2013</td>
  </tr>
  <tr>
    <td rowspan="6">DE analysis</td>
    <td><a href="https://cole-trapnell-lab.github.io/cufflinks/manual/">Cuffdiiff2</a></td>
    <td>cufflink-associated tool. utilize sam(bam)file to compare gene and isoform expression </td>
    <td>2013</td>
  </tr>
  <tr>
    <td><a href="https://bioconductor.org/packages/release/bioc/html/DESeq2.html">DESeq2</a></td>
    <td>R package, employ shrinkage estimation techniques and utilizes RLE (Relative Log Expression) normalization.</td>
    <td>2014</td>
  </tr>
  <tr>
    <td><a href="https://bioconductor.org/packages/release/bioc/html/edgeR.html">EdgeR</a></td>
    <td>R package, Use raw count value as input file. TMM(Trimmed Mean M-values) normalization ���</td>
    <td>2010</td>
  </tr>
  <tr>
    <td><a href="https://bioconductor.org/packages/release/bioc/html/limma.html">limma</a></td>
    <td>R package. Effective for a small number of samples, using TMM normalization</td>
    <td>2015</td>
  </tr>
  <tr>
    <td><a href="https://www.bioconductor.org/packages/release/bioc/html/NOISeq.html">NOISeq</a></td>
    <td>R package. Using a nonparametric approach and an RPKM/TMM/uppartile normalization approach</td>
    <td>2011</td>
  </tr>
  <tr>
    <td><a href="https://github.com/jefferys/SamSeq">SAMSeq</a></td>
    <td>R package. Gene-level DE analysis using sam file as input file. Normalization based on the mean value of the total count</td>
    <td>2013</td>
  </tr>
  <tr>
    <td rowspan="3"><em>de novo</em> assembly</td>
    <td><a href="https://github.com/voutcn/megahit">megahit</a></td>
    <td>Single genome assembly, Multiple library analysis is possible</td>
    <td>2015</td>
  </tr>
  <tr>
    <td><a href="https://cab.spbu.ru/software/spades/">SPAdes</a></td>
    <td>Various types of data, such as RNA, virus RNA, plasmid, etc., can be assembled. Not only fastq, fasta files but also bam files can be inputted</td>
    <td>2012</td>
  </tr>
  <tr>
    <td><a href="https://github.com/trinityrnaseq/trinityrnaseq/wiki">trinity</a></td>
    <td>Transcriptome assembler</td>
    <td>2011</td>
  </tr>
  <tr>
    <td rowspan="4">Taxonomy assignment</td>
    <td><a href="https://bioinformatics-centre.github.io/kaiju/">kaiju</a></td>
    <td>Analyze the entire sequence of the meta-genome or the sequence of the meta-transcript using the GenBank protein-redundant database</td>
    <td>2016</td>
  </tr>
  <tr>
    <td><a href="https://ccb.jhu.edu/software/kraken/MANUAL.html">kraken</a></td>
    <td>Tazonomy analysis using GenBank nucleotide non-redundant database</td>
    <td>2014</td>
  </tr>
  <tr>
    <td><a href="https://huttenhower.sph.harvard.edu/metaphlan3/">MetaPhlAn</a></td>
    <td>Analysis of microbial composition from meta-genetic information at species level. Use your own marker genes</td>
    <td>2012</td>
  </tr>
  <tr>
    <td><a href="https://www.onecodex.com/">onecodex</a></td>
    <td>Web-based analysis tool using Genome database and targeted loci database</td>
    <td>2015</td>
  </tr>
  <tr>
    <td rowspan="4">Format transition</td>
    <td><a href="https://bedtools.readthedocs.io/en/latest/">BEDTools</a></td>
    <td>Software using bam or bed files. Raw count value can be obtained, but a candidate is required</td>
    <td>2010</td>
  </tr>
  <tr>
    <td><a href="https://cole-trapnell-lab.github.io/cufflinks/manual/">Cufflink</a></td>
    <td>Tool that assembles RNA-seq mapping results (sam file) and calculates an unbalance haved FPKM value as result</td>
    <td>2010</td>
  </tr>
  <tr>
    <td><a href="https://htseq.readthedocs.io/en/release_0.11.1/index.html">HTSeq</a></td>
    <td>Python package, calculation of read mapping using gff information</td>
    <td>2015</td>
  </tr>
  <tr>
    <td><a href="https://www.htslib.org/">SAMTools</a></td>
    <td>Software that converts or sorts sam files</td>
    <td>2009</td>
  </tr>
</tbody>
</table>

### References

1. Martin M. Cutadapt removes adapter sequences from high-throughput sequencing reads. *EMBnet.journal*. 2011;17(1):10-12. doi:10.14806/ej.17.1.200

2. Bolger AM, Lohse M, Usadel B. Trimmomatic: a flexible trimmer for Illumina sequence data. *Bioinformatics*. 2014;30(15):2114-2120. doi:10.1093/bioinformatics/btu170

3. Andrews S. FastQC: a quality control tool for high throughput sequence data. *Babraham Bioinformatics*. 2010.

4. Langmead B, Salzberg SL. Fast gapped-read alignment with Bowtie 2. *Nat Methods*. 2012;9(4):357-359. doi:10.1038/nmeth.1923

5. Li H, Durbin R. Fast and accurate short read alignment with Burrows-Wheeler transform. *Bioinformatics*. 2009;25(14):1754-1760. doi:10.1093/bioinformatics/btp324

6. Kim D, Langmead B, Salzberg SL. HISAT: a fast spliced aligner with low memory requirements. *Nat Methods*. 2015;12(4):357-360.

7. Dobin A, Davis CA, Schlesinger F, et al. STAR: ultrafast universal RNA-seq aligner. *Bioinformatics*. 2013;29(1):15-21. doi:10.1093/bioinformatics/bts635

8. Li D, Liu CM, Luo R, Sadakane K, Lam TW. MEGAHIT: an ultra-fast single-node solution for large and complex metagenomics assembly via succinct de Bruijn graph. *Bioinformatics*. 2015;31(10):1674-1676. doi:10.1093/bioinformatics/btv033

9. Bankevich A, Nurk S, Antipov D, et al. SPAdes: a new genome assembly algorithm and its applications to single-cell sequencing. *J Comput Biol*. 2012;19(5):455-477. doi:10.1089/cmb.2012.0021

10. Grabherr MG, Haas BJ, Yassour M, et al. Full-length transcriptome assembly from RNA-Seq data without a reference genome. *Nat Biotechnol*. 2011;29(7):644-652. doi:10.1038/nbt.1883

11. Love MI, Huber W, Anders S. Moderated estimation of fold change and dispersion for RNA-seq data with DESeq2. *Genome Biol*. 2014;15(12):550. doi:10.1186/s13059-014-0550-8

12. Robinson MD, McCarthy DJ, Smyth GK. edgeR: a Bioconductor package for differential expression analysis of digital gene expression data. *Bioinformatics*. 2010;26(1):139-140. doi:10.1093/bioinformatics/btp616

13. Ritchie ME, Phipson B, Wu D, et al. limma powers differential expression analyses for RNA-sequencing and microarray studies. *Nucleic Acids Res*. 2015;43(7):e47. doi:10.1093/nar/gkv007

14. Li H, Handsaker B, Wysoker A, et al. The Sequence Alignment/Map format and SAMtools. *Bioinformatics*. 2009;25(16):2078-2079. doi:10.1093/bioinformatics/btp352

15. Quinlan AR, Hall IM. BEDTools: a flexible suite of utilities for comparing genomic features. *Bioinformatics*. 2010;26(6):841-842. doi:10.1093/bioinformatics/btq033

16. Menzel P, Ng KL, Krogh A. Fast and sensitive taxonomic classification for metagenomics with Kaiju. *Nat Commun*. 2016;7:11257. doi:10.1038/ncomms11257

17. Wood DE, Salzberg SL. Kraken: ultrafast metagenomic sequence classification using exact alignments. *Genome Biol*. 2014;15(3):R46. doi:10.1186/gb-2014-15-3-r46

18. Segata N, Waldron L, Ballarini A, Narasimhan V, Jousson O, Huttenhower C. Metagenomic microbial community profiling with species-level resolution using MetaPhlAn 2.0. *Nat Methods*. 2012;9(8):811-814. doi:10.1038/nmeth.2066

19. Minot SS, Krumm N, Greenfield NB. One Codex: A Sensitive and Accurate Data Platform for Genomic Microbial Identification. mBio. 2015;6(5):e00860-15.

20. Anders S, Pyl PT, Huber W. HTSeq—a Python framework to work with high-throughput sequencing data. *Bioinformatics*. 2015;31(2):166-169. doi:10.1093/bioinformatics/btu638

21. Robinson JT, Thorvaldsdottir H, Winckler W, et al. Integrative Genomics Viewer. *Nat Biotechnol*. 2011;29(1):24-26. doi:10.1038/nbt.1754