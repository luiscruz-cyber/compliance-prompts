# ISO 27001 — Policy Gap Analysis

**Use case:** You have an existing policy document (Information Security Policy, Access Control Policy, etc.) and want to know what's missing, weak, or out of alignment with ISO 27001:2022 Annex A controls before submitting it to an external auditor or your ISMS review.

**Inputs you'll provide:**
- The full text of the policy (or a representative excerpt)
- The ISO 27001 Annex A controls the policy is meant to address
- Your organization's industry / size if relevant for context

---

## Prompt

```
You are an ISO 27001 Lead Auditor with deep experience reviewing policies from small and mid-size organizations seeking certification under ISO/IEC 27001:2022 (which superseded ISO 27001:2013 with the updated 93-control Annex A structure).

I'm doing a self-review of a policy before submitting it to my external auditor / management review. Please give me a structured gap analysis.

Annex A controls this policy is meant to address:
{{e.g., A.5.1, A.5.10, A.8.1 — list specific controls or control families}}

Organization context:
{{1-2 sentences: industry, size, regulatory environment if any}}

Policy text:
"""
{{paste the policy text here}}
"""

Please respond with the following structure:

1. **Overall coverage** — which Annex A controls (from those listed above) does this policy adequately address? Which ones does it miss or only partially cover?

2. **Critical gaps** — specific clauses that an ISO 27001 auditor would flag as missing or insufficient. For each, cite the relevant Annex A control reference and one-sentence rationale.

3. **Alignment with ISMS expectations** — does the policy align with the broader ISMS requirements in clauses 4-10 of ISO 27001 (e.g., clear ownership, review cadence, links to risk treatment, references to supporting procedures)? If not, what's missing?

4. **Tone / specificity issues** — any places where the policy is so vague that operational implementation could go in any direction (auditors flag these as "policy without teeth"), or so specific that it boxes you into impractical commitments.

5. **Suggested additions** — concrete language to add for the top 3 gaps. Provide draft sentences I could paste in (clearly marked as draft and noting I should adapt to my org's reality).

6. **Things to verify before relying on this analysis** — flag any places where you're inferring intent from ambiguous policy language and could be wrong about my actual practice.
```

---

## Notes

- This prompt is meant to be a first pass before paying a consultant or your auditor for a formal gap analysis. It will catch the obvious stuff but won't catch issues that only an auditor familiar with your specific environment would see.
- ISO 27001:2022's 93-control Annex A is significantly restructured from 2013's 114 controls. If your policy was written against 2013, much of the "alignment" output will be about porting to 2022 references.
- For multi-policy reviews (e.g., your full ISMS policy stack), run this prompt per policy. Models lose track of cross-policy consistency when given everything at once.
