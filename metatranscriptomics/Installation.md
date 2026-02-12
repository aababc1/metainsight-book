# Metatranscriptomic analysis tools
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
	- DESeq2, ggplot2, pheatmap  

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_4_1.png?raw=true" style="width:90%">
  <figcaption><b>Metatranscriptomics analysis pipeline</b></figcaption>  
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

1. Martin M. Cutadapt removes adapter sequences from high-throughput sequencing reads. *EMBnet.journal*. 2011;17(1):10-12. doi:10.14806/ej.17.1.200

2. Langmead B, Salzberg SL. Fast gapped-read alignment with Bowtie 2. *Nat Methods*. 2012;9(4):357-359. doi:10.1038/nmeth.1923

3. Li H, Handsaker B, Wysoker A, et al. The Sequence Alignment/Map format and SAMtools. *Bioinformatics*. 2009;25(16):2078-2079. doi:10.1093/bioinformatics/btp352

4. Quinlan AR, Hall IM. BEDTools: a flexible suite of utilities for comparing genomic features. *Bioinformatics*. 2010;26(6):841-842. doi:10.1093/bioinformatics/btq033

5. Hyatt D, Chen GL, Locascio PF, Land ML, Larimer FW, Hauser LJ. Prodigal: prokaryotic gene recognition and translation initiation site identification. *BMC Bioinformatics*. 2010;11:119. doi:10.1186/1471-2105-11-119

6. Huerta-Cepas J, Szklarczyk D, Forslund K, et al. eggNOG 4.5: a hierarchical orthology framework with improved functional annotations for eukaryotic, archaeal and bacterial proteins. *Nucleic Acids Res*. 2016;44(D1):D286-D293.

7. Bankevich A, Nurk S, Antipov D, et al. SPAdes: a new genome assembly algorithm and its applications to single-cell sequencing. *J Comput Biol*. 2012;19(5):455-477. doi:10.1089/cmb.2012.0021

8. Franzosa EA, McIver LJ, Rahnavard G, et al. Species-level functional profiling of metagenomes and metatranscriptomes. *Nat Methods*. 2018;15(11):962-968. doi:10.1038/s41592-018-0176-y