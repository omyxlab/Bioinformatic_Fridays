# Lesson 4 — File Formats: FASTA, FASTQ, and GenBank

## Learning Objectives
- Recognise [FASTA](../File_Formats_Reference.md#fasta), [FASTQ](../File_Formats_Reference.md#fastq), and [GenBank](../File_Formats_Reference.md#genbank) files from their first characters
- Use `head` and `grep` to look inside FASTA and FASTQ files
- Count the records in each format correctly, and avoid the common FASTQ counting mistake
- Read the main parts of a GenBank record
- Say where SAM/BAM, VCF, and GFF/BED files fit in a workflow

## Conceptual Overview

Sequence data is stored in **plain text files** with strict conventions about layout. Each convention is a **file format**. Because they are plain text, you can look inside them with simple commands, and that is the best way to understand them.

Three formats cover most of what you will see early on:

| Format | Holds | Looks like |
|--------|-------|------------|
| **FASTA** | One or more sequences, with names | Header lines start with `>` |
| **FASTQ** | Sequencing reads with quality scores | Four lines per read; header lines start with `@` |
| **GenBank** | A sequence plus rich annotation (genes, source, references) | Starts with `LOCUS` |

In this lesson you will use three commands to look at real files. They are explained properly in [Module 2](../Module_2_Linux/README.md); for now, copy them as written.

| Command | What it does |
|---------|--------------|
| `head -n 12 file` | Prints the first 12 lines of a file |
| `grep "pattern" file` | Prints the lines of a file that contain the pattern |
| `grep -c "pattern" file` | Prints how many lines contain the pattern, instead of the lines |

> **On WSL (your own machine):** Open your Ubuntu terminal. Your data is in `~/Bioinformatic_Fridays/Training`.
>
> **On TLJH (shared server):** Open a terminal from the launcher. Use the `Training/` folder your facilitator pointed you to, or the one you downloaded in Module 0 Lesson 4.

## Worked Examples

### Part A: FASTA

#### 1) Set up your folders

Set the shortcut for the course data (it is forgotten each time you close the terminal, so set it again), and create a folder for reference sequences.

```bash
TRAINING=~/Bioinformatic_Fridays/Training
mkdir -p ~/Bioinformatic_Fridays/reference
cd ~/Bioinformatic_Fridays/reference
```
No output is expected when these commands succeed.

#### 2) Download five Ebola virus reference genomes

`Training/` has no FASTA files, so you will fetch some from NCBI. This command asks NCBI for five RefSeq genomes by accession and saves them as one FASTA file. `-q` keeps `wget` quiet and `-O` names the output file.

```bash
wget -q -O ebolavirus_refseq.fasta "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nuccore&id=NC_002549.1,NC_004161.1,NC_006432.1,NC_014373.1,NC_014372.1&rettype=fasta&retmode=text"
```
No output is expected when this command succeeds. Check the file is there:

```bash
ls -l ebolavirus_refseq.fasta
```
Output (the date and exact size may differ slightly):
```
-rw-r--r-- 1 yourname yourname 96451 Nov 13 10:44 ebolavirus_refseq.fasta
```

> **Note:** The part of the address after `id=` is a list of accessions from Lesson 2. This is the same pattern you would use to fetch any record by accession.

#### 3) Look at the start of the file

```bash
head -n 3 ebolavirus_refseq.fasta
```
Output:
```
>NC_002549.1 Zaire ebolavirus isolate Ebola virus/H.sapiens-tc/COD/1976/Yambuku-Mayinga, complete genome
CGGACACACAAAAAGAAAGAAGAATTTTTAGGATCTTTTGTGTGCGAATAACTATGAGGAAGATTAATAA
TTTTCCTCTCATTGAAATTTATATCGGAATTTAAATTGAAATTGTTACTGTAATCACACCTGGTTTGTTT
```

A FASTA record has two parts:

- A **header line** that starts with `>`. The first word is the sequence's identifier (here the accession `NC_002549.1`), and the rest is a free-text description.
- The **sequence**, on the lines that follow, wrapped at a fixed width (70 bases per line here). The record ends where the next `>` begins, or at the end of the file.

#### 4) List every sequence in the file

Every record starts with `>`, so searching for that character lists them all.

```bash
grep ">" ebolavirus_refseq.fasta
```
Output:
```
>NC_002549.1 Zaire ebolavirus isolate Ebola virus/H.sapiens-tc/COD/1976/Yambuku-Mayinga, complete genome
>NC_004161.1 Reston ebolavirus isolate Reston virus/M.fascicularis-tc/USA/1989/Philippines89-Pennsylvania, complete genome
>NC_006432.1 Sudan ebolavirus isolate Sudan virus/H.sapiens-tc/UGA/2000/Gulu-808892, complete genome
>NC_014373.1 Bundibugyo ebolavirus, complete genome
>NC_014372.1 Tai Forest ebolavirus isolate Tai Forest virus/H.sapiens-tc/CIV/1994/Pauleoula-CI, complete genome
```

To count the sequences instead of listing them, add `-c`:

```bash
grep -c ">" ebolavirus_refseq.fasta
```
Output:
```
5
```

> **Warning:** Always put quote marks around the `>`. In the terminal, an unquoted `>` means "send the output into a file". A command such as `grep > ebolavirus_refseq.fasta` would **overwrite your FASTA file with nothing**.

### Part B: FASTQ

#### 5) Look at the first three reads

Move to the Ebola reads and print the first 12 lines. A FASTQ record is exactly four lines, so 12 lines is three reads.

```bash
cd "$TRAINING"/short_reads/paired
head -n 12 SRR1553607_1.fastq
```
Output:
```
@SRR1553607.1 1 length=101
GTTAGCGTTGTTGATCGCGACGCAACAACTGGTAAAGAATCTGGAAGAAGGATATCAGTTCAAACGCTCAAGCGAGATGATGGATATTTTTGAACGACTCA
+SRR1553607.1 1 length=101
BB@FFFFFHHHHHJJJJJJJJJJJJJJJJJJJGHIJJJJJJJJJHHHHHFFFFFEEEEEEEEEDDDDDDDDDDDDDDDDDEDDDDEDEEEDDDDDDDDDDD
@SRR1553607.2 2 length=101
GGTGTAAGCACAGTACTCGGCCCACATCGCCTTTGTGTTAATGAAGTTTGGGTATCAACTTTCATCCCCAATCTTCCGTGGAAGGAGTATGTTCCGTCAAT
+SRR1553607.2 2 length=101
?@;BDDDDFHFHFFFGIIGHIIJJGJIGIJIIIIGDGGGHEIGJIIIGIIHJ5@FGHJJIEGGEEHHFFFFFFEEDEDCBB?CCDDD?CDDDDECDCB@>C
@SRR1553607.3 3 length=101
GGTCATCGGCGGTCTCTGGGTCGCCGGGACCGTTGGAGAAGAAGACTCCGTCCACGCCGAGTGCCTGGATCTCCTCGAAGGTGACCGTCGCGGGCAGCACG
+SRR1553607.3 3 length=101
@C@FFFFFGHHGDF@FDBGI?F@DHBGI6EHB6A=A5;;AACC>??>ACB?AB?C<BB75;28:A>@BACCACCAC>3A@B9@CCC><@BB>>B@<@B@BB
```

Each read has four lines:

| Line | Starts with | Holds |
|------|-------------|-------|
| 1 | `@` | The header: read name and information about the read |
| 2 | (bases) | The sequence: A, C, G, T (and N for an unknown base) |
| 3 | `+` | A separator, sometimes repeating the header |
| 4 | (characters) | The quality scores, one character per base |

Line 4 is the [Phred quality](../GLOSSARY.md#phred-score) from Lesson 1, written as characters. The sequence and its quality line are always the same length (101 here). Each character stands for a number: `J` is Q41 (very reliable), `@` is Q31, and `#` is Q2 (very unreliable).

#### 6) Search for the read headers, and see a trap

Headers start with `@`, so you might try searching for lines that begin with `@`. The `^` means "at the start of the line". Ask for the first four matches with `-m 4`:

```bash
grep -m 4 "^@" SRR1553607_1.fastq
```
Output:
```
@SRR1553607.1 1 length=101
@SRR1553607.2 2 length=101
@SRR1553607.3 3 length=101
@C@FFFFFGHHGDF@FDBGI?F@DHBGI6EHB6A=A5;;AACC>??>ACB?AB?C<BB75;28:A>@BACCACCAC>3A@B9@CCC><@BB>>B@<@B@BB
```

The fourth match is not a header. It is the **quality line of read 3**, which happens to begin with `@`. Because `@` is a legitimate quality character, any quality line can start with it.

#### 7) Count reads the safe way

Count reads using the line count (four lines per read), then compare with the unsafe method.

```bash
wc -l SRR1553607_1.fastq
```
Output:
```
813780 SRR1553607_1.fastq
```

813,780 lines divided by 4 is **203,445 reads**. Now the unsafe method, counting every line that starts with `@`:

```bash
grep -c "^@" SRR1553607_1.fastq
```
Output:
```
268597
```

That is wrong by 65,152, because it also counted quality lines that start with `@`. A safe alternative is to search for the specific header pattern, which includes the run name and a dot:

```bash
grep -c "^@SRR1553607\." SRR1553607_1.fastq
```
Output:
```
203445
```

> **Tip:** Never count reads with `grep -c "^@"`. Use the number of lines divided by 4, or a pattern that matches only your header format.

#### 8) Mates and long reads

The second file holds the mates of the first. Its first header is the same, which is how the two files stay paired:

```bash
head -n 1 SRR1553607_2.fastq
```
Output:
```
@SRR1553607.1 1 length=101
```

Headers from other machines look different. This is the first header of a Nanopore file:

```bash
head -n 1 "$TRAINING"/long_reads/barcode57.fastq
```
Output:
```
@5832c8b6-696e-46cd-be8d-73b789952b4e	st:Z:2024-06-27T02:52:17.771+00:00	RG:Z:fba2136ff67b57066e5c7e23383eba9e075ff2b2_dna_r10.4.1_e8.2_400bps_sup@v4.3.0
```

It has a unique read identifier, a timestamp, and details of the run. The line count trap applies here too: `barcode57.fastq` has 8,567 reads, but `grep -c "^@"` reports 8,763.

### Part C: GenBank

A GenBank record is much richer than a FASTA file. It wraps the sequence in annotation: what the sequence is, where it came from, who published it, and where its genes are. You can see one on the web at `https://www.ncbi.nlm.nih.gov/nuccore/NC_002549.1`. Below are the key parts of the same record, `NC_002549.1`. The full record is 772 lines long; `...` marks lines left out of the excerpts.

#### 9) The header block

```
LOCUS       NC_002549              18959 bp    cRNA    linear   VRL 13-AUG-2018
DEFINITION  Zaire ebolavirus isolate Ebola
            virus/H.sapiens-tc/COD/1976/Yambuku-Mayinga, complete genome.
ACCESSION   NC_002549
VERSION     NC_002549.1
DBLINK      BioProject: PRJNA485481
KEYWORDS    RefSeq.
SOURCE      Zaire ebolavirus
  ORGANISM  Zaire ebolavirus
            Viruses; Riboviria; Orthornavirae; Negarnaviricota;
            Haploviricotina; Monjiviricetes; Mononegavirales; Filoviridae;
            Orthoebolavirus; Orthoebolavirus zairense.
```

| Field | Meaning |
|-------|---------|
| `LOCUS` | The record name, then the length (18,959 bp), the molecule type (`cRNA`), the shape (`linear`, as opposed to `circular`), a division code (`VRL` for viral), and the date the record was last updated (yours may be later) |
| `DEFINITION` | A one-line description. It matches the header of the FASTA file |
| `ACCESSION` | The accession, without a version |
| `VERSION` | The accession with its version. This is the identifier to cite |
| `DBLINK` | Links to related records, here the BioProject |
| `KEYWORDS` | Labels. `RefSeq` marks it as a curated reference |
| `SOURCE` / `ORGANISM` | The organism, followed by its taxonomic lineage, from the broadest group (`Viruses`) to the species |

The molecule type is `cRNA` because Ebola is a negative-sense RNA virus. The record shows the complementary copy, which is what lets the genes read from left to right.

#### 10) References and comments

```
REFERENCE   1  (bases 1 to 18959)
  AUTHORS   Volchkov,V.E., Volchkova,V.A., Chepurnov,A.A., Blinov,V.M.,
            Dolnik,O., Netesov,S.V. and Feldmann,H.
  TITLE     Characterization of the L gene and 5' trailer region of Ebola virus
  JOURNAL   J. Gen. Virol. 80 (Pt 2), 355-362 (1999)
   PUBMED   10073695
...
COMMENT     REVIEWED REFSEQ: This record has been curated by NCBI staff. The
            reference sequence is identical to AF086833.
            COMPLETENESS: full length.
```

`REFERENCE` entries cite the papers behind the sequence (there are eight in this record). `COMMENT` gives free-text notes. Here it tells you that this RefSeq record is a curated copy of the GenBank submission `AF086833`.

#### 11) The feature table

This is the most useful part. Each feature has a **type**, a **location** (the range of positions, as in Lesson 3), and **qualifiers** that start with `/`.

```
FEATURES             Location/Qualifiers
     source          1..18959
                     /organism="Zaire ebolavirus"
                     /mol_type="viral cRNA"
                     /isolate="Ebola
                     virus/H.sapiens-tc/COD/1976/Yambuku-Mayinga"
                     /db_xref="taxon:186538"
     5'UTR           1..55
                     /note="leader region"
...
     gene            56..3026
                     /gene="NP"
                     /locus_tag="ZEBOVgp1"
                     /db_xref="GeneID:911830"
     mRNA            56..3026
                     /gene="NP"
                     /locus_tag="ZEBOVgp1"
                     /product="nucleoprotein"
                     /db_xref="GeneID:911830"
...
     CDS             470..2689
                     /gene="NP"
                     /locus_tag="ZEBOVgp1"
                     /function="encapsidation of genomic RNA"
                     /codon_start=1
                     /product="nucleoprotein"
                     /protein_id="NP_066243.1"
                     /db_xref="GeneID:911830"
                     /translation="MDSRPQKIWMAPSLTESDMDYHKILTAGLSVQQGIVRQRVIPVY
...
```

| Part | Meaning |
|------|---------|
| `source` | Covers the whole sequence (1..18959) and records the organism, the isolate, and the taxon ID (`taxon:186538`) |
| `gene`, `mRNA`, `CDS` | The gene structure from Lesson 3. This is the *NP* gene: 56..3026, with the coding sequence at 470..2689 |
| `/gene`, `/product` | The gene name (`NP`) and what it makes (`nucleoprotein`) |
| `/protein_id` | The accession of the protein record, `NP_066243.1` |
| `/codon_start=1` | The first base of the CDS is the first base of a codon, so translation starts in frame |
| `/translation` | The protein sequence, translated from the CDS (shortened here) |
| `/db_xref` | A link to the same item in another database, such as `GeneID:911830` |

Across the full record there are 7 `gene` features: the 7 genes of the Ebola genome.

#### 12) The sequence

```
ORIGIN      
        1 cggacacaca aaaagaaaga agaattttta ggatcttttg tgtgcgaata actatgagga
       61 agattaataa ttttcctctc attgaaattt atatcggaat ttaaattgaa attgttactg
...
//
```

The sequence follows `ORIGIN`, in lowercase, in blocks of 10 bases, 60 per line. The number at the start of each line is the position of its first base. The record ends with `//`. This is the same sequence as the FASTA record, which you saw begin with `CGGACACACAAAAAG...`.

### Part D: The other formats you will meet

Later modules produce files in other formats. You do not need them yet; this table says what is coming.

| Format | Holds | Where you meet it |
|--------|-------|-------------------|
| SAM / BAM | Where each read aligns on a reference (BAM is the compressed form) | Modules 7 and 8 |
| VCF | The variants found by comparing reads to a reference | Module 8 |
| GFF / BED | Annotation as coordinates: genes, exons, regions | When working with annotations |

Details and examples are in the [file formats reference](../File_Formats_Reference.md).

## Exercises

1) Run `head -n 8` on `SRR1553607_2.fastq`. Is the first read's name the same as in `SRR1553607_1.fastq`? Why?

2) Using `ebolavirus_refseq.fasta`, how many sequences does the file contain? What species is `NC_014373.1`?

3) Use `wc -l` to count the reads in `"$TRAINING"/long_reads/barcode57.fastq` the safe way. Then run `grep -c "^@"` on it. Why are the two numbers different?

4) In the GenBank excerpt, find: the accession with version, the organism, the length, and the protein accession of the *NP* protein.

5) Challenge: Print the header of only the Sudan ebolavirus genome, without printing any sequence. (Hint: the word `Sudan` appears only in a header, because sequence lines contain just A, C, G, and T.)

## Solutions

### Solution 1
```bash
cd "$TRAINING"/short_reads/paired
head -n 8 SRR1553607_2.fastq
```
Output:
```
@SRR1553607.1 1 length=101
TCATTCGTCACATCCCGTTCAACCTGATTGAGTCGTTCAAAAATATCCATCATCTCGCTTGAGCGTTTGAACTGATATCCTTCTTCCAGATTCTTTACCAG
+SRR1553607.1 1 length=101
CCCFFFFFHHHHHJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJIJJJIJJHIJJHHHFFFFFEDDEFEEEDDDDDDDDDDDDDEDDDDDD
@SRR1553607.2 2 length=101
CCGTACATGTTAACCCTGGGCCTGTTACTTGGGCCTTCACGGGTTCTAATACAAATTGACGGAACATACTCCTTCCACGGAAGATTGGGGATGAAAGTTGA
+SRR1553607.2 2 length=101
@@CFFFDFHFHHHJJJJJJIJJJJIJJJGJJIJIJJJJJJJJJGHIJJIIIIEIJIJJIJIJGHHFFFFFFEEEDEEDDDDDDBDDDDDDDDDDDDDDDDD
```
The first header is `@SRR1553607.1 1 length=101`, identical to the first header in `SRR1553607_1.fastq`, but the sequence is different. The two files hold the two ends (mates) of each fragment, and the same read number links a read to its mate.

### Solution 2
```bash
grep -c ">" ~/Bioinformatic_Fridays/reference/ebolavirus_refseq.fasta
```
Output:
```
5
```
`NC_014373.1` is Bundibugyo ebolavirus, as its header shows.

### Solution 3
```bash
wc -l "$TRAINING"/long_reads/barcode57.fastq
grep -c "^@" "$TRAINING"/long_reads/barcode57.fastq
```
Output:
```
34268 /home/yourname/Bioinformatic_Fridays/Training/long_reads/barcode57.fastq
8763
```
34,268 / 4 = **8,567 reads**. The `grep` count of 8,763 is higher because 196 quality lines also start with `@`, and `grep` counts them as if they were headers.

### Solution 4
- Accession with version: `NC_002549.1`
- Organism: *Zaire ebolavirus*
- Length: 18,959 bp
- Protein accession of the *NP* protein: `NP_066243.1` (from the `/protein_id` qualifier of the CDS)

### Solution 5
```bash
grep "Sudan" ~/Bioinformatic_Fridays/reference/ebolavirus_refseq.fasta
```
Output:
```
>NC_006432.1 Sudan ebolavirus isolate Sudan virus/H.sapiens-tc/UGA/2000/Gulu-808892, complete genome
```
