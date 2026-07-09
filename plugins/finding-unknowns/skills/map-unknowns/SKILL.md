---
name: map-unknowns
description: Map a task's unknowns before implementing it — a staged walk through four quadrants (known knowns, known unknowns, unknown knowns, unknown unknowns) that ends with a written unknowns map. Use when a request is ambiguous or underspecified, the codebase or domain is unfamiliar, the work is "I'll know it when I see it" (design, taste), a reference must be understood before porting, or before committing to an implementation plan. The map is not the territory; burn off the fog before writing code.
---

# Map Unknowns

The prompt, the plan, and the context window are the **map**. The codebase, the
domain, and the user's real intent are the **territory**. The gap between them is
the **unknowns** — and an unknown found before code costs minutes, while the same
unknown found three PRs later costs the three PRs. This skill walks that gap to
zero *before* implementation. The deliverable is a written map, not code.

## Workflow

Walk the four quadrants in order, one at a time, naming the quadrant you are in
so the user always knows where they stand on the map. **Read the territory —
inspect the repo — before asking anything the code can answer.**

1. **Declare the starting point.** Ask the user, and state for yourself, how
   familiar each side already is with this codebase, domain, and goal.
   Habituation decides which unknowns are real: a stranger's blind spots are not
   an expert's. This single disclosure changes everything downstream.

2. **Known knowns — settle the ground.** Inventory what is already certain:
   constraints living in the repo, decided requirements, sacred contracts that
   must not break. Write them down; this is what goes straight into the plan.

3. **Known unknowns — resolve one at a time.** List the open questions you can
   name. Ask the highest-leverage first — the ones that would change the
   architecture, not the paint color — **one question per turn, each with your
   recommended answer** so the user accepts, rejects, or edits in one word.

4. **Unknown knowns — react, don't imagine.** Surface tacit taste nobody has put
   into words. Never ask the user to describe what they want when you can hand
   them something concrete to react to: a decisions table, or — for anything
   visual — **three or four genuinely divergent directions built as throwaway
   HTML**, not variations on one. Reaction extracts knowledge the user holds but
   cannot articulate unprompted.

5. **Unknown unknowns — blind spot pass.** Name it out loud: hunt for what is not
   being considered at all — unstated assumptions, domain conventions this plan
   likely violates, failure modes nobody raised. For a fresh, unprimed
   perspective, dispatch the **blind-spot-scout** subagent on the task and plan;
   primed eyes pass what fresh eyes catch.

6. **Hand over the map.** Produce `unknowns-map.md`: the four quadrants filled in,
   plus a first implementation plan that **orders the most volatile decisions
   first** (data models, type seams, UX flow — whatever ripples furthest when it
   changes). The map in the user's hands is the *only* done-condition. Do not
   start implementing here — that is a separate task that begins after the map is
   handed over.

## Rules

- **Order governs presentation, never disclosure.** A finding that bears on a
  decision in flight is surfaced the moment you have it, then filed under its
  quadrant — never held back for its stage's scheduled turn.
- **The best reference is source code** — a working implementation, even in
  another language, beats prose describing one. Ask for one, or go find one.
- **Cite real files you actually read.** A fabricated specific destroys the map's
  authority; label a guess as a guess.
- **Reacting beats imagining** at every stage: concrete artifact first,
  open-ended question last.
