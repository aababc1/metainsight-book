# Transcriptional expression profiling

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_7_1.png?raw=true" style="width:65%">
  <figcaption><b> </b></figcaption>  
</figure>

RNA-seq read alignment results provide information for assessing the expression levels of individual genes.
Furthermore, it is possible to obtain expression information for individual contigs or MAGs generated from de novo assembly results of the metagenome.
In some cases, for more systematic analysis, it may be necessary to categorize genes with similar functions or group genes involved in specific metabolic pathways to analyze their expression levels.
To accomplish this, annotation information for each CDS in functional databases is required.
The [eggNOG-mapper](https://github.com/eggnogdb/eggnog-mapper) can be used to easily obtain this information. eggNOG-mapper requires an input file in which the amino acid sequences of each gene are listed in a .faa file format.
When running with default options, eggNOG-mapper uses BLAST to find the most similar information for each gene's amino acid sequence, extracting data related to [COG](https://www.ncbi.nlm.nih.gov/research/cog-project/)(Clusters of Orthologous Groups), [KEGG](https://www.genome.jp/kegg/)(Kyoto Encyclopedia of Genes and Genomes), [CAZy](http://www.cazy.org/)(Carbohydrate-Active EnZymes), and [Pfam](http://pfam.xfam.org/).  

```bash
# download eggnog-mapper from https://github.com/eggnogdb/eggnog-mapper/releases/latest
$ tar -xvzf eggnog_mapper_(version).tar.gz
# download eggnog-mapper database
$ download_eggnog_data.py
# run eggnog-mapper
$ emapper.py (option) -i sample_MAG.prodigal.faa -o sample_MAG.eggnog.out
```

The resulting files include eggnog.out.hit, eggnog.out.annotation, and eggnog.out.seed_ortholog, with eggnog.out.annotation containing annotation information from various databases such as COG and KEGG.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_7_2.png?raw=true" style="width:90%">
  <figcaption><b>Example of an announcement file among EGGNOG-mapper results</b></figcaption>  
</figure>

Using the COG information obtained from EGGNOG-mapper results, it is possible to predict the expression levels of each COG functional category across the entire metatranscriptome.  

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_7_3.png?raw=true" style="width:90%">
  <figcaption><b>Example of COG distribution</b></figcaption>  
</figure>

Additionally, the extracted COG or KEGG ORTHOLOGY information can be visualized using tools like KEGG mapper, [IPATH3](https://pathways.embl.de/), allowing for the exploration of the overall correlations among highly expressed genes. Depending on the options chosen, you can select a few genes with high count values, adjust line thickness based on count (i.e., expression level), or use different colors for each MAG, among other possibilities, to obtain diverse results.  

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_7_4.png?raw=true" style="width:70%">
  <figcaption><b> Example of iPATH3 results </b></figcaption>
</figure>

### References

1. Huerta-Cepas J, Szklarczyk D, Forslund K, et al. eggNOG 4.5: a hierarchical orthology framework with improved functional annotations for eukaryotic, archaeal and bacterial proteins. *Nucleic Acids Res*. 2016;44(D1):D286-D293.

2. Huerta-Cepas J, Forslund K, Coelho LP, et al. Fast genome-wide functional annotation through orthology assignment by eggNOG-mapper. *Mol Biol Evol*. 2017;34(8):2115-2122. doi:10.1093/molbev/msx148

3. Kanehisa M, Goto S. KEGG: Kyoto Encyclopedia of Genes and Genomes. *Nucleic Acids Res*. 2000;28(1):27-30. doi:10.1093/nar/28.1.27

4. Tatusov RL, Koonin EV, Liphardt J. A genomic perspective on protein families. *Science*. 1997;278(5338):631-637. doi:10.1126/science.278.5338.631

5. Mistry J, Chuguransky S, Williams L, et al. Pfam: The protein families database in 2021. *Nucleic Acids Res*. 2021;49(D1):D412-D419. doi:10.1093/nar/gkaa913

6. Lombard V, Golaconda Ramulu H, Drula E, Coutinho PM, Henrissat B. The carbohydrate-active enzymes database (CAZy) in 2013. *Nucleic Acids Res*. 2014;42(D1):D490-D495. doi:10.1093/nar/gkt1178

7. Darzi Y, Falony G, Vieira-Silva S, Raes J. Towards enhanced ecosystem predictive modelling by decoupling turbulence and nutrient transport. *Nucleic Acids Res*. 2018;46(W1):W510-W513. doi:10.1093/nar/gky299