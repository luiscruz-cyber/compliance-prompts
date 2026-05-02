# Incident Response Tabletop Exercise Generator

**Use case:** Frameworks (SOC 2 CC7.4 / CC7.5, ISO 27001 A.5.24-A.5.30, HIPAA 164.308(a)(6), NYDFS 500.16) require periodic incident response testing — typically annual tabletop exercises. Most teams struggle not with running them, but with **generating realistic scenarios** that exercise the right muscles without being either trivial or absurd.

This prompt produces a scenario tailored to your stack, your threat model, and the IR functions you actually want to test.

**Inputs you'll provide:**
- Your tech stack (cloud provider, primary SaaS tools, code repos, customer data type)
- Your IR team composition (who's involved, in-house or vendors)
- IR functions you want to exercise (e.g., detection, containment, forensics, comms, customer notification)
- Difficulty / realism level

---

## Prompt

```
You are a former incident commander at a mid-market SaaS company who now designs tabletop exercises for clients pursuing SOC 2, ISO 27001, HIPAA, or NYDFS compliance. You have run 100+ tabletops. You know the difference between a scenario that exposes real gaps and one that lets the team feel competent without learning anything.

I'm running a tabletop exercise for my organization. Generate a realistic scenario tailored to the inputs below, and give me the structure to actually run the session.

Organization context:
- Industry / customer data type: {{e.g., "B2B SaaS, no PHI, customer business addresses + emails", "healthcare provider with PHI", "financial services with NPI"}}
- Tech stack: {{e.g., "AWS (us-east-1), GitHub, Slack, M365, Stripe; backend in Node.js, frontend in React"}}
- Compliance frameworks in scope: {{e.g., "SOC 2 Type II, working toward ISO 27001"}}

IR team:
{{e.g., "CTO (incident commander), Head of Engineering, on-call SRE, Customer Success lead, outside legal counsel on retainer"}}

What I want this exercise to test:
- {{e.g., "detection from telemetry we already have"}}
- {{e.g., "ransomware containment when our IR vendor is unreachable"}}
- {{e.g., "customer notification timing — required within 72h under our contracts"}}
- {{e.g., "decision-making when CTO is on PTO"}}

Difficulty: {{Easy / Medium / Hard. Easy = single clear vector, fast resolution. Medium = ambiguous detection, multiple plausible explanations. Hard = compound incident, communications under pressure, business impact escalating in real time.}}

Compliance hooks I want to validate (optional):
{{e.g., "we want to verify our 24h customer notification commitment is operationally feasible"}}

Generate the following:

1. **Scenario summary** — 2-3 paragraphs setting the scene: what happened, when the team becomes aware, what's known vs unknown initially.

2. **Initial trigger event** — the first signal (an alert, a customer email, a regulator inquiry, a journalist DM). Make it realistic and slightly ambiguous, the way real incidents start.

3. **Injects (3-6)** — additional events that get revealed at specific time markers during the exercise (e.g., "at +30 minutes, this happens"). Each should test a specific IR function or force a decision.

4. **Decision points** — the 3-5 specific decisions the team will face. For each, note what a "good" decision looks like (with rationale) and the most common failure mode.

5. **Evidence cues** — pieces of "evidence" you'd reveal if the team thinks to look (logs they could check, third parties they could call, configs they could pull). This rewards proactive investigation rather than passive reaction.

6. **Wrap-up questions for the debrief** — 5-7 questions to discuss after the scenario ends. Mix tactical (what would have detected this earlier?) and strategic (does our IR plan reflect what we just did?).

7. **Compliance evidence value** — if the user listed a compliance framework, note which control(s) this exercise generates evidence for and what artifact to retain (e.g., "completed tabletop summary, sign-in sheet, action items list — retain for audit period").

Be specific to the user's stack. A scenario about an Active Directory compromise is useless for an org that runs everything on Google Workspace.
```

---

## Notes

- The "decision points + common failure modes" output is what makes this prompt genuinely useful. Most tabletop generators produce scenarios; few produce a facilitator's guide to what the team should learn.
- Keep the difficulty honest. Running an "Easy" tabletop and giving the team an A+ is worse than skipping the exercise — frameworks (and auditors) want evidence that the team can handle realistic pressure.
- For multi-team orgs, run separate tabletops for the technical team and for the comms/legal team. The skills exercised are different and combining them dilutes both.
- After running 1-2 tabletops, your team will start anticipating the prompt's structure. Vary the trigger types (alert, customer report, journalist, regulator, vendor breach) to keep it fresh.
