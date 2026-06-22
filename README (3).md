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

The [`/mappings/IAM-control-mapping.csv`](mappings/IAM-control-mapping.csv) file contains the master mapping table with the following columns:

| Control ID | Control Name | Family | Baseline | Mapped Tool | Implementation Notes | Evidence Artifact | Status |
|---|---|---|---|---|---|---|---|

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
[LinkedIn](#) | [GitHub](#)

---

## References

- [NIST SP 800-53 Rev. 5](https://csrc.nist.gov/publications/detail/sp/800-53/5-1/final)
- [NIST SP 800-53B Control Baselines](https://csrc.nist.gov/publications/detail/sp/800-53b/final)
- [Microsoft Entra ID Documentation](https://learn.microsoft.com/en-us/entra/identity/)
- [AWS IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/)
- [CyberArk Documentation](https://docs.cyberark.com/)
