# Framework and Regulation Crosswalk

How the playbooks map to the main standards, controls and notification rules an auditor, a
customer or a regulator is likely to ask about.

**Author:** Omar Babba · **Status:** Living document · **Last updated:** 2026-10-09

This is a working mapping built from public texts. Standards are revised and regulations differ by
sector and country, so check the current official text and involve Legal before relying on any
deadline.

## Lifecycle crosswalk

| SANS phase (used in the playbooks) | NIST SP 800-61 Rev. 2 | NIST CSF 2.0 | ISO/IEC 27035-1 | ISO/IEC 27001:2022 Annex A |
|---|---|---|---|---|
| Preparation | Preparation | GV (Govern), ID.RA, PR | Prepare | A.5.24 Incident management planning and preparation |
| Identification | Detection and Analysis | DE.CM, DE.AE | Detect and report; Assess and decide | A.5.25 Assessment and decision on information security events |
| Containment | Containment, Eradication and Recovery | RS.MI, RS.MA | Respond | A.5.26 Response to information security incidents |
| Eradication | Containment, Eradication and Recovery | RS.MI | Respond | A.5.26 |
| Recovery | Containment, Eradication and Recovery | RC.RP, RC.CO | Respond | A.5.26 |
| Lessons Learned | Post-Incident Activity | GV.OC, ID.IM | Learn lessons | A.5.27 Learning from incidents |
| Evidence handling (all phases) | Evidence handling | RS.AN | Respond | A.5.28 Collection of evidence |

CSF 2.0 categories used above: DE.CM continuous monitoring, DE.AE adverse event analysis, RS.MA
incident management, RS.AN incident analysis, RS.MI incident mitigation, RS.CO incident response
reporting and communication, RC.RP incident recovery plan execution, RC.CO incident recovery
communication, ID.RA risk assessment, ID.IM improvement.

## Repository artefact to control crosswalk

| Artefact in this repo | Supports |
|---|---|
| [Playbooks](../playbooks/) | NIST 800-61 incident handling; ISO 27001 A.5.24 to A.5.26; CIS 17.4 incident response process |
| [Severity matrix and impact classification](../README.md#severity-matrix-used-consistently-across-all-five-playbooks) | ISO 27001 A.5.25; CIS 17.9 incident thresholds |
| [Templates: chain of custody, executive summary, stakeholder notification, post-incident review](../templates/) | ISO 27001 A.5.27 and A.5.28; CIS 17.6 and 17.8; CSF RS.CO |
| [Risk methodology and scenarios](../risk/) | CSF ID.RA and GV.RM; ISO/IEC 27005; NIST SP 800-30 |
| [GDPR procedure and breach register](../compliance/) | GDPR Art. 33 and 34; ISO 27001 A.5.34 privacy and protection of personal data |
| [ATT&CK mapping and Sigma rules](../detection/) | CSF DE.CM and DE.AE; CIS Control 8 audit log management |
| [Metrics guide](../metrics/ir-metrics.md) | CIS 17.9 and 17.8; ISO 27001 clause 9.1 monitoring and measurement |
| [Tabletop exercises](../exercises/tabletop-exercises.md) | CIS 17.7; NIST SP 800-84; ISO 27001 clause 7.2 competence |

## CIS Controls v8, Control 17 (Incident Response Management)

| Safeguard | Summary | Where it is addressed |
|---|---|---|
| 17.1 | Designate personnel to manage incident handling | Playbook ownership and the roles in the GDPR procedure |
| 17.2 | Establish contact information for reporting incidents | Playbook prerequisites and escalation tables |
| 17.3 | Establish an enterprise process for reporting incidents | Phishing report button and mailbox in the Phishing playbook |
| 17.4 | Establish and maintain an incident response process | The five playbooks |
| 17.5 | Assign key roles and responsibilities | Roles tables in the playbooks and the GDPR procedure |
| 17.6 | Define mechanisms for communicating during incident response | Communication templates |
| 17.7 | Conduct routine incident response exercises | Tabletop exercises |
| 17.8 | Conduct post-incident reviews | Post-Incident Review template |
| 17.9 | Establish and maintain security incident thresholds | Severity matrix and impact classification |

## Notification obligations at a glance

Always check the current text and the applicable sector rules.

| Regime | Who | Trigger | Deadline (summary) |
|---|---|---|---|
| GDPR Art. 33 | Controllers (and processors, to the controller) | Personal data breach likely to result in a risk | Authority within 72 hours of awareness where feasible; processor without undue delay |
| GDPR Art. 34 | Controllers | Breach likely to result in a high risk | Individuals without undue delay |
| NIS2 Directive, Art. 23 | Essential and important entities in the EU | Significant incident | Early warning within 24 hours, incident notification within 72 hours, final report within one month |
| DORA, Art. 19 | EU financial entities | Major ICT-related incident | Initial, intermediate and final reports; timings set by the regulatory technical standards |
| US SEC Form 8-K, Item 1.05 | US-listed companies | Material cybersecurity incident | Within four business days of determining materiality |
| Morocco | Entities in scope of Law 09-08 (personal data, CNDP) and Law 05-20 (cybersecurity, DGSSI) | Depends on entity type and sector | Verify with Legal which duties and deadlines apply to the entity |

For Morocco, the national authorities to know are the DGSSI (national cybersecurity authority and
its maCERT) and the CNDP (personal data protection). This repo does not state their notification
deadlines; confirm them against the current texts and the entity's sector.

## Using this crosswalk in an audit

1. Pick the control or clause the auditor asks about.
2. Point to the artefact in the table above and the section that implements it.
3. Show evidence of operation: a closed case with timestamps, a Post-Incident Review, an exercise
   report, a register entry.

A document alone proves intent. Evidence of use proves the control works.

## References

- NIST SP 800-61 Rev. 2 and Rev. 3: <https://csrc.nist.gov/pubs/sp/800/61/r3/final>
- NIST Cybersecurity Framework 2.0: <https://www.nist.gov/cyberframework>
- ISO/IEC 27035-1, *Information security incident management, Part 1: Principles and process*
- ISO/IEC 27001:2022, Annex A controls 5.24 to 5.28 and 5.34
- CIS Controls v8: <https://www.cisecurity.org/controls/v8>
- GDPR, Regulation (EU) 2016/679, Articles 33 and 34
- NIS2, Directive (EU) 2022/2555, Article 23
- DORA, Regulation (EU) 2022/2554, Article 19
- US SEC, Form 8-K Item 1.05
- Morocco: Law 09-08 (CNDP) and Law 05-20 on cybersecurity (DGSSI)
