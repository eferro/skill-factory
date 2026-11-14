# Kent Beck's Thinkies Catalog

All Thinkies in this catalog were created and curated by Kent Beck (https://kentbeck.com/).

## General Principles

- A Thinkie is a habit of thought that generates an idea given some context
- Each Thinkie consists of a **Pattern** (situation to recognize) and a **Transformation** (action to apply)
- The process: Match the pattern, apply the transformation, then evaluate results
- Focus on *generating ideas*, not necessarily *good ideas*
- Many applications won't yield useful results—don't be discouraged
- Separate idea generation from judgment; pre-judging prevents effectiveness
- Thinkies help shift perspectives from "local minima" and unstick thinking

## Categories

**Language-oriented Thinkies:** Manipulating syntax and words being used
**Project Management Thinkies:** Related to how projects are managed and seen
**Models:** Using mental models or analogies to view situations
**Frames:** Re-framing troublesome situations

---

## Index

Search this file with grep for a name (e.g. `grep -n "### .*Half in Half"`) instead of reading it whole.

"Obviously...", Abundance, Break Dependency, Can't/Because, Customer's Voice, Dependency Merging, Direct Feedback, Goldilocks & The 3 Tradeoffs, Half in Half, Incongruence, Laughter, Personal Feedback, Project Buffer First, Reverse Phrase, Serialize, Shift Left & Right, 1, 10, 100, Compared to What? (CTW?), Contradiction, Defer Decision, Else?, End To End, Envelope Calculation, Force Decision, Grow Then Split, Half Wavelength Shift, Just Apply, Latency, Throughput, & Variance, Match the Pipes, McDonald's, Measure Later, Measure Sooner, Measure What Matters, Parallel Decision, Rate-Limiting Resource, Reduce Utilization, Self-description, Separate Observation From Judgement, Special-Cause Versus Common-Cause Variation, Tradeoff, Upside/Downside, Work/Wait Ratio, Agreements, Analogy, And Then…, But If You Could..., Composed Solution, Easy Bit, Explore or Extract? (Explore/Exploit), Exponential Growth / Growth Rate, Not Absolute Number, Extrapolate Further, Fun Bit, Hard Problem, Hill Climbing, Invert the Goal, Legibility, More General Solution, My Perspective, Naive Solution, Nash Equilibrium, One Pass Quickly, One Pass Good, Perfect Setup, Prisoners' Dilemma, Put Skin In The Game, Sampling Rate, Scale Down, Search Space, Sensitivity Analysis, Survivable?, The Real Question, Win/Win, Work Backwards, Your Position, Inhibiting Loop, Aligning Incentive, Perverse Incentive, Reverse Causality, Change Tradeoff Curves, No Time Axis, Set-Based Design, What Fact?, Fix Time, Flex Scope, Wider Scope, Reinforcing Loop (aka positive feedback loop), Ask the Genie, Edges, Influence Diagram (How do effects affect effects?), Trust The Market, One Room At A Time, Complain & Propose, Ergodic (Ergodicity)

---

## The Thinkies

### 1. "Obviously..."
**Pattern:** Someone begins a sentence with, “Obviously…”.
**Transformation:** Ask yourself what is true if they are wrong. What happens if you make the opposite assumption?
**Detail:** This is a language-oriented Thinkie. It encourages questioning assumptions, even if the "obvious" statement turns out to be true.

### 2. Abundance
**Pattern:** You're cutting corners because you have too much to do/not enough time.
**Transformation:** What would you do if you had enough time?
**Detail:** A project Thinkie. Some of the activities you come up with you may not be able to do for now; others may actually be cheap & pay off quickly enough that they put you in a better place. In the same post Beck explains why he enjoys writing Thinkies: unlike advice such as TDD, which people copy thoughtlessly and then blame him for, a Thinkie is just "see this pattern? try this thing, judge the result"—responsibility for evaluation & execution is entirely on you, and if it didn't work, that's because it usually doesn't.

### 3. Break Dependency
**Pattern:** Your project can’t progress because you’re waiting on another project/team/organization/company.
**Transformation:** Break the dependency. What would happen if you did just enough work yourself?
**Detail:** Highlights that elaborate dependency structures built for "efficiency" can actually hinder progress, likening them to "lilliputian threads" that tie one down.

### 4. Can't/Because
**Pattern:** Someone says, "We can't X because of Y."
**Transformation:** "When (not Y), then we can X."
**Example:** "We can't release software after every change because there would be too many defects." → "When we have fewer defects we can release software after every change." Now you can talk about ways & means: how would we have fewer defects? Quantify "fewer". Is that reasonable/possible/economic? What should we do first?
**Detail:** A language Thinkie, good for getting unstuck. When folks are making excuses, they don't notice they are also telling themselves how to get unstuck—your job isn't to be smarter than they are, just to notice. Make a habit of converting Can't/Because into When/Can: tell a colleague you're trying it, try it together, keep notes; Beck's hypothesis is that it soon becomes a habit that speaks up on its own. In the same post Beck describes Thinkie anatomy—match the pattern, apply the transformation if it matches, evaluate the results—and notes that people often skip to evaluating expected results a priori and give up if they don't anticipate value. In unpredictable situations you may as well try all the Thinkies all the time (he tests all language Thinkie patterns as he listens/reads, all at once).

### 5. Customer's Voice
**Pattern:** The team is being tugged in so many directions by so many people that they can’t make progress on anything.
**Transformation:** Have the customer speak with one voice.
**Detail:** This Thinkie was conceived as an inverse to Direct Feedback.

### 6. Dependency Merging
**Pattern:** Progress is blocked by a dependency on another project/team/organization/company.
**Transformation:** Merge, temporarily or permanently, whole or in part, the two entities.
**Detail:** Sometimes a blocking dependency suggests that the current organizational structure is incorrect, and a reorganization could eliminate the dependency.

### 7. Direct Feedback
**Pattern:** Feedback between those who make changes (programmers, but it could be anyone) & those affected by changes runs through one or more layers.
**Transformation:** What would happen if the programmers talked 1x1 with the users?
**Detail:** A project Thinkie. As projects scale, it becomes necessary to aggregate, summarize & filter feedback, and it's easy to miss that this loses something; if a project starts to sputter, restoring direct feedback might help. What would happen, how to coordinate different users talking to different customers, how to keep other stakeholders (customer service, marketing, sales, training, consulting, executives, investors) informed—that's for you to figure out. Is it even a good idea? Thinkies don't generate good ideas, just lots of ideas. Customer's Voice was conceived as its inverse.

### 8. Goldilocks & The 3 Tradeoffs
**Pattern:** (No explicit pattern in the post—this is a chapter on the structure of tradeoffs.) You face a decision where too much and too little of something are both bad.
**Transformation:** (Implied) Draw the tradeoff: a payoff dimension, a minimum acceptable payoff, a control dimension between 2 extremes, and two counteracting cost curves; sum them to find the acceptable range.
**Detail:** Uses the Goldilocks story as three structurally similar decisions. Porridge: heat is the control dimension; too hot and too cold are both "yuck"; summing the curves and extending the acceptable line gives the acceptable range. Bed: same shape, but curves aren't fixed—someone with a bad back has a different curve, so a different acceptable range. Chairs: no single control dimension (from "little & delicate" to "big & sturdy") and no solution in the bears' house; a solution would be to de-couple size & sturdiness (see Change Tradeoff Curves). Beck draws better downwards. Don't be fooled by the precision implied by the curves: the goal is to inform your gut, not to compute a mathematically optimal decision. Beck also notes people need emotional energy, not just ideas, to change how they make tradeoffs.

### 9. Half in Half
**Pattern:** Someone gives you a date for a scope of work.
**Transformation:** Ask which half of it you can see in half the time. For example, for a nine-month project: "Which half of that can you do in four months?"
**Detail:** Kent Beck's all-time favorite Thinkie, and the one he's made the most consulting money with. Folks—especially smart folks buried in the problem—don't prioritize well. Awesome thing 1: it forces a step back to think about succession—half has to get done before the other half, so what are the halves? Sales (a demo)? User feedback (a working but incomplete system)? Technical validation & de-risking (a prototype measured under production conditions)? The discussion of priorities creates value on its own. Awesome thing 2: you don't have to be smart—match the pattern, ask the question, watch the creativity flow. Awesome thing 3: it's practically scale-free ("big release in 6 months" → "which half in 3 months?" → "by noon" → "at the coffee break?"). The only downside: teams start asking the question on their own.

### 10. Incongruence
**Pattern:** Something about the story doesn't add up, but you can't put your finger on what.
**Transformation:** Let go of trying to figure it out. Find a spot where the words don't match the actions & surface it.
**Detail:** A consulting Thinkie: in consulting there's a short period to observe, orient, decide & communicate, no time for deep relationships or multiple messages, so the first thing you say must have impact. Use with care—it's a "very spectrum-y" way of looking at situations; Beck relies on being blunt-but-trustworthy, which some people can hear and many can't. Incongruence is not an excuse to be an asshole: saying it in the most hear-able way is part of the expertise. Focusing on where words & actions contradict narrows your focus in a complicated, history-rich situation. Incongruence costs energy—you keep saying what doesn't match what you do—so when a client is freed to match actions to words (or words to actions), they discover a new source of energy. Companion of Contradiction.

### 11. Laughter
**Pattern:** A statement in conversation is followed by nervous laughter.
**Transformation:** Take the statement seriously.
**Example:** "If we could just throw away all the source code & start over we could certainly succeed." Maybe so. Defer judgement: what would it look like? What would be required? Who would win? Who would lose? Now what do you think of the idea?
**Detail:** "Many a true word hath been spoken in jest" (Shakespeare, *King Lear*). Originally classified as a language Thinkie, though more of a social game. Real example (2024): in a workshop for non-technical executives, Beck said "I dream of a day when you ask for a feature and, given an estimate, say 'It's okay if you take a little more time'"—big, nervous, long laugh; then "And the geeks say, 'No, we can do a little more than that'"—smaller laugh, then silence as it sank in. The laughter sounded like fear of hope (that programming could ever be abundant for them); taking it seriously generated the idea that the message had enough attraction to build a workshop around it. Listen for laughter—there's information there, unique if everyone else ignores it. Similar premise to But If You Could…

### 12. Personal Feedback
**Pattern:** There's a system worked on by another system.
**Transformation:** Use the system on itself.
**Detail:** A project Thinkie: make feedback personal. At Gusto, a payroll company, they paid themselves with their own system in the early days but stopped as the company grew because it seemed too distracting—cutting themselves off from valuable feedback & emotional energy ("How seriously are you going to take quality if your own paycheck is on the line?"). Other stories: an optimizing compiler slower than its predecessor until it compiled itself, then much faster; Beck terrified an engineering director at a networking company by suggesting the daily build of their router software be installed nightly on their own internal routers. An example of the Skin In The Game principle. Close relative of Self-description.

### 13. Project Buffer First
**Pattern:** You’re starting to plan a project with a fixed delivery date.
**Transformation:** Start by saying, “How certain do we need to be about the scope & date? Okay, we’ll start with 15% (or 10% or 20%) project buffer”.
**Detail:** This Thinkie can be unsettling to people because traditional planning often involves over-promising and under-delivering.

### 14. Reverse Phrase
**Pattern:** A phrase with 2 symmetric parts.
**Transformation:** Reverse the phrase structure to generate new ideas.
**Example:** Transforming the platitude "engineering turns ideas into reality" by asking "what turns reality into ideas?" led to the popular tweet "science turns reality into ideas". Beck notes that most of the time, this Thinkie won't produce useful results.

### 15. Serialize
**Pattern:** The team is doing things in parallel.
**Transformation:** Perform the same tasks serially.
**Example:** The team is implementing 2 features at the same time. Have the whole team work on one feature, ship it, then work on the next feature.
**Detail:** First of the project management Thinkies: Taylorism has gifted us a set of mostly unspoken dysfunctional assumptions about projects, so it takes relatively little effort to come up with better ideas (antidote: Mary Parker Follett, *Dynamic Administration*). Whether serializing results in improvement or disaster is for you to evaluate—the Thinkie has done its job as soon as it suggests an experiment. Don't serialize everything; consider serializing something currently done in parallel where the parallel tasks have unexpected interference.

### 16. Shift Left & Right
**Pattern:** You have a multi-stage process with handoffs & you’d like to eliminate a handoff.
**Transformation:** Look at the value realized by the person handed off to. What would it take for someone else to realize that value earlier or later in the process?
**Example:** The classic relationship between developers and testers.

### 17. 1, 10, 100
**Pattern:** Progress is blocked by a big, scary worry.
**Transformation:** Quantify the order of magnitude of the worry. For example, if something is "too expensive," ask: "$1000? $10,000? $100,000?".
**Detail:** A key technique is to choose the magnitudes such that the largest suggested number remains relatively manageable or less intimidating. This Thinkie was posted by Paul Tavis and realized by Beck as a personal habit.

### 18. Compared to What? (CTW?)
**Pattern:** You hear a judgment without context.
**Transformation:** Ask: “Compared to what?”.
**Detail:** Described as a "highly profitable Thinkie" and a useful tool, despite the adage "comparison is the thief of joy". It can "unstick" one's brain by challenging vague judgments. For instance, if "Development is so slow," ask "Compared to what?". This Thinkie was adopted from Jerry Weinberg.

### 19. Contradiction
**Pattern:** You are faced with a big, complicated situation in need of improvement.
**Transformation:** Find 2 statements by the client that contradict & (gently) point out the contradiction.
**Detail:** A consulting Thinkie: you take in a river of information, make sense of it quickly & pick one or two salient points—clients don't want to pay for deep analysis, at least not at first. Example: "We are totally aligned with the Agile Values. But also everything needs to be tracked in Jira."—a naive interpretation puts the two in direct contradiction. As with Incongruence, the trick is the delivery: these 2 Thinkies together are pretty much guaranteed to deliver a salient message; delivering it while building rather than damaging the relationship is another challenge, out of scope for Thinkies.

### 20. Defer Decision
**Pattern:** A decision is being made & you’re not convinced all the relevant information is available or that the team is not all on board.
**Transformation:** Don’t decide today. Ask, “What would happen if we just didn’t decide for a while?” or suggest a later decision date.
**Detail:** This is one of three decision-related Thinkies presented by Beck, and they can contradict each other.

### 21. Else?
**Pattern:** You have a situation where a condition has a consequence.
**Transformation:** What happens if the condition does not hold?
**Example:** Applied to TCR (Test-Commit-Revert), asking what happens if you don't always get back to green tests.

### 22. End To End
**Pattern:** You have a large, complicated, multi-layered project, typically structured layer-by-layer for "efficiency".
**Transformation:** What would it look like if you structured the project to go end-to-end for a tiny subset of the possible inputs instead?
**Example:** A payroll system consulting scenario with over 100 people involved.

### 23. Envelope Calculation
**Pattern:** You see some data. Do they matter?
**Transformation:** Do the math to put the numbers into context.
**Detail:** These calculations are not complex. If a spreadsheet is needed, it's likely too much investment at the initial stage. Example: Calculating 350K H100s as nearly 20% of worldwide units to understand its significance.

### 24. Force Decision
**Pattern:** There’s a decision that needs to be made & nobody is making it for no good reason that you are aware of.
**Transformation:** Ask, “If we had to decide today, what would we…?”.
**Detail:** This is the first of three decision-related Thinkies, which are intentionally contradictory, highlighting that each generates an idea that then needs evaluation.

### 25. Grow Then Split
**Pattern:** You are creating something that will end up with many elements & you are stuck on where to start.
**Transformation:** Start with one tiny element. Grow it. When it gets uncomfortably large, split it along the revealed natural fault lines.
**Detail:** Contrasts with the natural inclination to preemptively split components (e.g., X from Y).

### 26. Half Wavelength Shift
**Pattern:** You have a multi-stage process A→B→C→D.
**Transformation:** What happens if you start with B, C, or D?
**Example:** Test-driven development (TDD), where testing precedes coding, instead of the traditional code-then-test sequence. This Thinkie tests one's ability to defer judgment, as the conventional order usually has "good reasons".

### 27. Just Apply
**Pattern:** You’re faced with a confusing situation & you don’t know what to do next.
**Transformation:** Take a model or an analogy or a frame & just apply it.
**Detail:** This Thinkie encourages application without concern for whether the model "makes sense," and it applies other Thinkies like "Separate Observation From Judgment" and "Self Description".

### 28. Latency, Throughput, & Variance
**Pattern:** Someone says, “I need you to go faster!” You’re going as fast as you can. OR Someone says, “We need to go faster!!!”. OR You aren’t responding to change in time. Everyone is pushing to get more done.
**Transformation:** The situation is under-constrained. “Go faster!” can mean any of several things. Find out which, then bias towards reducing variance first. OR Ask “latency or throughput.” Continue asking until a specific answer is provided, or it becomes clear the organization is unwilling to differentiate. OR How would you reduce the variance in your work, even if that would “take longer”?
**Detail:** Latency refers to the distribution of time from when work enters to when it leaves the system. Throughput refers to the number of items processed per unit time. Based on Kingman’s Formula, as the utilization of a rate-limiting resource approaches 100%, the time required to process new work approaches infinity. Increased variance also leads to infinite lead time for new work, and reducing variance "magically" improves responsiveness. Examples include developer testing (like Test-Driven Development, TDD) which makes work more reliably "done," and reducing coupling (as in Tidy First?) which reduces the likelihood of disruptive "jackpot changes". Beck realized he was much more relaxed after his first Waymo autonomous ride.

### 29. Match the Pipes
**Pattern:** Insufficient value is flowing through a series of steps.
**Transformation:** Compare the capacity of each of the steps. Whichever step is the constraint, add capacity to it, even at the expense of other steps. Once the pipes match, you can think about how to improve overall capacity.
**Detail:** First of the systems thinking Thinkies, addressing the tendency to get bogged down in details & miss more effective action at a different scale. Divide et impera fails because separate solutions must be integrated (which can consume all the gains) and each part becomes an organization with its own imperfectly aligned incentives. Classic example: engineering going "too fast" for testing (easy to justify more engineers, hard to justify testers) → engineering starved for feedback, doom cycles; shortcutting testing ships defects; XP's answer was for engineers to "go slower" by writing demonstrably production-ready code, matching capacities for a larger, smoother flow. Pipe analogy (2025 post): two pipes of capacity 5 deliver 5; expanding either to 20 or a million still delivers 5. For executives, who can see the whole chain (Product → Design → Engineering → Ops/Sales/Marketing) and are responsible for it: find the narrowest pipe (look for half-done work piling up upstream); keep just enough buffer before it, even reducing upstream output; expand only the narrowest pipe (expanding others at best doesn't help, at worst floods the system); reduce demand on it by routing work elsewhere; stop improving & shift attention when a new pipe becomes narrowest. Pressure ("80-hour weeks or else") stresses the system without changing it—low benefit, high & permanent human cost. Augmented coding creates a slew of new Match the Pipes problems. Related (unwritten): Observe Later, Observe What You Care About Imperfectly.

### 30. McDonald's
**Pattern:** You sense that a group may be ready to make a decision but is stalling.
**Transformation:** You propose a bad-but-not-ludicrous alternative.
**Detail:** Part of the "Decision Thinkies" series. It is named after the scenario of a group stalling on deciding where to eat, prompting someone to suggest "McDonald's" to elicit a definitive "no," thus forcing an actual decision.

### 31. Measure Later
**Pattern:** You’re stuck trying to improve a multi-step process.
**Transformation:** What is something you could measure later in the process?
**Detail:** Addresses the human tendency to measure what is easy rather than what is important or provides leverage.

### 32. Measure Sooner
**Pattern:** You’re measuring the end of a multi-stage process, but the measurement doesn’t provide guidance for change.
**Transformation:** Measure something that seems correlated to success sooner in the process.
**Example:** If production error rates aren't helpful, measure something earlier in the process.

### 33. Measure What Matters
**Pattern:** You are measuring the steps of a multi-stage process but are not seeing the desired large-scale improvement.
**Transformation:** Measure the value you actually want to change, even if that measure is vague, not actionable, or complicated.
**Example:** If profit is the goal, measure profit. If customer satisfaction is the goal, measure customer satisfaction.

### 34. Parallel Decision
**Pattern:** You have to decide between 2 alternatives, the decision is unclear, & the stakes are high.
**Transformation:** Ask: “Why not both?”.
**Detail:** This is the final decision-related Thinkie, intentionally contradicting "Force Decision" and "Defer Decision". Beck learned this from Ward Cunningham in the early days of the web.

### 35. Rate-Limiting Resource
**Pattern:** Your product is growing fast but you’re nervous about the limits of that growth.
**Transformation:** What is the one resource you’re going to run out of next? How can you increase the supply & decrease the demand to delay the day of reckoning?
**Detail:** This Thinkie applies to the "Expand" phase of a product's growth.

### 36. Reduce Utilization
**Pattern:** We need to get more done but we’re already busy as we can be.
**Transformation:** What would happen if we *reduced* utilization?
**Detail:** Based on Kingman’s Formula, which demonstrates that as the utilization of a rate-limiting resource approaches 100%, the time required to process new work approaches infinity.

### 37. Self-description
**Pattern:** You have a system that models other systems.
**Transformation:** Use the system to model itself.
**Examples:** A design system that models user interfaces → use it to model its own UI. An auction system → use auctions to prioritize its next feature. JUnit tested itself (tricky to avoid a broken JUnit reporting all was well).
**Detail:** First of the "models" Thinkies ("if this were an X, then the logical consequences are Y & Z"); applying a model temporarily detaches emotions from the problem and can get you out of a local minimum. Meta-circularity provides leverage 3 ways: a good description of your own system is valuable; a poor description gives rapid feedback on its holes; second-order effects are powerful (an optimizing compiler written in its own language gets faster with every optimization, letting you improve it faster). Beck also uses one Thinkie to explain another (e.g., Self-description to explain Just Apply). Close relative of Personal Feedback.

### 38. Separate Observation From Judgement
**Pattern:** You are getting carried away in your reaction to a situation.
**Transformation:** List the externally observable facts about the situation. With the list in hand, judge the situation.
**Example:** When receiving negative feedback from a boss, list the facts to avoid becoming defensive and generating stronger negative feelings.

### 39. Special-Cause Versus Common-Cause Variation
**Pattern:** A process has gone haywire for some reason.
**Transformation:** First decide if that reason happens repeatedly (common cause) or just this once (special cause). React accordingly.
**Detail:** This is a process control Thinkie derived from Deming. It addresses the mistake of not paying attention to a process and helps differentiate between systemic issues and isolated incidents.

### 40. Tradeoff
**Pattern:** Someone is trying to maximize some outcome, perhaps getting frustrated that progress has slowed.
**Transformation:** Ask—How much increase do you need? What are you giving up as you increase the outcome? What will increase friction as you increase the outcome?.
**Detail:** Mentioned as a Thinkie that even comes with its own gesture. Beck has realized there's a deep underlying structure, biases, and refinements to tradeoffs, leading to a dedicated "Tradeoff Booklet" series of Thinkies.

### 41. Upside/Downside
**Pattern:** You’re faced with an evenly-balanced decision.
**Transformation:** List the upside & downside consequences of the decision. If there's an upside and no downside, proceed with it.
**Detail:** Though it sounds simplistic, it helps when one is overwhelmed by details and expectations during a decision-making process.

### 42. Work/Wait Ratio
**Pattern:** You have a multi-step process where responsibility moves from person to person (or organization to organization).
**Transformation:** Trace a typical recent work item through the process. Add up the time spent actually working on the item & the time the item spends waiting. Divide these totals.
**Detail:** This calculation alone can sometimes be enough to transform a process by revealing inefficiencies in waiting times.

### 43. Agreements
**Pattern:** You are locked in an argument & you want progress.
**Transformation:** Pause & make a list of everything you agree on.
**Detail:** Stretches the scope of Thinkies toward inter-personal advice, but Beck stores it in the same box. "Heated Agreement" is an apparent argument where participants are committed to the conversational form of arguing without actually disagreeing—catch it early. Once adrenaline & cortisol are pumping it's hard to get out of the back-and-forth; Agreements gives space & time to evaluate the conversation itself and focus on the actual issues. Maybe you realize you don't actually have an argument, maybe that you're so far apart further conversation is worthless, maybe you find the actual issue.

### 44. Analogy
**Pattern:** You’re struggling to explain a concept.
**Transformation:** Explain it in terms of another domain your listener already understands.
**Detail:** This seems simplistic when written down, but analogizing gets easier with practice, and the "Thinkie Motto" (generate then evaluate) applies.

### 45. And Then…
**Pattern:** You have a potential decision to evaluate.
**Transformation:** Ask, “…and then?”.
**Example:** Setting higher goals for lines of code programmers write per day to increase productivity, which everyone knows how it ends. Beck has personally witnessed the introduction of line counts to performance evaluation at a large, highly respected company.

### 46. But If You Could...
**Pattern:** Someone is stuck trying to make progress. They fantasize about what would be required to get unstuck.
**Transformation:** You respond with, "But what if you could <do whatever they just said>…"
**Detail:** Same premise as Laughter: people often know exactly what to do but prevent themselves from doing it. Example: "We'd love to deploy more often." "What if you could?" "Yeah, that'd be great. But we can't." "What if you could?" Requires "one foot on the dock & one foot in the boat": in the situation enough to be trusted with their frustration & fantasized solution, detached enough not to get co-stuck. Expect resistance—people get attached to their stuckness ("I'm the person who just can't write software without bugs"). Your job is to hold space long enough for them to reframe themselves without the stuckness; you're not fixing them, you're opening a door. Even when it doesn't "work", spin-offs are useful: we can't deploy more often because of bugs, breaking changes & lack of monitoring—so we work on monitoring & life gets better before the overall goal moves.

### 47. Composed Solution
**Pattern:** You’re stuck solving a big problem.
**Transformation:** Imagine a sequence of steps that seem like they would solve the problem.
**Detail:** This Thinkie contrasts with "Scale Down," which unsticks problem-solving by ignoring the whole problem and addressing a seemingly-knowable subpart. "Composed Solution," by contrast, solves the whole problem by seeing it as a pipeline.

### 48. Easy Bit
**Pattern:** You’re paralyzed by the magnitude of the problem facing you.
**Transformation:** Pick the absolutely easiest thing to do that will help & do it.
**Detail:** This Thinkie follows from "Thinkie Hard Problem". Beck has come to believe that confidence & energy are more important than ideas, and with confidence & energy, one can solve problems (with the help of Thinkies).

### 49. Explore or Extract? (Explore/Exploit)
**Pattern:** You are doing something for the nth time. Should you do it in a predictably good way or a new way?. OR You’re faced with a choice between doing something the same old way or trying a new way.
**Transformation:** Kinda flip a coin (more details below). OR Mentally flip a coin (or actually flip an actual coin). That way you don’t have to feel bad about either option.
**Detail:** It’s not strictly 50/50; the odds should be adjusted based on the situation, considering risks, potential gains, and ergodicity (chance of game o…). This format has settled down after initial thrashing.

### 50. Exponential Growth / Growth Rate, Not Absolute Number
**Pattern:** Is this small thing competition for this large thing?. OR You’re trying to understand if a trend is significant.
**Transformation:** Compare growth rates, not absolute size. If the small thing is growing much faster then yes, take it seriously. OR Look at its growth rate, not its current size.
**Example:** Early in COVID, people compared 50,000 potential deaths to traffic fatalities, but ignored the exponential growth rate, focusing instead on absolute numbers.

### 51. Extrapolate Further
**Pattern:** You’re trying to predict the consequences of a trend.
**Transformation:** Extrapolate further than other people, further than seems reasonable.
**Detail:** Beck learned this Thinkie watching Bill Joy (Sun founder) talk about processor performance when he was an engineer at Tektronix, observing the awesome performance of 32-bit processors as they appeared.

### 52. Fun Bit
**Pattern:** You’re paralyzed by the size & complexity of the problem you’re addressing.
**Transformation:** Pick the bit of it that will be the most fun & do that.
**Detail:** This Thinkie follows up on "Thinkie Hard Problem" & "Thinkie Easy Bit". It is another confidence/energy management strategy. It prompts one to consider what would be fun, or what they have always wanted to do but haven’t.

### 53. Hard Problem
**Pattern:** You're stuck addressing a hairy problem. Or you're addressing it but have a nagging feeling you're missing something important, prioritizing incorrectly.
**Transformation:** List absolutely everything you can think of that makes the problem hairy. Technical aspects. Social aspects. Economic. History. Perverse incentives. Uncertainty. Cognitive biases. Absolutely everything.
**Detail:** First of a group of related Thinkies for intimidating problems (Beck had just done it with software design). Panicked fear of failure is a serious waste—people freeze; listing all the reasons discharges the tension (feeling fear is reasonable, freezing is optional). Partial acknowledgement is another waste: you understand bits, get scared & ignore the rest, so priorities and understanding of second-order effects are incomplete and you risk ineffective or counter-productive work. Face the hairy problem.

### 54. Hill Climbing
**Pattern:** Something isn’t good enough but you’re stuck improving it.
**Transformation:** Recast the situation as hill climbing—Identify a fitness function for the situation. What means “better”?.
**Detail:** This Thinkie prompts identifying a threshold for the fitness function above which one is satisfied (for the moment—nobody’s satisfied for long). It is one of Beck's favorite analogies.

### 55. Invert the Goal
**Pattern:** You’re stuck trying to make progress toward a goal.
**Transformation:** Try to achieve the opposite.
**Example:** If you’re trying to optimize a user experience and users refuse to cooperate, despite your best ideas, user behavior remains unchanged. Invert the goal: What’s the largest change you can make to the experience that will result in no change in user behavior?.

### 56. Legibility
**Pattern:** Someone is estimating or counting something that doesn’t matter.
**Transformation:** Listen carefully to understand the need they are satisfying with those metrics & find a way to meet that need another way.
**Detail:** This Thinkie highlights that "false precision creates false control". An example is measuring developer productivity with various made-up numbers that simply cannot matter.

### 57. More General Solution
**Pattern:** You’re stuck solving a complex problem.
**Transformation:** You solve a more general problem of which your specific problem is a special case.
**Detail:** This is one of three Thinkies that help get unstuck by reframing the solution. The basic idea comes from mathematics, where it occurs frequently, such as in algebra.

### 58. My Perspective
**Pattern:** You’re having trouble communicating with someone.
**Transformation:** Invite them to look at the situation from your perspective.
**Detail:** This is the opposite of the usual advice to look at the situation from the other person’s perspective. It's a Thinkie that generates ideas, not necessarily good ones. Beck has used this when evaluating investment opportunities.

### 59. Naive Solution
**Pattern:** The team is stuck solving a complicated problem. They are focused on complicated solutions.
**Transformation:** You ask, "Why is this any more complicated than <naive solution>?"
**Detail:** One of a class of Thinkies that work not because of superior skill but because you maintain perspective while others are stuck in a local maximum—you don't have to work hard or compete, just maintain composure, and can be valuable out of all proportion to your technical skill. Dual-purpose: it may get the team onto a new track; even if not, the explanation helps you understand and helps the team understand their situation. The only way it completely loses is interrupting the team just as they're about to make progress.

### 60. Nash Equilibrium
**Pattern:** Two or more parties are stuck in a dysfunctional relationship but everyone refuses to change.
**Transformation:** Take a step back & show the whole dynamic to all parties.
**Detail:** These kinds of change-encouraging Thinkies are fraught because people don’t make rational choices. Beck still tends to assume they do, which often leaves him baffled.

### 61. One Pass Quickly, One Pass Good
**Pattern:** You have a project that requires many fairly independent pieces.
**Transformation:** Radically scale back your ambitions for the pieces & deliver all of them in a first pass, then go through all the pieces & improve them.
**Example:** Regulators require variations for all 50 US states within 5 months, or 💀. Options: (1) deliver all states with buffer (done in 4 months, 1 month slack); (2) 10 states a month, most important/riskiest/most instructive first, raising the alarm if off track at month 2; (3) do the jankiest conceivable job of all 50 states in 2 months—manual processes, plain text, PNAMBIC—then optimize for 3 months.
**Detail:** The incentives are asymmetrical (deliver: pat on the back; don't: really bad stuff), so organize the project around them. Nobody wants to operate a system built from the worst conceivable solutions, but it beats not operating at all because the company is gone. Options 1 & 2 suffer from accelerating anxiety as the deadline nears; One Pass Quickly, One Pass Good removes the threat of failure early, giving experience, confidence & energy to improve the system where it turns out to matter. Inspired by Anna Goodman; the project management corollary of Make It Run, Make It Right, Make It Fast.

### 62. Perfect Setup
**Pattern:** You're having trouble making progress in a situation.
**Transformation:** List the properties that would set the situation up perfectly for success. Back off only reluctantly.
**Detail:** Too often the reason for lack of progress isn't effort but context: we get used to the proverbial pebble in our shoe & complain about our walking speed instead of taking the pebble out. Poker example—the perfect setup: good sleep, meditation, exercise, eating well, feeling sharp, a learning goal, the most profitable game, the table with the weakest opponents, 2 conservative players acting right after you, 1–2 loose/easy-to-read players right before. Insist on every property under your control. Extreme Programming is an exercise in Perfect Setup: strong social ties, rapid feedback at all scales, constant adjustment to reality ("Well, of course if we had a customer on the team we'd succeed." Um, okay?). The question isn't how to eke out progress in a nearly-impossible situation, but how to set the situation up for success & keep it set up.

### 63. Prisoners' Dilemma
**Pattern:** Two or more parties are struggling to cooperate.
**Transformation:** Model the situation as a Prisoners' Dilemma. If it fits, apply Thinkie Put Skin In The Game or iteration to break the impasse.
**Detail:** In the Prisoners' Dilemma 2 arrested parties: if neither confesses, both go free; if one confesses & the other doesn't, the squealer goes free & the other goes to prison; if both confess, both go to prison for less time. Check whether the parties feel they're in one ("If I work on this urgent task Saturday & you don't, I'll feel like a sucker"). What makes it intractable is lack of information; the way out is information: Put Skin In The Game (signal that you're opening yourself to negative consequences); iteration (players who play 100 times build a habit of cooperation—slice cooperation into many iterations); call out the dilemma ("You're afraid of being taken advantage of. Me too. What are we going to do about this?").

### 64. Put Skin In The Game
**Pattern:** Someone needs to make better decisions. They have plenty of information. They just aren't using it well.
**Transformation:** Re-arrange feedback so the decision maker directly experiences the consequences of their decisions.
**Detail:** Origin: a reader (a diabetic) described his insulin pump's useless alerts (e.g., night-time beeps that the sensor expires in 24 hours) and companies ignoring his feedback; Beck replied "Maybe if the Product Owner wore an insulin pump?"—the Thinkie in action. Historical examples: WWII aircraft maintenance chiefs flew on the first ride after major repairs; the Code of Hammurabi put to death a builder whose house collapsed and killed the owner. It may seem like harsh justice but the net effect is to reduce harm. Extending the example: the device designer should wear a pump running today's software—and if the "requirements" come from the FDA, the FDA auditor too. As with all Thinkies, evaluate the idea afterwards: a big investment, but compared to the potential benefit? Related to metrics-driven product development subtracting value for users without foundational principles (Fitbit). Used by Prisoners' Dilemma; Personal Feedback is an instance of it.

### 65. Sampling Rate
**Pattern:** You are monitoring a system & feel like you’re missing something.
**Transformation:** Increase your sampling rate.
**Detail:** Observing a system is a tradeoff between the cost of observation and the accuracy of observation. If you feel like you’re missing something, think about the ratio of the duration of events of interest to the frequency of sampling.

### 66. Scale Down
**Pattern:** You are stuck & overwhelmed trying to solve a big problem.
**Transformation:** What thing would, if you had it, make the big problem more tractable? Make that.
**Detail:** In a way, "Scale Down" seems "too simple to need naming & explaining." However, when overwhelmed, it serves as a reminder that it’s okay to solve a part of a problem. It contrasts with "Composed Solution".

### 67. Search Space
**Pattern:** You need to act in a context where you can't predict what the result of actions will be.
**Transformation:** Treat the choice of action as moves around a search space. Characterize the space: ensure actions are reversible; identify the dimensions of variability; observe whether the space is smooth or spiky (do small changes in action cause large changes in outcome?); identify the cost of missing a good outcome. Then search: take an action (at random if there's no better start); use smooth vs. spiky to decide how far to jump next; update the dimensions of variability with experience; reduce the cost of experiments; stop an experiment as soon as you have your answer.
**Detail:** Examples: a police evidence search is spiky (small differences in where you search matter), so be thorough & methodical; product decisions in a rich, rapidly emerging sector are spiky with many sources of value, so mostly take big jumps with the occasional small step. Exploring a search space is a tricky mix of intuition & chaos; intuition speaks loudly because it wants predictable success, but if it's truly a search you can't predict success, only discover it. Used in No Time Axis.

### 68. Sensitivity Analysis
**Pattern:** You need to tune the operation of a system with many inputs. Which dial to twist or lever to pull?.
**Transformation:** Pick an input that seems to matter. Vary it (in a model if possible). See if the output changes. If not, let it go.
**Detail:** Beck's recent post on his motivation for writing *Tidy Together?* is an example of Sensitivity Analysis.

### 69. Survivable?
**Pattern:** You are stuck making a decision.
**Transformation:** Ask if the negative outcome is survivable. Either: the negative outcome is survivable, in which case do the quickest, cheapest thing that generates value (information, time, or other resources); or the negative outcome puts you out of the game permanently, in which case mitigate risks—but get moving.
**Detail:** The root of a set of Thinkies spawned (or brought into focus) by Luca Dellanna's book *Ergodicity*. Jeff Bezos called these "Type One" and "Type Two" decisions; "Irreversible" & "Reversible" are more descriptive. Which space you're in completely changes how you should decide. Sometimes you're stuck because you're unconsciously treating a non-survival decision as a survival one—realizing any outcome is acceptable gets you going. Sometimes you're consciously making a survival decision & you're afraid—you should be, but still get going. Insight to develop later: deliberately making lower-level decisions into survival decisions makes higher-level decisions reversible.

### 70. The Real Question
**Pattern:** Someone asks you for information that makes no sense.
**Transformation:** Ask, “What’s the real question?”.
**Detail:** Fred George suggested this Thinkie after reading "Thinkie Legibility." It’s another way to get to the actual issue. However, sometimes people don’t want to get to the real issue, as they may know their fears are absurd.

### 71. Win/Win
**Pattern:** You’re stuck on a decision because someone is going to be negatively affected.
**Transformation:** What are solutions that would be good for everyone?.
**Detail:** Although it's a cliché, it works, and it's a Thinkie because it's easy to forget under stress. A recent example is Beck taking on sponsors.

### 72. Work Backwards
**Pattern:** You’re stuck trying to work forwards from where you are towards your goal.
**Transformation:** Instead, start at the goal & work backwards.
**Detail:** Beck has used "Work Backwards" many times. It is the essence of TDD (Test-Driven Development) and User Stories, and it is related to "Shining City On A Hill" (another Thinkie).

### 73. Your Position
**Pattern:** A conversation has gotten stuck short of resolution but the conversation remains promising.
**Transformation:** Summarize the other party’s position in a way they would agree with.
**Detail:** It’s natural to judge during a conversation, but one might be missing something.

### 74. Inhibiting Loop
**Pattern:** You want to improve but instead you’re going backwards.
**Transformation:** Look for a loop of reasons, not just a list.
**Detail:** This is the first in a series on systems thinking (recommended reading: Diana Montalion's *Learning Systems Thinking*, Donella Meadows' *Thinking in Systems*). If the cause of slowness is obvious, other Thinkies (Fun Bit, Easy Bit) help you get started; but when you don't remember things being this bad and the further you go the worse it gets, use Gerald Weinberg's influence diagrams: draw the effects you're seeing; draw an arrow between effects that influence each other (more of this leads to more of that); put a circle (dot) on the arrow if the influence is negative. State each influence aloud ("more revenue leads to more saturation")—it catches mistakes in the direction of influence. Example (newsletter revenue, Thinkie Self-Description): revenue has stalled; more subscribers → more market saturation; more saturation → less revenue. Loops are more powerful than lonely causes—the more times around this loop, the greater the friction. Trick: count the dots. Loops with an odd number of dots are inhibiting loops (aka negative feedback loops); see Reinforcing Loop for the even case. Within the diagram, what might help is clear: increase market size → less saturation → more revenue. But you can keep adding effects (limits to market growth, revenue → ads → larger market…) and easily go too far, ending up with 15–20 effects & 20–30 influences that nobody gets anything useful out of—the "Curse of Completeness".

### 75. Aligning Incentive
**Pattern:** You can see that folks are working at cross purposes.
**Transformation:** Give them an incentive that will influence their actions towards a common goal. (Revised Sep 2025 version: rather than tell people what to do to work together, give them an incentive that will indirectly require collaboration.)
**Detail:** When people hear "incentive" they think "money". Money is a powerful incentive, but it also tends to distort behavior because it is so useful and personal—it is one of the most dangerous incentives, most subject to Goodhart's Curse ("Don't pay people a dollar for each bug fixed"). Still, "$100 to everyone when we all get there" will influence behavior. The strongest incentives uncover intrinsic motivations that were already there, just suppressed. More powerful still is a sense of belonging: in Goldratt's Scout story (*The Goal*), the hikers spread out by fitness level, the leaders reach camp early and spend the night rounding up the stragglers; the next day, rather than saying "Everyone stay together", the leader ropes everyone together with the slowest walkers in front. The rope is the Aligning Incentive: they redistribute the weight they carry so their paces match, and everyone gets there or no one does. Not terribly realistic, but the impulse is right—step back from "what's to be done?" & lead through incentives instead. Contrast with pure talk with no backup ("You guys really need to work together!"): nothing changes, because they aren't working together for reasons, and you need to change the reasons or the behavior won't change. Companion of Perverse Incentive.

### 76. Perverse Incentive
**Pattern:** People are working so as to sabotage progress towards a desired outcome.
**Transformation:** Look at their incentives from their perspective. Change the incentives. The behavior will follow. (Unless you screw up the incentives, which is easy to do).
**Example:** Sales people poaching sales from other regions, resulting in lower overall sales for the company. "Bad sales people!" Hang on—they're doing what they're incentivized to do. Make quota or else? I'll make quota. So would you in their position.
**Detail:** Identifying perverse incentives requires thinking, just for a moment, the worst of people: "What would I do if I was a greedy, venal, short-term, selfish person facing those incentives?" Then think about how to change the incentive system. "Incentive" doesn't mean only money: we are incentivized by a broad range of factors, some present, some from our past. Stories told about us—and stories we tell about ourselves—incentivize. Approval, status, recognition, belonging, and sometimes disapproval all incentivize us.

### 77. Reverse Causality
**Pattern:** You’ve tried to make a change by Thinkie Move Upstream.
**Transformation:** Treat the effect as the cause.
**Example:** As an organization grows, too many meetings prevent work from being pushed to production. Eliminating meetings causes them to spring back up like mushrooms.

### 78. Change Tradeoff Curves
**Pattern:** You’re stalled trying to make progress changing the outcome of a tradeoff.
**Transformation:** Rather than trying to change the outcome directly, change the shape of the tradeoff curves.
**Example:** Continuous deployment is an example, where the desire to deploy more frequently is hindered by the cost per deployment.

### 79. No Time Axis
**Pattern:** You’re stuck trying to understand or explain the relationship between two factors over time.
**Transformation:** Ignore time & graph the two factors as the two axes.
**Detail:** This Thinkie is a significant departure, as it introduces visualizations as a major part of Beck's thinking and communication strategy. Beck claims no originality: it comes from Edward Tufte's *The Visual Display of Quantitative Information* (a book that "rewired how I thought"). Example: explaining why coding genies (as of April 2025) aren't suitable for unsupervised operation—they're good at adding functionality but terrible at design, so they paint themselves into a corner. Thinkie Search Space showed the genie going from one local maximum to another by burning optionality, but made it hard to contrast with "augmented coding"; after days of clunky attempts (colors, time flowing both ways), Beck plotted optionality on one axis and functionality on the other. The genie's path burns optionality for ever-diminishing functionality gains until no options are left; the empirical approach alternates adding complexity for a feature with tidying to add options. The new frame also shows expert vs. novice implementation of the same feature: the expert is partly a better designer able to climb out of deep holes, but also gives themself shallower holes to climb out of—"The expert pilot demonstrates superior judgement to avoid having to demonstrate superior flying skills."

### 80. Set-Based Design
**Pattern:** You are choosing between 2 or more options & you don’t have the information needed to choose wisely yet.
**Transformation:** Implement some of them all until one is clearly superior.
**Detail:** This Thinkie is also referred to as "¿Por qué no los dos?" (Why not both?). Beck is currently applying this to a personal project involving the server-grade implementation of Smalltalk: should the VM be a bytecode interpreter or an abstract syntax tree interpreter? Go, Rust, C++, or JavaScript? He doesn't want to waste time on an implementation he'll throw away, and ignorance is abundant, so he's trying most of the combinations—augmented coding helps, since the genie makes rapid progress possible on several fronts (almost) simultaneously. If implementing them all is too expensive: Thinkie Compared To What, Thinkie Fun Bit/Easy Bit—or, sometimes, you can only afford one roll of the dice. Effort on the eventually doomed variants is not dead weight loss: code & tests from one variant are useful in others, lessons learned carry over, and progress on one variant encourages work on the others.

### 81. What Fact?
**Pattern:** You're faced with a situation that just doesn't make sense.
**Transformation:** Ask yourself what fact would, if true, cause the situation to make sense.
**Detail:** Relies on the fundamental Thinkie skill of separating generation from judgement: you aren't looking for a fact that makes sense or that fits your world view. Examples: "Why is he acting that way? If he's attracted to her but feels ashamed, his behavior makes sense." / "Why are people so angry when I point out the limitations of AI? If they're panicked about their own job, it makes sense." A fact that makes the situation make sense isn't necessarily true—you may still be missing critical context—but it's a place to start. What Fact? is a generalization of Thinkie Trust The Market (88). Beck notes the caveat that sometimes the world doesn't make sense and the best strategy is to roll with it; the harder problem is figuring out which situation is which. Opening quote: "When you have eliminated the impossible, whatever remains, however improbable, must be the truth." (Sherlock Holmes).

### 82. Fix Time, Flex Scope
**Pattern:** You're in a loop where longer & longer feedback loops seem to give you bigger results.
**Transformation:** Fix the time for the feedback loop instead & figure out how to gradually get more scope into the loop.
**Detail:** Came up while re-conceiving augmented coding around human needs: agent turns are getting longer (Anthropic reported median autonomous turn length unchanged Aug–Dec 2025 while p99 almost doubled), and long loops disrespect human attention. What would augmented coding be if the genie had to respond in under a second? Earlier applications of the same Thinkie: fixed one-week iterations with adaptable scope; Pomodoro (25 min on, 5 off); Spikes (how much uncertainty can we reduce in an hour/day/week?); JUnit Max (ran tests on every save, riskiest first, so the first second of feedback was the most interesting). Next time you think "this is just going to take a while," try "here's how long I'm willing to wait—how much can I get done?" Related to Half in Half (which starts from a project estimate rather than a feedback loop).

### 83. Wider Scope
**Pattern:** You're stuck thinking about a complicated problem.
**Transformation:** Look at the problem in its wider context. What are the "sources & uses" (from Permaculture) of the problem? What feedback loops does it participate in?
**Detail:** Another way a bigger problem can be easier to solve (compare More General Solution, which generalizes the problem rather than placing it in context). Example: the slogan "Profit is theft" makes sense if the picture is only wage → produce → sell, with the owner pocketing the surplus. Zooming out to the larger sequence—capital owner invests in a factory, worker is paid, widget produced, sold at a profit, capital owner repaid with interest—shows that without step 5 there is no incentive to build the factory, so the surplus has to be split somehow. Beck's point isn't to settle that debate (though the question of incentives for those producing content digested by LLMs holds), but that rather than picking apart the pieces of a complicated problem, it's sometimes more productive to zoom out & see it in context.

### 84. Reinforcing Loop (aka positive feedback loop)
**Pattern:** The worse things get, the worse things get. Every time you try to intervene, it gets even worse. (Dec 2025 version adds a second pattern: you are looking for a way to create large effects with a small investment.)
**Transformation:** Map the effects & how they affect each other. Find the cycle with an even number of inhibitions. Go upstream & push one of the effects the opposite direction. (Dec 2025 wording: find a loop of effects in an influence diagram—see Thinkie Influence Diagram—with an even number of negative connections; go backwards in that loop until you find something you can push in the opposite direction.)
**Example (Dec 2025):** Code reviews are taking too long & it's getting worse. "Don't take so long!" or OKRs on review delay (which people would game) won't help. Look at the system: delays grow because PRs grow; PRs grow because frustrated people pack more into each PR; frustration is caused by the delays—a reinforcing loop (zero negative connections). "Delay less!!! Or else!" brings unintended consequences; instead step back in the loop & encourage smaller PRs, or step back again & directly address the frustration. Switching polarity: quick review → less frustration → smaller size → quicker review (two negative connections, still reinforcing). An odd number of negative connections would make it an Inhibiting Loop.
**Detail:** Beck's favorite and "the most powerful tool I have for making big changes with small efforts." Example: too many deployment problems → add reviews → reviews increase the number of changes deployed at once (bigger batches) → more problems. Effects reinforce themselves: the more problems, the more problems; the bigger the batch, the bigger the batch (inhibiting loops, not shown, keep effects from growing forever). A cycle with an even number of inhibitions is still reinforcing—two "lesses" make a "more". Reversing the polarity of the effects is a fruitful exercise: more successful pushes → less review needed → smaller changes → more success. The day you find your undesired effect in a reinforcing loop is a very good day: go somewhere else in the loop & push that effect the opposite way (e.g., smaller batches or less review). The intervention isn't as easy as it sounds—mandating smaller batches yields poorly batched changes, mandating less review loses its value—so work one more step backwards: how do we get the value of reviews without the variable delay? Beck renamed "positive feedback loop" to "reinforcing loop" while teaching systems thinking with Jessica Kerr. Counterpart of Inhibiting Loop.

### 85. Ask the Genie
**Pattern:** You have a question, any question, especially a question you have tended to abandon because it would be too much work.
**Transformation:** Ask the genie.
**Detail:** A new habit—highly profitable but also highly variable: sometimes the genie has a great answer & sometimes just distraction, but the great answers are really great & not something you'd come up with another way. Josh Cannon taught it to Beck by answering every question with "Ask Claude!" until that voice played in Beck's head on its own. Example: after decades of avoiding matrix math, Beck asked the genie to teach him about eigenvalues; after half an hour of back & forth (pushing back on examples that didn't make sense—sometimes the genie was wrong, sometimes he didn't understand yet) he had an intuition about eigenvalues & their relationship to oscillation, with the chat still there to dig deeper. Every time you think "I wonder…", quickly figure out a way to ask the genie.

### 86. Edges
**Pattern:** You aren't getting enough resources coming in externally to be successful.
**Transformation:** Increase the interaction of different kinds of resources.
**Detail:** Analogy (from permaculture): should a pond be round or irregular? Round maximizes the excavator's efficiency (the mistake of valuing "simplicity" in XP), but living at the edge between two biomes gives access to two sets of resources—riparian flora & fauna draw on both water and land; insects eat on land and escape underwater from predators. As a designer, increase the irregularity/length of the interface between elements: programmers frequently talking to real customers, back-end engineers collaborating intimately with front-end engineers, designers pairing with programmers, more frequent whole-team planning. Edges sacrifices micro-optimization for macro-optimization—one of the hardest tests of courage in software development ("If I just did this myself, I'd be done already." Yeah, but it's not how much you get done, it's how much we get done). More edges don't magically create more resources, but they conjure the magic of collaboration: discovering unexpected harmony ("That would be easy to implement if only we…", or a designer's experiment users unexpectedly love) gives the effect of more resources without needing more resources.

### 87. Influence Diagram (How do effects affect effects?)
**Pattern:** You have a big, complicated system that's acting up & you'd like to regain influence over it.
**Transformation:** Diagram the effects you observe in the system & their influence on each other.
**Detail:** Follows from Thinkie Separate Observation From Judgement: you aren't rushing to act—more likely you've stepped back from actions that weren't working or were counter-productive. You need to know the parts (especially those you weren't aware of) and how they relate (especially the connections you weren't aware of). Example: should Beck make more newsletter content public? Contradictory advice: less public material incentivizes paid subscriptions; more public material grows the audience. More public material → more views → more valuable sponsorships → more revenue → more sustainability. But more private material → more attractive paid subscriptions (his free→paid conversion is low; maybe he gives away too much). And advertising products while claiming to help geeks feel safe makes some (vocal) geeks feel unsafe, reducing subscriber revenue. You can keep adding observations and connections, switching perspectives, comparing effects & time lags, and finally choose which experiment to try next. Why it works: one kind of stuck thinking grows from frustration ("everything I do makes it worse"); influence diagrams (learned from Gerald Weinberg) force more precise questions and new perspectives until you reach a genuine, specific conundrum (here: can sponsorships build instead of erode trust?)—then you have something to do. Thinking in terms of effects affecting effects is the foundation for Inhibiting Loop and Reinforcing Loop.

### 88. Trust The Market
**Pattern:** A market is acting in a confusing or irrational or unsustainable way.
**Transformation:** Answer the question, "What would have to be true for the market to be right & me to be wrong?"
**Example:** Early in COVID many people moved out of San Francisco (a moving van on every block every day), yet rents & house prices didn't drop—contradicting the naive "demand decreases, prices decrease". What would have to be true? Half the vans were bringing people into vacated units; pre-COVID unmet demand was so large that demand still outstripped supply; markets take a while to adjust; a grand conspiracy of banks, real estate & government (when you reach conspiracy theories, it's time to turn back).
**Detail:** Born of Beck's drive to make sense of a confusing world (he grew up in a chaotic household). A great example of a Thinkie: you don't use it to generate good ideas, you generate ideas you then evaluate. Sometimes markets seem irrational because they are—you see clearly. But when your group is wrong, you gain advantage from being the first to re-evaluate your position. Generalized by Thinkie What Fact?.

### 89. One Room At A Time
**Pattern:** You're stalled completing a long, static list of tasks.
**Transformation:** Start at one end of the list & work through it in order.
**Detail:** Origin: after building their house, Beck's family moved the most important items out of a trailer, leaving it half full for years; moving the rest in priority order meant ever-waning motivation (since everything left was, by definition, less important)—"Zeno's Moving Out Of The Trailer Paradox". They emptied one room at a time, closed the door & never opened it. Same with drafting the remaining Thinkies after using Fun Bit to choose them. Constraints: you have a known list (not for getting started or discovery); order doesn't matter much any more (early on it did—Obviously & Can't/Because went first because they're accessible); all items need to be done (a different Thinkie covers drawing a line & saying "Good enough!"). Under those constraints, One Room At A Time is close enough to optimal & doesn't suffer the diminishing motivation of most-important-first.

### 90. Complain & Propose
**Pattern:** You disagree with a decision & want to send a complaint up (or across) the organization. (Implied—the post tells a story rather than stating a formal pattern.)
**Transformation:** Always bundle a proposal with the complaint: say what you would like to happen.
**Detail:** Story from Apple, 1988: young, cocky Beck emailed head of engineering Jean-Louis Gassée about how stupid a decision was. JLG called him in and said: "Think about it from my perspective. What am I going to do if I agree with you? Ask my report for a proposal, who asks his report… eventually your boss asks you. Rewrite your message and make a proposal—you'll save us a week and get to solve the problem you want to solve." Lessons: (1) it's hardly ever that big a deal; (2) always bundle a proposal with a complaint—vent or think things through in private, and when you increase the scope of a communication, say what you'd like to happen; (3) "Think about it from my perspective"—communication begins by putting yourself in your reader's place (see also My Perspective); bonus for the senior: don't get caught up in young hotshots' emotions—assume good intentions & lack of skills. Beck applied it when reacting to an "80-hour weeks or else" pronouncement (see Match the Pipes).

### 91. Ergodic (Ergodicity)
**Pattern:** The outcome for an individual is different from the outcome for a population (1000 people playing Russian Roulette once: ~167 die; 1 person playing 1000 times: dies).
**Transformation:** Distinguish resilient (ergodic) parts of the system, where failure is temporary, from survival (non-ergodic) parts, where failure is game over; transform some of the irreversible cost into the reversible part of the population.
**Detail:** "Good Thinkie, awful name." Example: a medical organization using LLMs to summarize patient histories saves practitioner time & improves care for most, but in rare cases the obscure, not-clearly-relevant detail is the hint to effective treatment—the summarizer degrades care for the unlucky few. Resilient systems need maintenance, monitoring & care but allow free experimentation; survival systems should be approached conservatively, and if possible survival risk should be transferred to resilient parts. Life insurance transfers a family's financial survival risk (losing an earner) to society, where its impact is negligible. Inspired by Luca Dellanna's *Ergodicity*; the root of Survivable?.
