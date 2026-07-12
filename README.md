# Business Outcome Research Skill

An evidence-first Codex Skill for high-impact product, architecture, payment, compliance, marketplace, and operational decisions.

It requires the agent to reconstruct the complete business and code lifecycle, verify current primary sources and eligibility, distinguish defects from product choices, respect the business owner's authorized scope, and make one feasible recommendation.

## Install

```bash
git clone https://github.com/tidego/business-outcome-research-skill.git
cp -R business-outcome-research-skill/business-outcome-research ~/.codex/skills/
```

The Skill declares Exa MCP as an external research dependency in `agents/openai.yaml`.

## Appropriate use

Use it when a locally correct technical answer could still cause financial loss, an incomplete refund or settlement lifecycle, a compliance failure, unsafe authorization changes, or an unavailable product recommendation.

Do not force it onto ordinary, fully specified local coding tasks. The public evaluation found no correctness lift when it was injected into unrelated software-engineering tasks and measured a token penalty. See [evaluation/SWE_SKILLS_BENCH.md](evaluation/SWE_SKILLS_BENCH.md).

## License

MIT.
