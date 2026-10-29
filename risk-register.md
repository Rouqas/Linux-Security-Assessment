# Security Risk Register

System: Ubuntu 22.04 LTS VirtualBox VM
Assessment: Linux Vulnerability Assessment
Risk ratings: Provisional, based on this lab environment

## R-01: Inactive Host Firewall

Finding:
UFW was inactive. Lynis reported FIRE-4512.

Potential risk:
Unnecessary network exposure if services become
accessible without host-level filtering.

Priority: Low in the current lab environment; potential risk increases if network services become exposed.

Remediation:
Enabled UFW with default deny incoming and
allow outgoing policies.

Verification:
Nmap changed from 1000 closed TCP ports to
1000 filtered TCP ports.
Lynis FIRE-4512 warning cleared.

Status: Remediated and verified.

## R-02: Outdated CUPS Packages

Finding:
Older CUPS-related package versions were observed
during the initial assessment.

Potential risk:
Outdated printing components may lack security fixes.

Priority: Medium (provisional; exposure not confirmed)

Verification:
cups-filters upgrade recorded on 22 October 2026.
Version 1.28.15-0ubuntu1.5 installed.
Both cups.service and cups-browsed.service remained active.
No UDP port 631 listener detected in follow-up testing.

Status:
Updated. Update mechanism not established.
No manual remediation claimed.

## R-03: Outstanding Package Updates

Finding:
Lynis warning PKGS-7392 remained after reassessment.

Potential risk:
Some installed packages may lack applicable
security fixes.

Priority: Not yet determined.

Recommended action:
Identify outstanding security updates and prioritise
patching according to severity and exposure.

Status: Open — further investigation required.
