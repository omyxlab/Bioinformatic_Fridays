# Module 1: Bioinformatics Foundations

This module gives you the shared vocabulary and mental models for the rest of the course. It is a single two-hour session. You will learn what bioinformatics is, where sequence data comes from and where it is stored, what the common file formats look like, how genes are structured, and the handful of ideas (alignment, assembly, graphs, variants, homology, trees) that return in almost every later module.

Nothing here asks you to master a tool. Every idea gets a short explanation, a real example from the course data, and a pointer to the module that teaches it properly. The only commands are a few copy-and-paste ones in Lesson 4 that let you look at real files; Module 2 explains them in detail.

## Learning objectives

By the end of this module, you will be able to:

- Describe bioinformatics as the combination of biology and computation, and outline a typical workflow from sample to result
- Explain what a read is, how short and long reads differ, and what quality scores and coverage mean
- Find a record in NCBI and read its accession
- Distinguish a gene, a CDS, an exon, and an intron
- Recognise FASTA, FASTQ, and GenBank files and read their parts
- Explain alignment, reference-based and de novo assembly, and why graphs appear in bioinformatics
- Explain what a variant is, what homology means (orthologs and paralogs), and how to read a phylogenetic tree

## Lessons

| Lesson | Title | Time | What it covers |
|--------|-------|------|----------------|
| 1 | What Is Bioinformatics? | 20 min | The field, a typical workflow, sequencing technologies, reads, quality, coverage |
| 2 | Databases and Accessions | 12 min | NCBI and its main databases, what an accession is, finding a record |
| 3 | Genes and Genomes | 12 min | Genome, gene, mRNA, CDS, exon, intron, UTR, protein |
| 4 | File Formats: FASTA, FASTQ, and GenBank | 25 min | Looking inside real files, counting records, reading a GenBank record |
| 5 | From Reads to Genomes | 18 min | Alignment, reference-based and de novo assembly, contigs, graphs |
| 6 | From Sequences to Meaning | 18 min | Variants, similarity and homology, naming and ontologies, reading a tree |

That is about 105 minutes of content, leaving time for a break and questions.

## Course data used in this module

The examples use files from the `Training/` folder you downloaded in [Module 0](../Module_00_Getting_Ready/README.md):

| Files | What they are |
|-------|---------------|
| `Training/short_reads/paired/SRR1553607_1.fastq` and `_2.fastq` | Illumina paired-end reads from an Ebola virus sample |
| `Training/long_reads/barcode57.fastq` | Oxford Nanopore reads from a cassava leaf sample |
| `Training/short_reads/unpaired/*.fastq.gz` | Illumina amplicon reads from human gut samples (case and healthy) |

Reference sequences (FASTA, GenBank) come from NCBI, which you will visit in Lessons 2 and 4.

> **Note:** If you did not finish Module 0, do that first. Lesson 4 needs your terminal, internet access, and the `Training/` folder.

Reference material for this module: [Glossary](../GLOSSARY.md) and [File formats reference](../File_Formats_Reference.md).
