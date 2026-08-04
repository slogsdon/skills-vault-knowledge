# Source Recipes

> Per-source extraction rules for `/source-mine`. Derived from the mining runs of
> 2026-04-08 → 2026-04-18 that built the original knowledge graph.

## GitHub (public API, no auth)

```bash
curl -s "https://api.github.com/users/<user>"
curl -s "https://api.github.com/users/<user>/repos?sort=updated&per_page=100&type=owner"
curl -s "https://api.github.com/users/<user>/starred?per_page=100"
```
Extract: active vs dormant repos (by `pushed_at`), language mix, what the starred
set says about interests and tools followed. Starred repos are the signal most
often missed — they show direction before the code does.

## Local filesystem (`~/Code`)

Per project: stack (from `package.json`, `Cargo.toml`, `go.mod`, `composer.json`),
the README's stated purpose, `git -C <path> log --oneline -5` for recent activity,
and last-modified for liveness. Distinguish **active** (commits this month) from
**parked** from **abandoned** — the distinction is the whole value of the sweep.

## Google (Drive + Gmail)

Via the Google MCP tools. Extract: recurring document types, project names that
appear in both Drive and mail, and commitments made in mail that never reached
the vault. Read-only — never send, archive, or delete while mining.

## ChatGPT / Claude.ai / Perplexity conversation history

Via the browser tools, with the user already signed in. Scan the conversation
list first, then open only the substantive ones — skip one-off lookups. Extract:
frameworks and mental models developed, recurring themes across threads, and
research that was never written down anywhere else.

These are the highest-yield and slowest source. Timebox it and say what you
skipped.

## The vault itself

Re-reading the vault counts as mining when the goal is to surface what is already
there but unlinked. Prioritize `Daily/` (richest personal signal), then `Inbox/`,
then `Archive/`.

## Rules for every source

- **Read-only at the source.** Mining never writes back to Gmail, GitHub, or a chat service.
- **Attribute every extracted note** to its source and the date mined, in the note body. An unattributed claim is unverifiable a month later.
- **Skip the transient.** Order confirmations, notifications, one-line lookups. If it will not matter in six months, it does not belong in the graph.
- **Report the skips.** A mining run that silently sampled reads as exhaustive when it was not.
