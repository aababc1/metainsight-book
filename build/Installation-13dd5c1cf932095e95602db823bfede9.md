# Metagenomic analysis tools

This chapter provides a comprehensive guide to installing the bioinformatics software required for the metagenomic analysis pipeline described in this protocol. Metagenomic analysis relies on a diverse set of specialized tools spanning quality control, assembly, binning, taxonomic and functional annotation, and phylogenetic reconstruction. Managing these tools and their dependencies can be challenging, particularly when different programs require incompatible software versions. We recommend using Conda, a cross-platform package and environment manager, which allows each tool to be installed in an isolated environment, thereby avoiding version conflicts and ensuring reproducibility across different computing systems.

- Preprocessing of the sequencing reads : Kneaddata, minimap2, samtools
- Read-based profiling : HUMAnN 3.0, MetaPhlAn
- De novo assembly : MEGAHIT, Quast, hifiasm_meta, Bandage
- Taxonomic annotation : Kaiju
- Functional annotation : Prodigal, EggNOG
- Binning : MetaBAT2, BBmap, minimap2, samtools, CheckM
- Phylogenetic tree construction : GTDB-tk, PhyloPhlAn3

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_4_1.png?raw=true" style="width:90%">
  <figcaption><b>Metagenomics analysis pipeline</b></figcaption>  
</figure>

# Installation

### An introduction to Conda
Metagenomic analysis necessitates the installation of various analysis programs, a process that can sometimes result in conflicts or version dependencies between these programs.
For instance, when program A relies on a specific version of program B, and program C depends on a different version of program B, it can be challenging and time-consuming for beginners to set up program C.
In such scenarios, conda, a Python package and environment management tool, offers an effective solution for resolving these version conflicts.

For this Standard Operating Procedure (SOP), we recommend installing the analysis tools using conda.
You can find the official documentation for conda at the following [website](https://docs.conda.io/projects/conda/en/latest/user-guide/index.html).
This approach ensures a smoother and more efficient installation process, making metagenomic analysis more accessible and less prone to compatibility issues.

### Making a new environment 
It is highly recommended to create a new conda environment every time you install a program. Doing so helps to avoid conflicts between programs and ensures a clean, isolated environment for each analysis tool.
An example of how to create a new conda environment is provided below.
```bash
# Create a new conda environment
$ conda create -n new-env 
```
Use the `conda create` command with the `-n` flag to designate and save the name of your new environment.
### Entering & exiting an environment
```bash
# Enter that environment
$ conda activate new-env
# Exit whatever conda environment we are running
$ conda deactivate
```

The table below provides example installation codes and Anaconda addresses for the programs used in this SOP. 

| Program | Installation code | ANACONDA addresses |
| ------ | ------ | ------ |
| KNEDDATA | `conda create -n kneaddata -c bioconda kneaddata` | https://anaconda.org/bioconda/kneaddata |
| HUMANN3.0 | `conda create -n humann -c biobakery humann` | https://anaconda.org/biobakery/humann |
| METAPHLAN3.0 | `conda create –n metaphlan -c bioconda metaphlan` | https://anaconda.org/bioconda/metaphlan |
| MEGAHIT | `conda create –n MEGAHIT -c bioconda MEGAHIT` | https://anaconda.org/bioconda/MEGAHIT |
| QUAST | `conda create –n quast -c bioconda quast` | https://anaconda.org/bioconda/quast |
| KAIJU | `conda create –n kaiju -c bioconda kaiju` | https://anaconda.org/bioconda/kaiju |
| MINIMAP2 | `conda create –n minimap2 -c bioconda minimap2` | https://anaconda.org/bioconda/minimap2 |
| HIFIASM_META | `conda create –n hifiasm_meta -c bioconda hifiasm_meta` | https://anaconda.org/bioconda/hifiasm_meta |
| KRONA | `conda create –n krona -c bioconda krona` | https://anaconda.org/bioconda/krona |
| PRODIGAL | `conda create –n prodigal -c bioconda prodigal` | https://anaconda.org/bioconda/prodigal |
| EGGNOG | `conda create –n eggnog -c bioconda eggnog-mapper` | https://anaconda.org/bioconda/eggnog-mapper |
| METABAT2 | `conda create –n MetaBAT2 -c bioconda MetaBAT2` | https://anaconda.org/bioconda/MetaBAT2 |
| BBMAP | `conda create –n bbmap -c bioconda bbmap` | https://anaconda.org/bioconda/bbmap |
| SAMTOOLS | `conda create –n samtools -c bioconda samtools` | https://anaconda.org/bioconda/samtools |
| CHECKM | `conda create -n CheckM python=3.9` <br> `conda activate CheckM` <br>`conda install -c bioconda numpy matplotlib pysam`<br>`conda install -c bioconda hmmer prodigal pplacer`<br>`pip3 install CheckM-genome` | https://anaconda.org/bioconda/CheckM-genome |
| GTDB-TK | `conda create -n gtdbtk-2.1.1 -c conda-forge -c bioconda gtdbtk=2.1.1` | https://anaconda.org/bioconda/gtdbtk |
| PHYLOPHLAN3 | `conda create –n phylophlan -c bioconda phylophlan` | https://anaconda.org/bioconda/phylophlan |

### References

1. Li D, Liu CM, Luo R, et al. MEGAHIT: an ultra-fast single-node solution for large and complex metagenomics assembly via succinct de Bruijn graph. *Bioinformatics*. 2015;31(10):1674-1676. doi:10.1093/bioinformatics/btv033
2. Nurk S, Meleshko D, Korobeynikov A, et al. metaSPAdes: a new versatile metagenomic assembler. *Genome Res*. 2017;27(5):824-834. doi:10.1101/gr.213959.116
3. Kang DD, Li F, Kirton ES, et al. MetaBAT 2: an improved binning algorithm, assembly-independent binning and recovering metagenome-assembled genomes from heterogeneous sources. *PeerJ*. 2019;7:e7359. doi:10.7717/peerj.7359
4. Parks DH, Imelfort M, Skennerton CT, et al. CheckM: assessing the quality of microbial genomes recovered from isolates, single cells, and metagenomes. *Genome Res*. 2015;25(7):1043-1055. doi:10.1101/gr.186072.114
5. Chaumeil PA, Mussig AJ, Hugenholtz P, et al. GTDB-Tk: a toolkit to classify genomes with the Genome Taxonomy Database. *Bioinformatics*. 2020;36(6):1925-1927. doi:10.1093/bioinformatics/btz848
6. Hyatt D, Chen GL, Locascio PF, et al. Prodigal: prokaryotic gene recognition and translation initiation site identification. *BMC Bioinformatics*. 2010;11:119. doi:10.1186/1471-2105-11-119
7. Huerta-Cepas J, Forslund K, Coelho LP, et al. eggNOG 4.5: a hierarchical orthology framework with improved functional annotations for eukaryotic, prokaryotic and viral sequences. *Nucleic Acids Res*. 2016;44(D1):D286-D293. doi:10.1093/nar/gkv1248
8. Asnicar F, Thomas AM, Beghini F, et al. Serotype and clonal analysis of pathogenic Listeria monocytogenes strains. *Nat Commun*. 2020;11(1):2500. doi:10.1038/s41467-020-16366-7
9. Franzosa EA, McIver LJ, Rahnavard G, et al. Species-level functional profiling of metagenomes and metatranscriptomes. *Nat Methods*. 2018;15(11):962-968. doi:10.1038/s41592-018-0176-y
10. Segata N, Waldron L, Ballarini A, et al. Metagenomic microbial community profiling using unique clade-specific marker genes. *Nat Methods*. 2012;9(8):811-814. doi:10.1038/nmeth.2066
