# Risk Assessment Methodology

How the five playbooks in this repository connect to risk management: which risks each playbook
treats, how those risks are scored, and when a risk must be escalated to a management decision.

**Author:** Omar Babba · **Status:** Living document · **Last updated:** 2026-10-09

## Why risk management belongs next to incident response

A playbook describes what to do *after* something goes wrong. A risk assessment explains *why*
that playbook exists, how likely and how damaging the scenario is, and whether the controls that
prevent or detect it are good enough. NIST SP 800-61 Rev. 3 makes the same point by folding
incident response into continuous risk management under CSF 2.0 (Govern, Identify, Protect,
Detect, Respond, Recover). This folder makes that link explicit for the five scenarios covered
here.

## Frameworks used

| Source | What this repo takes from it |
|---|---|
| [NIST SP 800-30 Rev. 1](https://csrc.nist.gov/pubs/sp/800/30/r1/final), *Guide for Conducting Risk Assessments* | Risk model: threat source, threat event, vulnerability, likelihood, impact; qualitative scales |
| [ISO/IEC 27005](https://www.iso.org/standard/80585.html) | Process: identify, analyse, evaluate, treat, monitor; risk register as the core record |
| [NIST CSF 2.0](https://www.nist.gov/cyberframework) | Govern function: risk appetite and ownership; mapping of controls to Protect, Detect, Respond, Recover |
| This repo's [severity matrix](../README.md#severity-matrix-used-consistently-across-all-five-playbooks) and [impact classification](../README.md#incident-impact-classification-nistcisa-aligned) | Incident-time severity; reused to calibrate the impact scale below |

## Process

1. **Identify the scenario.** One scenario per playbook: a threat source exploiting a weakness
   to cause an incident of that type.
2. **Analyse.** Score likelihood and impact on a 1 to 5 scale (definitions below), before and
   after the existing controls.
3. **Evaluate.** Compare the score to the risk appetite thresholds.
4. **Treat.** Choose a treatment (reduce, accept, transfer, avoid), name an owner and a date.
5. **Monitor.** Track key risk indicators (KRIs) and review the register on a fixed cadence and
   after every Critical or High incident.

## Likelihood scale

| Score | Level | Description |
|---|---|---|
| 1 | Rare | Not expected within three years; no known recent attempts |
| 2 | Unlikely | Could occur once within one to three years |
| 3 | Possible | Could occur within the year; similar events seen in the sector |
| 4 | Likely | Expected several times a year; attempts already observed |
| 5 | Almost certain | Occurs monthly or more; continuous attempts |

## Impact scale

Impact is the highest of the three NIST/CISA axes used in this repo (Functional Impact,
Information Impact, Recoverability), expressed on one scale so that it can be multiplied by
likelihood.

| Score | Level | Functional impact | Information impact | Recoverability |
|---|---|---|---|---|
| 1 | Negligible | No service affected | No data affected | Regular, under 1 hour |
| 2 | Minor | Non-critical service briefly degraded | Small non-sensitive dataset | Regular, under 1 day |
| 3 | Moderate | Some business services degraded | Limited personal or internal data | Supplemented, days |
| 4 | Major | Significant services down | Large personal or proprietary dataset; integrity loss | Extended, weeks |
| 5 | Severe | Organisation-wide loss of a critical function | Regulated or critical data destroyed or exfiltrated | Not recoverable, or external assistance required |

## Risk matrix and appetite

Risk score = likelihood x impact.

| Score | Level | Required response | Decision owner |
|---|---|---|---|
| 17 to 25 | **Critical** | Treatment plan within 30 days; formal management decision on any acceptance | Executive management |
| 10 to 16 | **High** | Treatment plan within 90 days; acceptance requires CISO sign-off | CISO |
| 5 to 9 | **Medium** | Treatment planned in the normal roadmap; acceptance by the risk owner | Risk owner |
| 1 to 4 | **Low** | Monitor; accept by default | Risk owner |

These thresholds are an example appetite. An organisation sets its own and records it in the
register header.

## Treatment options

| Option | Meaning | Example in this repo |
|---|---|---|
| Reduce | Add or improve controls to lower likelihood or impact | MFA, email filtering, tested backups, rate limiting |
| Accept | Knowingly keep the residual risk, with an owner and a review date | Residual DDoS risk on a non-critical public site |
| Transfer | Share the financial impact | Cyber insurance, DDoS protection from an ISP or CDN |
| Avoid | Stop the activity that creates the risk | Retire an exposed legacy service |

## Key risk indicators

KRIs turn the playbooks into measurable signals. Each scenario in the
[scenario register](incident-risk-scenarios.md) lists the ones that matter for it. Typical examples:

- Phishing report rate and click rate in simulations
- Mean time to acknowledge and to contain, per severity (from the Post-Incident Review template)
- Share of privileged accounts protected by phishing-resistant MFA
- Age of the last successful backup restore test
- Number of incidents closed without a lessons-learned review

## Review cadence

- **Quarterly:** full register review, together with the quarterly playbook review.
- **After every Critical or High incident:** update the likelihood and impact of the related
  scenario using the Post-Incident Review, and check whether the residual score still matches
  reality.
- **On material change:** new system, new supplier, new regulation.

## Limits

The scores in this repository are an **illustrative worked example for a generic mid-size
organisation**, not the result of a real assessment. They show the method and the link to the
playbooks. A real assessment needs the organisation's own assets, controls, incident history
and risk appetite.
