# Linux Vulnerability Assessment and Security Hardening

## Project Overview

This project demonstrates a security assessment of an Ubuntu 22.04 LTS virtual machine using Nmap, Lynis and manual configuration checks.

The objective was to identify potential security weaknesses, assess their risks, implement justified hardening measures and verify the results.

The assessment was performed in a controlled VirtualBox lab environment.

## Lab Environment

| Component | Configuration |
|---|---|
| Host | Windows 11 Home |
| Target | Ubuntu 22.04 LTS |
| Virtualisation | Oracle VirtualBox |
| Network | NAT and Host-only adapters |
| Assessment tools | Nmap 7.99, Lynis 3.0.7 |
| Firewall | UFW |

## Assessment Methodology

### 1. Network Assessment

Performed a TCP connect scan from Windows against the Ubuntu VM using:

`nmap -sT --reason 192.168.26.101`

The initial scan found all 1,000 tested TCP ports closed.

Used `ss` within Ubuntu to examine listening sockets and associated processes.

### 2. Security Configuration Audit

Ran a baseline Lynis audit:

`sudo lynis audit system`

Baseline findings:

- Hardening Index: 59
- Warnings: 2
- Suggestions: 42

The assessment identified inactive UFW filtering, outstanding package-related concerns and opportunities for additional hardening.

### 3. Investigation and Risk Assessment

Investigated selected findings involving package updates, firewall configuration and CUPS printing services.

Documented potential security impacts, provisional priorities, remediation actions and outstanding risks in a risk register.

### 4. Security Hardening

Enabled UFW with the following default policies:

- Deny incoming connections
- Allow outgoing connections

CUPS-related package updates were observed during the assessment, but were not claimed as manually performed remediation.

### 5. Verification

Repeated the Nmap scan and Lynis audit after the configuration change.

| Measurement | Before | After |
|---|---|---|
| Nmap TCP port states | 1,000 closed | 1,000 filtered |
| Lynis Hardening Index | 59 | 60 |
| Lynis warnings | 2 | 1 |
| Lynis suggestions | 42 | 43 |
| UFW status | Inactive | Active |

### Nmap Before Firewall Hardening

![Before UFW](screenshots/nmap-before-ufw.png)

### Nmap After Firewall Hardening

![After UFW](screenshots/nmap-after-ufw.png)

The repeated assessment demonstrated the following:

- Lynis warning **FIRE-4512** was no longer reported after enabling UFW.
- Nmap results changed from **1,000 closed TCP ports** to **1,000 filtered TCP ports**, consistent with the firewall dropping incoming connection attempts.
- Warning **PKGS-7392** remained unresolved and requires further investigation.

## Risk Management

Security findings were documented in a risk register, including potential impact, provisional priority, remediation status and recommendations.

See [Risk Register](risk-register.md) for individual findings, statuses and recommendations.

## Limitations

- Nmap tested the 1,000 commonly scanned TCP ports, not every possible port.
- No comprehensive UDP or authenticated vulnerability scan was performed.
- Lynis suggestions do not automatically establish exploitable vulnerabilities.
- The outstanding package warning requires further investigation.
- Results reflect a controlled virtual lab, not a production environment.

## Project Documentation

- [Risk Register](risk-register.md)
- [Management Report](management-report.md)

Selected baseline and verification evidence will be included after reviewing it for sensitive system information.

## Key Learning Outcomes

- Network scanning and service exposure analysis
- Linux security auditing with Lynis
- Firewall configuration and verification
- Package security investigation
- Security risk assessment and documentation
- Evidence-based reporting of findings and remediation
