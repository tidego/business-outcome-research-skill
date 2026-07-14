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

Do not force it onto ordinary, fully specified local coding tasks. The public evaluation found no correctness lift when it was injected into unrelated software-engineering tasks and measured a token penalty. See [evaluation/SWE_SKILLS_BENCH.md](evaluation/SWE_SKILLS_BENCH.md) and the accompanying essay [Skill 到底有没有用？一次没有提升的编程基准实验](https://guzhaolin.art/blog/agent-skill-evaluation).

## Design note

The payment-lifecycle example behind this Skill is documented in [AI 为什么永远还能再找出一个 P0？](https://guzhaolin.art/blog/ai-p0-review-loop). A 90-day voucher could not be protected by a payment product that released ordinary profit-sharing funds after 30 days. The mismatch was visible only after the product deadline, merchant authority, and refund obligation were checked together.

## License

MIT.
