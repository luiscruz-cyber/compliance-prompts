# Evidence Collection Helper

**Use case:** You have a control to demonstrate (for an audit, a customer security questionnaire, or a regulator) and you want a structured list of the specific artifacts that would actually satisfy a reviewer — without over-collecting.

Framework-agnostic. Works for SOC 2, ISO 27001, HIPAA, NYDFS, PCI-DSS, etc.

**Inputs you'll provide:**
- The control or requirement reference
- The framework
- A short description of how the control is implemented
- The reviewer audience (auditor, customer, regulator, internal)

---

## Prompt

```
You are an experienced compliance practitioner who has been on both sides of audits — preparing evidence packages and reviewing them. You know the difference between evidence that demonstrates operating effectiveness and evidence that just looks like it does.

I need to gather evidence for the following:

Framework: {{e.g., SOC 2 Type II, ISO 27001:2022, NYDFS 23 NYCRR 500}}
Control / requirement: {{e.g., SOC 2 CC6.6, NYDFS 500.07, ISO A.8.5}}
Reviewer audience: {{auditor / customer / regulator / internal}}
How the control is implemented:
{{2-4 sentences}}
Audit period or point-in-time: {{e.g., "Operating effectiveness across 7/1/2026 – 12/31/2026" or "Point-in-time as of today"}}

Please respond with:

1. **Evidence categories needed** — the 3-5 categories of evidence that, taken together, demonstrate this control. (e.g., "policy reference," "configuration snapshot," "operational log sample," "review record")

2. **For each category — specific artifacts** — what to collect (file format, source system, screenshot vs export, sample size for periodic operations). Be specific enough that a junior team member could collect it without further guidance.

3. **What auditors REJECT or push back on** — common evidence types that look fine but get rejected (e.g., screenshots without timestamps, policy without effective date, sample sizes that aren't representative of the audit period). Flag the equivalents for this control.

4. **Sample size guidance** for any periodic evidence (e.g., "monthly access reviews — pull 3 from the audit period: first month, midpoint, last month").

5. **Naming convention** — suggest a consistent file naming pattern for the evidence so it's easy to organize and reference later (e.g., "CONTROL-CC6.6_EVIDENCE-01_AccessReview_2026-09.pdf").

6. **Things I might be missing about my own implementation** — if my description above is light on a particular detail (frequency, ownership, scope), call it out so I can clarify before collecting evidence.
```

---

## Notes

- The "what auditors REJECT" section is the highest-value part of this prompt. Most evidence collection guides tell you what to gather; few tell you what gets thrown back.
- For SOC 2 Type II especially, sample size and date coverage are the two things that get pushed back on most often. The prompt explicitly asks for sample size guidance.
- Pair the output with your auditor's published "PBC list" (Provided By Client) if you have one. They'll often be more specific than the prompt's output for your engagement.
