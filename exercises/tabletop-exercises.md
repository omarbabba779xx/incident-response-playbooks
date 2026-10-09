# Tabletop Exercises

Five discussion-based exercises, one per playbook, to test the procedures, the contacts and the
decisions without touching any production system.

**Author:** Omar Babba · **Status:** Living document · **Last updated:** 2026-10-09

All scenarios are fictional. They are designed to be run around a table, with no technical
execution and no real malware.

## Why run exercises

A playbook is only useful if people know it, trust it and can follow it under stress. Exercises
reveal missing contacts, unclear decision rights, outdated steps and gaps in logging before a real
incident does. CIS Controls v8 (safeguard 17.7) and NIST SP 800-84 both recommend routine
exercises.

## Format

| Item | Guidance |
|---|---|
| Duration | 60 to 90 minutes per scenario |
| Frequency | At least one scenario per quarter; cover all five within a year |
| Facilitator | Runs the clock, reads the injects, keeps discussion on the playbook; does not play a role |
| Participants | SOC analysts and lead, IT operations, Legal or compliance, communications, DPO, a business owner |
| Observer | Records decisions, delays and gaps in the exercise report |
| Ground rules | No blame; decisions must cite the playbook step or note that the step is missing |

## How each scenario runs

1. The facilitator reads the opening situation.
2. Every 10 to 15 minutes, a new **inject** adds information or pressure.
3. After each inject, the group answers the **decision questions** and names the playbook step it
   is using.
4. At the end, the observer lists gaps and assigns actions with an owner and a date.

## Scenario 1 – Phishing with credential entry

Playbook: [Phishing](../playbooks/phishing-incident-playbook.md)

**Situation.** Three employees in finance report the same email about an "urgent supplier invoice".

| Time | Inject |
|---|---|
| T+0 | The email gateway shows 40 recipients received the message |
| T+15 | One user admits clicking the link and typing their password |
| T+30 | Sign-in logs show that account used from a new country 10 minutes ago |
| T+45 | A mailbox forwarding rule to an external address is found on that account |

**Decision questions.** What severity is assigned and why? Who is told, and when? Which accounts
are reset first? Do we treat this as the Account Compromise playbook now? Is personal data in that
mailbox, which would start the [GDPR assessment](../compliance/gdpr-breach-response.md)?

**Expected outputs.** Severity and handoff decision, list of affected recipients, containment steps
with times, first draft of an internal notice.

## Scenario 2 – Ransomware on a file server

Playbook: [Malware Infection](../playbooks/malware-infection-playbook.md)

**Situation.** At 02:10 the EDR raises a high alert on a Windows workstation, then on a file server.

| Time | Inject |
|---|---|
| T+0 | EDR alert: shadow copies deleted on a workstation |
| T+15 | Users report files renamed with a new extension on a shared drive |
| T+30 | The file server stops responding; the last backup is from 3 days ago |
| T+45 | A note demands payment and claims data was stolen |

**Decision questions.** Do we isolate the server now, and who authorises it? What is the business
impact and who must be called at night? Which backups are trusted? How do we preserve evidence
before wiping? Who decides on any contact with the attacker? What are the legal obligations if
the claim of data theft is credible?

**Expected outputs.** Containment decision with owner, evidence preservation plan, recovery
priorities, communication to executives.

## Scenario 3 – Account takeover and business email compromise

Playbook: [Account Compromise](../playbooks/account-compromise-playbook.md)

**Situation.** A customer says the bank details on an invoice from your company changed.

| Time | Inject |
|---|---|
| T+0 | The customer forwards an email from a sales manager's address with new bank details |
| T+15 | The sales manager says they did not send it |
| T+30 | Sign-in logs show a legacy-protocol login from a foreign IP |
| T+45 | Two other customers received similar emails |

**Decision questions.** How do we confirm compromise without alerting the attacker too early?
What do we revoke and in what order? Which customers must be warned, and by whom? Is a payment
already made, and who contacts the bank?

**Expected outputs.** Containment and revocation sequence, customer notification list, finance and
bank contact steps, evidence kept.

## Scenario 4 – Personal data exfiltration

Playbook: [Data Breach](../playbooks/data-breach-playbook.md)

**Situation.** A researcher emails the security mailbox claiming to have found customer records
posted online.

| Time | Inject |
|---|---|
| T+0 | The message includes a sample of 20 records that look genuine |
| T+15 | A check shows the records match a database that an external contractor can access |
| T+30 | Logs show a large export two weeks ago from the contractor's account |
| T+45 | The press office receives a call from a journalist |

**Decision questions.** When does the 72-hour clock start, and who writes it down? Who are the
controller and the processor here? What do we tell the regulator on day one, in phases? Do we
inform individuals, and in what words? What do we say to the journalist?

**Expected outputs.** Time of awareness, risk assessment using the
[GDPR factors](../compliance/gdpr-breach-response.md), draft notification content, holding
statement, breach register entry.

## Scenario 5 – DDoS during a business-critical period

Playbook: [DDoS Attack](../playbooks/ddos-attack-playbook.md)

**Situation.** The public website becomes slow during a promotion.

| Time | Inject |
|---|---|
| T+0 | Latency alarms and a spike in requests per second |
| T+15 | The traffic comes from thousands of addresses; the origin server is saturated |
| T+30 | An email demands payment to stop the attack |
| T+45 | The attack changes to a different protocol and the mitigation stops working |

**Decision questions.** Who calls the ISP or the DDoS provider, and what is the contact number?
What degradation is acceptable? Do we pay, and who decides? How do we check that the DDoS is not
covering a second intrusion?

**Expected outputs.** Mitigation activation steps, communication to customers, escalation record,
check for secondary activity.

## Scoring grid

Score each criterion from 1 (not met) to 4 (fully met) during the debrief.

| Criterion | 1 | 4 |
|---|---|---|
| Detection and triage | Delayed, unclear severity | Fast, severity justified with the matrix |
| Use of the playbook | Not referenced | Each decision tied to a step |
| Roles and escalation | Confusion on who decides | Clear owners, correct escalation |
| Containment decisions | Hesitation or unsafe action | Timely, proportionate, evidence preserved |
| Communication | Inconsistent or late | Accurate, timely, to the right audiences |
| Regulatory awareness | Deadlines unknown | Clock and obligations identified |
| Documentation | None | Timeline and decisions recorded |

## After-action report template

```text
Exercise:            <scenario and date>
Participants:        <roles>
Facilitator/observer:
Objectives:
What worked:
Gaps observed:         (playbook, tooling, contacts, logging, training)
Decisions that were slow or unclear:
Actions:               <action | owner | due date | linked playbook or rule>
Score grid:
Next exercise:
```

Close every action. An exercise with no closed actions is a meeting, not an improvement.

## References

- NIST SP 800-84, *Guide to Test, Training, and Exercise Programs for IT Plans and Capabilities*
- CIS Controls v8, safeguard 17.7 (conduct routine incident response exercises)
- CISA Tabletop Exercise Packages: <https://www.cisa.gov/resources-tools/services/cisa-tabletop-exercise-packages>
- ISO/IEC 27035-1, information security incident management
