# Lesson 2 — Installing WSL

> **On TLJH (shared server):** You do not need WSL. Skip this entire lesson and go to Lesson 3.

## Learning Objectives
- Install Ubuntu Linux on Windows using WSL
- Create your Linux username and password
- Update the Ubuntu software list after installation
- Recognise and fix the most common installation problems

## Conceptual Overview

**WSL** (Windows Subsystem for Linux) lets a full Linux system run inside Windows, sharing your files and hardware without a separate computer or a slow virtual machine. You install it once, and from then on you open "Ubuntu" like any other program to get a Linux terminal.

The install has two halves. First you run **one command in Windows** (not in Linux — Linux does not exist on your machine yet). That command downloads and sets up Ubuntu. After a restart, you open Ubuntu and do the second half **inside Linux**: create your user and update the software list.

> **Note:** WSL needs Windows 10 (version 2004 or later) or Windows 11. Almost all machines from the last few years qualify.

## Worked Examples

### 1) Open Windows PowerShell as Administrator

This step is in **Windows**, not in a Linux terminal. Click the **Start menu**, type `PowerShell`, right-click **Windows PowerShell**, and choose **Run as administrator**. Click **Yes** if Windows asks for permission.

### 2) Install WSL with Ubuntu

In that PowerShell window, run:

```powershell
wsl --install
```

This downloads WSL and installs Ubuntu (the default Linux version), which is what this course uses. It can take several minutes.

Output (abbreviated; wording varies by Windows version):
```
Installing: Windows Subsystem for Linux
Installing: Ubuntu
The requested operation is successful. Changes will not be effective until the system is rebooted.
```

### 3) Restart your computer

Save your work and restart Windows. After the restart, an **Ubuntu** window usually opens on its own to finish setup. If it does not, open the Start menu, type `Ubuntu`, and press Enter.

### 4) Create your Linux username and password

The first time Ubuntu opens, it asks you to create a user. This user is separate from your Windows account.

```
Enter new UNIX username:
```
Type a short, lowercase name (for example `bodeoni`) and press Enter.

```
New password:
```
Type a password and press Enter. **The screen stays blank as you type the password — this is normal.** Type it again when asked to confirm.

When it finishes, you see the Linux prompt:
```
yourname@computer:~$
```

> **Warning:** Write your WSL username and password down somewhere safe. You will need the password whenever you run an administrative command (one that starts with `sudo`), and there is no "reset password" button.

### 5) Update the software list

Ubuntu keeps a list of available software. Refresh it so later installs work smoothly. `sudo` runs the command with administrative rights and will ask for the password you just created.

```bash
sudo apt update
```
Output (last lines; details vary):
```
Reading package lists... Done
Building dependency tree... Done
All packages are up to date.
```

## Exercises

1) Run `wsl --install` in PowerShell (as Administrator) and restart when it finishes. Did Ubuntu open automatically after the restart?

2) Create your Linux username and password. Confirm you end at a prompt that looks like `yourname@computer:~$`.

3) Run `sudo apt update`. Enter your password when prompted. Did it finish without an error?

4) Challenge: In PowerShell, run `wsl --status`. What version of WSL does it report?

## Solutions

### Solution 1
```powershell
wsl --install
```
On most machines Ubuntu opens by itself after the restart. If it does not, open the Start menu, type `Ubuntu`, and press Enter to finish setup.

### Solution 2
When Ubuntu first opens it prompts for a new UNIX username and password. After you set them, the prompt `yourname@computer:~$` means Linux is installed and you are logged in.

### Solution 3
```bash
sudo apt update
```
Enter your Linux password when asked (the screen stays blank while you type). A successful run ends with the package lists updated and no error.

### Solution 4
```powershell
wsl --status
```
Output (example):
```
Default Distribution: Ubuntu
Default Version: 2
```
Version 2 is what you want.

---

## If something goes wrong

- **`wsl --install` is not recognised, or nothing installs.** Your Windows may be older. In PowerShell (Administrator) run `wsl --update`, then try again. If it still fails, check that Windows is fully updated.
- **An error mentions "virtualization" or "BIOS".** Virtualization is switched off in your computer's firmware. Restart, enter the BIOS/UEFI setup (often by pressing F2, F10, or Delete during startup), enable the virtualization setting (often called "Intel VT-x", "AMD-V", or "SVM"), save, and restart. Your facilitator can help with this.
- **You forgot your Linux password.** It cannot be recovered, but it can be reset with help from a facilitator. Bring it to a session rather than reinstalling.
