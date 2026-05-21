# SOC Detection Lab

## Overview
To familiarize myself with Kali Linux and real attack scenarios 
I built this SOC homelab. It simulates a real enterprise security 
monitoring setup where attacks are launched against a monitored 
machine and detected in real time by a SIEM.

---

## Architecture

| VM | OS | Role |
|----|-----|------|
| VM1 — SOC-SIEM | Ubuntu Server | Wazuh SIEM — collects and analyzes logs |
| VM2 — SOC-Agent | Ubuntu Desktop | Simulated office worker machine |
| VM3 — Attacker | Kali Linux | Simulates the attacker's machine |

---

## Tools Used

**Wazuh** — the SIEM. Collects logs from monitored machines, 
runs detection rules, and displays security events in one place 
via the dashboard.

**VirtualBox** — virtualization software that creates isolated 
sandboxed environments for each VM.

**Kali Linux** — a modified version of Linux built specifically 
for security testing and offensive tool practice.

**Hydra** — a network login cracker used to simulate SSH brute 
force attacks by automating password guessing using a wordlist.

---

## Attacks Simulated

| Attack | Tool | Target | Write-up |
|--------|------|--------|----------|
| SSH Brute Force | Hydra | VM2 Ubuntu Agent | [View Analysis](attacks/ssh-bruteforce/analysis.md) |

---

## Skills Demonstrated

- Deploying and configuring a SIEM in a virtualized environment
- Connecting Wazuh agents across multiple machines
- Simulating real attack scenarios using industry standard tools
- Detecting and analyzing brute force attacks in real time
- Network configuration across multiple VMs
- Log analysis and security event investigation
