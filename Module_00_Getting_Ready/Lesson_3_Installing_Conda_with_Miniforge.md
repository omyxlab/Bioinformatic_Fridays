# Lesson 3 — Installing Conda with Miniforge

## Learning Objectives
- Explain what a package manager is and why bioinformatics needs one
- Check whether conda is already installed
- Install Miniforge, a lightweight conda distribution
- Confirm conda works and understand the `(base)` prompt

## Conceptual Overview

Bioinformatics tools are hard to install by hand: each depends on other software, specific versions, and system libraries, and getting one wrong breaks everything. A **package manager** solves this. You ask for a tool by name and it fetches that tool and everything it needs, already built to work together.

The package manager this course uses is **conda**. Conda installs tools into isolated **environments**, so different projects can use different tool versions without clashing. You will learn to build environments properly in Module 3 — for now you just need conda itself installed.

We install conda through **Miniforge**, a small distribution that is configured out of the box to use **conda-forge**, the community software channel. Miniforge avoids the commercial licensing terms attached to the full Anaconda distribution, which matters for training and institutional use, and it keeps the install small.

> **On TLJH (shared server):** conda is usually already installed for you. Run the check in Example 1 first. If it prints a version, skip the rest of this lesson and go to Lesson 4.

## Worked Examples

### 1) Check whether conda is already installed

```bash
conda --version
```
If conda is installed, you see a version (yours may differ):
```
conda 24.1.0
```
If instead you see `conda: command not found`, continue to Example 2 to install it.

### 2) Download the Miniforge installer

This downloads the installer script for Linux into your home directory. `-O` names the saved file.

```bash
wget -O Miniforge3.sh "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh"
```
Output (last lines; numbers vary):
```
Saving to: 'Miniforge3.sh'
Miniforge3.sh    100%[===============>]  ...  in ...s
'Miniforge3.sh' saved
```

### 3) Run the installer

```bash
bash Miniforge3.sh
```
The installer walks you through a few prompts:

- It shows a licence. Press **Enter** to scroll, then type `yes` to accept.
- It asks where to install. Press **Enter** to accept the default location in your home directory.
- At the end it asks whether to run `conda init` to set up your shell. Type `yes`.

Output (final lines, abbreviated):
```
Thank you for installing Miniforge3!
...
modified /home/yourname/.bashrc
```

### 4) Restart your shell

The setup only takes effect in a new shell. Close the terminal and open a new one, or run:

```bash
source ~/.bashrc
```

Your prompt now starts with `(base)`:
```
(base) yourname@computer:~$
```
`(base)` is the name of conda's default environment. Its presence confirms conda is active.

### 5) Confirm conda works

```bash
conda --version
```
Output (version will vary):
```
conda 24.1.0
```

> **Note:** Do not install project tools into the `(base)` environment. In Module 3 you will create a dedicated `bioinfo` environment for the course's tools and keep `base` clean.

## Exercises

1) Run `conda --version`. Is conda already installed, or do you need to install it?

2) If you needed to install it, download and run the Miniforge installer, accepting the defaults and allowing `conda init`.

3) Open a new terminal. Does your prompt start with `(base)`?

4) Challenge: Run `conda info`. Find the line that reports the "base environment" path. Where on your system did conda install?

## Solutions

### Solution 1
```bash
conda --version
```
A version number means conda is installed; `command not found` means you need to install it with Examples 2–4.

### Solution 2
```bash
wget -O Miniforge3.sh "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh"
bash Miniforge3.sh
```
Accept the licence with `yes`, accept the default location with Enter, and answer `yes` to `conda init`.

### Solution 3
After opening a new terminal (or running `source ~/.bashrc`), the prompt begins with `(base)`, for example:
```
(base) yourname@computer:~$
```

### Solution 4
```bash
conda info
```
Look for a line like:
```
base environment : /home/yourname/miniforge3
```
That path is where conda installed, inside your home directory.
