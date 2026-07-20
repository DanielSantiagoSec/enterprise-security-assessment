# Policy Recommendations — BrainMeld Integration

Based on the vulnerability assessment and access control audit findings, the following policy updates are recommended for the BrainMeld environment prior to full integration with Grey Matter systems.

---

## 1. Password Policy

**Gap identified:** Five systems running default credentials (admin:guest, root:guest, etc.). Shared local administrator account with static password across all workstations.

**Recommendation:**
- Mandate password changes on all assets before network integration — no default credentials permitted
- Prohibit shared accounts; all accounts must be tied to a named individual
- Enforce password complexity and rotation schedule through Group Policy
- Audit all local administrator accounts and remove or rotate immediately

**Controls addressed:** AC-1, AC-2

---

## 2. Multi-Factor Authentication Policy

**Gap identified:** MFA not enforced on VPN, remote employee access, remote administrator access, or most web applications. Only the financial management application meets the MFA requirement.

**Recommendation:**
- Require MFA for all remote access to internal systems — VPN, web applications, and administrative access without exception
- Extend MFA to all administrative account access whether remote or on-premise
- Use the financial management application's MFA model as the baseline standard
- Evaluate modern VPN replacement or zero trust network access (ZTNA) solution to replace legacy VPN

**Controls addressed:** AC-3, AC-6

---

## 3. Privileged Access Policy

**Gap identified:** Administrators use regular accounts for domain-level tasks. Departmental directors hold Domain Administrator privileges. Administrators use shared devices for both business and admin tasks.

**Recommendation:**
- Require dedicated administrative accounts for all privileged operations — separate from regular user accounts
- Remove Domain Administrator membership from departmental directors immediately; assign role-appropriate permissions only
- Provision dedicated, hardened admin workstations segmented from the general network for all administrative tasks
- Log and alert on all changes to privileged group membership

**Controls addressed:** AC-4, AC-5, AC-7

---

## 4. Access Control and RBAC Policy

**Gap identified:** All VPN users receive identical network access. File services default to open access. BYOD devices access corporate resources without access controls. Third-party vendors have unrestricted VPN access.

**Recommendation:**
- Implement network segmentation for VPN — provision access based on role, not blanket authentication
- Apply RBAC to file services — default to restricted access, grant explicitly based on business need
- Define and enforce a BYOD policy requiring device registration, MFA, and mobile device management (MDM) enrollment before accessing corporate resources
- Implement a third-party access policy — vendors receive only the specific access required for their engagement, time-limited, and reviewed on contract renewal

**Controls addressed:** AC-9

---

## 5. Centralized Identity Management Policy

**Gap identified:** VPN accounts managed outside Active Directory. Multiple web applications use application-specific accounts. No SSO for internal applications.

**Recommendation:**
- Migrate all VPN account management into Active Directory — no standalone account stores
- Implement SSO for all internal web applications — centralize authentication through the directory
- Establish a formal offboarding checklist that includes all systems, not just AD — verify access revocation across VPN, web applications, file services, and third-party integrations
- Conduct quarterly access reviews to identify orphaned or over-privileged accounts

**Controls addressed:** AC-10

---

## 6. Patch Management Policy

**Gap identified:** Multiple critical vulnerabilities with available vendor patches unaddressed. SQL Server running end-of-life software with no patch support.

**Recommendation:**
- Establish a patch management cadence: critical patches within 7 days of release, high within 30 days, medium within 90 days
- Immediately isolate end-of-life SQL Server from network access and begin upgrade planning
- Implement vulnerability scanning on a recurring schedule — not as a one-time assessment
- Track patch compliance metrics and report to leadership quarterly

---

## 7. Incident Response Policy

**Gap identified:** No documented incident response procedures identified during assessment.

**Recommendation:**
- Define an incident response plan covering detection, containment, eradication, recovery, and post-incident review
- Establish escalation paths and communication templates for different incident severity levels
- Conduct a tabletop exercise to validate the plan before integration is complete
- Define what constitutes a reportable incident and the notification timeline for regulatory obligations

---

## Implementation Priority

| Priority | Policy Area | Driver |
|---|---|---|
| Immediate | Password Policy | Default credentials are actively exploitable today |
| Immediate | Patch Management | CVSS 10.0 vulnerabilities with available patches |
| Week 1-2 | MFA Rollout | No MFA on VPN or admin access is unacceptable for integration |
| Month 1 | Privileged Access | Admin account separation and workstation controls |
| Month 1-2 | RBAC and Access Control | Least privilege across VPN, file services, BYOD, vendors |
| Month 2 | Centralized Identity | SSO, directory integration, offboarding process |
| Ongoing | Incident Response | Plan, test, maintain |
