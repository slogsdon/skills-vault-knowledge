# Knowledge Briefing Protocol

Run these three checks via bash, then format as the block below.

## New Clippings (last 24h, unprocessed)

Run both of these to find recent Clippings:

```bash
obsidian search query='Clippings/' limit=20
```

```bash
find "$HOME/Library/Mobile Documents/iCloud~md~obsidian/Documents/Personal/Knowledge/Reference/Clippings" -name "*.md" -mtime -1 2>/dev/null
```

Use the `find` results to identify files modified in the last 24 hours. For each file found, run `obsidian read file='[title without .md]'` to check whether it has been processed (look for an `#ingested` tag or a `## Notes` / `## Key Points` section — match headings case-insensitively; `## Key points` is also in use). Files without any of those markers are unprocessed.

Output: list of unprocessed Clipping titles, or "none."

## Open questions from recent /connect or /trace runs

```bash
obsidian search query='open question' limit=10
obsidian search query='unresolved' limit=10
```

Also check yesterday's daily note for lines starting with `?` or "open question." Output: up to 3 open questions with source note, or "none."

## vault-index delta

```bash
obsidian read file='vault-index'
```

Compare to the snapshot in yesterday's `## Knowledge Briefing` section. Surface new Concept pages, new Clippings folders, or deleted notes. If vault-index doesn't exist, skip and note "vault-index not found." Output: brief delta summary or "no changes."

## Format

```
**New Clippings (unprocessed):** [list or "none"]
**Open questions:** [list or "none"]
**Vault delta:** [summary or "no changes"]
```
