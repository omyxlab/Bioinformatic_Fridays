# Lesson 3 — Genes and Genomes

## Learning Objectives
- Define [genome](../GLOSSARY.md#genome), chromosome, and [gene](../GLOSSARY.md#gene)
- Describe how a gene becomes a protein
- Distinguish a gene, an mRNA, a [CDS](../GLOSSARY.md#cds), and an untranslated region
- Explain what [exons](../GLOSSARY.md#exon) and [introns](../GLOSSARY.md#intron) are and how splicing joins them
- Read feature coordinates for a simple gene and for a split gene

## Conceptual Overview

You will meet the words in this lesson in database records, in annotation files, and in the output of almost every tool in the course. They describe how information is organised inside a genome.

### Genome, chromosome, gene

- A **genome** is the complete set of genetic material of an organism. The Ebola virus genome is a single RNA molecule of 18,959 bases. The human genome is about 3 billion base pairs.
- A **chromosome** is one long, continuous molecule of that material. Humans have 23 pairs. A virus like Ebola has just one.
- A **gene** is a region of the genome that encodes a functional product, most often a protein. The Ebola genome has 7 genes. The human genome has around 20,000 protein-coding genes.

### From gene to protein

The flow of information in a cell goes from DNA to RNA to protein:

1. **Transcription** copies a gene into RNA.
2. In organisms with introns, the RNA is **spliced**: some parts are cut out and the rest are joined together. The result is the **mRNA** (messenger RNA).
3. **Translation** reads the mRNA three bases at a time. Each group of three bases, a **codon**, specifies one amino acid. The amino acids are joined into the **protein**.

### The parts of a gene

Four terms describe different parts of this picture, and they are easy to confuse:

| Term | Meaning |
|------|---------|
| **Exon** | A part of the gene that is kept in the mRNA after splicing |
| **Intron** | A part of the gene that is cut out by splicing and is not in the mRNA |
| **UTR** (untranslated region) | A stretch at each end of the mRNA that is not translated: the 5' UTR before the coding region and the 3' UTR after it |
| **CDS** (coding sequence) | The part of the mRNA that is actually translated, from the start codon to the stop codon. Its length is always a multiple of three |

So the mRNA is made of the exons joined together, and inside the mRNA the CDS is the stretch that makes protein. The UTRs are in the mRNA but not in the protein, and the introns are in the gene but not in the mRNA.

This is what a split gene looks like (not to scale):

```
Gene (genomic DNA):   exon 1 ---- intron 1 ---- exon 2 ---- intron 2 ---- exon 3
                         |                         |                         |
                         |       splicing removes the introns                |
                         v                         v                         v
mRNA:                 [5' UTR + CDS ... exon 1][exon 2][exon 3 ... CDS + 3' UTR]
Protein:                 translated from the CDS only
```

### Not every organism has introns

Genes in bacteria are almost always continuous, and so are the genes of Ebola virus: they have no introns, so the CDS is a single unbroken stretch and no splicing is needed. Genes in humans and other eukaryotes are often split into several exons by introns. In human genes, introns are frequently much longer than the exons.

This matters when you read a database record. A gene's location is written as a range such as `56..3026`. A split gene's location is written as a `join` of several ranges, one per exon.

## Worked Examples

Both examples use real records. The coordinates are positions along the record's sequence, counted from 1.

### 1) A continuous gene: the Ebola *NP* gene

In the Ebola reference genome `NC_002549.1`, the nucleoprotein gene is annotated like this:

```
gene    56..3026      /gene="NP"
CDS     470..2689     /gene="NP"   /product="nucleoprotein"   /protein_id="NP_066243.1"
```

Reading it:

- The **gene** is 3026 − 56 + 1 = **2,971 bases** long.
- The **CDS** is 2689 − 470 + 1 = **2,220 bases** long. Divided by three, that is 740 codons: 739 amino acids plus one stop codon. The protein `NP_066243.1` is 739 amino acids long.
- The CDS is shorter than the gene. The 414 bases before it (positions 56 to 469) and the 337 bases after it (2690 to 3026) are untranslated regions of the mRNA.
- The CDS is one range, with no `join`, because the gene has no introns.

### 2) A split gene: human *HBB* (beta-globin)

In the RefSeq record `NG_059281.1`, which holds the human beta-globin gene and its surroundings, the same kinds of features are annotated, but the locations are written as joins:

```
gene    5001..6608
mRNA    join(5001..5142,5273..5495,6346..6608)
CDS     join(5051..5142,5273..5495,6346..6474)
exon    5001..5142
exon    5273..5495
exon    6346..6608
```

Reading it:

- The gene spans positions 5001 to 6608, which is **1,608 bases**.
- There are **three exons**: 5001..5142 (142 bases), 5273..5495 (223 bases), and 6346..6608 (263 bases). Together they make the **628-base mRNA**.
- The **introns** are the gaps between the exons: 5143..5272 (**130 bases**) and 5496..6345 (**850 bases**). Introns are not listed as features in this record; you find them by looking between the exons.
- The **CDS** is also a join of three pieces. It starts at 5051, inside exon 1 (so exon 1 begins with 50 bases of 5' UTR), and ends at 6474, inside exon 3 (so the rest of exon 3 is 3' UTR). Its pieces total 92 + 223 + 129 = **444 bases**, which is 148 codons: 147 amino acids plus a stop codon.

Notice what this means in practice: if you took the genomic DNA from position 5051 and translated it straight through, you would run into the introns and get the wrong protein. Splicing has to happen first.

## Exercises

1) The Ebola *VP35* gene in `NC_002549.1` is annotated as `gene 3032..4407` and `CDS 3129..4151`. How long is the gene? How long is the CDS? How many amino acids does the protein have?

2) Using the *HBB* coordinates in Example 2, add up the two intron lengths. What fraction of the 1,608-base gene is intron?

3) For each of the following, say whether it is present in (a) the gene, (b) the mRNA, (c) the protein: an exon, an intron, a 5' UTR, the CDS.

4) Why can you not predict the beta-globin protein by translating the genomic DNA of *HBB* from start to end?

5) Challenge: Ebola *NP* has no introns, but *HBB* has two. Which gene would you expect to have a CDS written as a single range, and which as a join? How would you recognise each in a database record?

## Solutions

### Solution 1
Gene: 4407 − 3032 + 1 = **1,376 bases**. CDS: 4151 − 3129 + 1 = **1,023 bases**. 1,023 / 3 = 341 codons, which is 340 amino acids plus a stop codon.

### Solution 2
130 + 850 = **980 bases** of intron. 980 / 1,608 ≈ 0.61, so **about 61%** of the gene is intron.

### Solution 3
- **Exon:** in the gene, in the mRNA, and (the coding part of it) in the protein.
- **Intron:** in the gene only. Splicing removes it from the mRNA, so it is not in the protein.
- **5' UTR:** in the gene and in the mRNA, but not in the protein.
- **CDS:** in the gene and in the mRNA; it is the part that is translated into the protein.

### Solution 4
The introns sit between the exons in the genomic DNA. Translating straight through would read intron sequence as if it were coding, shifting the reading frame and giving a wrong protein. The introns must be removed and the exons joined first, which is what splicing does to make the mRNA.

### Solution 5
*NP* (Ebola) would have a CDS written as a single range, such as `470..2689`, because it has no introns. *HBB* would have a CDS written as a `join(...)` of several ranges, such as `join(5051..5142,5273..5495,6346..6474)`, one per coding exon. In a database record the word `join` in a location tells you the feature is made of separate pieces.
