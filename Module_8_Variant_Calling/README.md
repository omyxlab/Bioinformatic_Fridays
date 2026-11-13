# Module 8: Variant Calling

> **Status: planned, not yet written.** This file records the plan so that numbering and cross-references are correct. Write the lessons following [`STYLE_GUIDE.md`](../STYLE_GUIDE.md).

This module takes a sequencing sample from raw reads to a list of variants. You will map short reads to a reference, call the differences, read and filter the resulting VCF file, and build a consensus genome.

## Planned dataset

The Ebola virus sample `SRR1553607` (paired-end Illumina reads in `Training/short_reads/paired/`, trimmed in Module 6) is mapped against the reference genome `NC_002549.1`, a 1976 isolate from the Democratic Republic of the Congo. The sample is from the 2014 outbreak, so the two genomes are about four decades apart. The reference is downloaded from NCBI by accession; if you already downloaded it in [Module 1](../Module_1_Bioinformatics_Foundations/Lesson_4_File_Formats.md), you can reuse it.

## Planned learning objectives

- Explain what a variant is and what variant calling does
- Prepare a reference and map short reads to it
- Call variants with `bcftools`
- Read the header, columns, and `INFO` fields of a VCF file
- Count and filter variants, and judge them with simple checks
- Explain how the choice of reference changes the number of variants
- Build a consensus genome from the variants

## Planned lessons

| Lesson | Title | Content |
|--------|-------|---------|
| 1 | Variants and variant calling | SNP versus indel; the pileup-then-decide idea; why reference choice matters |
| 2 | Preparing a reference and mapping short reads | Download the reference by accession; index it; map with `bwa mem`; sort and index with `samtools`; check with `flagstat` and coverage; look at pileups in `samtools tview` |
| 3 | Calling variants | `bcftools mpileup` piped to `bcftools call -mv --ploidy 1`; reading the command piece by piece; why the ploidy is 1 for a virus |
| 4 | Reading a VCF | Header lines, the `#CHROM` line, the columns, and the `DP`, `DP4`, and `MQ` fields; `bcftools query` |
| 5 | Counting and filtering variants | `grep` and `bcftools stats`; filtering with `bcftools view -i`; transitions versus transversions as a check |
| 6 | Reference choice and the consensus genome | Why a distant reference gives many variants; comparing with a closer reference; `bcftools consensus`; viewing in IGV |

Optional extras: annotating variants with SnpEff, and a brief mention of other callers (FreeBayes, GATK) and of long-read callers.

## Prerequisites

[Module 6](../Module_6_Omics_QC_Trimming/README.md) (trimmed Ebola reads), [Module 4](../Module_4_Conda/README.md) (the `bioinfo` environment, which needs `bwa`, `samtools`, and `bcftools`), and [Module 1](../Module_1_Bioinformatics_Foundations/README.md) (the vocabulary of variants and alignment).

## Design notes

This module is adapted from the variant calling lesson in the Bowen 2026 training. Keep the discussion question about why the variant count depends on the reference, the `INDEL` header trap when counting with `grep`, and a "if something looks different" troubleshooting table in each lesson. Re-style code blocks to this course's guide (no `$` prompt characters).
