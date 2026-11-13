# Lesson 2 — Databases and Accessions

## Learning Objectives
- Name the main NCBI databases and say what each holds
- Explain what an [accession](../GLOSSARY.md#accession) is and read its prefix
- Tell a raw sequencing run from a finished reference sequence
- Find and read a record on the NCBI website

## Conceptual Overview

Almost every analysis in this course starts or ends with a public database. You download reference sequences from one, compare your results against another, and submit your own data to a third. Learning to find things in them is a core skill.

### NCBI

The **National Center for Biotechnology Information (NCBI)** hosts the databases you will use most. These are the ones that matter for this course:

| Database | What it holds | Example from this course |
|----------|---------------|--------------------------|
| **SRA** (Sequence Read Archive) | Raw sequencing reads, as they came off the machine | `SRR1553607`, the Ebola reads in `Training/` |
| **GenBank** | Annotated nucleotide sequences submitted by researchers | `AF086833` |
| **RefSeq** | Curated, non-redundant reference sequences, built from GenBank | `NC_002549.1`, the Ebola reference genome |
| **Taxonomy** | The classification of every organism, with an ID for each | Taxon `186538`, *Zaire ebolavirus* |
| **BioProject** | A project that groups related data, samples, and papers | `PRJNA257197`, the project behind `SRR1553607` |

Two other resources are worth knowing by name. **Ensembl** provides genome browsers and annotation, mostly for vertebrates and other well-studied organisms. **UniProt** is the main database of protein sequences and their functions. This course focuses on NCBI, so you will meet those two only briefly.

### Raw data versus reference sequences

The most important distinction is between:

- **Raw reads** (SRA): the untouched output of a sequencer. Millions of short pieces, with quality scores. This is what you analyse.
- **Reference sequences** (GenBank, RefSeq): finished, assembled sequences that someone has checked and annotated. This is what you compare your reads against.

The Ebola example in `Training/` uses one of each. `SRR1553607` holds the raw reads from a 2014 sample. `NC_002549.1` is the finished genome of the first Ebola virus found, in 1976, and is used as the reference in Module 8.

### Accessions

An **accession** is a unique identifier for a record, and it never changes meaning. Everyone who cites `NC_002549.1` is pointing at exactly the same sequence. The letters at the start tell you what kind of record it is:

| Prefix | Meaning | Example |
|--------|---------|---------|
| `SRR` | An SRA sequencing run | `SRR1553607` |
| `PRJNA` | A BioProject | `PRJNA257197` |
| `NC_` | A RefSeq complete genomic molecule (chromosome or complete genome) | `NC_002549.1` |
| `NM_` | A RefSeq mRNA | `NM_000518.5` |
| `NP_` | A RefSeq protein | `NP_066243.1` |
| `NG_` | A RefSeq genomic region (for example one gene and its surroundings) | `NG_059281.1` |
| Two letters plus digits | A GenBank record from a submitter | `AF086833` |

A number after a dot, such as the `.1` in `NC_002549.1`, is the **version**. If the sequence is ever corrected, the version goes up (`.2`), so you can always tell exactly which sequence an analysis used. Always report the full accession with its version.

> **Tip:** Writing the accession and version of every reference you use in your notes is one of the easiest habits to adopt, and it makes your work reproducible.

## Worked Examples

### 1) Look up a RefSeq genome

In your web browser, open the NCBI record for the Ebola reference genome:

```
https://www.ncbi.nlm.nih.gov/nuccore/NC_002549.1
```

You will see a page that opens with a header block. Read these parts of it:

- **Title:** *Zaire ebolavirus isolate Ebola virus/H.sapiens-tc/COD/1976/Yambuku-Mayinga, complete genome*. The isolate name records the host (human), the country (COD, the Democratic Republic of the Congo), and the year (1976).
- **Length:** 18,959 bp.
- **Organism:** *Zaire ebolavirus*, with its classification below it.

### 2) Look up a sequencing run

Open the SRA record for the Ebola reads you have in `Training/`:

```
https://www.ncbi.nlm.nih.gov/sra/SRR1553607
```

Find these details:

- **Platform:** Illumina HiSeq 2500
- **Layout:** paired
- **Spots:** 203,445 (each spot is one read pair)
- **Organism:** *Zaire ebolavirus*

> **Note:** NCBI redesigns its pages from time to time, so the layout may differ from this description. The information is still there; look for the same labels.

## Exercises

1) Open `https://www.ncbi.nlm.nih.gov/nuccore/NC_002549.1`. What organism is it, and how long is the sequence?

2) In the title of that record, what do `COD` and `1976` tell you?

3) Open `https://www.ncbi.nlm.nih.gov/sra/SRR1553607`. What sequencing platform was used, and is the data single-end or paired-end?

4) For each accession, say what kind of record it is: `SRR11282407`, `NM_000518.5`, `NP_000509.1`.

5) Challenge: Search NCBI Nucleotide for `AF086833`. How does it relate to `NC_002549.1`? (Hint: read the comment on the `NC_002549.1` record.)

## Solutions

### Solution 1
*Zaire ebolavirus*, 18,959 bp (base pairs).

### Solution 2
`COD` is the country code for the Democratic Republic of the Congo, where the virus was isolated, and `1976` is the year of isolation. This is the first recognised Ebola outbreak, near Yambuku.

### Solution 3
Illumina HiSeq 2500, paired-end (layout: paired).

### Solution 4
`SRR11282407` is an SRA sequencing run (one of the gut amplicon samples in `Training/`). `NM_000518.5` is a RefSeq mRNA (the human beta-globin gene, *HBB*). `NP_000509.1` is a RefSeq protein (the beta-globin protein).

### Solution 5
`AF086833` is the original GenBank submission. The RefSeq record `NC_002549.1` is NCBI's curated copy of it, and the comment on the RefSeq record states that the reference sequence is identical to `AF086833`. This is the usual relationship: GenBank holds what submitters sent in, and RefSeq holds a checked reference derived from it.
