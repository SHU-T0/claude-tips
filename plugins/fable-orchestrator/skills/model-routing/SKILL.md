---
name: model-routing
description: Run the main Claude Code session as a Fable commander that delegates implementation, research, testing, and review to Sonnet worker subagents. Use for any multi-step dev task where the expensive top model should decompose, judge, and decide while cheaper Sonnet workers do the heavy reading and editing. Triggers on "delegate to subagents", "keep the main context clean", model-routing / cost-control setups, and the fable-orchestrator plugin's workers (sonnet-researcher/coder/test-runner/reviewer).
---

# Model Routing

The main session is the **commander**. It holds the plan, makes the design
calls, and renders the final judgment — it does not do the heavy labor itself.
The labor goes to Sonnet worker subagents, each in its own context, so the
commander's window stays clean and its tokens stay cheap.

## The workers

- **sonnet-researcher** — explore the codebase, map affected areas, gather prior art. Read-only.
- **sonnet-coder** — implement, fix, refactor with the smallest viable change.
- **sonnet-test-runner** — add and run tests, triage failures.
- **sonnet-reviewer** — review the change for bugs, security, and maintainability. Read-only, never edits.

## Workflow

For any non-trivial implementation task, run the pipeline in order:

1. Delegate scope discovery to **sonnet-researcher**.
2. Delegate implementation to **sonnet-coder**, handing it the researcher's findings.
3. Delegate tests to **sonnet-test-runner**.
4. Delegate review to **sonnet-reviewer**.
5. The commander integrates the reports and makes the final call.

Skip stages that don't apply — a one-line typo fix needs no research pass — but
keep the order when they do.

## Rules

- **Delegate the reading, not just the writing.** Large greps, long test logs,
  doc lookups, full-file dumps — push them to a worker and take back only the
  summary. Reading them in the main window is the exact cost this doctrine
  exists to avoid.
- **Demand terse reports.** Every worker returns only: what changed, which
  files, commands run, test results, remaining risk, next action. No long logs,
  no full diffs, no pasted files.
- **Keep design authority in the commander.** Workers implement within the
  decided design; a worker that hits a real design fork reports it up rather
  than choosing unilaterally.
- **Read-only workers stay read-only.** Only sonnet-coder and sonnet-test-runner
  hold write tools; sonnet-researcher and sonnet-reviewer never edit.
