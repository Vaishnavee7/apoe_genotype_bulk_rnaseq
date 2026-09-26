# APOE3/APOE4 Brain Organoid Bulk RNA-seq Analysis

## Overview

This repository contains the analysis of bulk RNA-seq data from human brain organoids carrying either the **APOE3** or **APOE4** genotype and exposed to an induced ageing treatment for different durations.

The dataset consists of:

- 2 APOE genotypes: APOE3 and APOE4
- 3 treatment durations: CTRL, 10D and 20D
- 3 biological replicates per experimental condition
- 18 samples in total

The main objective was to investigate how **APOE genotype** and **induced ageing treatment** affect the transcriptional state of human brain organoids.

## Research Questions

The analysis focused on four main questions:

1. **Does APOE genotype affect gene expression?**
   - APOE4 vs APOE3 at baseline (CTRL)

2. **How does 20D ageing affect APOE3 organoids?**
   - APOE3 20D vs APOE3 CTRL

3. **How does 20D ageing affect APOE4 organoids?**
   - APOE4 20D vs APOE4 CTRL

4. **Does 20D treatment change the transcriptional difference between APOE4 and APOE3?**
   - Genotype × 20D interaction

## Analysis Workflow

The analysis included:

1. **Quality control and preprocessing**
   - Inspection of sequencing QC metrics using the supplied MultiQC report
   - Gene filtering based on minimum count thresholds
   - Library-size assessment

2. **Exploratory analysis**
   - Log-transformed CPM
   - Principal component analysis (PCA)
   - Sample-to-sample correlation
   - Replicate consistency and distance analysis

3. **Differential expression analysis**
   - DESeq2-based differential expression analysis
   - Multiple-testing correction using FDR
   - Identification of upregulated and downregulated genes
   - Volcano plots and top-gene heatmaps

4. **Functional enrichment**
   - Gene Ontology Biological Process enrichment
   - Separate analysis of positively and negatively regulated genes
   - g:Profiler was used for enrichment analysis

5. **Interaction analysis**
   - Genotype × 20D interaction using a factorial DESeq2 model
   - Used to identify genes whose response to 20D differed between APOE3 and APOE4

6. **Biological interpretation**
   - Interpretation of genotype-associated transcriptional programs
   - Comparison of ageing responses between APOE3 and APOE4
   - Consideration of bulk-organoid-specific limitations

## Main Findings

### APOE genotype at baseline

APOE4 and APOE3 organoids showed substantial transcriptional differences at baseline.

The baseline APOE4-associated transcriptional state was characterized by enrichment of:

- immune and defense-related processes
- inflammatory/response-related programs
- cell-cycle and mitotic processes

A total of **1,984 genes** were differentially expressed between APOE4 and APOE3 at baseline:

- 1,308 higher in APOE4
- 676 lower in APOE4

### Effect of 20D treatment

20D treatment induced extensive transcriptional remodeling in both genotypes.

#### APOE3

APOE3 20D vs CTRL identified **4,503 DE genes**:

- 2,310 higher after 20D
- 2,193 lower after 20D

Enriched processes included signaling, transport, extracellular organization, immune/defense responses, and chromatin/cell-cycle-related programs.

#### APOE4

APOE4 20D vs CTRL identified **4,895 DE genes**:

- 2,501 higher after 20D
- 2,394 lower after 20D

Upregulated genes were enriched for developmental, proliferative, differentiation and cell-cycle processes, while downregulated genes were enriched for cilium movement, axoneme assembly, microtubule-associated processes, nucleosome organization and viral-response processes.

### Genotype × 20D interaction

The genotype × 20D interaction identified **3,548 genes** whose APOE4–APOE3 difference changed following 20D treatment:

- 1,778 positive interaction effects
- 1,770 negative interaction effects

Positive interaction effects were enriched for developmental, proliferative, differentiation and cell-cycle processes.

Negative interaction effects were enriched for sensory perception, chemical stimulus detection and synaptic/trans-synaptic signaling.

Overall, the interaction analysis indicates that the transcriptional response to 20D is **genotype-dependent**.

## Important Experimental Consideration

The 10D samples were harvested at a different experimental time point from the CTRL and 20D samples.

Therefore, **ageing treatment and harvest day are confounded for the 10D condition**.

For this reason, the genotype × treatment interaction analysis was restricted to CTRL and 20D samples, which were both harvested at the same experimental time point.

## Organoid-Specific Considerations

Because this is bulk RNA-seq from brain organoids, observed transcriptional differences can arise from:

- cell-intrinsic changes in gene expression
- changes in the relative abundance of cell populations
- both effects simultaneously

Therefore, the identified pathways represent transcriptional programs associated with the experimental conditions but cannot establish cell-type-specific mechanisms.

## Circular RNA Analysis

Circular RNA analysis was not performed because the supplied data consisted of **gene-level count matrices**.

Reliable circRNA analysis requires information such as **back-splice junction reads**, which was not available in the supplied dataset.

## Repository Structure

```text
.
├── data/
│   ├── counts.tsv
│   ├── RNAseq_challenge_metadata.csv
│   └── multiqc_report.html
│
├── APOE3_APOE4_ageing_bulkRNAseq_analysis.ipynb
│
└── README.md