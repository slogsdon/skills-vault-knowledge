---
name: source-mine
description: Mine one external source — GitHub, Google Drive/Gmail, ChatGPT or Perplexity history, or the local filesystem — into attributed vault notes on a fixed schema. Use when Shane says "mine my GitHub", "pull context out of my ChatGPT history", "what's in ~/Code that isn't in the vault", "extract X into the knowledge graph", or when bootstrapping vault context for a new project. Do NOT use for a single document or article (use /ingest), for reading the vault itself (use /vault-retrieve), or for web research on a topic (use /research-sweep).
---

# Skill: /source-mine [source]

Turn an account, corpus, or directory you already own into attributed vault notes — the sweep that gets the graph from empty to useful, and the one nobody wants to hand-write twice.

**Don't:** write a note without its source and mine date in the body; an unattributed claim is unverifiable a month later and indistinguishable from something you made up. **Don't** mine and synthesize in one pass — extract first, decide what deserves a note second, or the interesting-but-irrelevant all gets written up. **Don't** touch the source: mining is read-only, always.

## Inputs

`source` is one of: `github`, `filesystem`, `google`, `chat-history` (ChatGPT / Claude.ai / Perplexity), or `vault` (re-reading for unlinked material). If ambiguous, ask which — the extraction rules differ per source.

## Steps

1. **Read [source-recipes.md](../_lib/source-recipes.md)** for this source's endpoints, extraction targets, and known pitfalls.
2. **Inventory before extracting.** List what exists — repo count, thread count, directory listing — and report the scale. A sweep whose size is unknown at the start silently becomes a sample.
3. **Extract to a scratch list**, not to the vault. One line per candidate: what it is, why it might matter, where it came from.
4. **Check each candidate against the vault** before writing: `obsidian search query='<candidate>' limit=5`. Existing note → append an `## Update — <date>` section. No note → create.
5. **Write the notes.** Route by type:
   - a durable idea or framework → `Knowledge/Concepts/` via `/ingest` (it enforces the Vault Schema)
   - project state → `Knowledge/Projects/<project>/`
   - an external artifact worth keeping → `Knowledge/Reference/`
   - anything you cannot place → `Inbox/`, for `/inbox-triage` to route
6. **Attribute in the body:** `*Source: <source> — mined <date>*`.
7. **Commit the vault** once at the end, not per note:
   ```bash
   VAULT="$HOME/Library/Mobile Documents/iCloud~md~obsidian/Documents/Personal"
   git -C "$VAULT" add -A && git -C "$VAULT" commit -m "docs: mine <source> → N notes"
   ```

## Output

Report, before the commit:

```
Source: <source>          Inventoried: <n>    Extracted: <n>    Written: <n>
Created:  <paths>
Updated:  <paths>
Skipped:  <n> — <why: transient, duplicate, out of scope>
Not read: <n> — <why: timeboxed, auth failed>
```

`Skipped` and `Not read` are the load-bearing lines. Without them a partial sweep reads as complete.

## Scope guard

Mining reads widely across personal accounts. Extract only what serves the stated goal — do not compile a profile because the data is reachable. When a source needs a sign-in that isn't already active, stop and ask rather than working around it.
