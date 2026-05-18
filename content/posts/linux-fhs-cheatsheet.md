+++
title = "Linux File Tree Map: A Cheat Sheet for the FHS"
date = "2026-05-08"
draft = false
tags = ["Linux", "FHS", "Cheat Sheet", "OS Internals"]
+++

Before diving into deep operating system mechanics, it's crucial to understand the layout of the Linux Filesystem Hierarchy Standard (FHS). Coming from a Windows environment, the lack of `C:\` or `D:\` drives can be confusing. In Linux, everything starts at the root (`/`), and everything is treated as a file.

Here is a quick cheat sheet I compiled to map out the most critical directories for administration and security analysis:

### The Root and Core
* **`/` (Root):** The very top of the filesystem hierarchy. Every single file and directory on the system is nested under this starting point.
* **`/root`:** The personal home directory for the `root` user (the superuser). Regular users cannot enter this directory.
* **`/home`:** Contains the personal directories for all standard users (e.g., `/home/kali`).

### Binaries (Executables)
* **`/bin` (Binaries):** Contains essential command-line utilities used by all users (like `ls`, `pwd`, `cat`).
* **`/sbin` (System Binaries):** Contains administrative executables used primarily by the `root` user for system maintenance (like `fdisk`, `iptables`).

### Configuration and Variable Data
* **`/etc`:** The "brain" of the system. It contains all the global configuration files for the OS and installed services (e.g., `/etc/shadow` for password hashes, `/etc/ssh/` for SSH server configs). *Blue Team note: If a service is misconfigured, this is where you fix it.*
* **`/var` (Variable Data):** Contains files to which the system writes data during the course of its operation. The most important subdirectory here is `/var/log/`, which holds system and service logs.

### Temporary and Device Files
* **`/tmp`:** A directory for temporary files created by the system and users. It is usually cleared upon reboot. It's heavily used by both programs and attackers to drop temporary payloads.
* **`/dev` (Devices):** In Linux, "everything is a file." This folder contains special device files representing hardware components (like hard drives as `/dev/sda`).

Keeping this mental map handy makes navigating the terminal and understanding system logs significantly easier.