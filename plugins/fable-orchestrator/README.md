# fable-orchestrator

Run Claude Code as a **Fable commander** that delegates the heavy work to
**Sonnet workers**. The expensive top model decomposes, judges, and decides;
cheap Sonnet subagents do the reading, editing, testing, and reviewing — each in
its own context, so the commander's window stays clean and its tokens stay
cheap.

## What ships

| Piece | Kind | Role |
|-------|------|------|
| `model-routing` | skill | The commander doctrine — when and how to delegate. |
| `/orchestrate` | command | Run a task through research → implement → test → review. |
| `sonnet-researcher` | agent | Read-only scope discovery. |
| `sonnet-coder` | agent | Implement / fix / refactor. |
| `sonnet-test-runner` | agent | Write and run tests, triage failures. |
| `sonnet-reviewer` | agent | Read-only review gate. |
| `fable-coordinator` | agent | Optional main-session commander persona for `claude --agent`. |

## Install

```
/plugin marketplace add shu-t0/claude-tips
/plugin install fable-orchestrator@claude-tips
```

## Use

Start the main session on Fable and let it delegate:

```
claude --model fable
```

Then either drive it yourself — the `model-routing` skill fires on multi-step
dev tasks — or run the pipeline explicitly:

```
/orchestrate refactor the auth middleware to reject javascript: URLs
```

For a stricter commander that plans before it acts, launch the coordinator
persona:

```
claude --agent fable-coordinator --permission-mode plan
```

## Design choices

- **Models are aliases (`sonnet`, `fable`), not pinned IDs**, so the plugin
  keeps working when the next Sonnet/Fable version ships. Pin full IDs
  (`claude-sonnet-5`, …) in a fork if you need fixed cost/behavior.
- **The workers share your working tree — no `isolation: worktree`.** This
  pipeline is sequential and dependent: the test-runner and reviewer must see
  the coder's edits. Worktree isolation would strand each worker's changes on a
  separate branch. Reach for worktree isolation (or agent teams) only for
  *parallel* fan-out where workers would otherwise collide.
- **Read-only workers stay read-only.** `sonnet-researcher` and
  `sonnet-reviewer` carry no `Edit`/`Write`; only `sonnet-coder` and
  `sonnet-test-runner` can change files.
- **`fable-coordinator` ships in default permission mode** so it works on
  install. Add `--permission-mode plan` at launch if you want plan-first.

## Going parallel (optional)

For large parallel work — separate frontend/backend/review streams, big
refactors, multi-hypothesis bug hunts — Claude Code's experimental **agent
teams** spawn independent Sonnet teammates that message each other. It costs
more tokens than subagents and is off by default:

```
export CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1
```

Start with the subagents here; escalate to teams only when you actually need
parallelism.

---

**日本語メモ:** メインセッションを **Fable の指令塔**として使い、実装・調査・
テスト・レビューを **Sonnet の worker subagent** に委任する構成です。指令塔は
分解・設計判断・最終判断だけを担い、重い読み書きは各 worker が別コンテキストで
処理するので、メインの文脈は汚れず、トークンも安く済みます。まずは
`claude --model fable` + `/orchestrate` から。並列化が必要になったら agent
teams に拡張してください。
