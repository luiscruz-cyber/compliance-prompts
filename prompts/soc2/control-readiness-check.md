# SOC 2 — Control Readiness Check

**Use case:** You have a description of how a control is currently implemented and want a quick read on whether it's likely to pass an SOC 2 Type II audit, what an auditor will probe, and what evidence to gather.

**Inputs you'll provide:**
- The Trust Services Criterion or specific control reference (e.g., CC6.1, CC7.2)
- A short description of the current implementation
- Your audit period (e.g., "6 months starting July 2026")

---

## Prompt

```
You are an experienced SOC 2 readiness consultant who has led 50+ Type II audits across SaaS companies of various sizes. You have seen which controls auditors push back on and which sail through.

I'm assessing readiness for SOC 2 Type II under AICPA TSP Section 100 (Trust Services Criteria for Security, Availability, Processing Integrity, Confidentiality, and Privacy — 2017 with revised points of focus).

Trust Services Criterion: {{e.g., CC6.1 — Logical and physical access controls}}

Current implementation:
{{2-5 sentences describing how this control is currently implemented in the org. Include tools, frequency, owner if known.}}

Audit period: {{e.g., "Type II covering July 1 2026 – December 31 2026"}}

Please respond with the following structure:

1. **Likelihood of passing as-is** (rate as Strong / Moderate / Weak / Likely Fail)
2. **Why** — 2-4 bullets on what's working and what's missing relative to the points of focus for this criterion
3. **What an auditor will probe** — the 3-5 specific questions / evidence requests an auditor will likely ask
4. **Evidence to collect** — for each probe above, the specific artifact (screenshot, log export, policy excerpt, ticket, etc.) that would best demonstrate operating effectiveness across the audit period
5. **Top 1-2 remediation actions** — if there are gaps, what should be fixed BEFORE the audit period starts (or before the next observation window)
6. **What you're NOT confident about** — flag any aspect of my description that's ambiguous or that you'd need to clarify before giving a stronger opinion
```

---

## Notes

- The "what you're NOT confident about" line is doing a lot of work here. Without it, models confidently fill in details that turn out to be wrong (e.g., assuming the org has a SIEM when nothing in your description said so).
- For multi-control batches, run this prompt per-control rather than asking the model to evaluate 10 at once. Quality drops sharply when you batch.
- Pair the model's output with a quick read of the actual TSP point-of-focus text for that criterion. The points of focus update — the model's training data may lag.
