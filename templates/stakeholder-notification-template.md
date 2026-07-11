# Template: Stakeholder Notification

Use this as the base structure for any incident notification, internal or external. Fill in
brackets; delete sections that don't apply. Severity-specific and incident-type-specific
quick-reference wording lives in each playbook's own Communication Templates section — this file
is the general-purpose structure underneath those.

---

## Internal notification (SOC → IT Leadership / CISO)

**Subject:** [SEVERITY] — [Incident type] — [one-line description]

**Status:** [Detected / Investigating / Contained / Eradicated / Recovering / Resolved]

**Summary:** [2–3 sentences: what happened, what's affected, what's being done]

**Severity:** [Critical/High/Medium/Low] — [one-line justification]

**Impact:**
- Systems/services affected: [list]
- Users/customers affected: [count/scope if known]
- Business impact: [description]

**Actions taken so far:**
- [Bulleted list of containment/response actions]

**Next steps:**
- [What happens next, and by when]

**Next update:** [time or trigger condition, e.g. "on material change" for active incidents]

**Incident owner:** [name/role] · **Contact:** [contact method]

---

## External notification (customers/partners)

**Subject:** [Clear, non-alarmist subject reflecting actual severity]

**What happened:** [Factual, plain-language description — no jargon, no speculation beyond
confirmed facts]

**What we've done:** [Containment/remediation actions taken]

**What you should do:** [Specific, actionable guidance if any — e.g. reset password, monitor
statements, no action needed]

**Who to contact:** [Dedicated incident contact/hotline, not a generic support queue, for
incident-related questions]

**Note:** Any external/customer-facing communication involving regulated data, financial impact,
or reputational risk must be reviewed and approved by Legal/Compliance and Communications/PR
before sending — this template is a technical starting point, not approved-for-send copy.

---

## Executive/board summary (for Critical-severity incidents)

**Incident:** [name/ID] · **Date detected:** [date] · **Status:** [current status]

**What happened:** [1 paragraph, plain language, no unnecessary technical detail]

**Business impact:** [customers affected, revenue impact, regulatory exposure, reputational
considerations]

**Response summary:** [key actions taken, current containment status]

**Outstanding risk:** [what's still open/unresolved]

**Regulatory/legal status:** [notification obligations determined, notifications sent/pending —
provided by Legal/Compliance]

**Recommended decisions needed from leadership (if any):** [e.g. public disclosure timing,
customer compensation, resource authorization]
