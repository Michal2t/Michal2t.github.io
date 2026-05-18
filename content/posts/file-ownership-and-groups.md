+++
title = "Who Owns the Code? Mastering chmod, chown, and Linux Groups"
date = "2026-05-15"
draft = false
tags = ["Linux", "Permissions", "Access Control", "Lab Diary"]
+++

After learning how to gain root privileges using `sudo`, my next logical step was to understand how the Linux operating system handles file access control on a granular level. Every file and directory in Linux has an Owner (User) and a Group associated with it.

To test this, I created a file named `secret_file.txt` containing a dummy secret.

### Inspecting Initial Permissions

When checking the file with `ls -l`, I noticed its permissions were set to `-rw-rw-r--`. Breaking this down:
* The first `rw-` belongs to the **Owner** (my `kali` user).
* The second `rw-` belongs to the **Group**. 
* The final `r--` belongs to **Others** (anyone else on the system).

This means that by default on my system configuration (determined by a mechanism called `umask`), anyone in my group could read and modify this file, while the rest of the world could only read it. 

### Creating a Target and Modifying Access

To simulate a real multi-user scenario, I created a secondary user named `bob` using `sudo adduser bob`. 

I wanted to completely lock Bob out of my file. To do this, I stripped away the read permission from "Others" using the `chmod` (Change Mode) command:

```bash
chmod o-r secret_file.txt
```

After running `ls -l` again, the permissions changed to `-rw-rw----`. Bob was successfully blind to my secret.

### Tricking the System: Changing Ownership

The ultimate test of control is transferring ownership. I used the `chown` (Change Owner) command to give full control of my file to Bob. The syntax used was:

```bash
sudo chown bob:bob secret_file.txt
```

This command acts like a bridge: it changes the owner to user `bob` and the group to group `bob`. 

During this experiment, I discovered an important Linux architecture design: **User Private Groups (UPG)**. When I created the user `bob` earlier, the system automatically created a corresponding group named `bob`. 

### The Ultimate Lockout

Once the ownership was transferred, I attempted to read my own file again using `cat secret_file.txt`. 

The result? A strict, clean **`Permission denied`**. 

Even though I was the one who originally created the file, the operating system strictly enforced the new ownership rules. Because my current user (`kali`) was no longer the owner, nor a member of Bob's private group, the kernel blocked my access request.

*In Linux, ownership is absolute—until root decides otherwise.*