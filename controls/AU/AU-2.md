# AU-2 – Event Logging

**Family:** Audit and Accountability (AU)  
**Baseline:** Moderate  
**Control Description:** The organization determines that the information system is capable of auditing defined events. Coordination between entities requiring audit information is established to ensure adequate coverage. The organization compiles a list of events requiring auditing and provides rationale for why those events are selected.

---

## Implementation

Audit logging across this hybrid cloud environment is centralized in Microsoft Sentinel, with source logs ingested from Microsoft Entra ID, Active Directory, and AWS via CloudTrail.

- **Entra ID Sign-In Logging:** All Entra ID sign-in events — including successes, failures, MFA challenges, and Conditional Access policy outcomes — are streamed to a Log Analytics Workspace via Entra ID Diagnostic Settings and ingested into Microsoft Sentinel.
- **Entra ID Audit Logs:** Administrative actions such as account creation, role assignments, group membership changes, and policy modifications are captured in Entra ID audit logs and forwarded to Sentinel.
- **Active Directory Logging:** Domain controller security event logs (Event IDs 4624, 4625, 4648, 4720, 4732, etc.) are collected via the Microsoft Monitoring Agent (MMA) or Azure Monitor Agent (AMA) and ingested into Sentinel.
- **AWS CloudTrail:** All AWS API activity — including IAM role assumptions, policy changes, S3 access, and console sign-ins — is logged in CloudTrail and forwarded to Sentinel via the AWS S3 connector.
- **CyberArk Session Logging:** Privileged session activity recorded by CyberArk is forwarded to Sentinel for centralized visibility into privileged access events.

### Auditable Events Defined

| Event Category | Source | Log Type |
|---|---|---|
| User sign-in success / failure | Entra ID | Sign-in logs |
| MFA success / failure | Entra ID | Sign-in logs |
| Account creation / modification / deletion | Entra ID / AD | Audit logs |
| Privileged role assignment / activation | Entra ID PIM | Audit logs |
| Group membership changes | Entra ID / AD | Audit logs |
| Conditional Access policy changes | Entra ID | Audit logs |
| AWS IAM role assumption | AWS CloudTrail | Management events |
| AWS console sign-in | AWS CloudTrail | Management events |
| Privileged session activity | CyberArk | Session logs |

---

## Mapped Tool(s)

| Tool | Configuration / Feature |
|---|---|
| Microsoft Sentinel | Central SIEM — log aggregation, correlation, alerting |
| Microsoft Entra ID | Diagnostic Settings → Log Analytics Workspace |
| AWS CloudTrail | Management and data event logging, S3 log storage |
| Active Directory | Security event logs via Azure Monitor Agent |
| CyberArk | Privileged session recording forwarded to Sentinel |

---

## Evidence Artifacts

The following artifacts would be collected to demonstrate compliance with AU-2 during an audit or assessment:

- Entra ID Diagnostic Settings configuration showing log categories enabled and Log Analytics Workspace destination
- Microsoft Sentinel data connector status screenshots confirming active ingestion
- AWS CloudTrail trail configuration showing all regions enabled and log file validation active
- Sample KQL queries run against Sentinel demonstrating log availability
- Log Analytics Workspace retention settings confirming required retention period
- CyberArk to Sentinel connector configuration

### Sample KQL Queries

**Failed sign-in attempts (last 24 hours):**
```kql
SigninLogs
| where TimeGenerated > ago(24h)
| where ResultType != 0
| project TimeGenerated, UserPrincipalName, ResultType, ResultDescription, IPAddress, Location
| order by TimeGenerated desc
```

**Privileged role activations (Entra ID PIM):**
```kql
AuditLogs
| where TimeGenerated > ago(7d)
| where OperationName == "Add member to role completed (PIM activation)"
| project TimeGenerated, InitiatedBy, TargetResources, Result
```

---

## Notes

- Log retention should meet the minimum required by your organization's policy and any applicable compliance requirements (NIST recommends retaining audit records for at least 3 years for Moderate systems)
- Sentinel's analytics rules should be configured to alert on high-priority audit events such as repeated sign-in failures, privilege escalations, and account lockouts
- AU-2 pairs closely with AU-3 (Content of Audit Records) and AU-9 (Protection of Audit Information) — ensure those controls are also documented

---

## Status

- [ ] Not Implemented
- [ ] Partially Implemented
- [x] Implemented

---

## References

- [NIST SP 800-53 Rev. 5 – AU-2](https://csrc.nist.gov/Projects/risk-management/sp800-53-controls/release-search#!/control?version=5.1&number=AU-2)
- [Microsoft Sentinel Overview](https://learn.microsoft.com/en-us/azure/sentinel/overview)
- [Entra ID Diagnostic Settings](https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-configure-diagnostic-settings)
- [AWS CloudTrail Documentation](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)
