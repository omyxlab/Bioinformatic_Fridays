# Lesson 1 — How Linux Works

> **Status: planned, not yet written.** This file records what the lesson will cover so that the numbering and cross-references in the module are correct. Write it following [`STYLE_GUIDE.md`](../STYLE_GUIDE.md).

This is a concepts lesson. It gives learners the picture of what is underneath the command line before they start typing commands, and it contains no commands to memorise.

## Planned learning objectives
- Explain what an operating system is and what it does
- Distinguish the kernel, the shell, and the terminal
- Explain what a Linux distribution is and why the course uses Ubuntu
- Describe the Linux filesystem as a single tree, and name the main directories
- Explain the idea that "everything is a file"
- Describe users, groups, and permissions as ideas
- Explain what a process is
- Explain how software is installed on Linux (package managers)
- Explain what WSL is and how it relates to Windows

## Planned topics
1. **What an operating system does:** manages hardware, runs programs, and provides files and users.
2. **Kernel, shell, terminal:** the kernel talks to the hardware; the shell reads your commands; the terminal is the window you type in. Link to Module 0 Lesson 1.
3. **Distributions:** Linux is a kernel plus a collection of software; Ubuntu is one distribution.
4. **The filesystem tree:** one tree rooted at `/`, with `/home`, `/etc`, `/usr`, `/tmp`, and `/mnt` (Windows drives under WSL).
5. **Everything is a file:** documents, directories, devices, and running processes are all presented as files.
6. **Users and permissions:** every file has an owner, a group, and read/write/execute permissions (the commands come in Lesson 4).
7. **Processes:** a program that is running, with its own ID.
8. **Package managers:** why Linux software is installed with `apt` or conda rather than by downloading installers.
9. **What WSL is:** a real Linux kernel running alongside Windows, and why files under `/mnt/c` are slower than files in your Linux home.

## Notes for the author
- Avoid repeating Module 0 Lesson 1, which only introduces the terminal and the prompt.
- Keep it to about 20 minutes of the first Linux session. Use diagrams over text where possible.
