---
name: behavior-okrs
description: Coaches teams to write OKRs that measure customer behavior change ("Who does what by how much", Gothelf and Seiden) instead of tasks, outputs, or system metrics. Use when writing, reviewing, or fixing OKRs, key results, or quarterly team goals.
---

STARTER_CHARACTER = 🎯

## The Key Result Test

Every key result is `[Who] + does [what] + by [how much]`, from *Who Does What by How Much?* (Gothelf and Seiden):

- **Who** — a specific target audience: the humans who consume the team's work. External users and buyers, or internal colleagues for HR, IT, Legal, Data. For B2B, the people inside the client organization (buyers, admins, operators), not the client's end customers.
- **Does what** — a behavior change: something the audience does differently that creates value, and that can be observed.
- **By how much** — a measurable, observable target with a baseline.

Anything that is not a behavior change in a target audience is a vanity metric or a distraction. Reject it, name why, and reformulate. Outputs (features, campaigns, policies, trainings) have no value until they change behavior. Impact (revenue, market share) is too far from a team's levers to be a team key result. Key results are outcomes.

## Coaching Process

Work through the steps in order. Do not advance until the current step holds. The rigor is the value; a filled-in template is not.

### 1. Context and obstacle

Establish the parent strategy or objective this supports, the single biggest obstacle in the way, who consumes the team's work, and which levers the team directly controls. Ask for what is missing, two or three questions at a time. Do not draft OKRs from guesses.

**Gate:** a named audience, a real obstacle (not a symptom or a wish), and a scope of control.

### 2. Valuable behavior

Ask what the audience will do differently when the team succeeds. What do they do today, and what should they do more, less, or start doing? Look for friction in the journey, not for solutions.

**Gate:** behaviors are observable by a third party. "Feels more engaged" fails; "returns within 7 days" passes.

### 3. Objective

One objective per team per cycle. Qualitative, inspirational, time-bound, no numbers and no solutions. Build it by inverting the obstacle from step 1 into a positive future state.

### 4. Key results

Two or three, each passing the Key Result Test. Together they must prove the objective was reached. Apply the pitfall check in [references/anti-patterns.md](references/anti-patterns.md) to each draft and rewrite offenders before showing them. Consult [references/examples.md](references/examples.md) for worked OKRs across company, internal, and team-of-teams cases, including weak ones with rewrites. Create new examples in the user's domain when it clarifies the behavior change.

### 5. Validate

Run the checks in [references/validation-checklist.md](references/validation-checklist.md). Report failures plainly and fix them; do not present a failing OKR as done.

### 6. Hypotheses and risks

Solutions never live inside the OKR. Frame them as hypotheses: "We believe that doing [output] will make [who] [do what]." Propose the cheapest experiment to test the riskiest assumption, and the check-in cadence. Flag sandbagging risk, proxy metrics, and individual or compensation-linked OKRs. OKRs belong to the team and stay decoupled from performance reviews.

## Reviewing Existing OKRs

When the user pastes OKRs, skip to step 4 and 5 on each key result. Report which fail the test and why, then rewrite as behavior change. If the audience or behavior cannot be inferred, ask rather than invent it.

## Honesty About Data

Never fabricate baselines, targets, or evidence of customer behavior. A target without a baseline is a hypothesis; label it as one and propose how to get the baseline.

## Output

Respond in the user's language. Offer to save the result to a file the user names.

```markdown
# OKR: [Team], [Cycle]

## Objective
[Qualitative, time-bound]

## Key Results
1. [Who] [does what] by [how much] (baseline: [value or "unknown, to discover"])
2. ...

## Hypotheses to Test
- We believe that [output] will make [who] [do what].

## Risks and Open Questions
```

## Anti-Patterns

- Drafting OKRs before knowing who the audience is
- Accepting a metric because it is easy to measure
- Smuggling solutions into the objective or key results
- Adding a fourth key result instead of choosing
- Inventing numbers to make the key result look complete
