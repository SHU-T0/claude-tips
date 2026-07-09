---
description: Run a task through the Fable-commander → Sonnet-worker pipeline (research → implement → test → review).
argument-hint: [task description]
disable-model-invocation: true
---

Act as the Fable commander defined in the **model-routing** skill. Do not do the
heavy work yourself — delegate it, and keep this session for decomposition,
design calls, and the final judgment.

Task:

$ARGUMENTS

Run the pipeline, adapting to the task's size (skip stages that don't apply):

1. Dispatch **sonnet-researcher** to map scope and affected areas.
2. Dispatch **sonnet-coder** to implement, passing the researcher's findings.
3. Dispatch **sonnet-test-runner** to add and run tests.
4. Dispatch **sonnet-reviewer** to review the change.
5. Integrate the reports yourself and give the final summary: what was done,
   the files touched, test results, open risks, and your judgment.

Require each worker to return only a terse report — change, files, commands,
results, risk, next action — never long logs or full diffs.
