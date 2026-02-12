# Standard Operating Procedure for Next-Generation Sequencing (NGS)-Based Metagenome Analysis

## Introduction to Metagenome

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_0_1.png?raw=true" style="width:90%">
  <figcaption><b>Metagenomics overview</b></figcaption>
</figure>

Metagenomes provide a foundation for observing the collective genetic repertoire of microbial communities through DNA sequences and inferring their functional potential—the theoretically feasible functions and biological composition—from these data. Although cells comprise multiple omics layers, including transcriptomes and proteomes, DNA represents the primary information source that defines the possible range of expression and function, following the central dogma where information flows from DNA through transcription and translation (Quince et al., 2017). Thus, examining DNA establishes a baseline framework for understanding both the functional potential of a community and its compositional structure—which community members are present and at what relative abundances.

This DNA-level organization serves as a practical reference plane in multi-omics integration. Signals observed in transcriptomic or proteomic data can only be meaningfully interpreted within the structural constraints of "existing genes, pathways, and genomes." Conversely, hypotheses arising from other omics layers can be tested or refined through metagenomics to verify the presence and functional feasibility of relevant elements (Heintz-Buschart & Wilmes, 2018). In this sense, metagenomics anchors observed changes into a structurally interpretable form within integrated analyses, while subsequent findings from other omics layers raise demands on metagenomics resolution and organizational units (genes, pathways, genomes), creating a recursive loop of hypothesis refinement and validation.

The independent value of metagenomics becomes evident in its ability to construct this reference plane without excessive dependence on culturability or reference databases. A substantial fraction of the microbiome remains unculturable, lacks species-level taxonomy, and persists as "dark matter" with only fragmentary functional hints (Rinke et al., 2013; Pasolli et al., 2019). Metagenomics thus becomes the entry point for capturing traces of genetic information actually present in communities, rendering them observable without awaiting cultivation or isolation of specific strains. In other words, metagenomics expands the genetic possibility space of microbial communities beyond known references, broadening the scope of questions addressable in integrated analyses and providing structural justification for attributing observed changes to specific biological units.

### Assembly-Free and Assembly-Based Approaches

Metagenomic analysis generally unfolds along two complementary axes: assembly-free (read-based) and assembly-based approaches (Quince et al., 2017). The former directly classifies and organizes individual reads to rapidly summarize sample composition and functional capacity, while the latter integrates reads into longer sequence units (contigs, or complete genomes when feasible) to interpret function and taxonomy within the same structural context. Rather than competing methods, these approaches differ in their observational units and forms of uncertainty, providing different evidence from the same data. In practice, they are frequently combined in a complementary manner.

The strength of assembly-free analysis lies in obtaining stable profiles that comprehensively cover the entire sample. Taxonomic composition is organized into comparable forms through marker gene detection or k-mer/alignment-based classification methods such as Kraken and MetaPhlAn (Wood & Salzberg, 2014; Segata et al., 2012), while functional profiles are summarized at the gene family or pathway level using tools like HUMAnN (Franzosa et al., 2018). These results are advantageous for rapidly identifying "what changes" across cohorts and for examining the impact of preprocessing and data quality variations on profiles. However, this approach is sensitive to the scope and accuracy of reference databases during classification and annotation; regions unmatched or over-matched to references yield increased unclassified signal and provide limited structural basis for directly answering "which functions are attributed to which organisms?"

Conversely, assembly-based analysis most prominently reveals the ability of metagenomics to characterize microbial "dark matter." Even organisms that are unculturable or insufficiently captured by reference databases can have their presence established as sequence data when DNA is reconstructed into longer units (Nurk et al., 2017), enabling simultaneous analysis of gene composition, pathway architecture, and phylogenetic position through binning approaches such as MetaBAT2 (Kang et al., 2019) and quality assessment with CheckM (Parks et al., 2015). This allows function to be understood not as a simple inventory but within the context of genomic repertoire, enabling interpretations about whether functional changes are driven by specific lineages or genetic units. However, assembly-based approaches show substantial variation in representativeness and quality depending on data conditions (coverage, complexity, strain diversity). These assembled units are most effective when used as evidence for structurally grounding signals detected in read-based profiles, rather than as direct summaries of entire samples.

The complementary operation of both approaches converges at the intersection of "stability" and "specificity." Functional changes observed in read-based data first constitute reproducible signals across samples; assembly-based results then narrow the explanation to specific genetic units driving those changes. Conversely, units recovered through assembly-based approaches are verified and quantified through read-based profiles, which provide their relative contribution and distribution across entire samples. Assembly-free methods more strongly answer "how much and where," while assembly-based approaches answer "what and who"; together, these perspectives transform taxonomic profiles into more continuous composition interpretations that encompass unclassified regions, and elevate functional profiles beyond simple abundance comparisons to reveal implementation strategies and contributing organisms.

### Read Length and Sequencing Technology

In parallel with these in silico analytical developments, inherent constraints in read length have long defined overall analytical uncertainty in metagenomics. Short-read-dominated data creates structural limitations during assembly in resolving connectivity and repetitive sequence regions; in taxonomy assignment and functional prediction, identical or similar sequences mapping to multiple candidates can distort biological interpretation. The distinction between the two analytical axes can be substantially understood not as algorithmic differences but as limits determined by the information content and contextual scope permitted by individual reads. Therefore, alongside refinement of analysis procedures, efforts to increase observational information—specifically, lengthening reads—have served as substantive turning points in metagenomic analysis.

For example, sequencing technologies providing longer reads, such as Pacific Biosciences (PacBio) and Oxford Nanopore Technologies (ONT), expand the "feasible solution space" of downstream analysis beyond read quality improvement alone. In assembly-based analysis, long reads increase assembly connectivity, reducing contig fragmentation and enabling more convincing treatment of repetitive and mobile element regions, ultimately transforming the character of quality assessment and downstream interpretation (Feng et al., 2022; Agustinho et al., 2024). Simultaneously, in assembly-free analysis, the increased contextual information carried by longer reads can alleviate uncertainty in taxonomy assignment and enable more direct mapping and interpretation of functional units. However, long reads do not always represent simple improvements; experimental and computational trade-offs in cost, sample preparation, error characteristics, and data requirements must be carefully weighed.

As a practical solution for managing these trade-offs, hybrid strategies combining short and long reads have recently become widespread. Hybrid approaches leverage the depth and relatively stable quantification offered by short reads alongside the connectivity and contextual advantages of long reads, mitigating failure modes and uncertainty arising at specific steps (for example, assembly, binning, annotation, or function attribution) (Feng et al., 2022; Agustinho et al., 2024). This trend increasingly incorporates read-type combination design—tailored to data characteristics and target outputs rather than constrained to a single sequencing technology—as an essential component of metagenomic workflow design. Following this trend, the present workflow is engineered to accommodate all three sequencing configurations (short-read, long-read, and hybrid), delivering outputs optimized for each sequencing modality and presenting consistent analytical direction regardless of data type.

### Scope of This Section

In the metagenomics sections that follow, quality control serves as the departure point, with assembly-free and assembly-based analyses organized systematically as parallel pipelines within a coherent analytical framework. Each step first defines essential outputs and minimum quality thresholds to ensure readers obtain consistent results, then presents the necessary tools, parameters, and validation metrics to meet these standards. Finally, each step couples its outputs with corresponding visualizations and QC reporting, preserving results as objectively verifiable evidence. The goal of this section is to equip readers with a metagenomics workflow at the standard operating procedure (SOP) level, enabling them to repeat and extend analyses under consistent principles and output specifications tailored to their data and research questions, rather than requiring de novo pipeline assembly for each project.

### References

1. Quince C, Walker AW, Simpson JT, Loman NJ, Segata N. Shotgun metagenomics, from sampling to analysis. *Nat Biotechnol*. 2017;35(9):833-844. doi:10.1038/nbt.3935
2. Heintz-Buschart A, Wilmes P. Human gut microbiome: function matters. *Trends Microbiol*. 2018;26(7):563-574. doi:10.1016/j.tim.2017.11.002
3. Rinke C, Schwientek P, Sczyrba A, et al. Insights into the phylogeny and coding potential of microbial dark matter. *Nature*. 2013;499(7459):431-437. doi:10.1038/nature12352
4. Pasolli E, Asnicar F, Manara S, et al. Extensive unexplored human microbiome diversity revealed by over 150,000 genomes from metagenomes spanning body sites, ages and lifestyles. *Cell*. 2019;176(3):649-662. doi:10.1016/j.cell.2019.01.001
5. Wood DE, Salzberg SL. Kraken: ultrafast metagenomic sequence classification using exact alignments. *Genome Biol*. 2014;15(3):R46. doi:10.1186/gb-2014-15-3-r46
6. Segata N, Waldron L, Ballarini A, Narasimhan V, Jousson O, Huttenhower C. Metagenomic microbial community profiling using unique clade-specific marker genes. *Nat Methods*. 2012;9(8):811-814. doi:10.1038/nmeth.2066
7. Franzosa EA, McIver LJ, Rahnavard G, et al. Species-level functional profiling of metagenomes and metatranscriptomes. *Nat Methods*. 2018;15(11):962-968. doi:10.1038/s41592-018-0176-y
8. Nurk S, Meleshko D, Korobeynikov A, Pevzner PA. metaSPAdes: a new versatile metagenomic assembler. *Genome Res*. 2017;27(5):824-834. doi:10.1101/gr.213959.116
9. Kang DD, Li F, Kirton ES, et al. MetaBAT 2: an adaptive binning algorithm for robust and efficient genome reconstruction from metagenome assemblies. *PeerJ*. 2019;7:e7359. doi:10.7717/peerj.7359
10. Parks DH, Imelfort M, Skennerton CT, Hugenholtz P, Tyson GW. CheckM: assessing the quality of microbial genomes recovered from isolates, single cells, and metagenomes. *Genome Res*. 2015;25(7):1043-1055. doi:10.1101/gr.186072.114
11. Feng X, Cheng H, Portik D, et al. Metagenome assembly of high-fidelity long reads with hifiasm-meta. *Nat Methods*. 2022;19(6):671-674. doi:10.1038/s41592-022-01478-3
12. Agustinho DP, Liu M, Karasikov M, et al. Unveiling microbial diversity: harnessing long-read sequencing technology. *Nat Methods*. 2024;21(6):954-966. doi:10.1038/s41592-024-02262-1
13. Lloyd-Price J, Arze C, Ananthakrishnan AN, et al. Multi-omics of the gut microbial ecosystem in inflammatory bowel diseases. *Nature*. 2019;569(7758):655-662. doi:10.1038/s41586-019-1237-9
14. Franzosa EA, Sirota-Madi A, Avila-Pacheco J, et al. Gut microbiome structure and metabolic activity in inflammatory bowel disease. *Nat Microbiol*. 2019;4(5):714-725. doi:10.1038/s41564-018-0306-4
15. Kim J, Kim MS, Koh AY, et al. Hybrid metagenomic sequencing strategies comparison for microbial community profiling. *Microbiol Spectr*. 2024;12(3):e03590-23. doi:10.1128/spectrum.03590-23

<div style="color: #1565C0;">

## Sequencing Technology Selection

Choosing the appropriate sequencing platform is one of the most critical decisions in metagenomic study design, as it directly determines the achievable resolution of taxonomic classification, assembly completeness, and overall analytical scope. Currently, three major platforms dominate the field: Illumina (short-read), Pacific Biosciences (PacBio, long-read), and Oxford Nanopore Technologies (ONT, long-read). Each platform has distinct strengths and trade-offs that must be carefully considered based on the research objectives, available budget, and sample characteristics.

### Platform Comparison

| Feature | Illumina NovaSeq 6000 | PacBio Revio (HiFi) | ONT PromethION |
|---|---|---|---|
| **Read length** | Up to 2 × 250 bp | 15–18 kb | up to 4 Mb (avg ~20 kb) |
| **Read accuracy** | ~99.75% (Q30+) | >99.5% (Q30+) | 97–99% (Q20+) |
| **Yield per run** | ~350 Gb | ~90 Gb per SMRT Cell (×4) | ~120 Gb |
| **Cost per Gb** | ~US$4 | ~US$8–11 | ~US$6–12 |
| **DNA input** | 1–500 ng | 150 ng – 1 µg | 150 ng – 1 µg |
| **Runtime** | 13–44 h | ~24 h | ~72 h |
| **Direct RNA-seq** | No | No | Yes |
| **Portability** | Low | Low | High (MinION) |

*Note: Sequencing costs are estimates and subject to rapid changes {cite:p}`Agustinho2024`.*

### When to Choose Short Reads (Illumina)

Short-read sequencing remains the most widely adopted approach in metagenomics due to its low cost per gigabase, high base-level accuracy, and lower DNA input requirements. It is particularly well-suited for:

- **Community profiling and abundance estimation** — when the primary goal is to determine which organisms are present and at what relative abundance, short reads provide cost-effective, high-throughput results.
- **Functional gene catalog construction** — read-based profiling tools such as HUMAnN and MetaPhlAn are optimized for short-read data.
- **Differential abundance studies** — when comparing microbial communities across many samples (e.g., case-control studies), the lower per-sample cost of short reads enables larger sample sizes.
- **Low-biomass samples** — Illumina library preparation with PCR amplification can work with as little as 1 ng of input DNA, an important advantage when sample material is limited.

However, short reads have well-documented limitations. Repetitive genomic regions longer than the read length (~250 bp) cannot be resolved, resulting in fragmented assemblies. This makes it difficult to recover complete genomes (MAGs), characterize mobile genetic elements (plasmids, transposons), and distinguish closely related strains that differ in only a few genomic loci.

### When to Choose Long Reads (PacBio HiFi or ONT)

Long-read sequencing has matured considerably in recent years, with significant improvements in accuracy, throughput, and cost. Long reads are recommended when the study requires:

- **Complete or near-complete MAGs** — long reads can span repetitive regions and resolve strain-level haplotypes, enabling the assembly of circularized genomes directly from metagenomic samples. For example, PacBio HiFi reads with hifiasm-meta have been shown to circularize 56 genomes from human gut microbiome samples.
- **Strain-level resolution** — intergenomic repeats (sequences shared between related organisms) are difficult to resolve with short reads alone. Long reads increase the likelihood that a read includes an organism-specific region, improving taxonomic classification at species and sub-species levels.
- **Structural variant detection** — insertions, deletions, inversions, and other large-scale genomic rearrangements (>50 bp) are far more reliably detected with long reads.
- **Methylation analysis** — both PacBio and ONT can detect DNA methylation patterns (5mC, 6mA, 4mC) directly during sequencing without bisulfite conversion, enabling epigenomic characterization of microbial communities.
- **Plasmid and mobile element recovery** — short-read assemblies disproportionately fail for multi-copy DNA elements such as 16S genes, transposons, and plasmids. Long reads overcome this by spanning entire elements in single reads.

#### PacBio HiFi vs. ONT

| Consideration | PacBio HiFi | ONT |
|---|---|---|
| **Best for** | High-accuracy MAG assembly, variant calling | Rapid/field sequencing, ultra-long reads, direct RNA-seq |
| **Accuracy** | >99.5% (comparable to Illumina) | 97–99% (improving with R10 chemistry) |
| **Read length** | 15–18 kb (consistent) | Up to 4 Mb (variable, avg ~20 kb) |
| **Methylation** | 5mC, 6mA | 5mC, 6mA, 4mC + RNA modifications |
| **Portability** | Lab-based only | MinION/Flongle can be used in field settings |
| **Error correction needed** | Rarely (HiFi reads are self-corrected) | Often recommended before assembly |

### Hybrid Approach (Short + Long Reads)

A hybrid sequencing strategy combines the strengths of both technologies: the high base-level accuracy of short reads with the long-range contiguity information from long reads. Hybrid assembly tools such as **OPERA-MS**, **Unicycler**, and **DBG2OLC** can leverage both data types to produce assemblies with improved contiguity, gene completeness, and binning accuracy compared to short-read-only approaches.

However, hybrid approaches involve higher costs (two library preparations and sequencing runs) and can introduce biases from combining different library preparation chemistries. With the increasing accuracy of PacBio HiFi reads (>Q30), long-read-only assemblies are now achieving comparable or superior quality to hybrid assemblies for many applications, making the hybrid approach less necessary than in previous years.

### Decision Framework

The choice of sequencing strategy depends on the study's objectives:

| Research Goal | Recommended Strategy |
|---|---|
| Large-scale community profiling (many samples) | **Illumina short reads** |
| Complete genome recovery (MAGs) | **PacBio HiFi** or **ONT + polishing** |
| Strain-level resolution | **Long reads** (PacBio or ONT) |
| Plasmid / mobile element tracking | **Long reads** |
| Antibiotic resistance gene surveillance | **ONT** (rapid, portable) |
| Low-biomass / clinical samples | **Illumina** (low DNA input) |
| Multi-omics integration (DNA + RNA) | **ONT** (direct RNA-seq capability) |
| Budget-constrained study | **Illumina** (lowest cost/Gb) |

In this SOP, we provide analysis pipelines for both **Illumina short-read** and **PacBio HiFi long-read** metagenomics, covering sample preparation through computational analysis for each approach.

</div>
