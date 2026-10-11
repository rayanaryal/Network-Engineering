
# Linux — Foundations, Commands and System Administration

Beginner-friendly Linux study notes covering the Linux kernel, GNU utilities, UNIX history, Ubuntu, terminal commands, file management, users, and system administration.

These notes are based on lecture material and practical learning using Ubuntu in VMware Fusion.

---

## Table of Contents

- [1. Full Forms and Quick Notes](#1-full-forms-and-quick-notes)
- [2. Linux Definition](#2-linux-definition)
- [3. History of UNIX](#3-history-of-unix)
- [4. What Is Linux?](#4-what-is-linux)
- [5. Linux Distributions](#5-linux-distributions)
- [6. GNU Utilities](#6-gnu-utilities)
  - [6.1 GNU Tools and the Linux Kernel](#61-gnu-tools-and-the-linux-kernel)
  - [6.2 Common Utilities](#62-common-utilities)
- [7. What Is the Kernel?](#7-what-is-the-kernel)
  - [7.1 Kernel Responsibilities](#71-kernel-responsibilities)
  - [7.2 Memory Management](#72-memory-management)
  - [7.3 Hardware and Software Interaction](#73-hardware-and-software-interaction)
  - [7.4 Command Output and Error Management](#74-command-output-and-error-management)
- [8. History of Linux](#8-history-of-linux)
- [9. Linux Infrastructure](#9-linux-infrastructure)
- [10. Linux in Information Centre Networks](#10-linux-in-information-centre-networks)
- [11. Installing Ubuntu with VMware Fusion](#11-installing-ubuntu-with-vmware-fusion)
- [12. Types of Users: Normal User and Root](#12-types-of-users-normal-user-and-root)
- [13. Understanding the Linux Terminal](#13-understanding-the-linux-terminal)
- [14. Linux File System Structure](#14-linux-file-system-structure)
- [15. Working with Directories](#15-working-with-directories)
- [16. Listing and Locating Files](#16-listing-and-locating-files)
- [17. Creating Files](#17-creating-files)
- [18. Managing Files from the Command Line](#18-managing-files-from-the-command-line)
- [19. Viewing File Contents](#19-viewing-file-contents)
- [20. Searching with `find`](#20-searching-with-find)
- [21. Searching Text with `grep`](#21-searching-text-with-grep)
- [22. Command History](#22-command-history)
- [23. Date, Time and Calendar](#23-date-time-and-calendar)
- [24. System Information and Processes](#24-system-information-and-processes)
- [25. Managing Users and Groups](#25-managing-users-and-groups)
- [26. Package Management with APT](#26-package-management-with-apt)
- [27. Getting Help in Linux](#27-getting-help-in-linux)
- [28. Text Editors](#28-text-editors)
- [29. The `vi` Editor](#29-the-vi-editor)
- [30. Important Configuration Files](#30-important-configuration-files)
- [31. Linux Shell and Windows Command Prompt](#31-linux-shell-and-windows-command-prompt)
- [32. Basic Security Notes](#32-basic-security-notes)
- [33. Practical Command Reference](#33-practical-command-reference)
- [34. Historical Claims to Verify](#34-historical-claims-to-verify)
- [35. Learning Checklist](#35-learning-checklist)

---

## 1. Full Forms and Quick Notes

| Term | Meaning or purpose |
|---|---|
| APT | Advanced Package Tool |
| PWD | Commonly used as an abbreviation for present working directory; `pwd` means **print working directory** |
| `sudo` | Runs a command with elevated privileges when authorised |
| `$` | Commonly used shell prompt symbol for a normal user |
| `#` | Commonly used shell prompt symbol for the root user |
| `rm` | Removes files and directories |
| `cd` | Changes directory |
| `ls` | Lists files and directories |
| `cp` | Copies files and directories |
| `mv` | Moves or renames files and directories |
| `mkdir` | Creates directories |
| `cat` | Displays or concatenates file contents |
| `touch` | Creates an empty file if it does not exist, or updates timestamps |
| `echo` | Displays text or expands shell variables |
| `grep` | Searches text for matching patterns |
| `find` | Searches for files and directories |
| `man` | Displays a command's manual page |
| `gcc` | GNU Compiler Collection; includes a C compiler |
| `clear` | Clears the visible terminal screen |
| `history` | Displays commands recorded in the shell history |

### Cisco comparison

For someone studying networking, the Linux prompt can be compared loosely with Cisco CLI prompts:

| Environment | Example | General meaning |
|---|---|---|
| Linux normal user | `$` | Ordinary user shell |
| Linux root user | `#` | Administrative shell |
| Cisco user EXEC | `Router>` | Basic CLI access |
| Cisco privileged EXEC | `Router#` | Privileged CLI access |

These are useful visual comparisons, but Linux shell privileges and Cisco CLI modes are not identical.

---

## 2. Linux Definition

Linux is an open-source operating system **kernel** that manages communication between software and computer hardware.

The kernel is the core component of many operating systems. It helps manage the CPU, memory, devices, and processes.

Linux is used in many environments, including:

- Desktop and laptop computers
- Servers and data centres
- Cloud infrastructure
- Network appliances
- Embedded systems
- Security and development environments

**Key point:** Linux technically refers to the kernel. A complete Linux distribution includes the kernel and the other software needed to operate a usable system.

---

## 3. History of UNIX

UNIX originated at Bell Labs in 1969. Its development helped establish an influential family of operating systems.

Important characteristics associated with UNIX include:

1. A relatively simple and elegant design.
2. The use of the C programming language in much of its later development, rather than relying entirely on assembly language.
3. Reusable software components and tools.
4. A design philosophy that encouraged combining smaller programs to perform larger tasks.

The Bell Labs developers named the operating system UNIX.

UNIX and UNIX-like systems have influenced many operating systems used today.

Examples of historical commercial UNIX systems include:

- SunOS
- Solaris
- SCO UNIX
- SGI IRIX
- IBM AIX
- HP-UX

Apple's macOS also has a UNIX heritage, with important foundations in NeXTSTEP and BSD-derived technology.

**Study note:** UNIX licensing and source-code availability varied across products and periods. It is more accurate to describe particular commercial UNIX versions as proprietary than to assume every UNIX-related system has identical licensing.

---

## 4. What Is Linux?

Linux is a free and open-source kernel used in many operating systems.

In everyday conversation, people often say "Linux" when referring to an entire operating system, such as Ubuntu.

A simplified model is:

```text
Applications and System Utilities
              |
        Shell / User Tools
              |
         Linux Kernel
              |
        Computer Hardware
```

The kernel manages essential system resources, while the shell, utilities, libraries, and applications allow users and programs to interact with the system.

### Simplified formula

```text
Linux Kernel + System Software + Applications
                     |
             Usable Linux System
```

GNU utilities are an important part of many Linux systems, although not every Linux distribution uses exactly the same set of tools.

---

## 5. Linux Distributions

A **Linux distribution**, or *distro*, is a packaged operating system built around the Linux kernel and supporting software.

Examples include:

- Ubuntu
- Debian
- Fedora
- Red Hat Enterprise Linux
- Linux Mint
- Kali Linux
- Arch Linux

Different distributions may be designed for desktop use, servers, security testing, education, or specialised environments.

### Ubuntu

Ubuntu is a Linux distribution. It includes the Linux kernel, system utilities, package-management tools, and applications.

A distribution may differ from another distribution in:

- Default software
- Package-management system
- Security configuration
- Release and update schedule
- Desktop environment
- Intended use

### Notes on security and specialised distributions

My lecture notes discuss the use of different operating-system packages in countries such as China and Russia, including the idea of separating government departments or organisations into different environments.

Separate systems can help reduce shared dependencies and limit some attack paths. However, **using different distributions alone does not guarantee that an attacker who compromises one system cannot compromise another**. Network segmentation, identity controls, patching, monitoring, and other security measures also matter.

**Conclusion:** The Linux kernel, system software, and applications work together to form a usable Linux system.

---

## 6. GNU Utilities

GNU provides many of the tools used on Linux systems.

My lecture notes describe the relationship using this analogy:

- **Linux kernel:** The engine that manages hardware and system resources.
- **GNU utilities:** Tools that let users interact with the system and perform tasks.

This partnership is why the name **GNU/Linux** is sometimes used for operating systems built around the Linux kernel and GNU software.

Not every Linux system uses GNU utilities exclusively; some use alternative implementations.

### 6.1 GNU Tools and the Linux Kernel

The kernel does not normally provide a complete command-line environment by itself.

A shell and utilities allow users to enter commands, manipulate files, inspect the system, and run programs.

For example:

```bash
ls
pwd
cp
mv
rm
mkdir
```

These commands are commonly available on Ubuntu.

### 6.2 Common Utilities

| Command or program | Purpose |
|---|---|
| `ls` | List directory contents |
| `cd` | Change directory |
| `cp` | Copy files |
| `mv` | Move or rename files |
| `rm` | Remove files |
| `mkdir` | Create directories |
| `nano` | Terminal text editor |
| `emacs` | Text editor |
| `gcc` | Compiler collection |
| `bash` | Command-line shell |

The exact origin of individual programs varies. For example, `nano` and `emacs` are editors, while `bash` is a shell.

---

## 7. What Is the Kernel?

The kernel is the central component of an operating system.

In a Linux distribution, the Linux kernel manages communication between applications and hardware while coordinating important system resources.

The kernel is involved in:

- Memory management
- Process scheduling
- Device and driver management
- File-system operations
- Networking
- System calls
- Access control and isolation mechanisms

### 7.1 Kernel Responsibilities

A simplified view:

```text
              USER
                |
       Applications / Shell
                |
          System Calls
                |
        +----------------+
        | Linux Kernel   |
        |                |
        | Memory         |
        | Processes      |
        | Drivers        |
        | Networking     |
        | File Systems   |
        +----------------+
                |
          Hardware Devices
```

This diagram shows the kernel's position between applications and the hardware. Real operating systems have additional layers and interfaces.

### 7.2 Memory Management

The kernel manages the allocation and use of memory by processes.

Memory management helps the system:

- Allocate memory to programs.
- Keep processes separated.
- Manage virtual memory.
- Reclaim memory when it is no longer needed.
- Coordinate access to physical memory.

Efficient memory management does not mean a Linux system can never freeze or run out of memory. Applications, drivers, hardware, and resource exhaustion can still cause problems.

### 7.3 Hardware and Software Interaction

The kernel coordinates access to hardware through device drivers and system interfaces.

Examples of hardware include:

- CPU
- RAM
- Storage devices
- Network interfaces
- USB devices

Applications generally request services from the kernel rather than controlling hardware directly.

### 7.4 Command Output and Error Management

When a command runs, its output is commonly sent to one of two streams:

- **Standard output (`stdout`):** Normal results.
- **Standard error (`stderr`):** Diagnostic or error messages.

Example:

```bash
ls /
```

This lists the contents of the root directory.

Another example:

```bash
ls /directory-that-does-not-exist
```

This normally produces an error message because the requested path does not exist.

You can redirect output:

```bash
ls / > files.txt
```

This saves standard output to `files.txt`, replacing the file's existing contents if it already exists.

To redirect standard error:

```bash
ls /directory-that-does-not-exist 2> error.txt
```

This saves the error message to `error.txt`.

---

## 8. History of Linux

Linux was created by Linus Torvalds in 1991. Its development was influenced by UNIX-like operating systems and the MINIX system.

Important milestones include:

- **1969:** UNIX development began at Bell Labs.
- **1991:** Linus Torvalds announced his work on the Linux kernel.
- **1991:** Early Linux kernel releases appeared.
- **1994:** Linux kernel version 1.0 was released.

Linux subsequently became widely used in servers, networking, cloud infrastructure, embedded devices, and personal computers.

### Important historical distinction

Linux is not simply another name for UNIX. Linux is a UNIX-like operating-system kernel developed independently, although it follows many similar design principles.

The detailed claims in my original lecture notes about a particular unnamed 1969 program and the first Linux distribution should be checked against reliable historical sources before being memorised as facts.

---

## 9. Linux Infrastructure

Linux is widely used in modern computing infrastructure.

Examples include:

- Web servers
- Database servers
- Cloud platforms
- Virtual machines
- Containers
- Network services
- Cybersecurity tools
- Embedded devices

### Memory management

My lecture notes emphasise that Linux has strong memory-management capabilities.

However, good memory management does not mean a system will never hang. A system can still become unresponsive because of excessive resource usage, software faults, driver issues, storage problems, or other failures.

### Why this matters for IT and cybersecurity

Understanding Linux is useful for:

- Managing servers
- Troubleshooting network services
- Inspecting system logs
- Managing accounts and permissions
- Automating tasks
- Investigating security incidents

---

## 10. Linux in Information Centre Networks

My lecture notes include an **Information Center Network** topic and associated diagrams.

The diagrams were not included in the text provided for this README, so their exact content cannot be reconstructed from the notes alone.

In general, Linux servers may provide network services such as:

- Web hosting
- DNS
- DHCP
- File sharing
- Authentication
- Application hosting
- Monitoring and logging

A typical network might connect user devices to switches and routers, with servers providing services over the network.

**Add the original lecture diagram here** if you want this section to match your class material precisely.

---

## 11. Installing Ubuntu with VMware Fusion

My practical learning environment uses VMware Fusion and Ubuntu on a Mac.

VMware Fusion allows a supported guest operating system to run inside a virtual machine.

### Basic virtual-machine model

```text
Mac Computer
     |
macOS Host Operating System
     |
VMware Fusion
     |
Ubuntu Virtual Machine
     |
Linux Kernel and User-Space Software
```

This is a simplified representation of the virtualisation environment.

### Important terminology

| Term | Meaning |
|---|---|
| Host | The physical computer and its main operating system |
| Hypervisor | Software that manages virtual machines |
| Virtual machine | An isolated virtual computer |
| Guest OS | The operating system running inside the virtual machine |
| Ubuntu | The Linux distribution used in this learning environment |

On an Apple Silicon Mac, an ARM64 Ubuntu image is generally appropriate for native virtualisation. The selected image must match the virtualisation environment and processor architecture.

---

## 12. Types of Users: Normal User and Root

Linux supports different user accounts and privilege levels.

### Normal user

A normal user typically has a home directory such as:

```text
/home/username
```

A normal account can run permitted commands and access files according to its permissions.

### Root user

The root user is the superuser account, traditionally identified by user ID `0`.

Root can perform many administrative operations that ordinary users cannot.

Because root has extensive privileges, it should be used carefully.

### Switching to a root shell

My lecture notes introduce:

```bash
sudo -i
```

This requests an interactive root login shell when the current user is authorised to use `sudo`.

To leave the root shell:

```bash
exit
```

### Checking your current identity

```bash
whoami
```

This displays the username associated with the current shell's effective user identity.

Example:

```text
username
```

When run in a root shell, the result is normally:

```text
root
```

**Security reminder:** Do not run commands as root unless the task requires elevated privileges and you understand what the command will do.

---

## 13. Understanding the Linux Terminal

The terminal provides a text-based interface for entering commands.

A command generally has this structure:

```text
command [options] [arguments]
```

Example:

```bash
ls -l /home
```

Here:

- `ls` is the command.
- `-l` is an option requesting a detailed listing.
- `/home` is the target directory.

### Clearing the screen

Keyboard shortcut:

```text
Ctrl + L
```

Command:

```bash
clear
```

Both commonly clear the visible terminal display. They do not delete your files.

### The `#` comment symbol

In Bash, `#` begins a comment in the appropriate syntactic position.

Example:

```bash
# This is a comment
ls /
```

The shell ignores the comment line and executes `ls /`.

A comment is not a method of securely hiding commands. Command history, logs, and other records may still contain information about commands that were executed.

---

## 14. Linux File System Structure

Linux organises files and directories in a hierarchical structure.

The top-level directory is `/`, called the **root directory**.

Do not confuse the root directory `/` with the root user's home directory, commonly `/root`.

### Common directories

| Directory | Typical purpose |
|---|---|
| `/` | Top of the file-system hierarchy |
| `/home` | Home directories for normal users |
| `/root` | Root user's home directory |
| `/bin` | Essential user commands; often linked to `/usr/bin` on modern Ubuntu |
| `/sbin` | System administration commands; often linked to `/usr/sbin` on modern systems |
| `/etc` | System configuration files |
| `/var` | Variable data, including many logs and caches |
| `/tmp` | Temporary files |
| `/usr` | Many applications, libraries, and shared resources |
| `/dev` | Device files |
| `/proc` | Virtual file system exposing process and kernel information |
| `/sys` | Virtual file system exposing device and kernel information |
| `/boot` | Files used during the boot process |
| `/mnt` | Common mount point for temporarily mounted file systems |
| `/media` | Common mount point for removable media |

### Why file-system locations matter

Linux relies heavily on file paths. A command can produce different results depending on which directory you are in and which path you provide.

Always check the target path before deleting, moving, or changing files.

---

## 15. Working with Directories

### Show your current directory

```bash
pwd
```

Example output:

```text
/home/username
```

### List directory contents

```bash
ls
```

Show hidden files as well:

```bash
ls -a
```

Show a detailed listing:

```bash
ls -l
```

Combine options:

```bash
ls -la
```

### Change directory

Go to your home directory:

```bash
cd ~
```

Move into a directory:

```bash
cd Documents
```

Move up one directory:

```bash
cd ..
```

Return to the previous directory:

```bash
cd -
```

### Create a directory

```bash
mkdir LinuxPractice
```

Create nested directories:

```bash
mkdir -p LinuxPractice/Commands/Files
```

### Absolute and relative paths

An **absolute path** begins from the root directory.

Example:

```bash
/home/username/Documents
```

A **relative path** is interpreted from the current directory.

Example:

```bash
Documents
```

---

## 16. Listing and Locating Files

Linux offers several ways to locate files.

### List files

```bash
ls
```

List a particular directory:

```bash
ls /etc
```

### Find a file by name

Use `find` to search directories:

```bash
find /home -name "learning-commands.txt"
```

Search case-insensitively:

```bash
find /home -iname "learning-commands.txt"
```

Search for directories named `Documents`:

```bash
find /home -type d -name "Documents"
```

Search for text files:

```bash
find /home -type f -name "*.txt"
```

### Understanding `find`

- `find` is the command.
- `/home` is the starting directory.
- `-name` specifies a filename pattern.
- `-type f` selects regular files.
- `-type d` selects directories.

The command searches the selected starting location and its accessible subdirectories. It may not find files outside that location or files you cannot access.

---

## 17. Creating Files

My first practice files were named:

- `learning-commands.txt`
- `another-new-file.txt`

### Create an empty file with `touch`

```bash
touch learning-commands.txt
```

Create another file:

```bash
touch another-new-file.txt
```

If the file does not exist, `touch` creates an empty file. If it already exists, `touch` normally updates its timestamps rather than erasing its contents.

### Create a file with `echo`

```bash
echo "My Linux learning notes" > learning-commands.txt
```

The `>` operator redirects output to a file. It creates the file if needed and replaces its existing contents.

To append instead:

```bash
echo "Learning basic Linux commands" >> learning-commands.txt
```

The `>>` operator appends to the end of the file.

### Verify the files

```bash
ls -l
```

Read the file:

```bash
cat learning-commands.txt
```

**Important:** Be careful with `>` because it can overwrite existing file contents.

---

## 18. Managing Files from the Command Line

### Copy a file

```bash
cp learning-commands.txt backup.txt
```

This creates a copy named `backup.txt`.

### Move a file

```bash
mv backup.txt Documents/
```

This moves the file into the `Documents` directory, assuming that directory exists relative to your current location.

### Rename a file

```bash
mv another-new-file.txt practice-notes.txt
```

The `mv` command can move or rename files.

### Remove a file

```bash
rm practice-notes.txt
```

Removal is usually immediate from the command-line perspective. Do not assume the file will be recoverable from a recycle bin.

### Remove an empty directory

```bash
rmdir EmptyFolder
```

### Remove a directory and its contents

```bash
rm -r LinuxPractice
```

**Warning:** Recursive deletion can remove many files. Check the directory path carefully before executing this command, especially when using root privileges.

---

## 19. Viewing File Contents

### `cat`

Display a file:

```bash
cat learning-commands.txt
```

Display two files consecutively:

```bash
cat learning-commands.txt another-new-file.txt
```

`cat` is useful for short files, but large files may be easier to read with a pager.

### `more`

```bash
more /etc/hosts
```

`more` displays text page by page.

### `less`

```bash
less /etc/hosts
```

`less` allows forward and backward navigation through a file.

### `head`

Display the first ten lines:

```bash
head learning-commands.txt
```

Specify a different number:

```bash
head -n 5 learning-commands.txt
```

### `tail`

Display the last ten lines:

```bash
tail learning-commands.txt
```

Display the last five lines:

```bash
tail -n 5 learning-commands.txt
```

Follow a growing log file:

```bash
tail -f /var/log/syslog
```

The file and permissions must be appropriate for the command to work.

---

## 20. Searching with `find`

The `find` command searches for files and directories using conditions such as names, types, sizes, and modification times.

### Search by exact name

```bash
find /home -name "learning-commands.txt"
```

### Search by file extension

```bash
find /home -type f -name "*.txt"
```

### Search for directories

```bash
find /home -type d -name "LinuxPractice"
```

### Search for recently modified files

```bash
find /home -type f -mtime -1
```

This searches for regular files modified less than approximately one day ago.

### Search the whole file system

```bash
find / -name "learning-commands.txt" 2>/dev/null
```

This starts at `/`. The redirection sends error messages to `/dev/null`, so permission errors and other standard-error messages are suppressed.

Suppressing errors can make the output easier to read, but it can also hide the fact that some locations could not be searched.

**Study note:** `find` is a powerful search tool, but it is not guaranteed to locate a file if the starting directory is wrong, access is denied, or the file is not present.

---

## 21. Searching Text with `grep`

The `grep` command searches text for matching patterns.

### Search for a word

```bash
grep "root" /etc/passwd
```

This displays lines in `/etc/passwd` containing the text `root`.

### Case-insensitive search

```bash
grep -i "root" /etc/passwd
```

### Show line numbers

```bash
grep -n "root" /etc/passwd
```

### Search recursively

```bash
grep -R "root" /etc
```

This searches recursively through accessible files under `/etc`. Some files may produce permission errors or binary-file notices.

### Search command output

```bash
history | grep "sudo"
```

This searches the output of `history` for lines containing `sudo`.

### `find` versus `grep`

| Command | Main purpose |
|---|---|
| `find` | Locates files and directories |
| `grep` | Searches text inside files or supplied input |

---

## 22. Command History

The `history` command displays commands recorded by the current shell.

```bash
history
```

Search the history for a command:

```bash
history | grep "apt"
```

Run a previous command by its history number:

```bash
!25
```

This attempts to execute the command numbered `25` in the shell history.

### Security considerations

Shell history is useful for learning and troubleshooting, but it can also expose sensitive information if secrets are typed directly into commands.

History may be incomplete, disabled, cleared, or configured to retain only a limited number of entries. It should not be treated as a complete audit log.

An attacker with sufficient access may attempt to tamper with local records. Administrators should use suitable centralised logging and monitoring when reliable audit trails are required.

**Best practice:** Avoid entering passwords, access tokens, or other secrets directly into commands that may be recorded in history.

---

## 23. Date, Time and Calendar

### Display the current date and time

```bash
date
```

### Display a calendar

```bash
cal
```

If `cal` is unavailable, the required package may not be installed on your Ubuntu system.

### Display a particular month

```bash
cal 10 2026
```

This requests a calendar for October 2026.

### Check the system time configuration

```bash
timedatectl
```

This displays system time and time-zone information on systems that use `systemd`.

---

## 24. System Information and Processes

My lecture notes include the `proc` topic. On Linux, `/proc` is a virtual file system that exposes information about processes and the kernel.

### Inspect `/proc`

```bash
ls /proc
```

### View CPU information

```bash
cat /proc/cpuinfo
```

### View memory information

```bash
cat /proc/meminfo
```

### View kernel information

```bash
uname -a
```

### View logged-in users

```bash
who
```

This displays information about users currently logged in through sessions recognised by the system.

### Display the current username

```bash
whoami
```

These commands may depend on the availability of the corresponding utility in the environment.

---

## 25. Managing Users and Groups

Linux uses accounts and groups to control access to resources.

### Display your username

```bash
whoami
```

### Display your user and group IDs

```bash
id
```

### Switch to an authorised root shell

```bash
sudo -i
```

### Create a user

On Ubuntu, an administrator can create a user with:

```bash
sudo adduser newuser
```

Follow the prompts to configure the account.

### View account information

```bash
cat /etc/passwd
```

This file contains account information, not users' plaintext passwords.

### View group information

```bash
cat /etc/group
```

### Important security note

Creating users, changing groups, and modifying permissions can affect system security. These operations generally require administrative privileges.

Do not modify system account files manually unless you understand the format and the consequences.

---

## 26. Package Management with APT

APT stands for **Advanced Package Tool**. It is used on Debian-based systems such as Ubuntu to manage software packages.

APT is conceptually similar to a software installer, although it also handles repositories and software dependencies.

### Update package information

```bash
sudo apt update
```

This refreshes the local package information from configured repositories. It does not normally install all available upgrades.

### Upgrade installed packages

```bash
sudo apt upgrade
```

This installs available upgrades for installed packages, subject to APT's normal dependency and package-management rules.

### Install a package

```bash
sudo apt install package-name
```

Replace `package-name` with the actual package name.

For example, if the `cal` command is missing, check which package provides it for your Ubuntu release before installing it.

### Remove a package

```bash
sudo apt remove package-name
```

### List upgradeable packages

```bash
apt list --upgradable
```

### Why does APT display `Get:`?

During operations such as `apt update`, you may see output like:

```text
Get:1 http://archive.ubuntu.com/ubuntu ...
```

`Get:` indicates that APT is retrieving information or data from a configured repository. During `apt update`, this commonly refers to package indexes and repository metadata.

You may also see a message similar to:

```text
237 packages can be upgraded.
```

This means newer versions are available according to the package information APT has retrieved. It does not mean that all those packages have already been upgraded.

**Memory trick:**

- `apt update` = Refresh the information about available software.
- `apt upgrade` = Install available upgrades.

---

## 27. Getting Help in Linux

Linux provides several built-in methods of discovering how commands work.

### `man`

Open the manual for a command:

```bash
man ls
```

Search within a manual page using `/`, followed by a search term.

Press `q` to quit.

### `--help`

Many commands provide a short help summary:

```bash
ls --help
```

### `info`

Some programs provide detailed documentation through `info`:

```bash
info coreutils
```

### Search manual-page descriptions with `man -k`

```bash
man -k password
```

This searches manual-page descriptions for matching keywords.

### Search for games

My lecture notes include:

```bash
man -k -6
```

Manual sections vary by system. Section 6 commonly covers games and screensavers. A keyword is generally useful when searching descriptions, for example:

```bash
man -k game
```

### Search administration commands

My lecture notes include section 8:

```bash
man -k -8
```

Section 8 commonly covers system-administration commands. A search keyword can narrow the results, for example:

```bash
man -k administration
```

### `pinfo` and `man2html`

My lecture notes also mention:

- `pinfo`: an alternative interface for reading Info documentation.
- `man2html`: a tool associated with converting manual pages into HTML.

These tools may not be installed by default. Their availability depends on the distribution and package configuration.

---

## 28. Text Editors

Text editors let users create and modify files from the terminal.

Examples include:

- `nano`
- `vi`
- `vim`
- `emacs`

### Edit a text file with Nano

```bash
nano learning-commands.txt
```

Common Nano shortcuts are displayed at the bottom of the editor.

Typical actions include:

- `Ctrl + O`: Write the file to disk.
- `Enter`: Confirm the filename when prompted.
- `Ctrl + X`: Exit Nano.

### Edit a file with Vim

```bash
vim learning-commands.txt
```

Vim is a modal editor, which means the same key can behave differently depending on the current mode.

---

## 29. The `vi` Editor

My lecture notes introduce creating a file called `Nepal.txt` using `vi`.

```bash
vi Nepal.txt
```

### Basic steps

1. Open the file with `vi Nepal.txt`.
2. Press `i` to enter Insert mode.
3. Type the text you want to add.
4. Press `Esc` to return to Normal mode.
5. Type `:wq` and press `Enter` to save and quit.

### Useful commands

| Command | Action |
|---|---|
| `i` | Enter Insert mode before the cursor |
| `Esc` | Return to Normal mode |
| `:w` | Save the file |
| `:q` | Quit if there are no unsaved changes |
| `:q!` | Quit without saving changes |
| `:wq` | Save and quit |

**Important:** The usual way to enter editor commands is to press `Esc`, type a colon command such as `:wq`, and then press `Enter`.

---

## 30. Important Configuration Files

My lecture notes include a reference to `More /etc/logins/defs`.

The exact path and command are unclear from the supplied notes, so this reference should be checked against the original lecture material before using it.

On Ubuntu, commonly encountered account-related files include:

| File | Purpose |
|---|---|
| `/etc/passwd` | User account information |
| `/etc/shadow` | Protected password-hash and password-aging information |
| `/etc/group` | Group information |
| `/etc/sudoers` | Configuration controlling `sudo` permissions |

To read files, use suitable commands and permissions. For example:

```bash
cat /etc/passwd
```

The `/etc/shadow` file contains sensitive authentication information and is normally restricted to privileged access.

Do not edit sensitive configuration files casually. Incorrect changes may prevent users from logging in or may weaken system security.

---

## 31. Linux Shell and Windows Command Prompt

My lecture notes refer to the Windows shell as DOS.

More precisely, Windows includes several command-line environments, including Command Prompt (`cmd.exe`) and PowerShell. DOS is a historical operating system and is not the name for every modern Windows shell.

Linux commonly uses shells such as Bash.

| Task | Linux example | Windows Command Prompt example |
|---|---|---|
| List files | `ls` | `dir` |
| Change directory | `cd` | `cd` |
| Display current directory | `pwd` | `cd` |
| Clear screen | `clear` | `cls` |
| Display text | `echo` | `echo` |
| Copy files | `cp` | `copy` |
| Move files | `mv` | `move` |
| Remove a file | `rm` | `del` |

The commands are not interchangeable in every situation. Linux and Windows also differ in path syntax, permissions, file systems, and command options.

---

## 32. Basic Security Notes

Linux administration requires care because some commands can make system-wide changes.

### Use privileges carefully

Use `sudo` only when required. Avoid remaining in a root shell longer than necessary.

### Check paths before deleting files

Before running a destructive command, verify the current directory and the target:

```bash
pwd
ls
```

Be particularly careful with commands that use `rm -r` or elevated privileges.

### Protect command history

History can be useful for troubleshooting, but it may expose commands containing sensitive information.

Do not treat local shell history as a tamper-proof security log.

### Keep packages updated

Refreshing package information and applying appropriate security updates helps maintain the system:

```bash
sudo apt update
sudo apt upgrade
```

On managed or production systems, follow the organisation's change-management and maintenance procedures.

### Understand permissions

Do not assume that being able to see a file means you are allowed to modify it. Linux permissions and ownership determine what users can do with many files and directories.

---

## 33. Practical Command Reference

| Task | Command |
|---|---|
| Show current directory | `pwd` |
| List files | `ls` |
| List hidden files | `ls -a` |
| Detailed listing | `ls -l` |
| Change directory | `cd directory-name` |
| Go home | `cd ~` |
| Go up one level | `cd ..` |
| Create directory | `mkdir directory-name` |
| Create an empty file | `touch file.txt` |
| Display file contents | `cat file.txt` |
| Copy a file | `cp source.txt destination.txt` |
| Move or rename a file | `mv old.txt new.txt` |
| Remove a file | `rm file.txt` |
| Search for a file | `find /home -name "file.txt"` |
| Search file contents | `grep "word" file.txt` |
| Display command history | `history` |
| Show current user | `whoami` |
| Show user and group IDs | `id` |
| Display date and time | `date` |
| Display calendar | `cal` |
| Show kernel/system information | `uname -a` |
| Get command help | `command --help` |
| Open a manual page | `man command` |
| Refresh package information | `sudo apt update` |
| Upgrade packages | `sudo apt upgrade` |
| Open a root shell | `sudo -i` |
| Clear terminal display | `clear` |

---

## 34. Historical Claims to Verify

Some historical details in the original lecture notes need further confirmation.

Before using these details in an assignment or examination, check the lecture slides or a reliable historical source:

- The exact list of people credited with early UNIX development.
- The description of an unnamed program developed in 1969.
- The claim that Brian Kernighan evaluated that program for client and networking purposes.
- The claim that Red Hat created the world's first Linux distribution in 1994.
- The precise relationship between the early Linux kernel releases and the first distributions.
- The exact file path written as `/etc/logins/defs`.

These points have been flagged because the supplied notes do not provide enough evidence to establish them precisely. The rest of this README organises the supplied learning topics and provides practical command examples.

---

## 35. Learning Checklist

Use this checklist to track your progress through Linux fundamentals.

- [ ] Explain the difference between the Linux kernel and a Linux distribution.
- [ ] Describe the historical relationship between UNIX and Linux.
- [ ] Explain the role of GNU utilities.
- [ ] Understand the purpose of the kernel.
- [ ] Identify important directories in the Linux file system.
- [ ] Use `pwd`, `ls`, and `cd`.
- [ ] Create files with `touch` and `echo`.
- [ ] Copy, move, rename, and remove files.
- [ ] Display file contents with `cat`, `more`, or `less`.
- [ ] Search for files with `find`.
- [ ] Search text with `grep`.
- [ ] Use `history` and understand its limitations.
- [ ] Check the date, time, and system information.
- [ ] Explain the difference between normal and root users.
- [ ] Use `sudo` appropriately.
- [ ] Install and update software with APT.
- [ ] Find command documentation using `man` and `--help`.
- [ ] Create and edit files using Nano or `vi`.
- [ ] Explain why file paths and permissions matter.
- [ ] Recognise common Linux security risks.

---

**End of Linux study notes**

*Keep practising the commands in your Ubuntu virtual machine. Always check your current directory and understand a command before running it with administrative privileges.*
````
