# Long-Horizon Coding

Long-Horizon Coding is an agent skill for substantial coding goals that are expensive or difficult to complete in one uninterrupted stretch. It helps a coding agent plan a viable route before making changes, track progress and resource runway, and reach the destination without unnecessary pauses.

## What it helps with

The skill guides an agent to:

- Recognize when a goal is long-horizon because its route is distant (many turns, tool calls, or difficult intermediate work) or because it consumes significant resources.
- Define a measurable destination and organize work into verifiable waypoints, preferably using project tickets with acceptance criteria.
- Estimate costs and uncertainty across relevant resources: tool calls, model/provider allowances or API spend, compute, storage, and time.
- Inspect and configure available harness limits before execution, where supported, and plan a continuation strategy when limits cannot be adjusted.
- Work autonomously while progress and constraints remain on track, with brief updates at completed waypoints.
- Pause for steering when budgets or constraints are threatened, the route becomes invalid, or repeated failed test-fix attempts indicate an anomaly.
- Preserve a temporary journey record across handoffs, then verify completion and discard the record when the goal is reached.

The goal is uninterrupted progress when things are healthy, and early, useful intervention when they are not.

## Install

Install this skill from the repository with the [Vercel Skills CLI](https://github.com/vercel-labs/skills):

```bash
npx skills@latest add jetpen/long-horizon-coding --skill long-horizon-coding
```

Or use the skill-selector shorthand:

```bash
npx skills@latest add jetpen/long-horizon-coding@long-horizon-coding
```

## Skill source

The agent instructions are in [`skills/long-horizon-coding/SKILL.md`](skills/long-horizon-coding/SKILL.md).
