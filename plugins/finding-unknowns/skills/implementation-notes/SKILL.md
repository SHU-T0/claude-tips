---
name: implementation-notes
description: Keep a running implementation-notes.md while building — capture every deviation from the plan, edge case discovered, and non-obvious judgment call, each with its reason. Use during implementation of a spec or plan, especially when you diverge from it, hit a surprise the plan did not anticipate, or decide something a reviewer will later question. Feeds the explainer and the understanding check at merge time.
---

# Implementation Notes

The plan is the map; implementation is where the territory answers back. Every
place the code forces a decision the plan did not foresee is an unknown surfacing
in real time — capture it while it is cheap, or re-derive it painfully later.

## Workflow

1. On the first deviation or surprise, create `implementation-notes.md` beside
   the work (or in the spec folder).
2. Append an entry whenever you **deviate** from the plan, **discover an edge
   case**, or make a **judgment call** the plan did not specify. Skip the
   routine — a note earns its place by recording a decision or a surprise, not
   progress.
3. Keep each entry to three lines: **Plan** (what it said or assumed), **Did**
   (what you actually did), **Why** (what the territory taught you).
4. At merge or handoff, feed these notes into the change explainer and the
   understanding check (see verify-understanding).

## Rules

- Append-only within a pass — do not rewrite history; the trail of wrong turns is
  the value.
- A note is a *decision or a discovery*, never a status log. "Implemented the
  importer" is not a note; "the API returns null for archived rows, so the
  importer skips them" is.
- Name the file identically everywhere so the next session and the reviewer both
  find it without hunting.
