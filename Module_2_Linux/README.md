# Module 2: Linux for Bioinformatics

This module introduces the Linux command line for bioinformatics workflows. You will learn how Linux is organised, how to navigate files, inspect sequencing data, and use core Unix tools that are standard in bioinformatics pipelines.

Linux is essential in bioinformatics because most tools run on the command line and expect a Unix-like environment. Understanding Linux basics lets you work efficiently on local machines and remote servers.

## Learning objectives

By the end of this module, you will be able to:

- Explain what an operating system, a kernel, and a shell are, and how Linux organises files
- Navigate directories and manage files using core commands
- Inspect and summarize text-based bioinformatics files
- Use pipes and redirection to build small workflows
- Write simple scripts and manage permissions
- Connect to remote systems with SSH and move files with SCP

## Lessons

| Lesson | Title | Status |
|--------|-------|--------|
| 1 | How Linux Works | Planned (not yet written) |
| 2 | Fundamentals and basic commands | Ready |
| 3 | Text processing, pipes, and redirection | Ready |
| 4 | Scripting and permissions | Ready |
| 5 | SSH and remote work | Ready |
| 6 | Absolute and relative paths | Ready |

- **Lesson 1** is a concepts lesson with no commands to memorise: what an operating system and a kernel are, the shell and the terminal, the Linux filesystem, and why "everything is a file".
- **Lesson 2** covers navigation, file listing, and basic file operations.
- **Lesson 3** introduces `grep`, `sort`, `uniq`, and combining commands with pipes.
- **Lesson 4** explains executable scripts, permissions, and safe automation.
- **Lesson 5** shows how to connect to remote systems and transfer files.
- **Lesson 6** covers the root directory, absolute and relative paths, and navigating mounted drives (`/mnt`).

> Note: All examples and exercises use the data in `Training/`.

> Note: In [Module 1](../Module_1_Bioinformatics_Foundations/README.md) you used `head`, `grep`, and `wc` to look inside sequence files. This module explains those commands properly.
