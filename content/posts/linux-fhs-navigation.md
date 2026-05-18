+++
title = "Navigating the Linux FHS: Where did the logs go?"
date = "2026-05-10"
draft = false
tags = ["Linux", "FHS", "Lab Diary", "Terminal"]
+++

Today marks the official start of my Purple Team home lab experiments. I booted up my Kali Linux virtual machine to explore the Linux Filesystem Hierarchy Standard (FHS). 

Coming from a Windows background where everything revolves around the `C:\` drive, getting used to the root directory `/` as the starting point of everything is a paradigm shift. I spent some time exploring core directories using basic commands like `pwd`, `ls -la`, and `cd`.

### The Mystery of the Missing Logs

As someone interested in security (Blue Team/Forensics), I know that log files are critical. Naturally, I navigated to `/var/log` expecting to find the classic `auth.log` (which records authentication attempts) and `syslog`.

To my surprise, **they weren't there**. 

After some research, I discovered that this isn't an error. It's a testament to how Linux distributions evolve. Modern Kali Linux (and many others like Ubuntu) have adopted `systemd`. Instead of writing flat text files for system logs, `systemd` uses a component called `journald`, which stores logs in a binary format inside `/var/log/journal/`.

To read these modern logs, we can no longer just use `cat` or `less` on a text file. Instead, we must use the `journalctl` command. It’s a great lesson in not relying solely on old cheat sheets—the OS ecosystem is constantly shifting.

### The Root Boundary

Finally, I attempted to navigate into the `/root` directory using `cd /root`. As expected, the system threw a strict:
`cd: permission denied: /root`

Even though I installed the system, my current user (`kali`) is just a standard user. The system successfully stopped me from entering the domain of the superuser. Understanding how to legitimately bypass this restriction (and how attackers do it maliciously via Privilege Escalation) will be the focus of my upcoming studies.

*Learning the map is more important than memorizing every tree in the forest.*