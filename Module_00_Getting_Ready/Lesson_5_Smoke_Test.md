# Lesson 5 — Smoke Test

## Learning Objectives
- Confirm your terminal, conda, and course data all work together
- Read a real sequencing file to prove the data is usable
- Recognise a correctly set-up environment before the course begins

## Conceptual Overview

A **smoke test** is a quick check that the basics work before you rely on them — the name comes from switching on a device and seeing whether it smokes. This lesson is the smoke test for your whole setup. If every step below gives the expected result, you are ready for Module 1. If one fails, you know exactly which earlier lesson to revisit.

Run these from a fresh terminal so you are testing the setup as it will actually start each session.

## Worked Examples

### 1) The terminal responds

```bash
whoami
```
Output (yours will differ):
```
yourname
```
If you see your username, your terminal and shell are working (Lesson 1, and Lesson 2 for WSL).

### 2) conda is active

```bash
conda --version
```
Output (version will vary):
```
conda 24.1.0
```
If you see a version, conda is installed and on your path (Lesson 3). Your prompt should also begin with `(base)`.

### 3) The data is present

```bash
TRAINING=~/Bioinformatic_Fridays/Training
ls "$TRAINING"
```
Output:
```
long_reads  short_reads
```
If you see both folders, the download and unpacking worked (Lesson 4).

### 4) The data is readable

This reads the first four lines of a real sequencing file — one complete record. `head -n 4` shows the first four lines.

```bash
head -n 4 "$TRAINING"/short_reads/paired/SRR1553607_1.fastq
```
Output:
```
@SRR1553607.1 1 length=101
GTTAGCGTTGTTGATCGCGACGCAACAACTGGTAAAGAATCTGGAAGAAGGATATCAGTTCAAACGCTCAAGCGAGATGATGGATATTTTTGAACGACTCA
+SRR1553607.1 1 length=101
BB@FFFFFHHHHHJJJJJJJJJJJJJJJJJJJGHIJJJJJJJJJHHHHHFFFFFEEEEEEEEEDDDDDDDDDDDDDDDDDEDDDDEDEEEDDDDDDDDDDD
```
Seeing real sequence text confirms the data is intact and readable. You do not need to understand this format yet — that is Module 5.

## Exercises

1) From a fresh terminal, run all four checks above in order. Did each one give the expected result?

2) If any check failed, which lesson does it point back to? (Hint: each worked example names the lesson it tests.)

3) Challenge: Count the lines in `"$TRAINING"/short_reads/paired/SRR1553607_1.fastq` with `wc -l`. A FASTQ file uses four lines per read — roughly how many reads is that?

## Solutions

### Solution 1
Work through Examples 1–4. A ready setup gives: your username, a conda version with a `(base)` prompt, both data folders listed, and readable sequence text from the FASTQ file.

### Solution 2
- Example 1 fails → revisit Lesson 1 (and Lesson 2 if on WSL).
- Example 2 fails → revisit Lesson 3 (conda).
- Examples 3 or 4 fail → revisit Lesson 4 (the data download).

### Solution 3
```bash
wc -l "$TRAINING"/short_reads/paired/SRR1553607_1.fastq
```
Output:
```
813780 /home/yourname/Bioinformatic_Fridays/Training/short_reads/paired/SRR1553607_1.fastq
```
813780 lines divided by 4 lines per read is 203445 reads.

---

## You are ready

If all four checks passed, your environment is set up and you are ready for **Module 1: Linux Foundations**. Keep the `~/Bioinformatic_Fridays` folder — you will use it throughout the course.
