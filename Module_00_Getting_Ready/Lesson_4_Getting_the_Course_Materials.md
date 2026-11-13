# Lesson 4 — Getting the Course Materials

## Learning Objectives
- Create a course working directory in the right place
- Download the course `Training/` data from Zenodo
- Unpack a `.tar.gz` archive
- Set a shortcut variable for the data folder

## Conceptual Overview

Every exercise in this course uses a shared dataset: real sequencing files kept in a folder called `Training/`. The dataset is published on **Zenodo**, a long-term repository for research data, so the link is stable and citable. You download it once.

Where you put it matters on WSL. Your Windows drive is available inside Linux under `/mnt/c`, but reading and writing large files there is **much slower** than in the Linux home directory. Keep course data in your Linux home (`~`), not under `/mnt/c`. This lesson puts everything in `~/Bioinformatic_Fridays`.

The data comes as a single compressed archive, `training.tar.gz`. A `.tar.gz` file is many files bundled into one (`.tar`) and then compressed (`.gz`) — the standard way large datasets are shared. You unpack it after downloading.

> **Note:** The dataset is published at <https://zenodo.org/records/24057548>. The archive is about 90 MB.

> **On TLJH (shared server):** The data may already be provided in your home directory or a shared folder — run `ls ~/Bioinformatic_Fridays/Training` to check. If it is there, skip to Example 4 (setting the variable). If not, the same download steps below work on TLJH.

## Worked Examples

### 1) Create and enter the course directory

`mkdir -p` creates the folder (and does nothing if it already exists). `cd` moves into it.

```bash
mkdir -p ~/Bioinformatic_Fridays
cd ~/Bioinformatic_Fridays
```
No output is expected when these commands succeed.

### 2) Download the data from Zenodo

Store the link in a variable first so the download command stays readable.

```bash
ZENODO_URL="https://zenodo.org/records/24057548/files/training.tar.gz?download=1"
wget -O training.tar.gz "$ZENODO_URL"
```
Output (last lines; size and time vary):
```
Saving to: 'training.tar.gz'
training.tar.gz    100%[===============>]  ...  in ...
'training.tar.gz' saved
```

> **Note:** This is the largest download in the course. On a slow connection it may take several minutes — start it before you need it, and do not close the terminal until it finishes.

### 3) Unpack the archive

`tar` unpacks the archive. The flags are: `-x` extract, `-z` decompress the `.gz`, `-v` list files as they come out, `-f` the file to read.

```bash
tar -xzvf training.tar.gz
```
Output (abbreviated — one line per file):
```
Training/
Training/long_reads/
Training/long_reads/barcode57.fastq
Training/short_reads/
...
```

Confirm the folder is there:

```bash
ls Training
```
Output:
```
long_reads  short_reads
```

> **Tip:** Once you have confirmed the data unpacked correctly, you can delete the archive to save space: `rm training.tar.gz`. Keep it if disk space is not a concern.

### 4) Set a shortcut variable for the data

Many later lessons refer to the `Training/` folder. Setting a variable saves typing its full path. This variable lasts until you close the terminal.

```bash
TRAINING=~/Bioinformatic_Fridays/Training
echo "$TRAINING"
```
Output:
```
/home/yourname/Bioinformatic_Fridays/Training
```

You can then refer to files as, for example, `"$TRAINING"/long_reads/barcode57.fastq`.

## Exercises

1) Create `~/Bioinformatic_Fridays` and move into it. Confirm with `pwd` that you are inside it.

2) Download `training.tar.gz` from Zenodo and unpack it. What two folders appear inside `Training/`?

3) Set the `TRAINING` variable and run `ls "$TRAINING"/long_reads`. Which FASTQ files do you see?

4) Challenge: Run `du -sh "$TRAINING"`. How large is the dataset on disk?

## Solutions

### Solution 1
```bash
mkdir -p ~/Bioinformatic_Fridays
cd ~/Bioinformatic_Fridays
pwd
```
Output (yours will differ in the username):
```
/home/yourname/Bioinformatic_Fridays
```

### Solution 2
```bash
ZENODO_URL="https://zenodo.org/records/24057548/files/training.tar.gz?download=1"
wget -O training.tar.gz "$ZENODO_URL"
tar -xzvf training.tar.gz
ls Training
```
Output:
```
long_reads  short_reads
```

### Solution 3
```bash
TRAINING=~/Bioinformatic_Fridays/Training
ls "$TRAINING"/long_reads
```
Output:
```
barcode57.fastq  barcode58.fastq  sample3.fastq
```

### Solution 4
```bash
du -sh "$TRAINING"
```
Output (example; your figure will vary):
```
1.2G	/home/yourname/Bioinformatic_Fridays/Training
```
`du -sh` reports the total size of the folder in human-readable units.
