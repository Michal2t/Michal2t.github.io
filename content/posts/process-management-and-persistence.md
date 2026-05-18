+++
title = "Hunting Processes: Signals, Services, and System Permissions"
date = "2026-05-17"
draft = false
tags = ["Linux", "Process Management", "Forensics", "Blue Team"]
+++

Moving on from file permissions, my lab work shifted to the dynamic side of the OS: Process Management. For a Blue Team analyst, monitoring processes is essential because malware cannot execute without becoming a process.

I used the `top` and `ps aux` commands to get a static and dynamic view of what was running on my system. 

### The `grep` Inception

To practice finding specific processes, I started a dummy background task using `sleep 1000 &`. This command doesn't pause the OS; it simply creates a harmless process that idles for 1000 seconds, perfect for lab targeting.

When I ran `ps aux | grep sleep` to find its Process ID (PID), I noticed two results:
1. `sleep 1000`
2. `grep --color=auto sleep`

This was a great "Aha!" moment. The `grep` command itself was actively running to filter the output. Because the word "sleep" was in its own command line, it caught itself in the filter!

### Termination and Signals (`kill` vs `kill -9`)

Once I found the PID, I terminated the process using the `kill` command. However, there is a distinct difference in how termination works:
* A standard `kill [PID]` sends a **SIGTERM** (Signal Terminate) to the process. It politely asks the program to save its data and shut down safely.
* Malware, or unresponsive programs, often ignore this polite request. In those cases, we use `kill -9 [PID]`, which sends a **SIGKILL**. This is handled directly by the kernel and terminates the process immediately, with no chance of resistance.

### Persistence: Why Services Matter

Standard processes die when the terminal closes or the system reboots. Attackers want "Persistence". They achieve this by hooking into the system's service manager, `systemd` (which always runs as PID 1). 

If a program is registered and enabled via `systemctl enable`, `systemd` is instructed to automatically launch it in the background every time the machine boots, long before any user logs in. This is exactly how legitimate services like SSH operate, and precisely how advanced backdoors survive reboots.

### Deep Dive: Special Permissions

While analyzing system binaries, I also reviewed special file permissions that bypass standard rules:
* **SUID (Set User ID):** Allows a user to execute a file with the permissions of the file's *owner*. (e.g., the `passwd` command runs as root so standard users can update their passwords). Misconfigured SUID binaries are prime targets for privilege escalation.
* **SGID (Set Group ID):** Similar to SUID, but executes with the group's privileges. On directories, it forces new files to inherit the directory's group.
* **Sticky Bit:** Used on shared directories like `/tmp`. It ensures that only the file's owner (or root) can delete or rename the file, protecting it from other users with write access to the directory.