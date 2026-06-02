---
title: "Security+ Series: Security Operations and Incident Response"
date: 2026-06-01
categories: ["Cybersecurity", "Security+"]
tags: ["SOC", "SIEM", "Incident Response"]
draft: false
---

## The SOC Toolkit: SIEM & SOAR

Security Operations Centers (SOC) rely on automation to handle massive amounts of data:
* **SIEM (Security Information and Event Management):** Aggregates logs from all devices across the network and correlates events to detect anomalies (e.g., an "Impossible Travel" alert).
* **SOAR (Security Orchestration, Automation, and Response):** Works alongside the SIEM to automatically execute remediation playbooks without human intervention (e.g., automatically isolating a compromised host).

## The NIST Incident Response Lifecycle

When a breach occurs, teams follow a strict 6-step framework:
1. **Preparation:** Writing policies, training staff, and deploying tools before an attack happens.
2. **Identification:** Analyzing alerts to confirm if an event is a true security incident or a false positive.
3. **Containment:** Stopping the spread immediately. *Crucial rule: Disconnect the network cable or block the switch port, but DO NOT power off the machine, as this destroys volatile RAM evidence.*
4. **Eradication:** Removing the malware, patching vulnerabilities, and eliminating the root cause.
5. **Recovery:** Restoring data from clean backups and carefully returning systems to production.
6. **Lessons Learned:** The most important phase. The team conducts a post-mortem to document what failed and how to improve defenses for the future.