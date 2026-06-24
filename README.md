# NIST 800-53 IAM Control Mapping

> A structured mapping of NIST SP 800-53 Revision 5 controls to real-world Identity and Access Management (IAM) tools and technologies, scoped to a **Moderate impact baseline** in a hybrid cloud environment.

![Framework](https://img.shields.io/badge/Framework-NIST%20800--53%20Rev.%205-blue)
![Baseline](https://img.shields.io/badge/Baseline-Moderate-yellow)
![Status](https://img.shields.io/badge/Status-In%20Progress-orange)
![License](https://img.shields.io/badge/License-MIT-green)

---

## Project Overview

This project demonstrates applied GRC (Governance, Risk, and Compliance) skills by mapping NIST 800-53 Rev. 5 security controls directly to IAM implementations across Microsoft Entra ID, AWS IAM, CyberArk, and Microsoft Sentinel. The goal is to bridge the gap between compliance frameworks and the technical controls that satisfy them — the way a security analyst or GRC engineer would in a real enterprise environment.

**Use cases this project simulates:**
- Preparing for a FedRAMP Moderate or FISMA Moderate authorization
- Performing an IAM-focused controls gap assessment
- Building a controls inheritance matrix for a hybrid cloud environment

---

## Scope

| Control Family | Code | Focus Area |
|---|---|---|
| Access Control | AC | Account lifecycle, least privilege, remote access |
| Identification & Authentication | IA | MFA, credential management, identity verification |
| Audit & Accountability | AU | Access event logging, log integrity |
| Personnel Security | PS | Onboarding/offboarding, access provisioning workflows |

**Baseline:** NIST 800-53 Rev. 5 — Moderate Impact  
**Environment:** Hybrid cloud (on-premises Active Directory + Azure + AWS)

---

## Tools & Technologies Referenced

| Tool | Role in IAM |
|---|---|
| **Microsoft Entra ID** (Azure AD) | SSO, MFA, Conditional Access, Privileged Identity Management (PIM) |
| **AWS IAM** | Role-based access control, least privilege policies, service account management |
| **CyberArk** | Privileged Access Management (PAM), session recording, credential vaulting |
| **Microsoft Sentinel** | SIEM, access event monitoring, audit log aggregation |
| **Active Directory** | On-premises identity source, group policy enforcement |

---

## Controls Mapped

<details>
<summary><strong>Access Control (AC)</strong></summary>

| Control | Name | Mapped Tool(s) |
|---|---|---|
| AC-2 | Account Management | Entra ID, Active Directory |
| AC-3 | Access Enforcement | AWS IAM, Entra ID Conditional Access |
| AC-6 | Least Privilege | AWS IAM Policies, Entra ID PIM |
| AC-17 | Remote Access | Entra ID Conditional Access, MFA |

</details>

<details>
<summary><strong>Identification & Authentication (IA)</strong></summary>

| Control | Name | Mapped Tool(s) |
|---|---|---|
| IA-2 | Identification and Authentication (Org Users) | Entra ID MFA, FIDO2 |
| IA-5 | Authenticator Management | Entra ID, CyberArk |
| IA-8 | Identification and Authentication (Non-Org Users) | Entra ID B2B, Guest Access Policies |

</details>

<details>
<summary><strong>Audit & Accountability (AU)</strong></summary>

| Control | Name | Mapped Tool(s) |
|---|---|---|
| AU-2 | Event Logging | Microsoft Sentinel, AWS CloudTrail |
| AU-9 | Protection of Audit Information | Sentinel Log Analytics, AWS S3 with MFA Delete |

</details>

<details>
<summary><strong>Personnel Security (PS)</strong></summary>

| Control | Name | Mapped Tool(s) |
|---|---|---|
| PS-4 | Personnel Termination | Entra ID automated offboarding, AD account deprovisioning |
| PS-5 | Personnel Transfer | Entra ID role reassignment, access review workflows |

</details>

---

## Repository Structure

```
├── /controls/
│   ├── AC/
│   │   ├── AC-2.md
│   │   ├── AC-3.md
│   │   ├── AC-6.md
│   │   └── AC-17.md
│   ├── IA/
│   │   ├── IA-2.md
│   │   ├── IA-5.md
│   │   └── IA-8.md
│   ├── AU/
│   │   ├── AU-2.md
│   │   └── AU-9.md
│   └── PS/
│       ├── PS-4.md
│       └── PS-5.md
├── /mappings/
│   └── IAM-control-mapping.csv       # Master mapping spreadsheet
├── /templates/
│   └── control-template.md           # Blank template for new controls
├── /gap-analysis/
│   └── gap-analysis-template.md      # Template for identifying control gaps
└── README.md
```

---

## Control File Format

Each control is documented using a consistent template:

```markdown
## [Control ID] – [Control Name]

**Family:** [Control Family]
**Baseline:** Low / Moderate / High
**Control Description:** [Paraphrased from NIST 800-53 Rev. 5]

### Implementation
[How this control is implemented in the scoped environment]

### Mapped Tool(s)
- Tool: [Tool Name]
- Configuration: [Relevant settings, policies, or features]

### Evidence Artifacts
- [What an auditor would look for to verify this control is in place]

### Status
- [ ] Not Implemented
- [ ] Partially Implemented
- [x] Implemented
```

---

## Methodology

1. **Baseline Selection** — Controls were scoped to the NIST 800-53 Rev. 5 Moderate baseline using the control catalog from [NIST SP 800-53B](https://csrc.nist.gov/publications/detail/sp/800-53b/final).
2. **IAM Scoping** — Only control families directly relevant to identity, access, authentication, and access auditing were included.
3. **Tool Mapping** — Each control was mapped to one or more IAM tools based on how that tool satisfies the control requirement in a hybrid cloud environment.
4. **Evidence Identification** — For each control, relevant evidence artifacts were documented to simulate what would be collected during a real audit or assessment.

---

## Mapping Summary

| Control ID | Control Name | Family | Baseline | Mapped Tool(s) | Implementation Notes | Evidence Artifact | Status |
|---|---|---|---|---|---|---|---|
| AC-2 | Account Management | Access Control | Moderate | Entra ID, Active Directory, CyberArk | Accounts provisioned in AD and synced to Entra ID via Entra Connect. Role-based access assigned via AD security groups. Lifecycle Workflows automate onboarding/offboarding. Privileged accounts managed via CyberArk and Entra PIM with JIT access. | Entra ID audit logs, access review reports, offboarding tickets, AD group membership reports, CyberArk privileged account inventory | Implemented |
| AC-3 | Access Enforcement | Access Control | Moderate | AWS IAM, Entra ID Conditional Access | Access to resources enforced through AWS IAM policies and Entra ID Conditional Access policies. Role assignments reviewed periodically via Entra ID Access Reviews. | AWS IAM policy documentation, Conditional Access policy export, access review completion reports | Implemented |
| AC-6 | Least Privilege | Access Control | Moderate | AWS IAM, Entra ID PIM | AWS IAM roles scoped to minimum required permissions. Entra ID PIM enforces JIT elevation for administrative roles — no standing admin access. Role assignments are time-bound and require approval. | AWS IAM role and policy documentation, Entra PIM role assignment reports, JIT activation logs | Implemented |
| AC-17 | Remote Access | Access Control | Moderate | Entra ID Conditional Access, MFA | Remote access requires MFA via Conditional Access policy. Legacy authentication protocols blocked. Conditional Access enforces compliant device requirement for remote connections. | Conditional Access policy export, sign-in logs showing MFA enforcement, device compliance reports | Implemented |
| IA-2 | Identification and Authentication (Org Users) | Identification & Authentication | Moderate | Entra ID MFA, Entra ID PIM | All org users authenticated via Entra ID with MFA enforced through Conditional Access. FIDO2 security keys supported for privileged users. Legacy auth blocked. PIM requires MFA at role activation. | Conditional Access policy export, MFA registration report, sign-in logs, PIM settings screenshot | Implemented |
| IA-5 | Authenticator Management | Identification & Authentication | Moderate | Entra ID, CyberArk | Password policies enforced via Entra ID. Privileged credentials vaulted in CyberArk with automatic rotation. SSPR enabled with identity verification. | Entra ID password policy configuration, CyberArk credential rotation logs, SSPR configuration screenshot | Implemented |
| IA-8 | Identification and Authentication (Non-Org Users) | Identification & Authentication | Moderate | Entra ID B2B, Guest Access Policies | External users authenticated via Entra ID B2B collaboration. Guest access policies restrict external user permissions. Cross-tenant access settings control inbound and outbound collaboration. | Entra ID B2B configuration, guest access policy export, cross-tenant access settings screenshot | Implemented |
| AU-2 | Event Logging | Audit & Accountability | Moderate | Microsoft Sentinel, AWS CloudTrail | Entra ID sign-in and audit logs forwarded to Sentinel via Diagnostic Settings. AD security event logs ingested via Azure Monitor Agent. AWS API activity logged in CloudTrail and forwarded to Sentinel. CyberArk session logs forwarded to Sentinel. | Entra ID Diagnostic Settings config, Sentinel data connector status, CloudTrail trail config, sample KQL query results | Implemented |
| AU-9 | Protection of Audit Information | Audit & Accountability | Moderate | Sentinel Log Analytics, AWS S3 with MFA Delete | Sentinel Log Analytics Workspace restricted via RBAC. AWS CloudTrail logs stored in S3 with MFA Delete enabled. Log file validation enabled in CloudTrail. | Log Analytics Workspace RBAC assignments, S3 bucket policy, MFA Delete configuration, CloudTrail log file validation settings | Implemented |
| PS-4 | Personnel Termination | Personnel Security | Moderate | Entra ID, Active Directory | Upon termination, accounts disabled in AD and Entra ID within 24 hours per offboarding SOP. Lifecycle Workflows automate account disable and access revocation triggered by HR system. CyberArk privileged access revoked immediately. | Offboarding tickets with timestamps, Entra ID audit logs showing account disable, Lifecycle Workflow execution logs | Implemented |
| PS-5 | Personnel Transfer | Personnel Security | Moderate | Entra ID, Active Directory | Upon role transfer, access is reviewed and adjusted to reflect new job function. Previous role group memberships removed. Entra ID Access Reviews triggered for transferred users. Privileged access re-evaluated via PIM. | Access review completion reports, AD group membership change logs, Entra ID audit logs, PIM role assignment history | Implemented |

---

## Related Frameworks

This project focuses on NIST 800-53 Rev. 5. The following cross-references are in scope for future expansion:

- **NIST Cybersecurity Framework (CSF) 2.0** — PR.AA (Protect: Identity Management & Access Control)
- **CIS Controls v8** — Control 5 (Account Management), Control 6 (Access Control Management)
- **ISO/IEC 27001:2022** — Annex A.5 (Organizational Controls), A.8 (Technological Controls)

---

## Author

**Tyler**  
GRC & IAM Security | Microsoft SC-300 (In Progress)  
[LinkedIn](https://www.linkedin.com/in/tyler-leath-a93781143) | [GitHub](https://github.com/tylerleath4-star)

---

## References

- [NIST SP 800-53 Rev. 5](https://csrc.nist.gov/publications/detail/sp/800-53/5-1/final)
- [NIST SP 800-53B Control Baselines](https://csrc.nist.gov/publications/detail/sp/800-53b/final)
- [Microsoft Entra ID Documentation](https://learn.microsoft.com/en-us/entra/identity/)
- [AWS IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/)
- [CyberArk Documentation](https://docs.cyberark.com/)
