# File Formats Reference

A quick reference for the file formats used in the course: what each holds, how it is laid out, one example, and where you meet it. Full mechanics are taught where each format is first produced. Examples marked *illustrative* show the layout but are not taken from a real file.

## fasta

**Holds:** one or more sequences with names.

**Layout:** each record has a header line starting with `>` followed by the sequence on one or more lines. The first word of the header is the identifier; the rest is a free-text description. Lines of sequence are usually wrapped at a fixed width.

**Example** (from the Ebola reference genome `NC_002549.1`):
```
>NC_002549.1 Zaire ebolavirus isolate Ebola virus/H.sapiens-tc/COD/1976/Yambuku-Mayinga, complete genome
CGGACACACAAAAAGAAAGAAGAATTTTTAGGATCTTTTGTGTGCGAATAACTATGAGGAAGATTAATAA
TTTTCCTCTCATTGAAATTTATATCGGAATTTAAATTGAAATTGTTACTGTAATCACACCTGGTTTGTTT
```

**Useful commands:** `grep ">" file` lists the headers; `grep -c ">" file` counts the sequences. Always quote the `>`.

**Where you meet it:** reference genomes and assembled contigs (Modules 1, 7, 8, 10).

## fastq

**Holds:** sequencing reads with a quality score for every base.

**Layout:** exactly four lines per read.

| Line | Content |
|------|---------|
| 1 | Header, starting with `@` |
| 2 | The sequence |
| 3 | A separator, starting with `+` |
| 4 | Quality scores, one character per base (Phred+33) |

**Example** (the first read of `SRR1553607_1.fastq`):
```
@SRR1553607.1 1 length=101
GTTAGCGTTGTTGATCGCGACGCAACAACTGGTAAAGAATCTGGAAGAAGGATATCAGTTCAAACGCTCAAGCGAGATGATGGATATTTTTGAACGACTCA
+SRR1553607.1 1 length=101
BB@FFFFFHHHHHJJJJJJJJJJJJJJJJJJJGHIJJJJJJJJJHHHHHFFFFFEEEEEEEEEDDDDDDDDDDDDDDDDDEDDDDEDEEEDDDDDDDDDDD
```

**Watch out:** a quality line can begin with `@`, so `grep -c "^@"` over-counts reads. Count reads as the number of lines divided by 4.

**Where you meet it:** raw reads from any sequencer (Modules 1, 6, 7, 8).

## genbank

**Holds:** a sequence together with rich annotation: source organism, references, and a feature table of genes, coding sequences, and more.

**Layout:** labelled sections. The main ones:

| Section | Content |
|---------|---------|
| `LOCUS` | Name, length, molecule type, shape, division, date |
| `DEFINITION` | One-line description |
| `ACCESSION`, `VERSION` | Identifier, and identifier with version |
| `SOURCE`, `ORGANISM` | Organism and taxonomic lineage |
| `REFERENCE`, `COMMENT` | Citations and notes |
| `FEATURES` | Feature table: `source`, `gene`, `mRNA`, `CDS`, and others, each with a location and `/qualifiers` |
| `ORIGIN` | The sequence, in lowercase, with positions numbered |
| `//` | End of the record |

**Example** (first lines of `NC_002549.1`):
```
LOCUS       NC_002549              18959 bp    cRNA    linear   VRL 13-AUG-2018
DEFINITION  Zaire ebolavirus isolate Ebola
            virus/H.sapiens-tc/COD/1976/Yambuku-Mayinga, complete genome.
ACCESSION   NC_002549
VERSION     NC_002549.1
```

**Locations:** `56..3026` is a continuous range; `join(5051..5142,5273..5495,6346..6474)` is a feature made of several pieces, as for a split gene.

**Where you meet it:** records downloaded from NCBI (Modules 1, 7, 10).

## sam-bam

**Holds:** reads aligned to a reference: where each read maps and how well. SAM is the text form; BAM is the same data compressed in binary form, which is smaller and faster. Use `samtools` to read BAM.

**Layout:** header lines starting with `@`, then one line per alignment with at least 11 tab-separated columns:

| # | Column | Meaning |
|---|--------|---------|
| 1 | QNAME | Read name |
| 2 | FLAG | A number encoding properties (paired, unmapped, reverse strand, ...) |
| 3 | RNAME | Name of the reference sequence |
| 4 | POS | Position on the reference where the alignment starts (1-based) |
| 5 | MAPQ | Mapping quality |
| 6 | CIGAR | How the read aligns: matches, insertions, deletions |
| 7-9 | RNEXT, PNEXT, TLEN | Information about the mate read |
| 10 | SEQ | The read sequence |
| 11 | QUAL | The read quality string |

**Example** *(illustrative)*:
```
read1   0   NC_002549.1   1203   60   20M   *   0   0   ACGTACGTACGTACGTACGT   IIIIIIIIIIIIIIIIIIII
```

**Where you meet it:** after mapping reads (Modules 7 and 8).

## vcf

**Holds:** variants: the positions where a sample differs from a reference.

**Layout:** header lines starting with `##`, one column-name line starting with `#CHROM`, then one line per variant with tab-separated columns:

| Column | Meaning |
|--------|---------|
| CHROM | Reference sequence name |
| POS | Position of the variant |
| ID | An identifier, or `.` if none |
| REF | The base(s) in the reference |
| ALT | The base(s) found in the sample |
| QUAL | Confidence that the variant is real |
| FILTER | `PASS`, a filter name, or `.` if no filter was applied |
| INFO | Extra details, such as read depth (`DP`) |
| FORMAT and sample columns | Per-sample details |

**Example** *(illustrative)*:
```
#CHROM        POS   ID  REF  ALT  QUAL  FILTER  INFO
NC_002549.1   295   .   A    C    225   .       DP=19
```

**Where you meet it:** the output of variant calling (Module 8).

## gff-bed

**Holds:** annotation as coordinates: where genes, exons, and other regions lie on a reference.

**GFF3** has nine tab-separated columns: sequence name, source, feature type, start, end, score, strand, phase, and attributes. Coordinates are **1-based** and include both ends.

**BED** has at least three columns: sequence name, start, end, with optional name and score columns. Coordinates are **0-based** and the end is not included, so BED and GFF positions for the same region differ by one at the start.

**Example (GFF3, illustrative)** for the Ebola *NP* gene, using the coordinates from the GenBank record:
```
NC_002549.1   RefSeq   gene   56   3026   .   +   .   ID=gene-NP;Name=NP
```

**Where you meet it:** annotation files for reference genomes and tools that report regions.
