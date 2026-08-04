---
name: ingest
description: Synthesize raw source material into the vault's Concepts wiki — turn a Clipping, article, transcript, or pasted source into a structured Concept page and register it in the index and log. Use when /ingest is invoked, when Shane says "ingest this", "add this to the wiki", "make a concept page from X", "process this clipping", or when /inbox-triage routes a source into Concepts. Do NOT use for raw capture (use /log), for polished writing (use /learned), or for surfacing links between existing notes (use /connect).
---

# Skill: /ingest [source]

Turn one raw source into a durable Concept page in the vault, following `Context/Vault Schema.md` exactly. The output is a wiki page a future LLM can trust, not a summary dump.

**Don't:** overwrite an existing Concept's `## Shane's Take` — append under `## Update — <date>` instead. Don't skip the index/log updates — an ingest that isn't registered is invisible. Don't ingest transient Inbox/Clippings cross-references into the link graph.

## Inputs

`source` is one of: a Clipping note name (`obsidian read file='...'`), a URL/article, a transcript, or pasted text. If ambiguous, ask which source before proceeding.

## Contract (from `Context/Vault Schema.md` — read it first)

Every Concept page MUST have, in order:
```
## Shane's Take        ← mandatory, first, captured before synthesis. Never omit.
## Summary             ← concise, factual
## Key Points          ← 3–7 bullets
## Cross-references / Related   ← [[Concept Name]] wikilinks, bidirectional
```
- **Create** when the concept has no page; **Update** (append `## Update — <date>`) when it does — never silently overwrite.
- On EVERY ingest, update both registry files (they live in `Inbox/`, not the vault root):
  - `Inbox/vault-index.md` → add/update `- [[Page Name]] — one-line description`
  - `Inbox/vault-log.md` → append `- <date> | <source> | <concept> | <change summary>`

## Steps

1. Read `Context/Vault Schema.md` (the governing contract) and resolve the `source`.
2. Capture **Shane's Take** first — ask Shane for his angle in one or two lines, or lift his verbatim words if already present. Never synthesize over an empty Take.
3. Follow [Qwen Protocol](_lib/qwen-protocol.md) with:
   - `task`: "Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md), `obsidian create name='Name' content='...'`. Synthesize the source '[source]' into a Concepts page following the four-section format (Shane's Take / Summary / Key Points / Cross-references). Search existing Concepts and add bidirectional [[wikilinks]]."
   - `skill`: "ingest"
4. Decide create vs. update by searching `Concepts/` for an existing page on this concept.
5. Write the page (`obsidian create` for new, `obsidian append` under `## Update — <date>` for existing).
6. Update `Inbox/vault-index.md` and `Inbox/vault-log.md` per the contract.
7. Commit the vault (Post-write protocol below).

## Fallback

If Qwen is unavailable:

1. `obsidian search query='[concept]' limit=10` to check for an existing Concept page.
2. Read the source and any related Concepts (`obsidian read file='...'`).
3. Draft the four sections; get Shane's Take in his words before synthesizing the rest.
4. `obsidian create` (new) or `obsidian append` (update under a dated heading).
5. Append the `Inbox/vault-index.md` and `Inbox/vault-log.md` lines.
6. Present the new/updated page path + the index/log deltas to Shane.

## Post-write protocol

After the writes, commit:
```bash
VAULT="$HOME/Library/Mobile Documents/iCloud~md~obsidian/Documents/Personal"
git -C "$VAULT" add -A && git -C "$VAULT" commit -m "docs: ingest [source] → Concept [name]"
```
