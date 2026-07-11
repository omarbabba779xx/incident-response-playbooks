# Incident Response Playbooks

A set of five incident-type playbooks — **Phishing, Malware Infection, Account Compromise, Data
Breach, and DDoS** — built for Tier-1/Tier-2 SOC analysts to execute consistently, regardless of
which analyst is on shift when an incident lands. Each playbook is authored as a standalone,
step-by-step procedure: what to check, what to preserve as evidence, when and to whom to escalate,
and what to communicate to stakeholders at each stage — grounded in published NIST and CISA
guidance rather than improvised process.

**Author:** Omar Babba · **Status:** Living documents, reviewed quarterly · **Last updated:** 2026-07-11

## Table of contents

- [Framework basis](#framework-basis)
- [Why this repo uses the SANS six-phase model operationally](#why-this-repo-uses-the-sans-six-phase-model-operationally)
- [Playbooks in this repo](#playbooks-in-this-repo)
- [Shared templates](#shared-templates)
- [Severity matrix](#severity-matrix-used-consistently-across-all-five-playbooks)
- [Incident impact classification (NIST/CISA-aligned)](#incident-impact-classification-nistcisa-aligned)
- [Decision-tree diagrams](#decision-tree-diagrams)
- [Repository structure](#repository-structure)
- [References](#references)

## Framework basis

This repository is built on two authoritative, publicly published sources, not internal opinion:

- **[NIST SP 800-61 Rev. 2](https://csrc.nist.gov/pubs/sp/800/61/r2/final), *Computer Security
  Incident Handling Guide*** (Aug. 2012) — the classic, four-phase incident-handling lifecycle
  (Preparation → Detection & Analysis → Containment, Eradication & Recovery → Post-Incident
  Activity). This is the model most SOC teams, certifications (GCIH, Security+), and
  federal/enterprise IR programs are actually built around today, and the one
  [CISA's own Federal Government Cybersecurity Incident and Vulnerability Response
  Playbooks](https://www.cisa.gov/resources-tools/resources/federal-government-cybersecurity-incident-and-vulnerability-response-playbooks)
  (Aug. 2024) explicitly cite as their process foundation.
- **[NIST SP 800-61 Rev. 3](https://csrc.nist.gov/pubs/sp/800/61/r3/final), *Incident Response
  Recommendations and Considerations for Cybersecurity Risk Management: A CSF 2.0 Community
  Profile*** (April 2025) — the current official replacement for Rev. 2. Rev. 3 deliberately
  **drops the standalone four-phase lifecycle** and instead maps incident-response activities
  across all six functions of the [NIST Cybersecurity Framework (CSF)
  2.0](https://www.nist.gov/cyberframework): Govern, Identify, Protect, Detect, Respond, Recover.
  The intent is to stop treating incident response as an isolated, bolt-on activity and instead
  fold it into continuous risk management — Preparation becomes an ongoing Govern/Identify/
  Protect responsibility rather than a one-time pre-incident checklist item.

**Both are cited here deliberately, not by oversight.** Rev. 3 is the current, correct reference
if you're asked "what does NIST currently publish on this," and this repo says so plainly rather
than quietly citing an outdated document as if it were still current. But Rev. 2's phase model
(and SANS' more granular six-phase derivative of it) remains the dominant *operational* structure
actually used for day-to-day incident handling, playbook authoring, and analyst training — CISA's
own 2024 federal playbooks are built on it, not on Rev. 3's function-mapping approach. Rev. 3 is a
governance/risk-integration document; it is not written as an analyst run-book, and doesn't
attempt to be one. These playbooks are run-books, so they use the lifecycle model Rev. 3
explicitly superseded at the framework level while remaining consistent with Rev. 3's underlying
guidance in substance (detection, containment, eradication, recovery, and lessons-learned
activities are all still exactly what Rev. 3 expects — they're just described under CSF 2.0
function headers there instead of standalone phases).

## Why this repo uses the SANS six-phase model operationally

SANS' six-phase model — **Preparation, Identification, Containment, Eradication, Recovery,
Lessons Learned** — is the same underlying lifecycle as NIST SP 800-61 Rev. 2 at finer
granularity: it splits Rev. 2's "Detection & Analysis" into a standalone **Identification** phase,
and splits "Containment, Eradication & Recovery" into three distinct phases. Every playbook in
this repo is organized by these six phases for step-by-step analyst clarity, with an explicit
mapping back to the NIST Rev. 2 model so either framework reference works when talking to
auditors, management, or anyone trained on the other terminology.

| SANS phase | Maps to NIST SP 800-61 Rev. 2 phase | Maps to CSF 2.0 function (Rev. 3) |
|---|---|---|
| Preparation | Preparation | Govern, Identify, Protect |
| Identification | Detection & Analysis | Detect |
| Containment | Containment, Eradication & Recovery | Respond |
| Eradication | Containment, Eradication & Recovery | Respond |
| Recovery | Containment, Eradication & Recovery | Recover |
| Lessons Learned | Post-Incident Activity | Govern (continuous improvement) |

## Playbooks in this repo

| Playbook | Covers | Severity range | Primary supporting reference |
|---|---|---|---|
| [Phishing Incident](playbooks/phishing-incident-playbook.md) | Reported/detected phishing emails, credential-harvesting links, malicious attachments | Low–Critical (depends on click/credential-entry outcome) | NIST SP 800-61 Rev. 2 §3 |
| [Malware Infection](playbooks/malware-infection-playbook.md) | Endpoint malware detection (AV/EDR alert, ransomware, trojans, worms) | Medium–Critical | [NIST SP 800-83 Rev. 1](https://csrc.nist.gov/pubs/sp/800/83/r1/final), CISA [#StopRansomware Guide](https://www.cisa.gov/stopransomware/ransomware-guide) |
| [Account Compromise](playbooks/account-compromise-playbook.md) | Stolen/abused credentials, impossible-travel logins, BEC | Medium–Critical | NIST SP 800-61 Rev. 2 §3 |
| [Data Breach](playbooks/data-breach-playbook.md) | Unauthorized access to or exfiltration of sensitive data | High–Critical | NIST SP 800-61 Rev. 2 §3; GDPR Art. 33 (72-hour notification) |
| [DDoS Attack](playbooks/ddos-attack-playbook.md) | Volumetric/protocol/application-layer denial of service | Medium–Critical | NIST SP 800-61 Rev. 2 §3 |

Each playbook follows the same section structure so any analyst can move between them without
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

This four-tier matrix is deliberately simple for fast triage decisions inside each playbook. For
incidents that require formal reporting up to leadership, regulators, or a parent
organization/ISAC, cross-reference it against the three-axis classification below, which is what
CISA and federal agencies actually use for incident scoring.

## Incident impact classification (NIST/CISA-aligned)

The [US-CERT/CISA Federal Incident Notification
Guidelines](https://www.cisa.gov/federal-incident-notification-guidelines) and CISA's National
Cyber Incident Scoring System (NCISS) — both built on NIST SP 800-61's incident-categorization
guidance — score an incident along three independent axes rather than a single severity label.
This repo's playbooks reference this triad wherever precision matters more than the four-tier
matrix's speed (e.g. for the Executive Summary and Post-Incident Review templates):

| Axis | What it measures | Example range |
|---|---|---|
| **Functional Impact** | Effect on the organization's ability to deliver business/mission functions | No impact → Low → Medium (some services degraded) → High (significant services down) → Critical (organization-wide loss of a critical function) |
| **Information Impact** | Effect on the confidentiality, integrity, and availability of the organization's information | No impact → Privacy breach of a small dataset → Proprietary information breach → Integrity loss → Critical system/data destruction |
| **Recoverability** | Scope of time and resources required to recover | Regular (recoverable with existing resources on a predictable timeline) → Supplemented (requires additional resources) → Extended (requires external assistance, timeline unpredictable) → Not recoverable |

Using all three axes independently (rather than collapsing to one number) is why a small-scope
but highly sensitive data exposure and a large-scope but fully-absorbed DDoS attack can both be
"significant" without being equivalent incidents — the axes make that distinction explicit
instead of forcing a single severity word to carry all three meanings at once.

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

## References

- NIST SP 800-61 Rev. 2 — [*Computer Security Incident Handling Guide*](https://csrc.nist.gov/pubs/sp/800/61/r2/final) (withdrawn, superseded by Rev. 3, but still the operational basis for this repo's phase model — see [Framework basis](#framework-basis))
- NIST SP 800-61 Rev. 3 — [*Incident Response Recommendations and Considerations for Cybersecurity Risk Management: A CSF 2.0 Community Profile*](https://csrc.nist.gov/pubs/sp/800/61/r3/final) (April 2025, current)
- NIST SP 800-83 Rev. 1 — [*Guide to Malware Incident Prevention and Handling for Desktops and Laptops*](https://csrc.nist.gov/pubs/sp/800/83/r1/final)
- NIST Cybersecurity Framework (CSF) 2.0 — [nist.gov/cyberframework](https://www.nist.gov/cyberframework)
- CISA — [Federal Government Cybersecurity Incident and Vulnerability Response Playbooks](https://www.cisa.gov/resources-tools/resources/federal-government-cybersecurity-incident-and-vulnerability-response-playbooks) (Aug. 2024)
- CISA — [#StopRansomware Guide](https://www.cisa.gov/stopransomware/ransomware-guide)
- CISA — [Federal Incident Notification Guidelines](https://www.cisa.gov/federal-incident-notification-guidelines) (Functional Impact / Information Impact / Recoverability classification)
- GDPR Article 33 — 72-hour personal data breach notification requirement to supervisory authorities
