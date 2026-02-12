# Standard Operating Procedure for Next-Generation Sequencing (NGS)-Based Metagenome Analysis

## Introduction to metagenome

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaGenomic/img/G_0_1.png?raw=true" style="width:90%">
  <figcaption><b>Metagenomics overview</b></figcaption>  
</figure>

A metagenome is the pool of genetic material present in various environmental samples (animal, plant, marine, etc.).
Metagenomic analysis extracts and analyzes the genetic information of all organisms present in a given environmental ecosystem.
Before the rise of metagenomics, microbial genomes could only be analyzed from culturable microorganisms. However, since only a small fraction of the microbes in a given environment are culturable, this approach results in biased information centered on culturable microbes.
Metagenomic analyses, on the other hand, analyze the entire genome of an environment, providing a more accurate picture of a given ecosystem.

Advancements in sequencing technology have made it easier for researchers to access whole metagenome shotgun sequencing, which sequences billions of nucleic acid fragments at once, beyond amplicon sequencing, which involves targeted amplification and sequencing of specific parts of the genome such as 16S ribosomal DNA, and the demand for research has increased.
For amplicon sequencing data, there are standard analysis protocols and platforms such as QIIME2, but for WMS analysis, there is no standard gold-standard analysis SOP.
In this SOP, we will describe the methods and flow for analyzing whole genome sequencing (WGS) data, focusing on the most commonly used tools among various analysis programs.

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
