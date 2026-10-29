# Linux Security Assessment — Management Report

**System:** Ubuntu 22.04 LTS Virtual Machine  
**Tools:** Nmap 7.99, Lynis 3.0.7, UFW  
**Assessment type:** Lab-based vulnerability assessment and security hardening

## Executive Summary

A security assessment was conducted on an Ubuntu virtual machine to identify potential security weaknesses and opportunities for improving its security configuration.

The assessment included network port scanning, operating system security auditing, package update investigation and firewall hardening.

## Key Findings

1. **Firewall configuration:** The Ubuntu firewall (UFW) was initially inactive. This could increase network exposure if additional services became accessible.

2. **CUPS software:** Outdated CUPS-related packages were identified. Subsequent checks confirmed updated versions, although the update mechanism was not established.

3. **Outstanding package updates:** Lynis continued to report a package-related warning requiring further investigation.

## Remediation and Verification

UFW was enabled with default-deny incoming and default-allow outgoing policies.

Network verification using Nmap showed that all 1,000 tested TCP ports changed from closed to filtered.

A repeat Lynis audit showed:

- Hardening Index increased from 59 to 60.
- Warnings decreased from 2 to 1.
- Firewall warning FIRE-4512 was cleared.

These results provide evidence that the firewall configuration improved. They do not establish that all vulnerabilities have been resolved. The assessment was limited to a controlled virtual environment and the 1,000 TCP ports tested; it did not establish that all network services or potential vulnerabilities had been assessed.

## Recommendations

- Investigate and prioritise outstanding security updates.
- Review whether printing services are necessary.
- Periodically reassess firewall rules and network exposure.
- Repeat security assessments following significant configuration changes.

## Conclusion

The assessment demonstrated a verified improvement in host firewall configuration while identifying further hardening opportunities.

Outstanding package-related findings require additional investigation before the system can be considered fully assessed.
