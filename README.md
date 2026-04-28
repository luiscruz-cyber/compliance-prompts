# Compliance Prompts

Curated LLM prompts for SOC 2, ISO 27001, and security compliance workflows.

This is a working library of prompts I use (and refine) in real compliance engagements at [Boriken AI Consulting](https://borikenaiconsulting.com). Prompts here are designed for use with frontier LLMs (Claude, GPT, Gemini) to accelerate work that practitioners typically do manually — control mapping, policy gap analysis, evidence collection, audit readiness, etc.

> Prompts are tools, not authoritative output. LLM responses always need to be reviewed by a human who understands the underlying control and the client's actual environment. The point of these prompts is to compress the work, not eliminate the judgment.

## Structure

```
prompts/
├── soc2/                  SOC 2 (Trust Services Criteria) workflows
├── iso27001/              ISO 27001 (Annex A controls) workflows
├── general/               Framework-agnostic compliance work
└── meta/                  Prompts about prompts (e.g., quality review)
```

## How to use

1. Find a prompt that matches your task.
2. Read the **Inputs** section to know what context to provide.
3. Paste the prompt template into your LLM, replacing `{{placeholders}}` with your real inputs.
4. **Always review the output** — LLMs hallucinate, especially when extrapolating beyond their training data on niche compliance questions.
5. Treat the LLM as a fast first-draft generator, not an oracle.

## Why these prompts work

Prompts in this repo follow a few patterns I've found reliably effective:

- **Role assignment** — putting the LLM in the role of a specific kind of expert (e.g., "SOC 2 readiness consultant who has led 50+ Type II audits") shapes the response register and depth.
- **Explicit framework anchors** — referencing AICPA TSP-100, ISO 27001:2022, NIST CSF, etc., grounds the response in the actual standard rather than the LLM's general "compliance vibes."
- **Structured outputs** — asking for tables, ranked lists, or specific fields makes the output usable without further reformatting.
- **Calibration cues** — asking the LLM to flag what it's NOT confident about catches hallucinations that would otherwise slip through.

## Contributing / disclaimer

This is a personal working repo. PRs are welcome but the prompts reflect my opinions and engagement experience.

Nothing here is legal or compliance advice. If you're using these on a real engagement, you (or your auditor) own the final output.

— [Luis Cruz](https://github.com/luiscruz-cyber)
