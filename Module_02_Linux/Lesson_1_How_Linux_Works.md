# Lesson 1 — How Linux Works

## Learning Objectives
- Explain what an [operating system](../GLOSSARY.md#operating-system) is and what it does
- Describe the [kernel](../GLOSSARY.md#kernel) and say how it differs from the [shell](../GLOSSARY.md#shell) and the [terminal](../GLOSSARY.md#terminal)
- Explain what a Linux [distribution](../GLOSSARY.md#distribution) is, and why Ubuntu, Debian, and Fedora are all "Linux"
- Describe the Linux [filesystem](../GLOSSARY.md#filesystem) as one tree that starts at the [root directory](../GLOSSARY.md#root-directory) (`/`)
- State what the main top-level directories contain, including `/home`, `/etc`, `/bin`, `/usr`, `/opt`, `/var`, `/tmp`, and `/mnt`
- Tell the root directory, the [root user](../GLOSSARY.md#root-user), and `/root` apart, and find your own [home directory](../GLOSSARY.md#home-directory)
- Explain the idea that "everything is a file" and read a file's [permissions](../GLOSSARY.md#permission)

## Conceptual Overview

This lesson is about what is underneath the command line. You will type only a few look-around commands. The commands themselves are taught in the lessons that follow; the aim here is a picture of the system in your head, so that nothing later feels like magic.

### What an operating system does

A computer is hardware: a processor, memory, a disk, and a network connection. Hardware does nothing useful on its own. An **operating system** is the software that sits between the hardware and the programs you want to run. It does three jobs:

- It **shares the hardware** between programs, so that many can run at once without getting in each other's way.
- It **stores and finds files**, so that your data has names and places.
- It **keeps users apart**, so that one person's files are protected from another's.

Windows, macOS, and Linux are all operating systems. Every program you run, from a web browser to `samtools`, asks the operating system to do things for it: read this file, use this much memory, send this over the network.

### The kernel

The core of an operating system is the **kernel**. It is the one program that talks directly to the hardware, and it runs all the time from the moment the computer starts. Other programs never touch the hardware themselves. They ask the kernel to do it for them.

The kernel is responsible for:

| Job | What it means |
|-----|---------------|
| Processes | Starting programs, giving each a turn on the processor, and stopping them |
| Memory | Giving each program its own share of memory, and keeping them separate |
| Files | Reading from and writing to disks, through the filesystem |
| Devices | Talking to disks, keyboards, screens, and network cards through drivers |
| Security | Deciding who is allowed to read, write, or run what |

The word **Linux**, strictly, names a kernel. It was started in 1991 by Linus Torvalds and is now developed by thousands of people. When you type a command, this is what happens:

```
You type:  ls Training
              |
              v
   +-----------------------+
   | The program `ls`      |   "Please list the contents of Training."
   +-----------------------+
              |   asks
              v
   +-----------------------+
   | The kernel            |   Finds the directory on the disk.
   +-----------------------+
              |   reads
              v
   +-----------------------+
   | Hardware (the disk)   |
   +-----------------------+
              |
              v
   `ls` receives the names and prints them to your screen.
```

### Shell and terminal

Two more words are easy to mix up with the kernel:

- The **terminal** is the window you type in. It displays text and passes your keystrokes on.
- The **shell** is the program inside the terminal that reads each line you type, works out what you mean, and runs the program you asked for. This course uses a shell called **bash**.

You met both in [Module 0, Lesson 1](../Module_00_Getting_Ready/Lesson_1_What_You_Need_and_Why.md). Put together with the kernel, they form layers:

```
       You at the keyboard
              |
              v
+-------------------------------------+
|  Terminal  (the window)             |
+-------------------------------------+
|  Shell: bash  (reads your commands) |
+-------------------------------------+
|  Programs: ls, grep, samtools ...   |      Everything from the kernel up to
+-------------------------------------+      here, plus the system tools that
|  Kernel                             |      come with it, is the operating
+-------------------------------------+      system.
|  Hardware: processor, memory, disk  |
+-------------------------------------+
```

Strictly, "Linux" is only the kernel. A complete, usable operating system also needs a shell and a set of everyday tools such as `ls` and `cp`, and many of those come from the GNU project. That is why you will sometimes see the whole system called GNU/Linux. In everyday speech, "Linux" means the whole thing, and this course does the same.

### Linux comes in flavours

The kernel is free and open source, so anyone can combine it with their own choice of tools, installers, and defaults, and release the result. Each such bundle is a **distribution**, or **distro**. They all run the same kernel and behave in much the same way, but they differ in how software is installed, how often it is updated, and who maintains it.

```
Linux kernel  (shared by every distribution)
 |
 |-- Debian family
 |      Debian
 |       `-- Ubuntu            <- used in this course
 |            `-- Linux Mint, Pop!_OS
 |
 |-- Red Hat family
 |      Fedora, Red Hat Enterprise Linux (RHEL),
 |      Rocky Linux, AlmaLinux
 |
 |-- Arch family
 |      Arch Linux, Manjaro
 |
 `-- Alpine Linux              <- very small; common inside containers
```

The family matters mostly for one reason: each uses a different tool to install system software, called a **package manager**.

| Family | Package manager | Example command |
|--------|-----------------|-----------------|
| Debian, Ubuntu | `apt` | `sudo apt install git` |
| Red Hat, Fedora, Rocky, AlmaLinux | `dnf` | `sudo dnf install git` |
| Arch | `pacman` | `sudo pacman -S git` |

You already used `apt` in Module 0 (`sudo apt update`). In bioinformatics you will install most tools with **conda** instead, which works the same way on every distribution (see [Module 4](../Module_04_Conda/README.md)). If you move to a university cluster running Rocky Linux or a cloud machine running Debian, the commands in this course still work. Only the system-level install command changes.

This course uses **Ubuntu**, a Debian-based distribution, because it is widely used, well supported, and the default for WSL.

### Processes

A **process** is a program that is running. When you start `fastqc`, the kernel creates a process for it, gives it memory, and schedules it on the processor. Every process has a number, its **process ID**, and an owner. Many processes run at once, including the shell itself and the many background services that keep the system working. Later in the course, long analyses will run as processes that you start, watch, and sometimes stop.

### The filesystem is one tree

A computer stores files in a hierarchy of folders. Linux calls a folder a **directory**. The way Windows handles this is different from Linux, and the difference trips up almost every newcomer:

- **Windows** has several separate trees, one per drive: `C:\`, `D:\`, and so on.
- **Linux** has **one** tree. Everything, including every disk and USB stick, appears somewhere inside it.

The top of that single tree is the **root directory**, written `/` (a single forward slash). Every file and directory on the system lies somewhere below it. It is called the root because the tree is drawn growing downward from this one point, like a family tree.

Here is the layout of a typical Linux system. The names and purposes are the same on all distributions, because they follow a shared standard.

```
/                         the root: the top of everything
|-- bin   -> usr/bin      essential programs (ls, cp, grep, bash)   [a link]
|-- boot                  files needed to start the system, including the kernel
|-- dev                   devices, shown as files (for example /dev/null)
|-- etc                   system-wide configuration files
|-- home                  the personal directories of the users
|   `-- yourname          YOUR home directory, also written ~
|-- lib   -> usr/lib      libraries that programs need              [a link]
|-- media                 USB sticks and other removable media
|-- mnt                   other drives mounted here (WSL: c = your Windows C: drive)
|-- opt                   optional, add-on software installed by hand
|-- proc                  live information about the system (not on disk)
|-- root                  home directory of the administrator (the root user)
|-- run                   data about the system since it started
|-- sbin  -> usr/sbin     system administration programs            [a link]
|-- srv                   data served by this machine (rarely used)
|-- sys                   information about devices and the kernel (not on disk)
|-- tmp                   temporary files
|-- usr                   most installed programs and their files
|   |-- bin               programs
|   |-- lib               libraries
|   |-- local             software added by the local administrator
|   `-- share             shared data such as documentation
`-- var                   data that changes while the system runs
    `-- log               log files
```

On recent versions of Ubuntu, `/bin`, `/sbin`, and `/lib` are not separate directories any more. They are **links** (shortcuts) that point to `/usr/bin`, `/usr/sbin`, and `/usr/lib`. You can still use either name.

You may see a few extra entries when you list `/` on your own machine, such as `snap` or `lost+found`, and on WSL a file called `init`. They are normal.

### What is in each main directory

| Directory | What it holds | Notes for you |
|-----------|---------------|---------------|
| `/home` | A personal directory for each user, such as `/home/yourname` | **Your work lives here.** Your data, scripts, and results go in your home |
| `/bin`, `/sbin` | Essential programs: `bin` for everyone, `sbin` for administration | Where commands such as `ls` and `cp` actually live. Leave alone |
| `/usr` | Most installed programs, libraries, and documentation | Leave alone. `/usr/local` is for software added locally |
| `/opt` | "Optional" software that comes as a self-contained directory | Large third-party tools are often installed here by hand |
| `/etc` | Configuration files for the system and its services, as plain text | Read-only for you. Changing it needs administrator rights |
| `/var` | Data that grows and changes: logs in `/var/log`, caches, mail | Useful when troubleshooting. Leave alone |
| `/tmp` | Temporary scratch files, which may be cleared when the machine restarts | Never keep results here |
| `/mnt` | A place to attach other drives | **On WSL, your Windows drives appear here**, as `/mnt/c`, `/mnt/d`, and so on |
| `/media` | Removable media such as USB sticks | |
| `/dev` | Devices, presented as files | See "everything is a file" below |
| `/proc`, `/sys` | Live information from the kernel. These are not stored on disk | Read-only windows into the running system |
| `/boot` | The kernel and the files needed to start up | Empty on WSL, because Windows starts the kernel |
| `/root` | The home directory of the administrator, not of you | You cannot enter it as an ordinary user |

For bioinformatics, `/opt` deserves a note. Some tools are not available through `apt` or conda, or are installed once for everyone on a shared server. These tend to go in `/opt`. For example, on one machine used to prepare this course, `/opt` held `ont-guppy-cpu`, a Nanopore base-calling tool, and `quarto`, a publishing tool. Your own tools, installed with conda in Module 4, live in your home directory instead.

> **Warning:** The directories outside your home (`/etc`, `/usr`, `/bin`, `/var`, and so on) are the machine's engine room. Deleting or changing files there can stop the system from working. As an ordinary user you are protected from most mistakes, because the system refuses. Do not use `sudo` to get around a "permission denied" message unless you are sure what you are doing.

### Three things called "root"

The word root causes more confusion than any other in this lesson, because Linux uses it for three different things:

```
        /                  <-- 1. The root DIRECTORY: the top of the whole file tree.

   user "root"             <-- 2. The root USER: the administrator account, which may
                                  do anything on the system.

        /root              <-- 3. The directory /root: the home directory of the root
                                  user. A directory called root, inside the root directory.
```

They are related by name only. The root directory `/` is *not* your home, and `/root` is *not* the same as `/`. Your home is `/home/yourname`.

### Your home directory

Every user has a **home directory**, which is where you start each time you open a terminal and where your own files belong. It is `/home/` followed by your username. The shell also gives it a short name, `~` (a tilde), and stores its full path in a variable called `HOME`. So `~/Bioinformatic_Fridays`, `$HOME/Bioinformatic_Fridays`, and `/home/yourname/Bioinformatic_Fridays` all mean the same place.

A path is the address of a file in the tree. Read it from left to right, starting at the root, and each `/` goes one level deeper. This is the full path of the first Ebola read file you used in Module 1:

```
/home/yourname/Bioinformatic_Fridays/Training/short_reads/paired/SRR1553607_1.fastq
|    |         |                      |        |           |      |
|    |         |                      |        |           |      `-- the file
|    |         |                      |        |           `-- a directory for paired reads
|    |         |                      |        `-- a directory for short reads
|    |         |                      `-- the course data
|    |         `-- the course directory you made in Module 0
|    `-- your username: your home directory
`--- the root directory (the first slash)
```

A path that begins at `/` like this is called an **absolute path**. [Lesson 6](Lesson_6_Absolute_and_Relative_Paths.md) covers absolute and relative paths in detail.

### Everything is a file

A central idea in Linux is that nearly everything is presented as a file. That includes:

- ordinary files, such as a FASTQ file
- directories, which are special files that list other files
- devices, such as a disk or a keyboard, in `/dev`
- live information from the kernel, in `/proc`

The benefit is that the same simple tools (the ones you will learn in the next lessons, such as `head` and `grep`) work on all of them. You can look at how much memory the machine has the same way you look at a FASTQ file. Two examples are in the worked examples below.

### Users and permissions

Linux is a multi-user system. Every file has an **owner** and a **group**, and a set of **permissions** that say what the owner, the group, and everyone else may do:

| Letter | Meaning for a file | Meaning for a directory |
|--------|--------------------|-------------------------|
| `r` | read the contents | list what is inside |
| `w` | change the contents | add or remove files inside |
| `x` | run it as a program | enter it |

A permission string looks like this, as printed for the `ls` program:

```
-  rwx  r-x  r-x   root  root   /usr/bin/ls
|  |    |    |     |     |
|  |    |    |     |     +--- the group that owns the file
|  |    |    |     +--------- the user that owns the file
|  |    |    +--------------- everyone else: read and execute, but not write
|  |    +-------------------- the group: read and execute
|  +------------------------- the owner: read, write, and execute
+---------------------------- type: - is an ordinary file, d a directory, l a link
```

Here the owner is the **root user**, the administrator, who may do anything. You and the other ordinary users may run `ls` but cannot change it. This is why you cannot accidentally break the system. When an administrator needs to run a single command with these rights, they put `sudo` in front of it. You will write your own permissions with `chmod` in [Lesson 4](Lesson_4_Scripting_and_Permissions.md).

### WSL and TLJH

> **On WSL (your own machine):** WSL 2 runs a real Linux kernel inside a lightweight virtual machine on your Windows computer. Your Linux home directory is stored in a virtual disk that Linux manages, and your Windows drives are attached to the single Linux tree under `/mnt`.
>
> **On TLJH (shared server):** There is no Windows underneath and no `/mnt/c`. TLJH runs on a Linux server, normally Ubuntu. Your home directory is on the server and is named after your login. You are an ordinary user, so you cannot change files outside your home unless a facilitator has made you an administrator.

```
+----------------------------------------------------------------+
|  Your Windows computer                                         |
|                                                                |
|    Windows programs          +-----------------------------+   |
|    (browser, Word, ...)      |  WSL 2                      |   |
|                              |  (lightweight virtual       |   |
|    Windows drive C:  <-------+-->  machine)                |   |
|    appears in Linux as       |  Linux kernel               |   |
|    /mnt/c                    |  /home/yourname  (Linux     |   |
|                              |     files, stored in a      |   |
|                              |     virtual disk)           |   |
|                              +-----------------------------+   |
+----------------------------------------------------------------+
```

This picture explains the advice you saw in Module 0. Files in `/home/yourname` are read and written by Linux directly. Files under `/mnt/c` have to cross the boundary to Windows each time, which is slower. For large sequencing files, keep them in your Linux home.

> **Warning:** On WSL, `/mnt/c` is your real Windows drive. Deleting something there deletes your real Windows files, with no recycle bin. Take extra care with `rm` under `/mnt`.

> **Tip:** To see your Linux files from Windows, type `\\wsl.localhost\Ubuntu` into the File Explorer address bar.

## Worked Examples

These commands only look around. Copy them as written; each is explained properly in the lessons that follow. Your output will differ in the details.

### 1) Which operating system and distribution am I on?

`head -n 6` prints the first six lines of a file. The file `/etc/os-release` describes the distribution.

```bash
head -n 6 /etc/os-release
```
Output (your version will differ):
```
PRETTY_NAME="Ubuntu 22.04.2 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.2 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
```

`NAME` and `ID` give the distribution (Ubuntu, from the Debian family). Notice that this information is stored in `/etc`, as a plain text file.

### 2) Which kernel is running?

`uname -r` prints the kernel's release number.

```bash
uname -r
```
Output (yours will differ):
```
6.18.58.1-microsoft-standard-WSL2
```

The number is the kernel version. On WSL the name ends in `microsoft-standard-WSL2`, which shows that this is the Linux kernel that WSL provides. On TLJH you will see an ordinary server kernel instead.

### 3) Look at the root directory

```bash
ls /
```
Output (abbreviated; you may see more entries):
```
bin   boot  dev  etc  home  init  lib  lib32  lib64  libx32  lost+found
media  mnt  opt  proc  root  run  sbin  snap  srv  sys  tmp  usr  var
```

Compare this with the tree above. These are the top-level directories of the whole system.

### 4) See that `/bin` is a link

`ls -ld` shows a directory entry itself, in long format, instead of listing what is inside it. The `l` at the start and the arrow show that these are links.

```bash
ls -ld /bin /sbin /lib
```
Output (the dates will differ):
```
lrwxrwxrwx 1 root root 7 Oct 25  2022 /bin -> usr/bin
lrwxrwxrwx 1 root root 7 Oct 25  2022 /lib -> usr/lib
lrwxrwxrwx 1 root root 8 Oct 25  2022 /sbin -> usr/sbin
```

### 5) Find your home directory

```bash
echo "$HOME"
```
Output (yours will show your own username):
```
/home/yourname
```

`pwd` prints the directory you are currently in. A new terminal starts in your home, so it gives the same answer.

```bash
pwd
```
Output:
```
/home/yourname
```

List the `/home` directory to see the home directories on the system:

```bash
ls /home
```
Output:
```
yourname
```

### 6) Try to enter the root user's home

```bash
ls /root
```
Output:
```
ls: cannot open directory '/root': Permission denied
```

This message is the system doing its job. `/root` belongs to the administrator, and you are an ordinary user.

### 7) On WSL: see your Windows drives

> **On WSL (your own machine):** Run the command below.
>
> **On TLJH (shared server):** Skip this example. There is no `/mnt/c`.

```bash
ls /mnt
```
Output (yours will show your own drive letters):
```
c  d  e  f  wsl  wslg
```

Each letter is a Windows drive, attached to the Linux tree. Your Windows `C:` drive is `/mnt/c`.

### 8) Everything is a file

A device appears in `/dev`. `ls -l` shows its type in the first character: `c` means a character device.

```bash
ls -l /dev/null
```
Output (the date will differ):
```
crw-rw-rw- 1 root root 1, 3 Nov 10 18:54 /dev/null
```

`/dev/null` is a special device that discards anything written to it. Live information from the kernel appears as files too. This prints the first three lines of the memory report in `/proc`:

```bash
head -n 3 /proc/meminfo
```
Output (your numbers will differ):
```
MemTotal:        7990940 kB
MemFree:           93088 kB
MemAvailable:    5382716 kB
```

This file is not stored on disk. The kernel generates it when you ask for it.

### 9) Read a permission string

```bash
ls -l /usr/bin/ls
```
Output (the date and size may differ):
```
-rwxr-xr-x 1 root root 138216 Feb  8  2024 /usr/bin/ls
```

Compare this with the permission diagram above: an ordinary file, owned by root, which everyone may read and run but only the owner may change.

## Exercises

1) In your own words, what is the difference between the kernel, the shell, and the terminal?

2) Run `head -n 6 /etc/os-release`. Which distribution are you on, and which family does it belong to?

3) Run `uname -r`. What kernel version do you have? If you are on WSL, what does the end of the version string tell you?

4) Run `ls /`. Pick three directories from the output and say what each is for.

5) Say which top-level directory you would look in to find: (a) your own data and scripts; (b) the configuration file of a system service; (c) the log files of the system; (d) a third-party tool an administrator installed by hand; (e) your Windows `C:` drive, if you are on WSL.

6) Explain the difference between `/`, `/root`, and `/home/yourname`.

7) Run `ls -l /dev/null` and `head -n 3 /proc/meminfo`. Neither is an ordinary file on your disk. What does this show about how Linux treats devices and system information?

8) Challenge: A friend runs Rocky Linux and you run Ubuntu. You both want to install `git`. Will the same command work? What will work on both?

## Solutions

### Solution 1
The **kernel** is the core of the operating system and the only program that talks directly to the hardware; it manages processes, memory, files, and devices. The **terminal** is the window you type in. The **shell** (bash) is the program inside the terminal that reads your commands and runs them. When you run a command, the shell starts the program, and the program asks the kernel to do the actual work.

### Solution 2
```bash
head -n 6 /etc/os-release
```
Output (yours may differ):
```
PRETTY_NAME="Ubuntu 22.04.2 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.2 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
```
This is Ubuntu, which belongs to the Debian family.

### Solution 3
```bash
uname -r
```
Output (yours will differ):
```
6.18.58.1-microsoft-standard-WSL2
```
The first part is the kernel version number. On WSL the ending `microsoft-standard-WSL2` shows that it is the Linux kernel provided by WSL 2, running inside Windows.

### Solution 4
Any three from the tree. For example: `/home` holds the users' personal directories; `/etc` holds system configuration files; `/tmp` holds temporary files; `/bin` holds essential programs such as `ls`; `/mnt` is where other drives are attached; `/dev` holds devices shown as files; `/var` holds changing data such as logs.

### Solution 5
(a) `/home/yourname`, your home directory. (b) `/etc`. (c) `/var/log`. (d) `/opt` (or `/usr/local`). (e) `/mnt/c`.

### Solution 6
`/` is the **root directory**, the top of the whole file tree. `/root` is a directory inside it: the home directory of the administrator, the **root user**. `/home/yourname` is **your** home directory, where your own files belong. Only the first is the top of the tree; the other two are ordinary directories.

### Solution 7
```bash
ls -l /dev/null
head -n 3 /proc/meminfo
```
Output (yours will differ):
```
crw-rw-rw- 1 root root 1, 3 Nov 10 18:54 /dev/null
MemTotal:        7990940 kB
MemFree:           93088 kB
MemAvailable:    5382716 kB
```
Linux presents devices (`/dev/null`) and live system information (`/proc/meminfo`) as if they were files, so the same tools you use on ordinary files, such as `ls` and `head`, work on them. This is the meaning of "everything is a file".

### Solution 8
The `git` install command is different, because the two distributions use different package managers: `sudo apt install git` on Ubuntu, and `sudo dnf install git` on Rocky Linux. What works on both is everything else in this course: the kernel is the same, the filesystem layout is the same, the shell commands (`ls`, `grep`, `head`) are the same, and conda installs tools the same way on both.
