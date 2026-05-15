---
name: vault-index
description: Rebuild the vault-index note from current vault state. Use when /vault-index is invoked, when the morning skill flags "vault-index not found" or a stale delta, when the user asks "what's in my vault" / "give me a vault overview" / "how's my vault organized", or after a large batch of new Concepts has landed. Do NOT use for searching specific notes — use the obsidian skill instead.
---

# Skill: /vault-index

Rebuild `vault-index.md` from current vault state so the morning skill's overnight delta is accurate — stale or absent index degrades morning briefings.

**Don't:** include Daily Notes in the index — they're temporal logs, not knowledge graph nodes. Don't run this for targeted note lookup — use the obsidian skill instead.

## Steps

1. Determine today's date and time (YYYY-MM-DD HH:MM)

2. Read the current vault-index if it exists, to capture the prior state for the "Recent changes" section:
   ```bash
   obsidian read file='vault-index'
   ```
   If it doesn't exist, note that this is a fresh build.

3. Scan the vault for current state:
   ```bash
   obsidian search query='Concepts/' limit=200
   obsidian search query='Clippings/' limit=200
   obsidian search query='Context/' limit=50
   obsidian search query='Projects/' limit=50
   ```

4. From the scan results, compile:
   - All Concept page names (as wikilinks)
   - All Clipping note names (newest first based on filename date prefix, if any)
   - All Context file names
   - All Project note names

5. Diff against the prior vault-index (from step 2) to identify what's new or missing. If no prior index exists, mark all entries as "Initial build."

6. Write the rebuilt vault-index by overwriting the file directly:
   ```bash
   VAULT="$HOME/Library/Mobile Documents/iCloud~md~obsidian/Documents/Personal"
   cat > "$VAULT/vault-index.md" << 'VAULTEOF'
   [insert rendered content here]
   VAULTEOF
   ```
   Use the exact format specified below.

7. Commit the change:
   ```bash
   VAULT="$HOME/Library/Mobile Documents/iCloud~md~obsidian/Documents/Personal"
   git -C "$VAULT" add -A && git -C "$VAULT" commit -m "docs: rebuild vault-index [YYYY-MM-DD]"
   ```

8. Report what changed: counts per section, and anything flagged in the diff.

## vault-index.md format

Write the note with this exact structure. The morning skill parses the section headers to detect drift — keep them verbatim.

```markdown
# Vault Index

*Last updated: YYYY-MM-DD HH:MM*

## Concepts (N)

[[Concept page 1]]
[[Concept page 2]]
...

## Clippings (N)

[[Clipping note 1]]
[[Clipping note 2]]
...

## Context (N)

[[Context/accountability]]
[[Context/patterns]]
...

## Projects (N)

[[Projects/Project Name]]
...

## Recent changes

*Since prior index:*
- Added: [[Note A]], [[Note B]] (or "none")
- Removed: [names] (or "none" — note: removals are best-effort based on what was in the prior index)
```

## When the morning skill flags drift

The morning skill reports drift when it finds Concept pages, Clippings, or Context files not listed in the current index. After morning surfaces this, invoke `/vault-index` to reconcile. The rebuilt index becomes the new baseline.

## Notes on scan completeness

`obsidian search` returns results sorted by recency, limit 200. If any section likely has more than 200 entries, note it in the output and suggest running the rebuild in sections. In practice, Concepts and Clippings are the two sections most likely to grow beyond this.

Do not include Daily Notes in the index — those are temporal logs, not knowledge graph nodes, and adding them would make the morning delta meaningless.
