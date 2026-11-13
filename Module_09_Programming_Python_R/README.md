# Module 9: Programming for Data (Python or R)

> **Status: planned, not yet written.** This file records the plan so that numbering and cross-references are correct. Write the lessons following [`STYLE_GUIDE.md`](../STYLE_GUIDE.md).

This module turns the outputs of earlier modules into tables and figures. You choose **one** of two parallel tracks, Python or R. Both cover the same competencies on the same datasets, so you can compare results with someone on the other track.

## Planned learning objectives

By the end of this module, you will be able to:

- Read a tabular output file into a data frame
- Filter, sort, group, and summarise it
- Produce a clean, labelled plot and save it to a file
- Apply this to real outputs you generated earlier in the course
- Commit the script or notebook and the figure to your repository

## Planned tracks

| Competency | Python track | R track |
|------------|--------------|---------|
| Environment | conda environment with Jupyter | conda environment with RStudio or Quarto |
| Read tabular data | `pandas.read_csv` | `readr::read_tsv` |
| Wrangle and summarise | `pandas` | `dplyr` |
| Plot | `matplotlib` and `seaborn` | `ggplot2` |

Planned lesson files come in pairs: `Lesson_N_<Title>_Python_Track.md` and `Lesson_N_<Title>_R_Track.md`.

## Planned worked datasets

1. MultiQC summary statistics, as a per-sample quality bar chart
2. `samtools depth` output, as a coverage line plot
3. BLAST tabular output, as a top-hits table and an identity histogram
4. `bcftools query` output from Module 8, as variants along the genome and a transition and transversion summary

## Prerequisites

[Module 3](../Module_03_GitHub/README.md) (committing your work), [Module 4](../Module_04_Conda/README.md) (installing packages), and outputs from Modules 6 to 8.
