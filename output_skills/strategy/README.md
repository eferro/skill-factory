# Strategy Skills Index

This directory contains skills focused on strategic thinking, decision-making, and pressure-testing high-stakes choices.

## Available Skills

| Skill | What it is for |
| --- | --- |
| [`strategy-kernel`](./strategy-kernel/SKILL.md) | Coaches through Rumelt's Strategy Kernel (diagnosis, guiding policy, coherent action) to build sound strategy. |
| [`customer-okrs`](./customer-okrs/SKILL.md) | Coaches teams to write OKRs as customer behavior change (Who does what by how much, Gothelf and Seiden) rather than tasks, outputs, or system metrics. |
| [`llm-council`](./llm-council/SKILL.md) | Runs a question through 5 AI advisors with different thinking styles, anonymous peer review, and chairman synthesis to pressure-test decisions with stakes. |

## Skill Origins

- `llm-council` — Adapted from Ole Lehmann's skill (shared by Charlie J. Hills: https://x.com/charliejhills/status/2049140787200528725). Built on Andrej Karpathy's [LLM Council](https://github.com/karpathy/llm-council) methodology: dispatch the same query to multiple models, have them peer-review anonymously, then synthesize via a chairman. This skill applies that pattern using Claude sub-agents with different thinking lenses (Contrarian, First Principles, Expansionist, Outsider, Executor) instead of different model providers.

## Notes

- Each skill lives in its own folder.
- The primary entry point for each one is its `SKILL.md` file.
