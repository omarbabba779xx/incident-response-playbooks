# Incident Response Metrics and KPIs

What to measure, how to define each timestamp, and how to turn the Post-Incident Review into
numbers that show whether the playbooks work.

**Author:** Omar Babba · **Status:** Living document · **Last updated:** 2026-10-09

## Why measure

A playbook that is never measured cannot be improved. The metrics below answer four questions:
how fast do we notice, how fast do we react, how fast do we stop it, and do we learn from it. They
also feed the key risk indicators of the [risk scenarios](../risk/incident-risk-scenarios.md).

## Timestamps every case must record

Record each in UTC, with the source of the value, in the case itself.

| Field | Meaning |
|---|---|
| `t_compromise` | Estimated start of the malicious activity (often found during analysis) |
| `t_detected` | First moment a control or a person produced a usable signal |
| `t_alert_raised` | Alert visible to the SOC queue |
| `t_acknowledged` | An analyst took ownership |
| `t_aware` | The organisation has reasonable certainty of the incident (starts regulatory clocks, see the [GDPR procedure](../compliance/gdpr-breach-response.md)) |
| `t_contained` | Spread stopped (host isolated, account disabled, address blocked) |
| `t_eradicated` | Attacker access and persistence removed |
| `t_recovered` | Service back to normal operation |
| `t_closed` | Case closed after the Post-Incident Review |

## Core metrics

| Metric | Definition | Formula |
|---|---|---|
| **Dwell time** | How long the attacker was present before detection | `t_detected - t_compromise` |
| **MTTD** (mean time to detect) | Average detection delay for known incidents | mean of `t_detected - t_compromise` |
| **MTTA** (mean time to acknowledge) | Delay between alert and analyst ownership | mean of `t_acknowledged - t_alert_raised` |
| **MTTC** (mean time to contain) | Delay between detection and containment | mean of `t_contained - t_detected` |
| **MTTR** (mean time to recover) | Delay between detection and service recovery | mean of `t_recovered - t_detected` |
| **Notification timeliness** | Share of regulated breaches notified inside the legal deadline | notified in time / notifiable breaches |

Report the **median and the 90th percentile** together with the mean. A few long incidents distort
a mean, and the 90th percentile shows how bad a typical bad day is.

## Targets by severity

Initial response times come from the repo's [severity matrix](../README.md#severity-matrix-used-consistently-across-all-five-playbooks).
Containment targets are an example to adapt.

| Severity | Acknowledge (MTTA) | Contain (MTTC, example) | Review completed |
|---|---|---|---|
| Critical | Immediate (page on-call) | 4 hours | 5 business days |
| High | Under 30 minutes | 1 business day | 10 business days |
| Medium | Under 2 hours | 3 business days | 15 business days |
| Low | Next business day | Not applicable | Monthly batch |

## Quality and process metrics

| Metric | Why it matters |
|---|---|
| False-positive rate per detection rule | Drives tuning and analyst fatigue |
| Escalation accuracy (alerts escalated and confirmed / alerts escalated) | Shows whether Tier 1 triage works |
| Reopen rate | Cases closed too early |
| Share of cases with a completed Post-Incident Review | Learning discipline |
| Share of playbook steps followed (spot-check) | Whether the playbooks are used |
| Evidence completeness (chain of custody filled) | Readiness for legal or regulatory follow-up |
| Exercises per year and actions closed | See [tabletop exercises](../exercises/tabletop-exercises.md) |

## Computing the metrics

If cases are stored in a table, the median and 90th percentile per severity over 90 days is a
single query. Example in PostgreSQL:

```sql
SELECT severity,
       count(*) AS cases,
       percentile_cont(0.5) WITHIN GROUP (ORDER BY acknowledged_at - alert_raised_at) AS median_mtta,
       percentile_cont(0.9) WITHIN GROUP (ORDER BY acknowledged_at - alert_raised_at) AS p90_mtta,
       percentile_cont(0.5) WITHIN GROUP (ORDER BY contained_at - detected_at)        AS median_mttc
FROM   incident_cases
WHERE  detected_at >= now() - interval '90 days'
GROUP  BY severity
ORDER  BY severity;
```

The same logic works in a SIEM or a case management tool as long as the timestamps above are stored
as fields and not only as free text.

## A measured example from a lab

The author's [SocForge](https://github.com/omarbabba779xx/soc-detection-lab) lab follows one
simulated attack from detection to case closure and records the timings: the SIEM raised the alert
within 1 to 7 seconds, the attacker's address was blocked 24 seconds after the alert reached the
orchestrator, the host isolation order went out at 29 seconds, and a threat hunt was requested at
35 seconds. These are lab figures on a single simulated attack with automation, not a benchmark for
a production SOC, but they show the kind of evidence a metrics page should rest on.

## Common pitfalls

- **Unclear start and stop.** Define each timestamp once, in writing, and keep it.
- **Averages only.** Use median and 90th percentile.
- **Measuring what is easy.** Alert counts say little; time to contain and quality of learning say more.
- **Gaming.** If analysts are judged on MTTA alone, they will acknowledge without working. Pair speed
  with quality metrics.
- **No feedback.** A metric with no owner and no action is decoration. Each one should map to a
  decision: tune a rule, change a threshold, add a playbook step.

## Review

Review the dashboard monthly with the SOC lead, and quarterly with the risk owner, using the same
meeting as the register review described in the
[risk assessment methodology](../risk/risk-assessment-methodology.md).

## References

- NIST SP 800-61 Rev. 2, section on post-incident activity and incident data
- CIS Controls v8, safeguard 17.9 (establish and maintain security incident thresholds) and 17.8 (post-incident reviews)
- ISO/IEC 27035-1, information security incident management, lessons learned phase
