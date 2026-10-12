---
name: long-horizon-coding
description: Use for costly, multi-stage coding goals.
---

# Long-Horizon Coding Skill

Use this skill to plan and execute coding goals whose destination is distant or costly to reach. A goal is long-horizon when either its route has substantial distance (turns, tool calls, or difficulty) or its resource cost is substantial; explain the signals and calibrate with the user when uncertain. The aim is to reach the goal with a viable route, visible runway, and minimal interruption—not to add ceremony to ordinary work.

## 1. Detect and assess

1. On a potentially long-horizon coding request, make a lightweight assessment before substantive work. Estimate route distance and resource cost from the request and available context. Read-only discovery—such as inspecting the repository, existing specs/tickets, project conventions, and available telemetry—is allowed before plan approval when its cost is ordinary and material costs are surfaced.
2. If neither distance nor cost is substantial, proceed normally. If either is substantial, state the concrete signals briefly and enter this workflow. If uncertain, state the uncertainty and ask the user to calibrate; do not silently impose the workflow on a clearly bounded task.
3. Identify the destination in observable terms. Reuse approved specs and project tickets when they adequately define it. If they do not, propose the missing spec and acceptance-criteria tickets as part of the route; do not invent approval or ticket conventions that the project does not use.

## 2. Establish budgets and constraints

Inventory relevant resources separately, including where applicable:

- Tool-call and interaction runway, including per-turn limits.
- Model/provider token allowances, subscription windows, or prepaid API spend.
- Compute, storage, elapsed time, and other project-specific scarce resources.

For each resource, classify its bound as an immutable external hard limit, a user-set cap/target, or an estimate. Respect external limits; never plan to exceed them. Preserve user-set bounds unless the user approves a change. Use measured telemetry where available. For unknown or poorly observable costs, label the estimate and confidence, give its evidence/basis, and propose a conservative cap or measurement step. If no cap can be proposed responsibly, ask before proceeding.

Estimate ranges and confidence per ticket and for the overall route, with an explicit contingency reserve. Separately estimate the next indivisible work slice before starting it. Use observed actuals to recalibrate later estimates. Compare the slice's plausible worst-case cost with remaining runway: do not begin work that is foreseeably unsafe to complete within hard limits or approved bounds.

Before execution, inspect all capabilities the harness exposes for adjusting operational limits that could interrupt the journey (for example, maximum tool calls per turn, continuation or context budgets, and delegated-work limits). Where supported, configure them to fit the approved route and safety reserve, within provider, product, user, and system limits. Verify that each adjustment took effect and record it in the plan. Do not assume a limit is adjustable; if no capability exists or a setting cannot be verified, record that and plan a continuation handoff. Never attempt to bypass or misrepresent an enforced limit.

## 3. Select a route and seek approval

Before substantive changes or costly execution, present a concise plan that includes:

- Destination and measurable completion bar.
- Route and ordered waypoints. Prefer project tickets with explicit acceptance criteria; a waypoint is complete only when its criteria and required verification are satisfied. Include required lifecycle steps such as PR/MR merge when the project requires them. Let normal project automation close completed tickets.
- Per-ticket and overall resource estimate ranges, confidence, basis, and contingency reserve.
- Hard limits, user-set caps/targets, other constraints, and planned safeguards, including which harness limits can be configured and the verified settings (or explicit lack of capability).
- A feasible baseline and at least one lower-cost alternative; compare outcome, resource use, risk, and reversibility. Preserve every hard limit first. Optimize stated user priorities; if none are stated, show tradeoffs and recommend a best-value route without assuming one resource outranks another.
- Checkpoint cadence and explicit warning/pause thresholds, including the signal that current-slice completion may exceed remaining runway and the fallback continuation strategy if an enforced harness limit cannot be adjusted.
- Assumptions, uncertainties, and any discovery or measurement needed.

Ask the user to approve the route, estimates, constraints, and any proposed provisional caps before substantive execution. Do not treat silence as approval. If no feasible route fits the hard limits and approved bounds, explain why and offer alternatives rather than starting.

## 4. Keep a journey record

Maintain a concise record in a temporary location chosen by the agent harness, not in the project repository by default. It exists for the journey lifecycle, may be carried across session handoffs, and can be discarded once the destination is reached. Record:

- Goal, completion bar, approved baseline, resource budgets, constraints, assumptions, and selected route.
- Ticket/waypoint acceptance criteria and expected ranges.
- Decisions and approvals, actual resource use, current estimates-to-complete, deviations, risks, and next waypoint.

Refresh the record at each waypoint, after a material deviation or surprise, and before a handoff. If the harness cannot preserve the record across a handoff, disclose that limitation and provide the state in a transfer note. Do not put secrets or credentials in the record.

## 5. Execute with runway checks

Proceed autonomously between waypoints while progress and constraints remain on track. Before each indivisible work slice, check that its estimated plausible worst-case cost fits within remaining runway and bounds. Track actual versus planned progress and resource use as work proceeds; use available telemetry and label estimates rather than presenting them as measured facts.

If a harness limit interrupts a slice despite preparation, preserve the journey record and resume through the harness's supported continuation or handoff mechanism. On resumption, first re-check state, remaining runway, and waypoint progress. Continue automatically without asking for steering only when substantial, verifiable progress is being made toward the next waypoint and every approved measure remains on track; otherwise pause and request steering. Do not treat a forced turn boundary or handoff alone as evidence of failure or as a reason to abandon the journey.

Reassess immediately when a tool/provider failure, blocker, unexpected scope, material variance, changed assumption, or other risk signal occurs. Record the event, re-estimate the remaining route and resources, and continue without interrupting the user only if the approved route remains feasible and in bounds. Small implementation decisions inside approved acceptance criteria do not need separate approval.

## 6. Checkpoints, alerts, and re-planning

At every completed ticket/waypoint, compare expected with actual progress and spend; recalculate remaining runway and constraints, assess risks, and identify the next segment. Update the journey record. When all measures are on track, give a brief, non-blocking checkpoint and continue uninterrupted.

Pause before crossing a limit or committing to a slice likely to exhaust its runway. Also pause when progress materially underperforms, a hard limit or other constraint is violated or significantly at risk, a route assumption is invalidated, or a required decision falls outside approved bounds. In particular, treat foreseeable inability to finish the current task slice before tool-call, provider-window, or prepaid-spend exhaustion as an early warning—not a failure to discover after exhaustion. A limit-triggered interruption is not by itself underperformance: after resuming, continue without user steering when substantial verifiable progress toward the next waypoint is evident and the journey is otherwise on-track by every measure.

For a test-fail-fix loop, count consecutive failed fix-and-retest attempts against the same underlying problem. After three unsuccessful attempts, treat the pattern as an anomaly: stop repeating the same loop, summarize hypotheses tried and evidence, reassess the route and budget, and request steering before further materially similar attempts. A distinct diagnosis or materially different fix may proceed only if it remains within the approved route and bounds; reset the counter only when evidence shows the underlying problem or strategy has genuinely changed.

When pausing, report the observed evidence, expected-versus-actual variance, remaining runway, affected bounds, consequence of continuing, and feasible choices. Recommend a revised route, smaller slice, measurement, or approved cap change as appropriate. Obtain approval before changing scope, priorities, user-set bounds, or materially changed assumptions. After approval, rebaseline estimates and the journey record before resuming. Never silently trade away a hard constraint or user priority.

## 7. Verify destination and finish

The destination is reached only when every approved ticket's acceptance criteria are verified, required tests and other verification pass, required lifecycle steps are complete, and the delivered result matches the stated goal. Ticket closure follows the project's normal lifecycle automation after these conditions are met; human review is not a substitute for automatic verification. If any condition is unmet, report the remaining work and do not claim completion.

On completion, give a concise final report of delivered outcome, verification evidence, planned-versus-actual resource use, remaining constraints or follow-ups, and any deviations. Then discard the temporary journey record. If the route proves infeasible, stop safely, preserve the record for continuation, and report the blocker and options.

## Operating principles

- Protect hard limits and the ability to finish the current work slice; detect jeopardy before the failure point.
- Make estimates, confidence, evidence, and unknowns visible. Keep measured actuals distinct from forecasts.
- Treat approval as bounded: execute freely inside the approved route and acceptance criteria; ask only when risk or material change requires steering.
- Keep routine updates short. Interruption is for preventing failure, not for narrating every step.
