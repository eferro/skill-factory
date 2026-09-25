# Credits

Adapted from Ole Lehmann's LLM Council skill, shared by Charlie J. Hills:
https://x.com/charliejhills/status/2049140787200528725

Built on Andrej Karpathy's LLM Council methodology:
https://github.com/karpathy/llm-council

Karpathy's version dispatches the same query to multiple models, has them
peer-review each other anonymously, then a chairman synthesizes the answer.
This skill applies the pattern with Claude sub-agents using different thinking
lenses (Contrarian, First Principles, Expansionist, Outsider, Executor) instead
of different model providers.

## Local changes

- Added `STARTER_CHARACTER` per this repo's convention.

Also recorded in `output_skills/strategy/README.md` (Skill Origins).
