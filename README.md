# claude-tips

A small [Claude Code](https://code.claude.com) plugin marketplace.

## Plugins

### [finding-unknowns](plugins/finding-unknowns)

Surface a task's unknowns *before, during, and after* implementation — a
`map-unknowns` quadrant walk, a `learn-the-domain` teaching pass, an
`implementation-notes` deviation log, a merge-time `verify-understanding` check,
and a `blind-spot-scout` subagent.
Based on Anthropic's *[A field guide to Claude Fable: finding your unknowns](https://claude.com/blog/a-field-guide-to-claude-fable-finding-your-unknowns)*.

## Install

```
/plugin marketplace add shu-t0/claude-tips
/plugin install finding-unknowns@claude-tips
```

> Replace `shu-t0/claude-tips` with your GitHub `owner/repo` if you forked or
> renamed it.

## Develop locally

```
claude --plugin-dir ./plugins/finding-unknowns   # load without installing
claude plugin validate .                          # validate the marketplace
```

---

**日本語メモ:** モデルが賢くなるほど、品質の律速は「モデルの能力」から
**あなたの不明点（unknowns）** に移る。`finding-unknowns` は、その不明点を
実装の前・中・後で安く炙り出すためのスキル群です。詳しくは
[plugins/finding-unknowns](plugins/finding-unknowns) を参照。

## License

MIT
