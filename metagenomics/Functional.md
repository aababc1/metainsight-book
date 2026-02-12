# Functional annotation of contigs

While taxonomic profiling reveals *who* is present in a microbial community, functional annotation addresses the equally important question of *what* they can do. Functional annotation assigns biological roles to the predicted genes within assembled contigs or metagenome-assembled genomes (MAGs), linking open reading frames (ORFs) to known metabolic pathways, enzyme functions, and gene ontologies. This step is essential for understanding the metabolic potential of microbial communities and for identifying genes of interest such as antibiotic resistance genes, carbohydrate-active enzymes, or novel biosynthetic gene clusters. In this chapter, we describe gene prediction using Prodigal and functional annotation using eggNOG-mapper against multiple reference databases.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_9_1.png?raw=true" style="width:90%">
  <figcaption><b></b></figcaption>
</figure>

After completing the taxonomic annotation of contigs, it is necessary to retrieve information about the open reading frame of the contigs to make a functional assignment.
Prodigal can predict protein-coding sequences of prokaryotes and can be used for metagenome analysis in addition to complete or draft genome analysis.

```bash
# run prodigal
$ conda activate prodigal
$ prodigal -i final.contigs.fa -p meta -a final.contigs.prodigal.faa -d final.contigs.prodigal.fna -f gff -o final.contigs.prodigal.gff 
$ conda deactivate
```

After gene prediction is completed, the contig file can be analyzed for functional annotation based on various databases, most commonly [KEGG](https://www.genome.jp/kegg/), [COG](https://www.ncbi.nlm.nih.gov/research/cog-project/), and [metaCyc](https://metacyc.org/) databases, and also specialized databases such as CAZyme [14] and ARDB [15] can be utilized.
One of the most widely used functional annotation programs is [eggNOG-mapper](https://github.com/eggnogdb/eggnog-mapper), which can perform fast functional annotation of novel sequences using the eggNOG database based on orthologs and phylogenies produced by the European Molecular Biology Laboratory (EMBL).
In addition to eggNOG-mapper, other tools that can be used are simple BLAST or programs such as [InterProScan](https://www.ebi.ac.uk/interpro/search/sequence/).

```bash
# run eggnog-mapper
$ conda activate eggnog
# download eggnog-mapper database
$ download_eggnog_data.py
# run eggnog-mapper
$ emapper.py -m diamond --cpu 5 -i final.contig.prodigal.faa -o eggnog.out
$ conda deactivate
```

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_9_2.png?raw=true" style="width:90%">
  <figcaption><b>Example of report.html </b></figcaption>  
</figure>

Besides the standalone version, eggNOG-mapper offers a [web-based analysis service](http://eggNOG-mapper.embl.de/) that can accommodate input of up to 100,000 proteins in FASTA format.

### References

1. Hyatt D, Chen GL, Locascio PF, et al. Prodigal: prokaryotic gene recognition and translation initiation site identification. *BMC Bioinformatics*. 2010;11:119. doi:10.1186/1471-2105-11-119
2. Huerta-Cepas J, Forslund K, Coelho LP, et al. eggNOG 4.5: a hierarchical orthology framework with improved functional annotations for eukaryotic, prokaryotic and viral sequences. *Nucleic Acids Res*. 2016;44(D1):D286-D293. doi:10.1093/nar/gkv1248
3. Huerta-Cepas J, Szklarczyk D, Heller D, et al. eggNOG 5.0: a hierarchical, functionally and phylogenetically annotated orthology resource with improved taxonomy and novel functional descriptors for proteins across the tree of life. *Nucleic Acids Res*. 2019;47(D1):D309-D314. doi:10.1093/nar/gky1085
4. Buchfink B, Xie C, Huson DH. Fast and sensitive protein alignment using DIAMOND. *Nat Methods*. 2015;12(1):59-60. doi:10.1038/nmeth.3176
5. Kanehisa M, Goto S. KEGG: Kyoto Encyclopedia of Genes and Genomes. *Nucleic Acids Res*. 2000;28(1):27-30. doi:10.1093/nar/28.1.27
6. Tatusov RL, Koonin EV, Liphardt J. A genomic perspective on protein families. *Science*. 1997;278(5338):631-637. doi:10.1126/science.278.5338.631

