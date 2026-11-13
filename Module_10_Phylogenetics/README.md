# Module 10: Phylogenetics

> **Status: planned, not yet written.** This file records the plan so that numbering and cross-references are correct. Write the lessons following [`STYLE_GUIDE.md`](../STYLE_GUIDE.md).

This module teaches how to place sequences in a phylogenetic tree: align them, infer a tree, and view it. It is the method the capstone project depends on.

## Planned learning objectives

- Explain what a multiple sequence alignment is and why trees are built from one
- Build a multiple sequence alignment with MAFFT
- Trim poorly aligned regions
- Infer a tree with IQ-TREE or FastTree
- View and annotate a tree, and read it correctly

## Planned lessons

| Lesson | Title | Content |
|--------|-------|---------|
| 1 | From sequences to a tree | The workflow; choosing sequences; why a good set of references matters |
| 2 | Multiple sequence alignment | MAFFT; reading an alignment; trimming with trimAl |
| 3 | Inferring a tree | IQ-TREE or FastTree; substitution models in plain terms; support values |
| 4 | Viewing and annotating trees | FigTree, `ggtree`, or `ete3`; rooting; labelling tips |

## Candidate practice data

The five Ebola virus reference genomes downloaded in [Module 1, Lesson 4](../Module_1_Bioinformatics_Foundations/Lesson_4_File_Formats.md) (`ebolavirus_refseq.fasta`), and the consensus genome from Module 8, are natural inputs for practising the workflow before the capstone.

## Prerequisites

[Module 1](../Module_1_Bioinformatics_Foundations/README.md) (trees and homology), [Module 4](../Module_4_Conda/README.md), and [Module 8](../Module_8_Variant_Calling/README.md).
