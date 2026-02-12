# Sequencing

Metatranscriptomic sequencing captures the actively expressed genes within a microbial community at a given point in time, providing a snapshot of community-level gene expression. Unlike DNA-based metagenomics, RNA is inherently unstable and degrades rapidly, making proper sample preservation, RNA extraction, and library preparation critically important. This chapter details the complete wet-lab protocol for metatranscriptomic sequencing, from fecal sample collection and RNA extraction through rRNA depletion and Illumina library preparation. Special attention is given to maintaining RNA integrity throughout the workflow, as the quality of the extracted RNA directly determines the reliability of downstream expression analyses.

## Biological samples

RNA is highly susceptible to degradation by ubiquitous RNases, making rapid and effective preservation essential for metatranscriptomic studies. RNAlater is a non-toxic aqueous reagent that permeates tissues and stabilizes RNA by inactivating RNases, allowing sample storage at -80°C without significant transcript degradation. Proper sample-to-reagent ratios and immediate processing are critical to ensuring that the captured transcriptional profile accurately reflects the in vivo state of the microbial community.

- Process 500 µL of RNAlater (Ambion) for every 1 g of fecal sample and store it at -80°C

## RNA preparation

Total RNA extraction from fecal samples requires a combination of mechanical lysis (bead-beating) and chemical purification to efficiently lyse diverse microbial cell types while preserving RNA integrity. The protocol below uses a phenol-chloroform extraction followed by silica column purification (RNeasy mini plus kit) to obtain high-quality total RNA. A critical downstream step is DNase treatment (TURBO DNase) to remove co-extracted genomic DNA, which would otherwise introduce false signals in expression analyses.

### Reagents
-RLT buffer (Qiagen), β-mercaptoethanol, Superase-In 20U/μL (Thermo Fisher Scientific), proteinase K (20mg/mL), 100% ethanol, 70% ethanol, 3M sodium acetate, phenol/chloroform/isoamyl alcohol 25:24:1 (pH5.2), RNase-free water
-kit RNeasy mini plus kit (Qiagen), TURBO DNA-free™ (Ambion) 

### Equipment  
FastPrep-24™ 5G(MP), pipette, aerosol barrier pipette tips, microcetrifuge, 1mm zirconia/silica beads  
Optional; Qubit fluorometer (Thermo Fisher Scientific), Fragment analyzer  

### Stock solutions

| Stock solution A | volume |
| --- | ---|
| RLT buffer(Qiagen) | 975 μL |
| β-mercaptoethanol | 10 μL |
| Superase-In, 20U/μL | 15 μL |
| Total | 1 ml |

### RNA preparation
- Place fecal sample and beads in each screw-top tube and process the reaction mixture.  
| Each tube |  |
| --- | --- |
| Fecal sample | 150mg |
| 1.0mm zirconia/silica beads | ~20 |
| Stock solution A | 600 μL |

- Perform two cycles of FastPrep-24™ at 6.0 m/s for 40 seconds each.
- Centrifuge at 12,000 rpm for 3 minutes, transfer 600 μL of the supernatant to an e-tube.
- Add 15 μL of Proteinase K and incubate at room temperature for 10 minutes.
- Centrifuge at 12,000 rpm for 3 minutes, and transfer the supernatant to a new e-tube.
- Treat with an equal volume of phenol/chloroform/isoamyl alcohol 25:24:1 and vortex for 3 minutes.
- Centrifuge at 12,000 rpm for 3 minutes, and repeat the process of transferring the supernatant to a new e-tube twice.
- Add 0.1 times the volume of 3M sodium acetate and 2.5 times the volume of ethanol to the supernatant and incubate on ice for 30 minutes.
- Centrifuge at 12,000 rpm at 4°C for 30 minutes and remove the supernatant.
- Resuspend the pellet in 100 μL of distilled water and add 600 μL of RLT plus buffer from the RNeasy plus mini kit.
- Apply the solution from step 10 to the gDNA eliminator spin column of the RNeasy plus mini kit.
- Centrifuge at 12,000 rpm for 30 seconds, discard the column, and treat the flow-through with 70% ethanol at a 1:1 ratio.
- Transfer the solution from step 12 to the RNeasy spin column, centrifuge at 12,000 rpm for 15 seconds, and discard the flow-through.
- Add 700 μL of RW1 buffer to the column, centrifuge at 12,000 rpm for 15 seconds, and discard the flow-through.
- Add 500 μL of RPE buffer to the column, centrifuge at 12,000 rpm for 15 seconds, and discard the flow-through.
- Add another 500 μL of RPE buffer to the column, centrifuge at 12,000 rpm for 2 minutes, and transfer the column to a new e-tube.
- Treat the column's membrane with 30-50 μL of RNase-free water and centrifuge at 12,000 rpm for 1 minute to obtain RNA.

[Optional: RNA QC]
- Measure the RNA concentration using a Qubit fluorometer*.  
*A NanoDrop spectrophotometer can also be used, but for accurate concentration measurement, it is recommended to use a Qubit fluorometer.
- Perform QC of the obtained RNA using a Fragment analyzer.

<figure align = "center">
  <img src="https://github.com/sujin9819/MetaInsight/blob/main/SOP/MetaTranscriptomic/img/T_2_1.png?raw=true" style="width:65%">
  <figcaption><b>Example of RNA sample analysis results using a Fragment analyzer</b></figcaption>  
</figure>

- Prepare the 10X TURBO DNase buffer to a 1X concentration and add 1 μL of TURBO DNase to the RNA.
- Incubate at 37°C for 20-30 minutes.
- Add 0.1 times the volume of DNase inactivation reagent.
- Incubate at room temperature for 5 minutes.
- Centrifuge at 10,000 rpm for 1 minute and 30 seconds, and transfer the supernatant to a new e-tube.

### rRNA depletion

Ribosomal RNA (rRNA) typically constitutes 80–90% of total RNA in microbial samples, vastly outnumbering messenger RNA (mRNA). Without rRNA depletion, the majority of sequencing reads would be uninformative for gene expression analysis. Because metatranscriptomic samples contain RNA from both the host and diverse bacterial species, two separate depletion kits are applied sequentially: one targeting host (plant/mammalian) rRNA and another targeting bacterial rRNA using probe-based enzymatic degradation (Ribo-Zero Plus).

- Host rRNA remove Illumina TruSeq Stranded Total RNA Library Prep Plant Kit (Illumina, # 20020611)
- Bacterial rRNA remove Illumina Stranded Total RNA Library Prep with Ribo-Zero Plus kit (Illumina, #20040529)


## Sequencing

Once rRNA-depleted RNA is obtained, it is converted into a strand-specific cDNA library suitable for Illumina sequencing. Strand-specific (stranded) library preparation preserves the information about which DNA strand was originally transcribed, enabling accurate determination of sense versus antisense transcription — a distinction that is particularly important in prokaryotic genomes where overlapping genes on opposite strands are common.

### Sequencing library preparation  
- Perform mRNA fragmentation using divalent cations.
- First strand cDNA synthesis using SuperScript II reverse transcriptase (Invitrogen, #18064014) with random primers.
- Second strand cDNA synthesis using DNA Polymerase I, RNase H, and dUTP. 
- Perform end repair on synthesized cDNA fragments, followed by the attachment of a single 'A' base and adaptor ligation.  
- Perform PCR to create the cDNA library for sequencing.  
*Progress Sequencing library quantification  
KAPA Library Quantificatoin kits for Illumina Sequecing platforms according to the qPCR Quantification Protocol Guide (KAPA BIOSYSTEMS, #KK4854)  
*Conduct quality control (QC) for the sequencing library.  
TapeStation D1000 ScreenTape (Agilent Technologies, # 5067-5582)     

### Sequencing
- Perform paired-end (2×150 bp) sequencing on an Illumina NovaSeq (Illumina) instrument using the final indexed sequencing library.

### References

1. Illumina. TruSeq Stranded Total RNA Library Prep Kit - Reference Guide. Document #15031048. Illumina, Inc.

2. Ambion. RNAlater Stabilization Solution - User Guide. Life Technologies Corporation.

3. Thermo Fisher Scientific. TURBO DNA-free Kit - User Guide. Document #AM1907.

4. Agilent Technologies. TapeStation D1000 ScreenTape System User Guide. Document #G2964-90030.