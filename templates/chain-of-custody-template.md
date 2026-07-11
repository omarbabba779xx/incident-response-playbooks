# Template: Evidence Chain of Custody

Use for any evidence item that may support HR/legal action, law enforcement referral, regulatory
inquiry, or litigation. Every transfer of custody — collection, storage, analysis, handoff to
another party — must be logged here. Gaps in this log can undermine the evidentiary value of the
item entirely, regardless of how the incident itself was handled.

---

**Incident ID:** [ID/name] · **Evidence item #:** [sequential number]

## Item description

- **Type:** [e.g. disk image, memory capture, email export, log export, physical device]
- **Source:** [system/account/device the evidence came from]
- **Collection method:** [tool used, e.g. FTK Imager, KAPE, EDR export]
- **Collection date/time:** [timestamp, with timezone]
- **Collected by:** [name]
- **Hash value (at collection):** [SHA256 or equivalent — compute immediately upon collection]
- **Storage location:** [where the evidence is stored, with access controls noted]

## Custody log

| Date/time | From | To | Purpose | Hash verified? |
|---|---|---|---|---|
| [timestamp] | [collector] | [evidence storage/analyst] | Initial collection | [Y, hash: ...] |
| [timestamp] | [name] | [name] | [reason for transfer, e.g. "forensic analysis"] | [Y/N] |
| ... | ... | ... | ... | ... |

## Analysis log

| Date/time | Analyst | Action performed | Findings summary |
|---|---|---|---|
| [timestamp] | [name] | [e.g. "extracted process tree from memory image"] | [brief finding] |

## Final disposition

- [ ] Retained per data retention policy — retention period: [duration]
- [ ] Transferred to law enforcement — recipient: [agency/contact], date: [date]
- [ ] Transferred to external counsel/forensics firm — recipient: [firm], date: [date]
- [ ] Destroyed per retention policy — date: [date], authorized by: [name]

**Notes:** [Any anomalies, gaps, or special handling considerations for this item]
