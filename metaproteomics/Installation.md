# Translatome Analysis Tools
- Sequencing reads trimming  
	- FastQC, cutadapt, trimGalore  
- Alignment  
	- [Bowtie2](https://bowtie-bio.sourceforge.net/bowtie2/manual.shtml)  
- Convert file (file format: sam to cov)  
	- SamTools, bedtools  
- Functional annotation  
	- eggNOG-mapper  
- Visualization  
	- iPATH3, KEGG-mapper, IGV  
- R package  
	- RiboseqR, DESeq2, pheatmap, ggplot2  

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_4_1.png?raw=true" style="width:90%">
  <figcaption><b>Translatome analysis pipeline</b></figcaption>  
</figure>

# Installation
Before proceeding with the analysis pipeline, let me first explain the program installation process.
## Install conda environment
Conda offers the advantage of creating virtual environments, allowing for independent program installations and management. This feature is particularly valuable as it significantly reduces the risk of program conflicts. Therefore, it is recommended to install Conda-compatible programs via Conda.

```bash
# set up conda environment (name and python version are set by user)
$ conda create --name NGS python=3.7
# active conda environment
$ conda activate NGS
# install program for conda 
$ conda install cutadapt				#cutadapt install
$ conda install humann –c biobakery3		#humann install
# download database
$ humann_databases --download chocophlan full $INSTALL_LOCATION --update-config yes
$ humann_databases --download uniref uniref90_diamond $INSTALL_LOCATION --update-config yes
$ humann_databases --download utility_mapping full $INSTALL_LOCATION --update-config yes
$ conda install bowtie2				#bowtie2 install
$ make
$ conda install cdhit
```

## Install program
However, it's important to note that some programs may still require manual installation. In such cases, you need to install these programs directly. For programs installed separately, you may also need to edit your bash_profile file to add the program and database directories to your system's $PATH for proper functionality. 

```bash
# create and specify installation folders
$ mkdir program
$ cd program
# SAMtools install
$ tar -xvf samtools.zip
$ cd samtools
$ ./configure -prefix==/where/to/install
$ make
$ make install
# install prodigal
$ cd prodigal/
$ make install
#install bedtools
$ tar -zxvf bedtools-2.29.1.tar.gz
$ cd bedtools2
# download eggnog-mapper from https://github.com/eggnogdb/eggnog-mapper/releases/latest
$ tar -xvzf eggnog_mapper_(version).tar.gz
# download eggnog-mapper database
$ download_eggnog_data.py
#install SPAdes
$wget http://cab.spbu.ru/files/release3.15.3/SPAdes-3.15.3-Linux.tar.gz
$tar -xzf SPAdes-3.15.3-Linux.tar.gz
$cd SPAdes-3.15.3-Linux/bin/
```

### References

Langmead B, Salzberg SL. Fast gapped-read alignment with Bowtie 2. *Nat Methods*. 2012;9(4):357-359. doi:10.1038/nmeth.1923

Li H, Handsaker B, Wysoker A, Fennell T, Ruan J, Homer N, Marth G, Abecasis G, Durbin R. The Sequence Alignment/Map format and SAMtools. *Bioinformatics*. 2009;25(16):2078-2079. doi:10.1093/bioinformatics/btp352

Quinlan AR, Hall IM. BEDTools: a flexible suite of utilities for comparing genomic features. *Bioinformatics*. 2010;26(6):841-842. doi:10.1093/bioinformatics/btq033

Hyatt D, Chen GL, Locascio PF, Land ML, Larimer FW, Hauser LJ. Prodigal: prokaryotic gene recognition and translation initiation site identification. *BMC Bioinformatics*. 2010;11:119. doi:10.1186/1471-2105-11-119

Dobin A, Davis CA, Schlesinger F, Drenkow J, Zaleski C, Jha S, Batut P, Chaisson M, Gingeras TR. STAR: ultrafast universal RNA-seq aligner. *Bioinformatics*. 2013;29(1):15-21. doi:10.1093/bioinformatics/bts635

Bolger AM, Lohse M, Usadel B. Trimmomatic: a flexible trimmer for Illumina sequence data. *Bioinformatics*. 2014;30(15):2114-2120. doi:10.1093/bioinformatics/btu170

Andrews S. FastQC: A quality control tool for high throughput sequence data. *Babraham Bioinformatics*. 2010.

Huerta-Cepas J, Szklarczyk D, Forslund K, Hedges LM, Lehmann G, Sasson O, Moreno-Escamilla V, Damashash R, Forslund SJ, Petersen TN, von Mering C, Bork P, Huerta-Cepas J. eggNOG 4.5: a hierarchical orthology framework with improved functional annotations for eukaryotic, archaeal and bacterial proteins. *Nucleic Acids Res*. 2016;44(D1):D286-D293. doi:10.1093/nar/gkv1248

Segata N, Waldron L, Ballarini A, Narasimhan V, Jousson O, Huttenhower C. Metagenomic microbial community profiling using unique clade-specific marker genes. *Nat Methods*. 2012;9(8):811-814. doi:10.1038/nmeth.2066

Franzosa EA, McIver LJ, Rahnavard G, Thompson LR, Schirmer M, Weingart G, Lipson KS, Knight R, Caporaso JG, Segata N, Huttenhower C. Species-level functional profiling of metagenomes and metatranscriptomes. *Nat Methods*. 2018;15(11):962-968. doi:10.1038/s41592-018-0176-y
```
