# Splunk SPL — Compliance Evidence Search Generator

**Use case:** You have a control that needs log-based evidence (failed login monitoring, privileged access, configuration changes, data exports, etc.) and you want a Splunk search that produces audit-ready output instead of a wall of raw events.

Works for SOC 2 (CC6.x, CC7.x), ISO 27001 (A.5.15, A.8.16, A.8.34), HIPAA 164.312(b), NYDFS 500.06, PCI-DSS 10.x.

**Inputs you'll provide:**
- The control being evidenced
- The data source(s) in your Splunk environment (sourcetype, index)
- The audit period
- Output format the auditor will accept (CSV table, dashboard PDF, sample of raw events with annotations)

---

## Prompt

```
You are a Splunk Power User with deep experience writing SPL for SOC 2 Type II and ISO 27001 audits. You know how to write a search that produces evidence an auditor will accept on the first review — not a raw event dump that gets pushed back with "please summarize."

I need an SPL search to evidence the following control.

Control:
- Framework + reference: {{e.g., "SOC 2 CC6.6 — restricts access through identification and authentication" or "ISO 27001:2022 A.8.15 — Logging"}}
- What I'm trying to demonstrate: {{e.g., "all failed login attempts to production were reviewed within 24h", or "privileged access was reviewed quarterly", or "MFA was enforced on all admin sign-ins"}}

Splunk environment:
- Sourcetype(s): {{e.g., "ms:o365:management", "aws:cloudtrail", "syslog_okta_system"}}
- Index(es): {{e.g., "main", "security"}}
- Splunk version / context: {{e.g., "Splunk Cloud, Enterprise Security app installed" or "Splunk Enterprise 9.1, no ES"}}

Audit period: {{e.g., "earliest=-90d@d latest=@d for a Type II covering the last 90 days"}}

Output format the auditor wants: {{e.g., "summary table with one row per user, sortable by event count" / "raw events with timestamp + actor + result, exported to CSV" / "trend chart by week"}}

Please provide:

1. **The SPL search** — clean, commented, copy-pasteable. Use `tstats` where appropriate for performance. Use field renames so the output columns have human-readable names (auditors don't know what `src_user` means; they know `User`).

2. **Why this search produces good evidence** — 2-3 sentences explaining what makes the output auditor-friendly vs. a raw event dump. (e.g., "by collapsing to one row per user with first/last event timestamps + count, the auditor can see coverage across the audit period at a glance instead of scrolling 10,000 rows.")

3. **What you're assuming about my data** — fields, value formats, time fields. Auditors often catch these gaps when the search runs on real data and the fields turn out to be named differently. Flag what would need to change if my data is structured differently.

4. **A second search for the inverse / anomaly case** — e.g., if the control is "MFA enforced on admin sign-ins," the inverse is "any admin sign-in WITHOUT MFA in the audit period." Auditors increasingly ask for both directions.

5. **Tips for productionizing** — if this search will run repeatedly (e.g., as a scheduled report for the audit period), what to do: save as Report, schedule cadence, alert thresholds. Otherwise note it's a one-off.

6. **What you'd NOT include** — fields or columns I might be tempted to add that would either bloat the output or accidentally reveal something the auditor doesn't need (e.g., user IP addresses if the audit doesn't require them).
```

---

## Notes

- The "inverse / anomaly search" output is the highest-value part of this prompt. Auditors increasingly ask "show me the times this control DIDN'T work" — without that, you're handing them only happy-path evidence and they'll push back.
- For SOC 2 Type II specifically: searches that produce a SUMMARY across the audit period beat searches that produce raw events. Auditors are doing pattern review, not forensic investigation.
- Always test the search on a small time range first. The model occasionally generates SPL that works syntactically but pulls vastly more data than expected. `| head 100` saves you on the first run.
- If you're on Splunk Enterprise Security, ask the model to use ES data models (`tstats` against `Authentication`, `Change`, etc.) — much faster than `search` against raw events.
