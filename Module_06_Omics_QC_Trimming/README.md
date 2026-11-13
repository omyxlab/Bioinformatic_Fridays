# Module 6: Omics, Quality Control, and Trimming

This module covers the first steps of any sequencing analysis: checking the quality of raw reads and cleaning them. You will use FastQC and MultiQC to assess data health, then trim poor-quality bases and artificial sequence from the reads.

This module builds on [Module 1](../Module_01_Bioinformatics_Foundations/README.md), where you met reads, quality scores, and the FASTQ format, and on [Module 4](../Module_04_Conda/README.md), which gives you the `bioinfo` environment.

## Learning objectives

By the end of this module, you will be able to:

- Assess the quality of raw sequencing reads with FastQC and MultiQC
- Interpret per-base quality and adapter content plots
- Trim adapters and low-quality bases from short reads
- Filter long reads by quality and length
- Confirm that trimming improved the data

## Lessons

| Lesson | Title | Status |
|--------|-------|--------|
| 1 | Precision quality control (QC) | Ready |
| 2 | Read trimming | Planned (not yet written) |

- **Lesson 1** runs FastQC and MultiQC on the data in `Training/` and explains how to read the reports.
- **Lesson 2** (planned) will trim adapters and low-quality bases from short reads with `fastp` and re-run FastQC for a before-and-after comparison, using the Ebola reads (`SRR1553607`) as the running example. It will also show quality and length filtering for long reads.

## Module toolbox

Activate the project environment before starting:

```bash
conda activate bioinfo
```

> Note: `Legacy_Lesson_1_The_Omics_Hierarchy.md` is the old first lesson of the Omics module. Its content is now covered by Module 1 (the omics layers, reads, and the FASTA, FASTQ, SAM/BAM, and VCF formats). It is kept here until it has been reviewed and can be removed.
