+++
title = "Escaping the User Space: Sudo, Root, and the Shadow File"
date = "2026-05-13"
draft = false
tags = ["Linux", "Privilege Escalation", "Cryptography", "Lab Diary"]
+++

Following up on my previous exploration of the Linux FHS, I decided to tackle the exact boundary that stopped me: the `/root` directory and the concept of system permissions. 

Linux is fundamentally a multi-user operating system. It strictly separates standard users (like my `kali` account) from the superuser (`root`). To see this in action, I attempted to read one of the most highly guarded files in a Linux system: `/etc/shadow`. 

Running `cat /etc/shadow` immediately resulted in a `Permission denied` error. 

### Enter `sudo`

To bypass this without fully logging out, Linux uses the `sudo` (SuperUser DO) command. It allows a permitted user to execute a command as the superuser. 

By running `sudo cat /etc/shadow`, and authenticating with my own password, I was able to view the file. This file is a goldmine for attackers because it contains the system's passwords. However, the passwords are not stored in plaintext. They are mathematically hashed (and salted!). The system never stores the real password, only the hash, making it a perfect example of a one-way cryptographic function in action.

### Becoming the Superuser

Sometimes, appending `sudo` to every command becomes tedious during administrative tasks. I learned that you can switch your shell environment entirely to the root user by executing:

    sudo su -

Immediately, my prompt changed from `$` to `#`, and running the `whoami` command returned `root`. I had complete, unrestricted access to the machine. 

Understanding how to control these privileges is the foundation of Blue Team defense, while finding misconfigurations in this exact mechanism is a classic Red Team tactic for Privilege Escalation.

*With absolute power comes absolute responsibility... or a really broken kernel.*