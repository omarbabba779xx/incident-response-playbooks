# Incident Risk Scenarios (illustrative register)

One risk scenario per playbook, scored with the [methodology](risk-assessment-methodology.md).
Scores are an illustrative example for a generic mid-size organisation, not a real assessment.

**Author:** Omar Babba · **Last updated:** 2026-10-09

L = likelihood (1 to 5), I = impact (1 to 5). Inherent = before controls, residual = after the
controls listed.

## Summary

| ID | Scenario | Playbook | Inherent (L x I) | Residual (L x I) | Residual level |
|---|---|---|---|---|---|
| R-01 | Phishing leads to stolen credentials | [Phishing](../playbooks/phishing-incident-playbook.md) | 4 x 3 = **12 High** | 3 x 3 = **9 Medium** | Medium |
| R-02 | Malware or ransomware executes on an endpoint | [Malware Infection](../playbooks/malware-infection-playbook.md) | 3 x 5 = **15 High** | 2 x 5 = **10 High** | High |
| R-03 | Account takeover or business email compromise | [Account Compromise](../playbooks/account-compromise-playbook.md) | 4 x 4 = **16 High** | 3 x 3 = **9 Medium** | Medium |
| R-04 | Unauthorised access to or exfiltration of personal data | [Data Breach](../playbooks/data-breach-playbook.md) | 2 x 5 = **10 High** | 2 x 4 = **8 Medium** | Medium |
| R-05 | Denial of service against a public-facing service | [DDoS Attack](../playbooks/ddos-attack-playbook.md) | 3 x 3 = **9 Medium** | 3 x 2 = **6 Medium** | Medium |

## Detail

### R-01 Phishing leads to stolen credentials

- **Threat source and event:** external actor sends a credential-harvesting email or lure.
- **Vulnerability:** users who click and enter credentials; no phishing-resistant MFA on some accounts.
- **Controls that reduce likelihood:** email gateway filtering, awareness training and phishing
  simulations, report button.
- **Controls that reduce impact:** rapid session revocation and password reset (playbook,
  Identification and Containment), MFA.
- **Treatment:** reduce. Extend MFA to all accounts; track click rate in simulations.
- **KRIs:** click rate and report rate in simulations; time to acknowledge a report.

### R-02 Malware or ransomware executes on an endpoint

- **Threat source and event:** commodity or targeted malware delivered by attachment, download
  or lateral movement.
- **Vulnerability:** unpatched software, excessive local rights, backups not restore-tested.
- **Controls that reduce likelihood:** EDR, patching, application control, email filtering.
- **Controls that reduce impact:** host isolation, network segmentation, offline backups,
  tested restore (playbook, Containment and Recovery).
- **Treatment:** reduce. Test restores quarterly; isolate Tier-0 assets. The residual stays High
  because the impact is Severe even when likelihood is low, so it needs CISO visibility.
- **KRIs:** age of last successful restore test; share of endpoints with a healthy EDR agent;
  patch latency for critical vulnerabilities.

### R-03 Account takeover or business email compromise

- **Threat source and event:** attacker uses stolen or guessed credentials, or abuses a session.
- **Vulnerability:** weak or reused passwords, legacy authentication, no conditional access.
- **Controls that reduce likelihood:** MFA, conditional access, blocking legacy authentication,
  impossible-travel alerts.
- **Controls that reduce impact:** least privilege, rapid token revocation, mailbox-rule audit
  (playbook, Containment).
- **Treatment:** reduce. Enforce MFA for privileged roles first.
- **KRIs:** share of privileged accounts with phishing-resistant MFA; number of risky sign-ins
  per month; time to revoke a compromised session.

### R-04 Unauthorised access to or exfiltration of personal data

- **Threat source and event:** external or internal actor copies sensitive data.
- **Vulnerability:** excessive access, missing data classification, weak egress monitoring.
- **Controls that reduce likelihood:** access reviews, encryption, DLP, logging.
- **Controls that reduce impact:** tested notification process, including the 72-hour regulator
  notification under GDPR Article 33, evidence preservation (playbook, Communication).
- **Treatment:** reduce, and transfer part of the financial impact through insurance. Notification procedure: [GDPR personal data breach response](../compliance/gdpr-breach-response.md).
- **KRIs:** share of sensitive datasets with a named owner; time from detection to the
  notification decision; open findings from access reviews.

### R-05 Denial of service against a public-facing service

- **Threat source and event:** volumetric, protocol or application-layer flood.
- **Vulnerability:** single internet path, no upstream scrubbing, no rate limiting.
- **Controls that reduce likelihood:** none fully; attacker motivation is external.
- **Controls that reduce impact:** upstream DDoS protection, rate limiting, runbook with ISP
  contacts, capacity headroom.
- **Treatment:** transfer (provider protection) and reduce. Accept the remaining risk for
  non-critical services, with an owner and a review date.
- **KRIs:** time to activate mitigation; percentage of critical services behind scrubbing.

## From risk back to the playbooks

When an incident closes, use the Post-Incident Review to ask three questions about the related
scenario:

1. Was the likelihood score right, given what just happened?
2. Did the impact match the actual functional, information and recoverability effect?
3. Did the controls listed above work, and does the residual score still hold?

Record any change in the register and, if the residual level moved up, raise it according to
the appetite table in the methodology.
