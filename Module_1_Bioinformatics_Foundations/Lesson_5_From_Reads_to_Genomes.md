# Lesson 5 — From Reads to Genomes

## Learning Objectives
- Explain what [alignment](../GLOSSARY.md#alignment) and [mapping](../GLOSSARY.md#mapping) are
- Distinguish [reference-based](../GLOSSARY.md#reference-based-assembly) from [de novo](../GLOSSARY.md#de-novo-assembly) assembly and say when to use each
- Define a [contig](../GLOSSARY.md#contig) and explain why repeats make assembly hard
- Explain what a [graph](../GLOSSARY.md#graph) is and name four places it appears in this course

## Conceptual Overview

A sequencer gives you millions of short reads, not a genome. This lesson covers the two basic ideas for turning reads into something useful: placing reads against a sequence you already have (alignment and mapping), and rebuilding a sequence from the reads alone (assembly).

### Alignment and mapping

An **alignment** lines up two sequences so that matching positions sit above each other, and shows where they differ. **Mapping** is the same idea applied to reads: each read is aligned against a **reference** sequence to find where it came from.

```
Reference:  A T G C C A T T G A C G T
Read:           G C C A T A G A C
Match:          | | | | | x | | |
```

This read fits the reference starting at position 3. Eight of its nine bases match. The read has an `A` where the reference has a `T` (position 8), which is marked `x`. One mismatch in one read could be a sequencing error. If most of the reads covering that position show the same difference, it is a real difference between your sample and the reference. That is a variant, covered in Lesson 6.

Mapping is used to find where reads come from, to count them, and to remove reads from an unwanted source such as the host. You will do it with real tools in Modules 7 and 8.

### Assembly

**Assembly** rebuilds longer sequences from reads. There are two strategies. Think of a jigsaw puzzle: with the picture on the box you can place each piece by looking at it, and without the picture you can only fit pieces together by their edges.

| | Reference-based assembly | De novo assembly |
|---|---|---|
| Idea | Map reads to a known genome and read off the sample's sequence | Join reads into longer sequences using only the overlaps between them |
| Needs | A good, closely related reference | Nothing but the reads |
| Use when | A close reference exists and you want to know how your sample differs | There is no suitable reference, or you expect sequence that the reference lacks |
| Strengths | Fast, simple, reproducible | Finds new sequence and rearrangements, without reference bias |
| Weaknesses | Misses sequence that is not in the reference | Needs more computing, and is sensitive to read quality and coverage |

Neither is better in general. In this course you use both: de novo assembly to find what virus is in a cassava leaf (the sequence is unknown), and reference-based work to compare the 2014 Ebola virus to the 1976 reference (the reference is known). Both are covered in Module 7, and the Ebola comparison is the subject of Module 8.

The sequences that de novo assembly produces are called **contigs**: contiguous stretches built from overlapping reads. An assembly is usually a set of contigs, not one complete genome. A good assembly has few, long contigs.

### Why repeats are hard

A **repeat** is a sequence that occurs more than once in a genome. If a read fits entirely inside a repeat, nothing in the read says which copy it came from. The assembler cannot tell how the repeat connects to the sequence on either side, and the assembly breaks there. Reads longer than the repeat can reach unique sequence on each side and resolve it. This is the main reason long reads are valuable for assembly.

### Graphs

You will hear about graphs in assembly, so it helps to know the idea. A **graph** is a set of dots, called **nodes**, joined by lines, called **edges**. It is a way of drawing things that are connected. You do not need any graph theory for this course.

In assembly, the pieces are nodes and an edge joins two pieces that overlap. A contig is a path through the graph, following the edges from one end to the other.

```
Read A  ->  Read B  ->  Read C  ->  Read D
```

A repeat shows up as a place where several paths meet and then split again:

```
Read A  --\                    /--> Read D
           +--> [ repeat ] ---+
Read B  --/                    \--> Read E
```

Here the assembler cannot tell whether A leads to D or to E. A read that spans from A through the repeat into D would settle it. Different assemblers use different kinds of graph (SPAdes uses a de Bruijn graph for short reads; Flye uses a repeat graph for long reads), but the picture is the same.

Graphs appear in four places in this course:

| Where | What the nodes and edges are |
|-------|------------------------------|
| Assembly (Module 7) | Pieces of sequence, joined by overlaps |
| Phylogenetic trees (Module 10) | Samples and common ancestors, joined by branches. A tree is a graph with no loops |
| Git history (Module 3) | Commits, joined to the commits they came from. Branching and merging make a graph |
| Workflow diagrams (Module 11 and the capstone) | Analysis steps, joined by the files passed between them |

## Worked Examples

### 1) Reading an alignment

Take the alignment at the top of this lesson. The read starts at reference position 3 and covers positions 3 to 11. Walking along:

| Position | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 |
|----------|---|---|---|---|---|---|---|----|----|
| Reference | G | C | C | A | T | T | G | A | C |
| Read | G | C | C | A | T | A | G | A | C |
| Match? | yes | yes | yes | yes | yes | **no** | yes | yes | yes |

### 2) Shred and rebuild a sentence

Think of a short sentence as a genome and cut copies of it into overlapping fragments. These are your reads:

```
Fragment A:  THE QUICK BROWN
Fragment B:  BROWN FOX JUMPS
Fragment C:  JUMPS OVER THE
Fragment D:  OVER THE LAZY
Fragment E:  LAZY DOG
```

**De novo.** With no guide, join fragments where the end of one matches the start of another. A ends with `BROWN` and B starts with `BROWN`. B ends with `JUMPS` and C starts with `JUMPS`. C ends with `OVER THE` and D starts with `OVER THE`. D ends with `LAZY` and E starts with `LAZY`. Joining all five along those overlaps gives:

```
THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG
```

**Reference-based.** Now suppose you have a close but not identical reference: `THE QUICK BROWN BOX JUMPS OVER THE LAZY DOG`. Place each fragment on it. A, C, D, and E match exactly. B matches except for one letter: your fragment says `FOX` where the reference says `BOX`. That single difference between your sample and the reference is a variant.

Notice also that `THE` occurs twice in the sentence, a tiny repeat. It causes no trouble here because every fragment is longer than `THE` and reaches unique words on either side. If the fragments were only three letters long, they could not be placed.

## Exercises

1) Align the read `GCCATAGAC` to the reference `ATGCCATTGACGT`. At which reference position does the read start, and at which reference position is there a mismatch?

2) Using the fragments in Example 2, rebuild the sentence de novo yourself, without looking at the answer. Which two fragments contain the repeated word `THE`?

3) For each case, choose reference-based or de novo assembly, and say why: (a) a well-studied bacterium with a high-quality reference genome; (b) a newly discovered virus with no close relatives; (c) comparing the 2014 Ebola virus (`SRR1553607`) to the 1976 reference `NC_002549.1`.

4) In the repeat graph above, what kind of read would let the assembler connect Read A to Read D?

5) Challenge: Name the four places in this course where a graph appears.

## Solutions

### Solution 1
The read starts at reference position **3**. The mismatch is at reference position **8**, where the reference has `T` and the read has `A`.

### Solution 2
The result is `THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG`. Fragments **A**, **C**, and **D** contain `THE`. Fragment A holds the first occurrence, at the start of the sentence. Fragments C and D, which overlap each other, both hold the second occurrence, near the end.

### Solution 3
(a) **Reference-based.** A good reference exists, so mapping is faster and simpler. (b) **De novo.** There is nothing to map to, and the virus may carry sequence no reference has. (c) **Reference-based.** The reference is known and the goal is to find how the sample differs from it. This is what Module 8 does.

### Solution 4
A read, or a long read pair, that spans from Read A across the repeat and into Read D. It shows that A and D belong together, so the assembler can resolve the branch.

### Solution 5
Assembly graphs (Module 7), phylogenetic trees (Module 10), Git history (Module 3), and workflow diagrams (Module 11 and the capstone).
