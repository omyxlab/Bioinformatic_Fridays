# Glossary

One-line definitions of the terms used across the course, in alphabetical order. The first time a key term appears in a lesson it links here. Terms marked *(taught later)* are only named in early modules and defined properly where they are first used.

## absolute path
A file's full address starting from the root directory, such as `/home/yourname/Bioinformatic_Fridays`.

## accession
A unique, permanent identifier for a database record, such as `NC_002549.1` or `SRR1553607`; the number after the dot is the version.

## adapter
*(taught later, Module 6)* A short synthetic sequence added during library preparation that can end up in reads and must be trimmed off.

## alignment
A lining-up of two sequences so that matching positions sit together, showing where they match and where they differ.

## barcode
*(taught later, Module 7)* A short tag added to a sample so that many samples can be sequenced together and separated afterwards.

## bioinformatics
The use of computation and statistics to turn biological data, especially sequence data, into biological answers.

## blast
Basic Local Alignment Search Tool: a program that searches a database for sequences similar to a query and reports the best matches with their percent identity and E-value.

## cds
Coding sequence: the part of an mRNA that is translated into protein, from start codon to stop codon; its length is a multiple of three.

## chromosome
One long, continuous molecule of genetic material; the Ebola genome is a single chromosome-like RNA molecule, and humans have 23 pairs.

## codon
A group of three bases that specifies one amino acid (or a stop signal) during translation.

## consensus
The best-estimate sequence of a sample, obtained by applying its variants to a reference.

## contig
A contiguous stretch of sequence assembled from overlapping reads; an assembly is usually a set of contigs.

## coverage
The average number of reads covering each position in a genome, calculated as (number of reads × read length) / genome size; also called depth.

## de bruijn graph
*(taught later, Module 7)* A graph built from short pieces of reads (k-mers) that short-read assemblers use to rebuild sequences.

## de novo assembly
Assembly of a genome from the reads alone, using the overlaps between them, without a reference.

## directory
A folder in the filesystem that can contain files and other directories.

## distribution
A complete Linux operating system, built from the Linux kernel plus a chosen set of tools and a package manager; Ubuntu, Debian, and Fedora are distributions (also called a distro).

## e-value
In a BLAST search, the number of hits at least this good expected by chance; smaller is better and a value near 0 means a chance match is very unlikely.

## exon
A part of a gene that is kept in the mRNA after splicing.

## filesystem
The way an operating system names, stores, and finds files; on Linux it is a single tree of directories starting at `/`.

## gene
A region of a genome that encodes a functional product, most often a protein.

## gene ontology
A controlled vocabulary (GO) describing what genes and proteins do, in three areas: molecular function, biological process, and cellular component.

## genome
The complete set of genetic material of an organism or virus.

## graph
A set of dots (nodes) joined by lines (edges); used to represent assemblies, trees, commit histories, and workflows.

## home directory
A user's personal directory, such as `/home/yourname`, where their own files belong; written `~` in the shell.

## homolog
A gene or sequence that shares a common ancestor with another; homologs are either orthologs or paralogs.

## host contamination
Reads in a sample that come from the host organism rather than the target, such as cassava reads in a sample from a cassava leaf infected with a virus.

## indel
An insertion or deletion of one or more bases relative to a reference.

## intron
A part of a gene that is cut out of the RNA by splicing and is not in the mRNA.

## k-mer
*(taught later, Module 7)* A short stretch of sequence of a fixed length k, used by some assemblers.

## kernel
The core of an operating system: the program that talks directly to the hardware and manages processes, memory, files, and devices; Linux is a kernel.

## mapping
Aligning each read to a reference sequence to find where it came from.

## metagenomics
*(taught later)* The sequencing of the mixed genetic material of a whole community of organisms, such as gut bacteria.

## mrna
Messenger RNA: the spliced RNA copy of a gene that is translated into protein; it consists of the exons joined together.

## n50
*(taught later, Module 7)* A summary figure for assembly quality: the contig length such that contigs this long or longer contain half of all the assembled bases.

## nomenclature
The agreed system for naming genes, proteins, and organisms.

## ontology
A shared, controlled vocabulary of terms with defined relationships between them.

## operating system
The software that sits between the hardware and your programs, sharing the hardware between them, storing files, and keeping users apart.

## ortholog
A homolog in a different species that diverged when the species split; the same gene in two species.

## package manager
A tool that installs software together with everything it depends on, such as `apt` on Ubuntu or conda for bioinformatics tools.

## paired-end
Sequencing both ends of a fragment, giving two reads (mates) a known distance apart, usually stored in two files.

## paralog
A homolog in the same genome that arose when a gene was duplicated.

## percent identity
The share of positions that are identical in the aligned region of two sequences.

## permission
A setting on a file saying whether its owner, its group, and everyone else may read (`r`), write (`w`), or execute (`x`) it.

## phred score
A quality score Q = −10 log10(P), where P is the probability that a base call is wrong; Q30 means a 1 in 1,000 chance of error.

## phylogenetic tree
A diagram of how samples, species, or genes are related by descent, with tips, nodes (common ancestors), and branches.

## ploidy
*(taught later, Module 8)* The number of copies of each chromosome in a cell; a virus like Ebola has one.

## process
A program that is running, with its own process ID, memory, and owner.

## protein
A chain of amino acids made by translating a CDS.

## read
One piece of sequence produced by a sequencer, with a quality score for each base.

## reference
A finished, trusted sequence that you compare your data against.

## reference-based assembly
Rebuilding a sample's sequence by mapping its reads to a known reference.

## refseq
NCBI's curated, non-redundant collection of reference sequences, built from GenBank records.

## repeat
A sequence that occurs more than once in a genome; repeats are hard to assemble because a read inside one does not show which copy it came from.

## root directory
The top of the Linux filesystem tree, written `/`; every file and directory lies somewhere below it.

## root user
The administrator account, which may do anything on the system; not the same as the root directory `/` or the directory `/root`.

## scaffold
*(taught later, Module 7)* A set of contigs ordered and oriented relative to each other, with gaps of estimated size between them.

## sequencing
Reading the order of bases in DNA or RNA.

## shell
The program inside the terminal that reads each command you type and runs it; this course uses bash.

## snp
Single-nucleotide polymorphism: a variant in which one base is replaced by another.

## sra
Sequence Read Archive: NCBI's database of raw sequencing reads.

## sudo
A prefix that runs one command with administrator (root) rights, after asking for your password.

## taxonomy
The classification of organisms into nested groups; each organism in NCBI has a stable taxonomy ID.

## terminal
The window you type commands into; it passes your keystrokes to the shell and shows the output.

## utr
Untranslated region: a stretch at either end of an mRNA that is not translated into protein (5' UTR before the CDS, 3' UTR after it).

## variant
A position where a sample differs from the reference.
