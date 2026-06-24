# AC-2 – Account Management

**Family:** Access Control (AC)  
**Baseline:** Moderate  
**Control Description:** The organization manages information system accounts, including establishing, activating, modifying, reviewing, disabling, and removing accounts. Account management includes defining account types, assigning account managers, and enforcing approval processes for account creation and access changes.

---

## Implementation

Account management in this hybrid cloud environment is handled through a combination of Microsoft Entra ID and on-premises Active Directory (AD).

- **Account Creation:** New user accounts are provisioned in Active Directory and synced to Entra ID via Microsoft Entra Connect. Access is assigned based on role using AD security groups mapped to job function.
- **Account Modification:** Access changes require a formal request and manager approval. Changes are applied through Entra ID group membership updates or AD group policy modifications.
- **Account Review:** Periodic access reviews are conducted using Entra ID Access Reviews. Reviewers confirm whether users still require their current access; unnecessary access is revoked.
- **Account Disabling/Removal:** Upon personnel termination, accounts are disabled in AD and Entra ID within 24 hours per offboarding SOP. Accounts are fully removed after a defined retention period.
- **Privileged Accounts:** Privileged accounts are managed separately via CyberArk and Entra ID Privileged Identity Management (PIM). Just-in-time (JIT) access is enforced for administrative roles.

---

## Mapped Tool(s)

| Tool | Configuration / Feature |
|---|---|
| Microsoft Entra ID | Lifecycle Workflows, Access Reviews, Privileged Identity Management (PIM) |
| Active Directory | OU structure, security group-based access assignment, Group Policy |
| CyberArk | Privileged account vaulting, session recording, JIT access |

---

## Evidence Artifacts

The following artifacts would be collected to demonstrate compliance with AC-2 during an audit or assessment:

- Entra ID audit logs showing account creation, modification, and deletion events
- Access review completion reports exported from Entra ID Access Reviews
- Offboarding ticket documentation showing account disable timestamps
- AD group membership reports tied to role-based access assignments
- CyberArk privileged account inventory and session logs
- Account management policy or SOP documentation

---

## Notes

- Entra ID Lifecycle Workflows can automate onboarding and offboarding tasks triggered by HR system events (e.g., Workday, SAP)
- Access reviews should be scheduled at minimum annually for standard users and quarterly for privileged users per NIST guidance
- Guest and external accounts (B2B) are managed separately under IA-8

---

## Status

- [ ] Not Implemented
- [ ] Partially Implemented
- [x] Implemented

---

## References

- [NIST SP 800-53 Rev. 5 – AC-2](https://csrc.nist.gov/Projects/risk-management/sp800-53-controls/release-search#!/control?version=5.1&number=AC-2)
- [Microsoft Entra ID Lifecycle Workflows](https://learn.microsoft.com/en-us/entra/id-governance/lifecycle-workflows-overview)
- [Microsoft Entra ID Access Reviews](https://learn.microsoft.com/en-us/entra/id-governance/access-reviews-overview)
- [CyberArk Privileged Access Management](https://docs.cyberark.com/)
