# Access Control Compliance Audit — BrainMeld Environment

## Overview

This audit assessed BrainMeld's access control posture against Grey Matter's 10-control access control policy framework. Each finding from the BrainMeld environment was evaluated for compliance and, where non-compliant, mapped to the specific violated control(s) with documented risk rationale.

**Result: 14 of 15 findings non-compliant.**

---

## Grey Matter Access Control Policy — Reference Framework

| Control | Title | Requirement |
|---|---|---|
| AC-1 | Change Default Passwords | All default passwords must be changed before deployment |
| AC-2 | Use Unique Accounts | Shared accounts are not permitted; all accounts must be unique to an individual |
| AC-3 | MFA for Remote Access to Sensitive Data | MFA and encrypted channels required for all remote access to sensitive systems |
| AC-4 | Dedicated Administrative Accounts | Elevated activities must use a dedicated secondary account, not a regular user account |
| AC-5 | Dedicated Workstations for Administrative Tasks | Admin tasks must be performed on a dedicated machine segmented from the primary network |
| AC-6 | MFA for All Administrative Access | MFA required for all administrative account access |
| AC-7 | Log and Alert on Admin Group Membership Changes | Systems must log and alert when accounts are added to or removed from admin groups |
| AC-8 | Log and Alert on Failed Admin Logins | Systems must log and alert on unsuccessful administrative login attempts |
| AC-9 | Role-Based Access Control | Access to information must be restricted based on job role and least privilege principle |
| AC-10 | Centralized Directory Services | Access controls must be enforced through a centralized directory (e.g., Active Directory) |

---

## Audit Findings

### Employee Access

**Finding 1:** Employees authenticate to laptops/workstations with Active Directory credentials and have local administrator rights.

| Compliant | No |
|---|---|
| **Violated Controls** | AC-4, AC-9 |
| **Risk** | Regular employees should not hold local admin rights. Admin privileges granted by default increase the risk of malware installation, accidental misconfiguration, and unauthorized system changes. This violates least privilege — users have access beyond what their job function requires. |

---

**Finding 2:** Employees use personal devices (BYOD) to access email, collaboration tools, and web applications. No MFA requirement is documented for these devices.

| Compliant | No |
|---|---|
| **Violated Controls** | AC-3, AC-9 |
| **Risk** | Personal devices accessing corporate resources without MFA creates an uncontrolled remote access vector. Without RBAC enforcement on BYOD, sensitive data is accessible from devices that may not meet corporate security baselines. A compromised personal device becomes a direct path into corporate systems. |

---

### Legacy BrainMeld VPN Service

**Finding 3:** VPN authentication uses username and password only — no MFA.

| Compliant | No |
|---|---|
| **Violated Controls** | AC-3, AC-10 |
| **Risk** | Username/password-only VPN authentication is vulnerable to credential theft, phishing, and brute force attacks. Without MFA, a single compromised credential provides full VPN access. VPN accounts are also not managed through centralized directory services, making enforcement inconsistent. |

---

**Finding 4:** VPN accounts are created manually by the local IT team, separate from the centralized directory.

| Compliant | No |
|---|---|
| **Violated Controls** | AC-2, AC-10 |
| **Risk** | Manual account creation outside of centralized systems increases the risk of duplicate, shared, or orphaned accounts. Without directory integration, access control policies cannot be enforced consistently, and departed users may retain VPN access after offboarding. |

---

**Finding 5:** All authenticated VPN users receive the same level of network access regardless of role.

| Compliant | No |
|---|---|
| **Violated Controls** | AC-9 |
| **Risk** | Flat network access for all VPN users violates least privilege. A graphic designer and a database administrator should not have identical network access. Over-permissive access increases lateral movement risk if any account is compromised. |

---

**Finding 6:** Employees use the legacy VPN to access internal services remotely — no MFA documented.

| Compliant | No |
|---|---|
| **Violated Controls** | AC-3 |
| **Risk** | Remote access to internal services using credentials alone is insufficient. Credential compromise through phishing or password reuse would provide an attacker direct access to internal systems with no additional authentication barrier. |

---

**Finding 7:** Administrators use the legacy VPN for after-hours remote access to internal systems — no MFA.

| Compliant | No |
|---|---|
| **Violated Controls** | AC-3, AC-6 |
| **Risk** | Administrative remote access without MFA represents an elevated risk. Admin accounts have privileged access to critical systems. A compromised admin credential accessed via VPN with no MFA could result in full environment compromise during off-hours when detection is less likely. |

---

**Finding 8:** Multiple third-party vendors (HVAC, security camera monitoring, database consultant, graphic designer) access internal systems through the legacy VPN with no documented access restrictions.

| Compliant | No |
|---|---|
| **Violated Controls** | AC-3, AC-9, AC-10 |
| **Risk** | Third-party vendors with unrestricted VPN access represent a significant supply chain risk. All vendors receive the same access level regardless of business need — an HVAC monitoring vendor has no legitimate need for the same network access as an internal database consultant. This violates least privilege and third-party access management principles. |

---

### System Administrator Access

**Finding 9:** All four system administrators use their regular Active Directory accounts, which are members of the Domain Administrators group.

| Compliant | No |
|---|---|
| **Violated Controls** | AC-4, AC-6, AC-7 |
| **Risk** | Administrators should use dedicated secondary accounts for privileged tasks. Using regular accounts for domain-level administration makes it impossible to distinguish between standard user activity and administrative actions in audit logs, and increases the risk of privilege misuse during routine work. |

---

**Finding 10:** Departmental directors (Sales, Marketing, Engineering, Accounting) are members of the Domain Administrators group.

| Compliant | No |
|---|---|
| **Violated Controls** | AC-4, AC-9 |
| **Risk** | Domain Administrator access for non-technical directors violates least privilege. Directors have no operational need for domain-level privileges. Unnecessary admin access increases the attack surface — a compromised director account becomes a domain admin compromise. |

---

**Finding 11:** System administrators use company-issued laptops for both regular business tasks and administrative functions.

| Compliant | No |
|---|---|
| **Violated Controls** | AC-5, AC-4 |
| **Risk** | Using the same device for email, web browsing, and administrative tasks exposes admin sessions to malware and credential theft introduced through normal business activity. Admin workstations should be dedicated, hardened, and network-segmented from the general environment. |

---

**Finding 12:** All system administrators share a common local administrator account with a consistent password across all workstations and laptops.

| Compliant | No |
|---|---|
| **Violated Controls** | AC-1, AC-2 |
| **Risk** | A shared admin account with a static password across all devices eliminates individual accountability. Actions cannot be traced to a specific administrator. If the password is compromised, every device in the environment is immediately at risk. This also violates the requirement to change default/shared passwords. |

---

### Web Application Access

**Finding 13:** No single sign-on (SSO) service exists for internal web applications.

| Compliant | No |
|---|---|
| **Violated Controls** | AC-10 |
| **Risk** | Without SSO, applications manage authentication independently. This makes it impossible to enforce consistent access control policies, increases the risk of orphaned accounts across applications, and makes offboarding incomplete — a departed user may retain access to applications not connected to the central directory. |

---

**Finding 14:** Some web applications use Active Directory authentication (username/password only); others use application-specific accounts.

| Compliant | No |
|---|---|
| **Violated Controls** | AC-3, AC-10 |
| **Risk** | Inconsistent authentication across applications creates security gaps. Applications outside centralized directory control cannot have access policies enforced uniformly. Password-only authentication without MFA leaves these applications vulnerable to credential-based attacks. |

---

**Finding 15 (Compliant):** The financial management web application requires Active Directory authentication plus a one-time password from a phone-based application.

| Compliant | Yes |
|---|---|
| **Notes** | This application correctly implements MFA for sensitive data access, meeting AC-3 requirements. This should be used as the model for all internal applications handling sensitive data. |

---

### File Services Access

**Finding 16:** Cloud file management service defaults to all-user access; individual file owners are responsible for restricting permissions manually.

| Compliant | No |
|---|---|
| **Violated Controls** | AC-9 |
| **Risk** | Defaulting to open access with manual owner-managed restrictions is not a scalable or reliable RBAC model. Most users will not proactively restrict file permissions, resulting in broad unintended data exposure. Access should default to restricted and be explicitly granted based on role, not the reverse. |

---

## Audit Summary

| Area | Total Findings | Non-Compliant | Compliant |
|---|---|---|---|
| Employee Access | 2 | 2 | 0 |
| VPN Service | 5 | 5 | 0 |
| System Administrator Access | 4 | 4 | 0 |
| Web Application Access | 3 | 2 | 1 |
| File Services | 1 | 1 | 0 |
| **Total** | **15** | **14** | **1** |

**Most violated controls:**
- AC-3 (MFA for remote access) — violated in 6 findings
- AC-9 (RBAC / least privilege) — violated in 7 findings
- AC-10 (centralized directory services) — violated in 5 findings

**Pattern:** The environment relies heavily on a legacy VPN that predates modern access control standards, has no MFA enforcement anywhere except the financial application, and has no RBAC model — all users receive equivalent access regardless of role. This represents systemic access control risk, not isolated configuration gaps.
