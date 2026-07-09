---
name: verify-understanding
description: Before merging a change, prove it is actually understood — produce a demo-first explainer for the reviewer and a short quiz for yourself, and do not merge until every quiz question is answered correctly. Use when finishing a change (yours or an agent's) before merge or handoff, when a change is large or subtle, or when you want reviewer buy-in fast. Guards against shipping code whose behavior nobody can account for.
---

# Verify Understanding

A change you cannot explain, and cannot be quizzed on, is a change you are
trusting on faith. Two artifacts convert faith into proof: an **explainer** that
gets the reviewer to yes, and a **quiz** that gets you to understanding. Both are
cheap; a wrong merge is not.

## Workflow

1. **Explainer, demo first.** Open with the result the reviewer can see — a GIF,
   a screenshot, or a runnable link — *then* what changed, *then* the parts most
   likely to be wrong. Lead with proof it works; reviewers approve what they can
   watch. Pull the risky bits from `implementation-notes.md` (see
   implementation-notes).
2. **Quiz.** Write a handful of questions on the change: why this approach, what
   breaks if input X, which contract must hold, what the notes flagged as risky.
   Aim at the load-bearing decisions, not surface facts the diff already shows.
3. **Gate.** Answer the quiz. **Do not merge until every answer is correct and
   complete.** A question you cannot answer is an unknown still sitting in the
   diff — resolve it, then re-quiz.

## Rules

- The merge gate is the only done-condition. Writing the explainer is not "done";
  passing the quiz is.
- When an agent wrote the change, the human takes the quiz. When you wrote it, a
  fresh agent writes the questions — the author's eyes are primed and pass what
  they should catch.
- Quiz what a future maintainer (or you in six months) would trip on, not trivia.
