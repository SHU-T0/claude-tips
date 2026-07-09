---
name: map-unknowns
description: Map a task's unknowns before implementing it — a staged walk through four quadrants (known knowns, known unknowns, unknown knowns, unknown unknowns) that ends with a written unknowns map. Use when a request is ambiguous or underspecified, the codebase or domain is unfamiliar, the work is "I'll know it when I see it" (design, taste), a reference must be understood before porting, before committing to an implementation plan, or when a long-horizon task keeps coming back wrong — a sign the unknowns, not the model, are the bottleneck. The map is not the territory; burn off the fog before writing code.
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

2. **Known knowns — settle the ground.** First calibrate scope with a quick
   brainstorm of what is in and out — a plan that is too narrow or too wide is
   itself an unknown; Claude surfaces options you would miss but can miss the
   forest for the trees, so you make the call. Then inventory what is already
   certain: constraints living in the repo, decided requirements, sacred
   contracts that must not break. Write them down; this is what goes straight
   into the plan.

3. **Known unknowns — resolve one at a time.** List the open questions you can
   name. Ask the highest-leverage first — the ones that would change the
   architecture, not the paint color — **one question per turn, each with your
   recommended answer** so the user accepts, rejects, or edits in one word.

4. **Unknown knowns — react, don't imagine.** Surface tacit taste nobody has put
   into words. Never ask the user to describe what they want when you can hand
   them something concrete to react to: a decisions table, or — for anything
   visual — **three or four genuinely divergent directions built as throwaway
   HTML**, not variations on one. Reaction extracts knowledge the user holds but
   cannot articulate unprompted — but it only works when you can recognize good
   on sight. When you cannot judge quality even while looking (the "do I know how
   good this can be?" test), run **learn-the-domain** first; variations you can't
   rank are noise. Prototypes serve a second job here too: throwaway spikes that
   test whether an approach is even feasible, not only what looks right.

5. **Unknown unknowns — blind spot pass.** Name it out loud: hunt for what is not
   being considered at all — unstated assumptions, domain conventions this plan
   likely violates, failure modes nobody raised. For a fresh, unprimed
   perspective, dispatch the **blind-spot-scout** subagent on the task and plan;
   primed eyes pass what fresh eyes catch.

6. **Hand over the map.** Produce `unknowns-map.md`: the four quadrants filled in,
   plus a first implementation plan that **orders the most volatile decisions
   first** (data models, type seams, UX flow — whatever ripples furthest when it
   changes). The map in the user's hands is the *only* done-condition. Do not
   start implementing here — implementation is a separate task, best begun in a
   **fresh session** that carries the map, the plan, and any prototype as
   artifacts, so the build runs on a clean context window rather than this worn
   one.

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
- **Instructions miss in both directions.** Too specific and Claude follows a
  path it should have pivoted from; too vague and it fills the gap with generic
  best practices that don't fit this work. Aim for intent plus room to adapt —
  and treat a wrong result as a signal the unknowns were underspecified, not
  just that the prompt needs more detail.
