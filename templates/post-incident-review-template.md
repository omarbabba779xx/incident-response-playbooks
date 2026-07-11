# Template: Post-Incident Review (Lessons Learned)

Complete within 5 business days of incident closure (immediately for Critical-severity
incidents — don't wait the full window). The goal of this document is process improvement, not
blame assignment — frame findings around "what changed as a result," not "who missed it."

---

**Incident ID:** [ID/name]
**Incident type:** [Phishing / Malware / Account Compromise / Data Breach / DDoS]
**Severity:** [Critical / High / Medium / Low]
**Date/time detected:** [timestamp] · **Date/time resolved:** [timestamp]
**Total duration:** [detection to closure]
**Playbook used:** [link to the specific playbook]
**Reviewers present:** [names/roles]

## Timeline

| Time | Event |
|---|---|
| [timestamp] | [Initial trigger/detection] |
| [timestamp] | [Key response action] |
| ... | ... |
| [timestamp] | [Containment achieved] |
| [timestamp] | [Eradication complete] |
| [timestamp] | [Recovery/closure] |

## Root cause

[What actually caused the incident — the underlying vulnerability, gap, or condition, not just
the immediate trigger. "User clicked a phishing link" is the trigger; "no URL sandboxing at the
email gateway" or "MFA was push-approval only, vulnerable to fatigue attacks" is closer to root
cause.]

## What went well

- [What worked as designed — detection fired correctly, escalation happened on time, playbook
  step X was clear and effective, etc.]

## What didn't go well / gaps identified

- [Detection gap: did existing tooling catch this, or was it found some other way?]
- [Process gap: did the playbook cover this scenario? Was an escalation step unclear or
  skipped?]
- [Tooling gap: did the analyst have the access/tooling needed, or was there friction/delay?]
- [Communication gap: did stakeholders get timely, accurate information?]
- [Time-to-detect / time-to-contain: how does this compare to target SLA, and why the gap if
  any?]

## Metrics

| Metric | Value |
|---|---|
| Time to detect (incident start → alert/report) | [duration] |
| Time to acknowledge (alert → analyst response) | [duration] |
| Time to contain (acknowledge → containment achieved) | [duration] |
| Time to eradicate | [duration] |
| Time to full recovery | [duration] |
| Total records/systems/users affected | [count] |

## Action items

| Action item | Owner | Due date | Priority |
|---|---|---|---|
| [Specific, assignable fix — e.g. "add rate-limiting to /api/login endpoint"] | [name/team] | [date] | [High/Medium/Low] |
| [Playbook update needed] | [name/team] | [date] | [priority] |
| [Tooling/access gap to close] | [name/team] | [date] | [priority] |

## Playbook feedback

- [ ] Playbook covered this scenario adequately — no changes needed
- [ ] Playbook needs updating — [specify what: missing decision branch, unclear escalation
      trigger, outdated tool reference, etc.]

## Sign-off

**Prepared by:** [name] · **Reviewed by:** [SOC Lead/CISO] · **Date:** [date]
