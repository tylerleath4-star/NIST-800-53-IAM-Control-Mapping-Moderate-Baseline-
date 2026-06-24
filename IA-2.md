# IA-2 – Identification and Authentication (Organizational Users)

**Family:** Identification and Authentication (IA)  
**Baseline:** Moderate  
**Control Description:** The information system uniquely identifies and authenticates organizational users (or processes acting on behalf of organizational users). Multi-factor authentication is required for network access to privileged and non-privileged accounts.

---

## Implementation

All organizational users authenticate through Microsoft Entra ID as the central identity provider. Authentication is enforced via Conditional Access policies that require multi-factor authentication (MFA) for all access scenarios.

- **Unique Identification:** Every user is assigned a unique Entra ID account tied to their corporate identity. Shared accounts are prohibited by policy.
- **MFA Enforcement:** Conditional Access policies require MFA for all users accessing cloud and on-premises resources. Legacy authentication protocols (SMTP, POP3, IMAP) are blocked to prevent MFA bypass.
- **Phishing-Resistant MFA:** FIDO2 security keys are supported and encouraged for privileged users as a phishing-resistant authenticator in compliance with IA-2(6).
- **Privileged Account Authentication:** Administrative roles require MFA at every sign-in with no persistent sessions. Entra ID PIM enforces JIT elevation with MFA re-authentication required at activation.
- **On-Premises Integration:** Entra ID Connect enables hybrid identity, extending cloud authentication policies to on-premises resources via Entra ID Pass-through Authentication or Password Hash Sync.

---

## Mapped Tool(s)

| Tool | Configuration / Feature |
|---|---|
| Microsoft Entra ID | Conditional Access policies, MFA enforcement, FIDO2 support |
| Entra ID PIM | MFA required at role activation for privileged accounts |
| Active Directory | Hybrid identity via Entra ID Connect |

---

## Evidence Artifacts

The following artifacts would be collected to demonstrate compliance with IA-2 during an audit or assessment:

- Conditional Access policy export showing MFA requirement for all users
- Entra ID sign-in logs confirming MFA challenges on authentication events
- MFA registration report showing percentage of users enrolled
- Legacy authentication block policy configuration screenshot
- Entra ID PIM settings showing MFA required at role activation
- FIDO2 authentication method policy configuration

---

## Notes

- NIST 800-53 Rev. 5 IA-2(1) requires MFA for privileged network access; IA-2(2) requires MFA for non-privileged network access — both are satisfied by the Conditional Access policy described above
- Microsoft Authenticator (push notifications) satisfies MFA requirements but is not phishing-resistant; FIDO2 or certificate-based authentication should be prioritized for admin accounts
- Number matching and additional context should be enabled in Microsoft Authenticator to mitigate MFA fatigue attacks

---

## Status

- [ ] Not Implemented
- [ ] Partially Implemented
- [x] Implemented

---

## References

- [NIST SP 800-53 Rev. 5 – IA-2](https://csrc.nist.gov/Projects/risk-management/sp800-53-controls/release-search#!/control?version=5.1&number=IA-2)
- [Microsoft Entra ID Conditional Access](https://learn.microsoft.com/en-us/entra/identity/conditional-access/overview)
- [Microsoft Entra ID MFA](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-mfa-howitworks)
- [FIDO2 Security Keys in Entra ID](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-passwordless)
