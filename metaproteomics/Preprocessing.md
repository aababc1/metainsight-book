# Preprocessing of the sequencing reads

# Preprocessing of the sequencing reads

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_5_1.png?raw=true" style="width:90%">
  <figcaption><b>Preprocessing of sequencing reads</b></figcaption>  
</figure>

Ribosome-bound mRNA reads differ from the mRNA extracted using the metatranscriptome SOP in that they have shorter RNA fragment lengths, requiring a different analysis approach.
While trimming and alignment (mapping) are conducted following the methods specified in the metatranscriptome SOP, there are differences in the subsequent analysis methods.
To utilize raw sequence data for analysis, it's necessary to go through a process of removing low-quality bases and eliminating adaptors. This process results in enhanced sequence quality and an increased mapping rate.
The Kneaddata program makes it easy to remove adaptor sequences used in Illumina platform-based sequencing and host genome sequences.

```bash
#host RNA removal and trimming
$ kneaddata --input sample_1.fastq.gz --input sample_2.fastq.gz --reference-db hg37dec_v0.1 --output ./1.Trim/sample --trimmomatic /where/to/Trimmomatic-0.36/ --trimmomatic-options="MINLEN:90" 
#--trimmomatic option; trimmomatic path
```

You can use the FastQC program to compare the quality of sequence reads before and after preprocessing, allowing you to verify the trimming results. FastQC provides comprehensive information about the fastq files, including parameters such as per base sequence quality, per sequence QC content, per sequence quality score, sequence length distribution, and more, to assess the outcomes of trimming.

```bash
#FastQC running(java script)
$./fastqc
#check fastq file with java
```

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_5_2.png?raw=true" style="width:90%">
  <figcaption><b>Example of quality check results of raw sequence with FastQC</b></figcaption>
</figure>

### References

Bolger AM, Lohse M, Usadel B. Trimmomatic: a flexible trimmer for Illumina sequence data. *Bioinformatics*. 2014;30(15):2114-2120. doi:10.1093/bioinformatics/btu170

Andrews S. FastQC: A quality control tool for high throughput sequence data. *Babraham Bioinformatics*. 2010.

Martin M. Cutadapt removes adapter sequences from high-throughput sequencing reads. *EMBnet.journal*. 2011;17(1):10-12. doi:10.14806/ej.17.1.200

Ingolia NT, Ghaemmaghami S, Newman JR, Weissman JS. Genome-wide analysis in vivo of translation with nucleotide resolution using ribosome profiling. *Science*. 2009;324(5924):218-223. doi:10.1126/science.1168978
