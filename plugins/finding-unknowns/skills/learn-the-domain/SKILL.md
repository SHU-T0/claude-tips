---
name: learn-the-domain
description: Have Claude teach you a domain before you generate options or commit to an approach — how it works, what "good" looks like, the common potholes, and the prior art. Use when you cannot yet judge whether an output is good ("do I know how good this can be?"), when you don't understand how a mechanism or domain actually works, or when you catch yourself picking among options you can't rank. Narrower than map-unknowns, which maps a whole task: this closes one knowledge gap so you can prompt and review from knowledge instead of guessing.
---

# Learn the Domain

Reacting to options only extracts taste when you can already recognize good. When
you *can't* — you don't know how good the result could be, what the domain's
conventions are, or which potholes exist — generating variations is noise, because
you cannot tell the better one from the worse. The move is to have Claude **teach
you** until you can prompt and judge from knowledge.

The Fable-5 launch video is the tell: the author first asked for a few
color-grade variations to pick from, then realized they didn't know what "good"
looked like — so they asked Claude to teach them color grading instead. Teaching
came before choosing.

## Workflow

1. **Name what you can't judge.** State the specific thing you cannot yet evaluate
   or understand — the quality ceiling ("how good can this be?"), the mechanism
   ("how does X actually work?"), or the landscape ("how do people usually do
   this?").
2. **Ask to be taught, not served.** Have Claude explain the domain: how it works,
   what separates good from mediocre, the standard approaches, and the common
   mistakes — grounded in primary sources or real code, not hand-waving.
3. **Check you can now judge.** You are done when you can look at a candidate and
   say *why* it is good or bad, and write a prompt that asks for the right thing.
   If you still can't, you haven't learned enough — keep going.
4. **Then generate or react.** Only now produce options, prototypes, or a plan,
   with criteria you can actually apply.

## Rules

- Teaching precedes choosing. If you catch yourself picking among variations you
  cannot rank, stop and come back here.
- A blind-spot pass is teaching, not just a list: the point is that Claude
  *explains* the unknowns so your next prompt is written from knowledge.
