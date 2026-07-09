# finding-unknowns

A Claude Code plugin for **finding your unknowns** — surfacing what you don't
know about a task *before, during, and after* you implement it, so the fog gets
burned off while it is still cheap.

Based on Anthropic's field guide
[*A field guide to Claude Fable: finding your unknowns*](https://claude.com/blog/a-field-guide-to-claude-fable-finding-your-unknowns).
As models get more capable, the bottleneck moves from the model's ability to
**your unknowns** — the gap between the map (your prompt, plan, context) and the
territory (the real code, domain, and intent). These techniques are
model-agnostic: they sharpen work on Sonnet and Opus just as much as Fable.

## What's inside

| Component | Kind | What it does |
|---|---|---|
| `map-unknowns` | skill | A staged walk through the four quadrants of unknowns that ends with a written `unknowns-map.md` and a volatile-first plan — run it *before* implementing. |
| `learn-the-domain` | skill | When you can't yet judge whether an output is good, have Claude *teach* you the domain — how it works, what "good" looks like, the potholes — before generating options or reacting. |
| `implementation-notes` | skill | Keep a running `implementation-notes.md` of every deviation, edge case, and judgment call *during* the build. |
| `verify-understanding` | skill | *After* a change, produce a demo-first explainer plus a quiz, and gate the merge on answering it. |
| `/unknowns` | command | One-line entry point that kicks off a `map-unknowns` walk on a task. |
| `blind-spot-scout` | subagent | A fresh, unprimed set of eyes that hunts unknown-unknowns in a task, plan, or diff. |

### The four quadrants

|  | Known (you can grasp it) | Unknown (you can't yet) |
|---|---|---|
| **Aware** | Known knowns — write them into the plan | Known unknowns — resolve one at a time |
| **Unaware** | Unknown knowns — react to prototypes to surface tacit taste | **Unknown unknowns** — run a blind-spot pass |

## Install

```
/plugin marketplace add shu-t0/claude-tips
/plugin install finding-unknowns@claude-tips
```

Then use it:

```
/finding-unknowns:unknowns build a CSV importer for the billing table
```

Or let Claude invoke the skills on their own when a task is ambiguous, when you
finish a change, or during a build — each skill's description carries its own
triggers.

## How the pieces fit

```
BEFORE ──▶ map-unknowns ──▶ (blind-spot-scout) ──▶ unknowns-map.md + plan
             └─ can't judge "good"? ──▶ learn-the-domain (get taught first)
DURING ──▶ implementation-notes.md   (deviations, edge cases, judgment calls)
AFTER  ──▶ verify-understanding       (demo-first explainer + quiz merge gate)
```

Reacting to variations only works once you can recognize good. When you can't —
you don't know how good it could be, or how the domain even works — `learn-the-domain`
has Claude teach you first, so you prompt and review from knowledge, not guesses.

## License

MIT
