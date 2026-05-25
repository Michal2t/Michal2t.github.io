---
title: "Security+ Series: OSI Model, Secure Protocols & Cloud Architecture"
date: 2026-05-24
categories: ["Cybersecurity", "Security+"]
tags: ["OSI Model", "Networking", "Cloud"]
draft: false
---

## The OSI Model for Security Analysts

To defend a network, you must understand how data travels through it.
* **Layer 2 (Data Link):** Operates using MAC addresses and Switches. Defended by MAC filtering and Port Security.
* **Layer 3 (Network):** Operates using IP addresses and Routers. Defended by IPsec and standard packet-filtering firewalls.
* **Layer 4 (Transport):** Manages TCP/UDP ports. Stateful firewalls operate here to block unauthorized port traffic.
* **Layer 7 (Application):** The software layer (HTTP, DNS). Defended by Web Application Firewalls (WAF) against attacks like SQL Injection.

## Secure Protocol Replacements

A key security principle is disabling plaintext protocols and replacing them with encrypted alternatives:
* Replace **Telnet (Port 23)** with **SSH (Port 22)** for secure remote CLI management.
* Replace **HTTP (Port 80)** with **HTTPS (Port 443)** for secure web browsing.
* Replace **FTP (Port 21)** with **SFTP (Port 22)** or **FTPS (Port 990)** for secure file transfers.
* Enhance **DNS (Port 53)** with **DNSSEC** to add digital signatures, preventing DNS poisoning (protecting Integrity).

## Cloud Computing and Shared Responsibility

Modern infrastructure relies heavily on the cloud. Understanding who is responsible for what is critical:
* **IaaS (Infrastructure as a Service):** You rent bare-metal virtual servers. *You* are responsible for patching the OS and managing the database.
* **PaaS (Platform as a Service):** You rent an environment to run your code. The provider manages the OS and hardware.
* **SaaS (Software as a Service):** A fully managed application (e.g., Google Workspace). The provider handles everything; you only manage user access and data.