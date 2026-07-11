# Incident Response Playbooks

A set of five incident-type playbooks built around **NIST SP 800-61 Rev. 2** ("Computer Security
Incident Handling Guide") and cross-referenced against SANS' six-phase model. Each playbook is a
standalone, analyst-usable procedure: a Tier-1 SOC analyst should be able to open one of these
during a live incident and know exactly what to check, what to preserve, when to escalate, and
what to tell stakeholders — without having to improvise process on top of technical triage.

## Why playbooks, and why these two frameworks

NIST SP 800-61 defines four incident-handling phases:

1. **Preparation** — tools, access, contacts, and playbooks in place *before* an incident happens.
2. **Detection & Analysis** — recognizing and validating that an incident is actually occurring.
3. **Containment, Eradication & Recovery** — stopping the damage, removing the cause, restoring
   normal operation.
4. **Post-Incident Activity** — lessons learned, documentation, process improvement.

SANS' popular six-phase model (Preparation, Identification, Containment, Eradication, Recovery,
Lessons Learned) is the same lifecycle at finer granularity — it splits NIST's "Detection &
Analysis" into **Identification** and splits "Containment, Eradication & Recovery" into three
distinct phases. Every playbook in this repo is organized by the **SANS six phases** for
step-by-step clarity, with an explicit mapping back to the NIST four-phase model so either
framework reference works when talking to auditors or management.

| SANS phase | Maps to NIST SP 800-61 phase |
|---|---|
| Preparation | Preparation |
| Identification | Detection & Analysis |
| Containment | Containment, Eradication & Recovery |
| Eradication | Containment, Eradication & Recovery |
| Recovery | Containment, Eradication & Recovery |
| Lessons Learned | Post-Incident Activity |

## Playbooks in this repo

| Playbook | Covers | Severity range |
|---|---|---|
| [Phishing Incident](playbooks/phishing-incident-playbook.md) | Reported/detected phishing emails, credential-harvesting links, malicious attachments | Low–Critical (depends on click/credential-entry outcome) |
| [Malware Infection](playbooks/malware-infection-playbook.md) | Endpoint malware detection (AV/EDR alert, ransomware, trojans, worms) | Medium–Critical |
| [Account Compromise](playbooks/account-compromise-playbook.md) | Stolen/abused credentials, impossible-travel logins, BEC | Medium–Critical |
| [Data Breach](playbooks/data-breach-playbook.md) | Unauthorized access to or exfiltration of sensitive data | High–Critical |
| [DDoS Attack](playbooks/ddos-attack-playbook.md) | Volumetric/protocol/application-layer denial of service | Medium–Critical |

Each playbook follows the same section structure so any analyst can jump between them without
relearning the format:

```
Purpose · Scope · Prerequisites · Detection Criteria · Response Steps (by SANS phase)
· Decision Tree · Escalation Procedures · Evidence Collection · Recovery Actions
· Communication Templates · Post-Incident Activities
```

## Shared templates

Reusable, incident-type-agnostic templates live in [templates/](templates/):

- [Stakeholder Notification Template](templates/stakeholder-notification-template.md)
- [Executive Summary Template](templates/executive-summary-template.md)
- [Post-Incident Review Template](templates/post-incident-review-template.md)
- [Evidence Chain-of-Custody Log](templates/chain-of-custody-template.md)

## Severity matrix (used consistently across all five playbooks)

| Severity | Definition | Initial response time | Who's notified |
|---|---|---|---|
| **Critical** | Active data exfiltration, ransomware detonation, domain admin compromise, business-critical system down | Immediate (page on-call) | CISO, IT leadership, Legal, possibly executive team/board |
| **High** | Confirmed compromise contained to limited scope, credential theft with evidence of use, malware on a sensitive system | < 30 minutes | SOC lead, IT manager, system owner |
| **Medium** | Suspicious activity requiring investigation, single-user phishing click without credential entry, isolated malware detection auto-contained by EDR | < 2 hours | SOC lead |
| **Low** | Reported phishing with no interaction, blocked/failed attack attempts, informational alerts | Next business day (documented, queued) | Logged only, no active notification |

## Decision-tree diagrams

Every playbook includes a Mermaid flowchart for its highest-value branching decision (e.g. "did
the user enter credentials?" for phishing, "is the affected host a Tier-0 asset?" for malware).
Mermaid renders natively in GitHub's markdown viewer — no external diagramming tool or account
required to view them. Editable source is inline in each playbook's `.md` file.

## Repository structure

```
README.md                                  this file
playbooks/
  phishing-incident-playbook.md
  malware-infection-playbook.md
  account-compromise-playbook.md
  data-breach-playbook.md
  ddos-attack-playbook.md
templates/
  stakeholder-notification-template.md
  executive-summary-template.md
  post-incident-review-template.md
  chain-of-custody-template.md
```
