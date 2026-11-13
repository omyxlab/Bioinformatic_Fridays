# Lesson 1 — What Is Bioinformatics?

## Learning Objectives
- Describe [bioinformatics](../GLOSSARY.md#bioinformatics) as the combination of biology and computation
- Outline a typical workflow from a biological sample to a result
- Explain what a [read](../GLOSSARY.md#read) is and how short and long reads differ
- Interpret a [Phred quality score](../GLOSSARY.md#phred-score) in plain terms
- Calculate [coverage](../GLOSSARY.md#coverage) from the number of reads, read length, and genome size

## Conceptual Overview

### What bioinformatics is

Modern sequencing machines read DNA and RNA in bulk, producing millions of short pieces of sequence in a single run. Nobody can read that by eye. **Bioinformatics** is the use of computation to turn that raw data into biological answers.

It sits between two fields, and needs both:

- **Biology** tells you what question is worth asking, what the data means, and whether an answer is believable. A result that is computationally clean but biologically impossible is still wrong.
- **Computation** (programming, statistics, and algorithms) is what makes it possible to handle data that is far too large to inspect by hand, and to repeat an analysis exactly.

You do not need to be an expert programmer. You do need to be comfortable asking a biological question and working out how data can answer it. The course data shows the range of questions:

| Question | Data in `Training/` |
|----------|---------------------|
| How does the Ebola virus from the 2014 outbreak differ from the first one found in 1976? | `short_reads/paired/SRR1553607_1.fastq` and `_2.fastq` |
| Which virus is infecting this cassava leaf? | `long_reads/barcode57.fastq` |
| Do gut bacteria differ between people with and without a condition? | `short_reads/unpaired/*Case*` and `*Healthy*` |

### A typical workflow

Most sequencing projects follow the same shape. Each step is a module in this course.

1. **Sample and sequence.** Extract DNA or RNA and run it through a sequencer. The output is a file of reads.
2. **Quality control.** Check the reads are good enough to use, and trim off poor-quality or artificial sequence (Module 6).
3. **Remove what you do not want.** A cassava leaf contains cassava DNA as well as virus DNA. Reads from the unwanted source are called [host contamination](../GLOSSARY.md#host-contamination) and are filtered out (Module 7).
4. **Assemble or map.** Rebuild the sequence from the reads, or place the reads on a known reference (Modules 7 and 8).
5. **Analyse.** Find variants, search for similar sequences, build a tree (Modules 8 and 10).
6. **Interpret.** Decide what the result means for the biological question.

### Sequencing technologies and reads

A [read](../GLOSSARY.md#read) is one piece of sequence that the machine read from a DNA or RNA fragment. Sequencers differ mainly in how long their reads are.

| | Short reads | Long reads |
|---|---|---|
| Typical technologies | Illumina | Oxford Nanopore, PacBio |
| Typical length | 50 to 300 bases | Thousands to tens of thousands of bases |
| Strength | Very accurate per base | Can span repetitive regions |
| Weakness | Cannot span long repeats | Historically less accurate per base |
| In `Training/` | Ebola reads: every read is exactly 101 bases | Cassava reads: average about 1,400 bases, longest 34,441 |

Short reads are often produced as **pairs**. The machine reads a fragment from both ends, giving two reads called mates. This is [paired-end](../GLOSSARY.md#paired-end) sequencing, and it is why the Ebola data comes as two files, `SRR1553607_1.fastq` and `SRR1553607_2.fastq`. The same read number in each file belongs to the same fragment. Knowing the two ends are a known distance apart helps with placing reads later.

### Quality scores

Sequencers are not perfect, so every base comes with a confidence score. The standard is the **Phred score**, written Q:

| Phred score (Q) | Chance the base is wrong | Accuracy |
|-----------------|--------------------------|----------|
| 10 | 1 in 10 | 90% |
| 20 | 1 in 100 | 99% |
| 30 | 1 in 1,000 | 99.9% |

A higher score means more confidence. In a FASTQ file each score is stored as a single character, so one line of characters describes every base in a read. You will see this in Lesson 4. Quality control and trimming are taught in Module 6.

### Coverage

[Coverage](../GLOSSARY.md#coverage) (also called depth) tells you how many times, on average, each position in a genome is represented by reads:

```
coverage = (number of reads × read length) / genome size
```

Higher coverage gives more confidence in what you see at a position, and it matters for assembly and for calling variants. Very uneven coverage still leaves gaps, even when the average looks high.

## Worked Examples

### 1) Total bases in the Ebola data

The Ebola run has 203,445 read pairs, so 406,890 reads in total, each 101 bases long.

```
406,890 reads × 101 bases = 41,095,890 bases
```

### 2) Best-case coverage of the Ebola genome

The Ebola virus genome is 18,959 bases long. If every read came from the virus and spread perfectly evenly:

```
41,095,890 / 18,959 ≈ 2,168
```

That is about 2,168× coverage, an upper limit. The real figure is lower, because a sample also contains reads from the host and reads do not land evenly. You will measure the real coverage in Module 8.

### 3) What a quality score means for one read

A 101-base read where every base is Q30 is expected to contain about 0.1 errors (101 × 1/1000). Most reads therefore have no errors at all, and an occasional read has one.

## Exercises

1) Match each question to the `Training/` data you would use: (a) which virus infects the cassava leaf; (b) how the 2014 Ebola virus differs from 1976; (c) how gut bacteria differ between groups.

2) The Nanopore file `barcode57.fastq` has 8,567 reads with an average length of about 1,421 bases. How many bases does it contain, roughly? If the viral genome in it were 2,800 bases and 5% of the bases came from the virus, what would the viral coverage be?

3) A base has a Phred score of 20. What is the probability that the base call is wrong?

4) Why would a short-read dataset struggle to assemble a genome with a 5,000-base repeated region, when every read is 101 bases?

5) Challenge: In Example 2 the best-case Ebola coverage was about 2,168×. Give two reasons the real coverage will be lower.

## Solutions

### Solution 1
(a) `long_reads/barcode57.fastq`; (b) `short_reads/paired/SRR1553607_1.fastq` and `_2.fastq`; (c) the files in `short_reads/unpaired/` whose names contain `Case` and `Healthy`.

### Solution 2
8,567 × 1,421 ≈ 12.2 million bases. Five percent of that is about 608,700 bases, and 608,700 / 2,800 ≈ 217. The viral coverage would be about 217×.

### Solution 3
Q20 means a 1 in 100 chance, or 1%, that the base is wrong.

### Solution 4
A 101-base read fits entirely inside a 5,000-base repeat. The read looks identical wherever the repeat occurs, so it gives no clue about which copy it came from, and the assembler cannot tell how the repeats connect to the sequence on either side. Reads longer than the repeat can reach unique sequence on both sides and resolve it.

### Solution 5
Any two of: (1) some reads come from the host or other sources, not the virus; (2) reads do not fall evenly across the genome, so some positions have far fewer reads than average; (3) some reads are discarded for poor quality; (4) some reads fail to map.
