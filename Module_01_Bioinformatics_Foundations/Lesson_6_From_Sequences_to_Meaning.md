# Lesson 6 — From Sequences to Meaning

## Learning Objectives
- Define a [variant](../GLOSSARY.md#variant) (SNP or indel) and a [consensus](../GLOSSARY.md#consensus) sequence
- Explain what a [BLAST](../GLOSSARY.md#blast) search reports, and what percent identity and E-value mean
- Distinguish similarity from [homology](../GLOSSARY.md#homolog), and an [ortholog](../GLOSSARY.md#ortholog) from a [paralog](../GLOSSARY.md#paralog)
- Explain what taxonomy and [Gene Ontology](../GLOSSARY.md#gene-ontology) are for
- Read a [phylogenetic tree](../GLOSSARY.md#phylogenetic-tree)

## Conceptual Overview

Once you have reads mapped or a genome assembled, the biological work begins: what is different, what is it similar to, what does it do, and how is it related to other things? This lesson introduces the vocabulary for those questions.

### Variants and consensus

A **variant** is a position where your sample differs from the reference. There are two basic kinds:

| Kind | Meaning | Example (reference → sample) |
|------|---------|------------------------------|
| **SNP** (single-nucleotide polymorphism) | One base replaced by another | `ATGCATT` → `ATGGATT` (the `C` became `G`) |
| **Indel** (insertion or deletion) | One or more bases added or removed | `ATGCATT` → `ATGCTT` (the `A` was deleted) |

**Variant calling** is the process of deciding, at every position in the genome, whether the sample really differs from the reference. It uses all the reads covering the position. One read that disagrees is probably an error; nearly all reads disagreeing is almost certainly a real variant. This is why [coverage](../GLOSSARY.md#coverage) matters.

The **consensus** sequence is what you get when you apply a sample's variants to the reference: the best estimate of the sample's own sequence. The 2014 Ebola sample and the 1976 reference are about four decades apart, so you will find many variants between them in Module 8.

### Searching for similar sequences

A common question is "what is this sequence?" **BLAST** (Basic Local Alignment Search Tool) answers it by searching a database for sequences similar to yours and listing the best matches. Each match, or hit, comes with two numbers worth understanding:

| Number | What it tells you |
|--------|-------------------|
| **Percent identity** | The share of positions that are identical in the aligned region. 99% means almost the same sequence |
| **E-value** | How many hits this good you would expect to find by chance in a database of this size. Smaller is better, and a value near 0 means a match this good is very unlikely to be an accident |

You use BLAST in Module 7 to find out which virus a contig comes from. A high identity with an E-value near 0 is strong evidence. A low identity with a large E-value is not.

### Similarity and homology

These two words are often confused.

- **Similarity** is something you measure: the percent identity between two sequences.
- **Homology** is a conclusion: that two sequences share a common ancestor. Sequences are either homologous or they are not. It makes no sense to say "70% homologous", though you can say they are 70% identical and therefore likely homologous.

Homologous genes fall into two groups, depending on how they came to be different:

| Term | Meaning | Example |
|------|---------|---------|
| **Ortholog** | Homologs in different species that diverged when the species split (speciation). Same gene, different species | The *NP* gene of Zaire ebolavirus and of Sudan ebolavirus; human *HBB* and chimpanzee *HBB* |
| **Paralog** | Homologs in the same genome that arose when a gene was copied (duplication) | Human *HBB* (beta-globin) and *HBD* (delta-globin) |

The distinction matters when you want to infer what a gene does. Orthologs usually keep the same function, so transferring function from an ortholog is fairly safe. Paralogs have often drifted apart in function after the copy was made, so the same inference is riskier. When a BLAST search returns many hits, it helps to ask whether each is an ortholog or a paralog of your gene.

### Names and ontologies

Biology has a naming problem: the same thing can be called many things. Two systems help.

**Taxonomy** is the classification of organisms into nested groups. Every organism in NCBI has a stable **taxonomy ID**, for example `186538` for *Zaire ebolavirus*. The GenBank record from Lesson 4 listed the lineage from the broadest group (`Viruses`) down to the species. Names are revised over time. That same lineage ends with a newer formal name, *Orthoebolavirus zairense*, while records still use *Zaire ebolavirus*. Identifiers and accessions stay put, which is why you cite them.

**Gene nomenclature** gives each gene a short symbol, such as *HBB* or *NP*. By convention the gene symbol is written in italics and the protein it makes in plain text.

An **ontology** is a shared, controlled vocabulary of terms with defined relationships between them. The **Gene Ontology (GO)** describes what genes and proteins do, in three areas:

### Phylogenetic trees

A **phylogenetic tree** is a diagram of how samples, species, or genes are related by descent. The labelled ends are the **tips**. The points where branches split are **nodes**, and each stands for a common ancestor.

```
              +---------- Sample_A
         +----|
         |    +---------- Sample_B
    -----|
         |         +----- Sample_C
         +---------|
                   +----- Sample_D
```

How to read it:

- **Closeness means a recent shared ancestor**, not nearness on the page. Sample_A and Sample_B join at a node that is more recent than the one joining them to Sample_C, so A and B are more closely related to each other than either is to C.
- The order of tips up and down the page carries no meaning. You can swap the two branches at any node without changing the tree.
- In many trees, the **length of a branch** shows the amount of change. Longer branches mean more change.

A tree is a graph with no loops, which connects back to Lesson 5. You will build trees from sequence alignments in Module 10, and the capstone project asks you to place a virus in a tree.

## Worked Examples

### 1) Classify variants

Compare the reference `ATGCATT` with two samples:

| Sample | Sequence | What happened |
|--------|----------|---------------|
| 1 | `ATGGATT` | Position 4 changed from `C` to `G`: a SNP |
| 2 | `ATGCTT` | The `A` at position 5 is missing: a deletion, so an indel |

### 2) Weighing the evidence at one position

Two positions each show a base that differs from the reference:

| Position | Reads covering it | Reads that disagree with the reference |
|----------|-------------------|----------------------------------------|
| 100 | 40 | 1 |
| 250 | 40 | 38 |

Position 100 is most likely a sequencing error in one read. Position 250, where nearly every read agrees on the difference, is very likely a real variant.

### 3) Reading a BLAST hit

A contig from the cassava sample returns this top hit (the values here are illustrative):

| Hit | Percent identity | E-value |
|-----|------------------|---------|
| A cassava begomovirus genome | 98% | 0.0 |

A 98% identical match with an E-value of 0 is strong evidence that the contig is from a closely related begomovirus.

## Exercises

1) Compare the reference `ACGTTGCA` with the sample `ACGTAGCA`, and the reference `ACGTTGCA` with the sample `ACGTGCA`. Name the variant in each case.

2) A position is covered by 50 reads. In one case 2 reads show a different base, and in another 47 do. Which is more likely to be a real variant, and why?

3) BLAST gives two hits for your sequence: Hit X at 96% identity with an E-value of 0.0, and Hit Y at 31% identity with an E-value of 2.0. Which is more believable?

4) For each pair, say whether the genes are orthologs, paralogs, or neither: (a) human *HBB* and chimpanzee *HBB*; (b) human *HBB* and human *HBD*; (c) the *NP* gene of Zaire ebolavirus and the *NP* gene of Reston ebolavirus.

5) Look at the tree in this lesson. Is Sample_C more closely related to Sample_D or to Sample_A? How can you tell?

6) Challenge: `GO:0015671` is "oxygen transport". Which of the three GO areas does it belong to?

## Solutions

### Solution 1
`ACGTTGCA` → `ACGTAGCA`: the `T` at position 5 became `A`, a **SNP**. `ACGTTGCA` → `ACGTGCA`: one of the two `T`s is missing, a **deletion** (an indel).

### Solution 2
The position with 47 of 50 reads in agreement. When almost every read shows the same difference, an error in each one is very unlikely. Two reads out of 50 is consistent with random sequencing errors.

### Solution 3
**Hit X.** High identity with an E-value of 0.0 means the match is very unlikely to be by chance. Hit Y has low identity and an E-value of 2.0, meaning you would expect about two hits that good by chance in a database of that size, so it tells you very little.

### Solution 4
(a) **Orthologs**: the same gene in two different species. (b) **Paralogs**: two related genes in the same genome, from a gene duplication. (c) **Orthologs**: the same gene in two different species.

### Solution 5
Sample_C is more closely related to **Sample_D**. C and D join at their own node, which is a more recent common ancestor than the node where C's branch meets A and B. Closeness is read from the shared ancestor, not from how near the labels are on the page.

### Solution 6
**Biological process.** It describes a larger process (moving oxygen), not a molecular activity or a location.
