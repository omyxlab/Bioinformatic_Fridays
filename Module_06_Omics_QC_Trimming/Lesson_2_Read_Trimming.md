# Lesson 2 — Read Trimming

> **Status: planned, not yet written.** This file records what the lesson will cover so that the numbering and cross-references in the module are correct (Lesson 1 already refers forward to trimming). Write it following [`STYLE_GUIDE.md`](../STYLE_GUIDE.md).

## Planned learning objectives
- Explain why adapters and low-quality bases are trimmed
- Trim paired-end short reads with `fastp`
- Read the `fastp` report
- Re-run FastQC to compare reads before and after trimming
- Filter long reads by quality and length

## Planned content
1. **Why trim:** adapter contamination and low-quality read ends (links back to Lesson 1's FastQC plots).
2. **Short reads:** `fastp` on the paired Ebola reads (`Training/short_reads/paired/SRR1553607_1.fastq` and `_2.fastq`). Keep the mates paired. Output trimmed FASTQ files and an HTML report.
3. **Before and after:** FastQC and MultiQC on the raw and trimmed reads side by side.
4. **Long reads:** a brief look at quality and length filtering with `chopper` or `filtlong` on `barcode57.fastq`.
5. **Reproducibility:** write the trimming command into a script so it can be rerun (links to Module 5).

## Notes for the author
- The trimmed Ebola reads are the input for Module 8 (Variant Calling).
- Check that `fastp` is in the `bioinfo` environment before teaching.
