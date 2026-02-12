# Small protein prediction
<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaProteomic/img/P_11_1.png?raw=true" style="width:65%">
  <figcaption><b></b></figcaption>  
</figure>

Ribosome profiling analysis allows obtaining information about small proteins that may not be accessible through genome or transcriptome analysis.
Small proteins refer to proteins with a size of less than 70 amino acids. These small proteins are known to be associated with the regulation of other genes or key factors in microorganisms, but their functional analysis can be challenging.
The goal of this process is to classify small proteins, perform new annotations, and discover previously unannotated genes with new functions.
To start, it's necessary to filter genes from DNA sequence files obtained through prodigal, which are less than 70 amino acids.
Using Linux, you can create a file containing only the small protein genes by employing `awk` and conditional statements. In most cases, these small, separated proteins correspond to hypothetical proteins.

```bash
# run prodigal 
$ prodigal -i sample_MAG.fa -p meta -a sample_MAG.prodigal.faa -d sample_MAG.prodigal.fna -f gff -o sample_MAG.prodigal.gff
# small amino acid filtering
$ awk '/^>/ {if (length(seq) <= 210) {print header; print seq} } {if (/^>/) {header = $0; seq = ""} else {seq = seq $0}} END {if (length(seq) <= 10) {print header; print seq}}' sample_MAG.prodigal.ffn > MAG_smallprotein.fnn
# run CD-hit for clustering
$ cd-hit -i MAG_smallprotein.ffn -o example -n 2 -p 1 -c 0.5 -d 200 -M 50000 -l 5 -s 0.95 -aL 0.95 -g 1
```
After this initial filtering, you can proceed to determine whether these small proteins have similar functions or if they represent new small proteins. To do this, you can use CD-HIT to cluster these proteins.
CD-HIT groups genes with similar sequences, generating files composed of representative sequences for each cluster.

Following the clustering step, you can use RNAcode to analyze and obtain information about the protein coding regions of the genes.
RNAcode requires an alignment file as input, so you can align the DNA sequences from the CD-HIT results using a tool like ClustalW.
The DNA sequence alignment file can then be used for analysis with RNAcode, allowing you to infer the coding sequences of small proteins.
Additionally, you can use read alignment information to obtain data on the expression of these small proteins.

```bash
# alignment multiple sequence
$ clustalw output
# run RNAcode
$ RNAcode output.aln --outfile results.gtf --gtf --best-only --cutoff 0.01 --eps data.aln
```

### References

Hyatt D, Chen GL, Locascio PF, Land ML, Larimer FW, Hauser LJ. Prodigal: prokaryotic gene recognition and translation initiation site identification. *BMC Bioinformatics*. 2010;11:119. doi:10.1186/1471-2105-11-119

Hemm MR, Paul BJ, Schneider TD, Storz G, Rudd KE. Small membrane proteins found by comparative genomics and proteomics. *Mol Microbiol*. 2008;70(6):1487-1501. doi:10.1111/j.1365-2958.2008.06495.x

Hao Y, Gong S, Otu D, Liu Z, Jiang W, Wang J, Shen Y. SmProt: A database of small proteins encoded by alternative translation initiation and uORFs. *Nucleic Acids Res*. 2018;46(D1):D567-D573. doi:10.1093/nar/gkx830

Ingolia NT, Ghaemmaghami S, Newman JR, Weissman JS. Genome-wide analysis in vivo of translation with nucleotide resolution using ribosome profiling. *Science*. 2009;324(5924):218-223. doi:10.1126/science.1168978

Ingolia NT. Ribosome profiling: new views of translation, from single codons to genome scale. *Nat Rev Genet*. 2014;15(3):205-213. doi:10.1038/nrg3645

Li H, Handsaker B, Wysoker A, Fennell T, Ruan J, Homer N, Marth G, Abecasis G, Durbin R. The Sequence Alignment/Map format and SAMtools. *Bioinformatics*. 2009;25(16):2078-2079. doi:10.1093/bioinformatics/btp352
