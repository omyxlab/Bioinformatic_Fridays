# Lesson 1 — What You Need and Why

## Learning Objectives
- Explain what the command line is and why bioinformatics relies on it
- Describe the difference between WSL and TLJH and decide which one you will use
- Open a terminal in your chosen environment
- Recognise the Linux prompt and run your first command

## Conceptual Overview

Most bioinformatics tools have no buttons to click. You run them by typing commands into a **terminal** — a text window where you type an instruction, press Enter, and the computer does it. The program that reads your typing and runs your commands is called the **shell**. This text-based way of working is the **command line**.

Bioinformatics relies on it for three practical reasons: the tools are built this way and often have no other interface; datasets are far too large to open by hand; and typing commands leaves a written record you can repeat, share, and trust. Learning the command line is the single most useful thing you can do early in bioinformatics, which is why it comes first.

The command line is a **Linux** skill. Windows and macOS can run a terminal too, but the bioinformatics world runs on Linux, so this course gives you a Linux environment one of two ways:

- **WSL** runs a full Linux system inside your own Windows computer. It is private to you, works offline, and uses your computer's own storage and processing. You set it up once, in Lesson 2.
- **TLJH** is a shared Linux server the facilitators run. You reach it through a web browser, so there is nothing to install and any computer works — but you need an internet connection and an account from your facilitator.

Both give you the same Linux command line. Pick the one that fits your situation and use it for the whole course. If you have a Windows laptop you control, WSL is the better long-term choice. If you cannot install software, or you are on a borrowed or locked-down computer, use TLJH.

## Worked Examples

### 1) Open a terminal

> **On WSL (your own machine):** You will install WSL in Lesson 2 first. After that, open the **Start menu**, type `Ubuntu`, and press Enter. A black terminal window opens.
>
> **On TLJH (shared server):** Open the web address your facilitator gave you, log in with your username and password, then choose **Terminal** from the launcher. A terminal opens in your browser tab.

### 2) Read the prompt

When the terminal is ready it shows a **prompt** — a line waiting for your command. It looks something like this (your username and computer name will differ):

```
yourname@computer:~$
```

The `~` means you are in your **home directory**, your personal space on the system. The `$` marks the end of the prompt; you type after it. You do not type the prompt itself — in this course, command blocks show only what you type.

### 3) Run your first command

`whoami` prints the username you are logged in as.

```bash
whoami
```
Output (yours will differ):
```
yourname
```

### 4) Ask where you are

`pwd` stands for "print working directory" — it shows the folder you are currently in.

```bash
pwd
```
Output (yours will differ):
```
/home/yourname
```

## Exercises

1) Decide which environment you will use for the course — WSL or TLJH — and write down why.

2) Open a terminal in your chosen environment and run `whoami`. What username do you see?

3) Run `pwd`. Which directory does it report? What do you think the `~` in the prompt refers to?

4) Challenge: Without looking it up yet, what do you expect would happen if you typed a word that is not a real command, for example `banana`, and pressed Enter? Try it and read the message.

## Solutions

### Solution 1
There is no single right answer. Choose WSL if you have a Windows laptop you can install software on and want a setup that works offline and lasts beyond the course. Choose TLJH if you cannot install software or are on a shared or borrowed computer.

### Solution 2
```bash
whoami
```
Output (yours will differ):
```
yourname
```
The command prints your account name on the system.

### Solution 3
```bash
pwd
```
Output (yours will differ):
```
/home/yourname
```
You start in your home directory. The `~` in the prompt is shorthand for that same home directory.

### Solution 4
```bash
banana
```
Output:
```
banana: command not found
```
The shell tells you it does not recognise the word as a command. This is a normal, harmless message — you will see it often, and it usually means a typo or a tool that is not installed yet.
