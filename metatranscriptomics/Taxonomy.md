# Transcript taxonomy classification

In metatranscriptome analysis, just as taxonomy profiling is conducted in metagenome analysis, performing taxonomy assignment based on reads or contigs allows us to obtain information about microorganisms actively expressing themselves in the environment.  
In addition to the approach using the Kaiju tool, which is introduced in the metagenome SOP, there's a simple method for taxonomy analysis available through the [One Codex](https://www.onecodex.com/) web server.
The One Codex website accepts fasta or fastq files as input data and provides results accordingly.
For taxonomy analysis, One Codex employs its own database containing over 110,000 genomes and targeted loci databases such as 16S, 5S, 23S, gyrB, ITS, and more. 

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_10_1.png?raw=true" style="width:75%">
  <figcaption><b>One codex reference database</b></figcaption>  
</figure>

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_10_2.png?raw=true" style="width:90%">
  <figcaption><b>example of taxonomy assignment results using the One Codex web server</b></figcaption>
</figure>

You can compare taxonomy information not only at the DNA level but also from RNA data.
If you have metagenomic information, it can be used for reference. In cases where metagenomic information is unavailable, you can verify taxonomy at the RNA level.
The analysis results allow for visualization of cluster composition and read count ratios at each taxonomy level, from phylum to species. Additionally, a taxonomy chart reflecting hierarchical taxonomy levels is available for examination.

### References

1. Menzel P, Ng KL, Krogh A. Fast and sensitive taxonomic classification for metagenomics with Kaiju. *Nat Commun*. 2016;7:11257. doi:10.1038/ncomms11257

2. Wood DE, Salzberg SL. Kraken: ultrafast metagenomic sequence classification using exact alignments. *Genome Biol*. 2014;15(3):R46. doi:10.1186/gb-2014-15-3-r46

3. Segata N, Waldron L, Ballarini A, Narasimhan V, Jousson O, Huttenhower C. Metagenomic microbial community profiling with species-level resolution using MetaPhlAn 2.0. *Nat Methods*. 2012;9(8):811-814. doi:10.1038/nmeth.2066

4. Minot SS, Krumm N, Greenfield NB. One Codex: A Sensitive and Accurate Data Platform for Genomic Microbial Identification. *mBio*. 2015;6(5):e00860-15.
