# Enterprise Security Assessment — Acquisition Integration Case Study

A full-cycle security assessment simulating the acquisition of a competitor company. The acquiring organization (Grey Matter) needed to evaluate the security posture of the acquired company (BrainMeld) before integrating its systems and users into the enterprise environment.

This case study covers the complete assessment lifecycle: vulnerability scanning and analysis, access control compliance auditing, executive risk communication, and remediation planning.

---

## Scenario

Grey Matter acquires BrainMeld. As part of the integration team, I was tasked with:

1. Analyzing vulnerability scan results from BrainMeld's network environment
2. Auditing BrainMeld's access control posture against Grey Matter's security policy
3. Producing an executive-level risk briefing for the board of directors
4. Recommending a prioritized remediation roadmap

---

## Repository Structure

```
├── README.md                          # This file
├── vulnerability-assessment.md        # Scan findings, CVSS analysis, remediation timeline
├── access-control-audit.md            # Compliance audit — 15 findings mapped to 10 controls
├── executive-summary.md               # Board-level risk communication
├── policy-recommendations.md          # Policy gaps and recommended updates
```

---

## Key Findings Summary

**Vulnerability Assessment**
- 13 vulnerabilities identified across critical, high, and medium severity
- Critical findings: SMB NTLM RCE (CVSS 10), HTTP.sys RCE (CVSS 10), SQL Server End-of-Life (CVSS 10)
- Policy-level findings: 5 instances of default credentials via SMB brute force, cleartext HTTP transmission, weak SSL/TLS cipher suites
- Remediation categorized into 1-week, 1-month, and 2-month timelines based on severity and operational impact

**Access Control Audit**
- 14 of 15 findings non-compliant with Grey Matter access control policy
- Critical gaps: shared admin accounts, missing MFA on VPN and remote access, all users provisioned at same network access level, no RBAC enforcement on file services
- Every finding mapped to specific violated control (AC-1 through AC-10) with documented risk rationale

---

## Tools & Frameworks Referenced

- **OpenVAS / Nessus** — vulnerability scanning
- **CVSS v3** — severity scoring and prioritization
- **CIS Controls / NIST principles** — access control framework alignment
- **RBAC, MFA, least privilege, network segmentation** — core control recommendations

---

## Skills Demonstrated

- Vulnerability assessment and CVSS-based risk prioritization
- Security controls assessment against organizational policy
- Access control gap analysis with control mapping
- Executive risk communication — translating technical findings to business impact
- Remediation planning with prioritized timelines

---

*Part of my public security portfolio. All analysis and findings are my own work product from a simulated enterprise scenario.*

*GitHub: [DanielSantiagoSec](https://github.com/DanielSantiagoSec) | Portfolio: [danielsantiagosec.github.io](https://danielsantiagosec.github.io)*
