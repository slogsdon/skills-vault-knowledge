# Knowledge Briefing Protocol

Run these three checks via bash, then format as the block below.

## New Clippings (unprocessed)

Run this one block — it dates every unprocessed clipping and splits new-since-yesterday from the standing backlog:

```bash
CLIPS="$HOME/Library/Mobile Documents/iCloud~md~obsidian/Documents/Personal/Knowledge/Reference/Clippings"
CUTOFF=$(date -v-1d +%Y-%m-%d)
find "$CLIPS" -name '*.md' -not -path '*/Archive/*' -print0 | while IFS= read -r -d '' f; do
  grep -qiE '#ingested|^## (Notes|Key Points|My Take|Take|Shane.s Take)' "$f" && continue
  d=$(awk '/^---$/{n++; if(n==2) exit; next} n==1 && /^created:/{sub(/^created: */,""); print $1; exit}' "$f")
  [ -n "$d" ] || d=$(stat -f '%SB' -t '%Y-%m-%d' "$f")
  printf '%s\t%s\n' "$d" "$(basename "$f" .md)"
done | sort -r > /tmp/_clips.tsv
echo "BACKLOG: $(wc -l < /tmp/_clips.tsv | tr -d ' ') unprocessed"
echo "NEW since $CUTOFF:"; awk -F'\t' -v c="$CUTOFF" '$1>=c' /tmp/_clips.tsv
echo "--- 5 most recent unprocessed ---"; head -5 /tmp/_clips.tsv
```

How it decides:

- **Processed** = the file contains an `#ingested` tag or a `## Notes` / `## Key Points` / `## My Take` heading (matched case-insensitively — `## Key points` and a bare `## Take` are also in use). Everything else is unprocessed. `## My Take` was missing from this list until 2026-08-09 and made three already-annotated clippings read as backlog forever.
- **Scope** = top-level `Clippings/` only. `Clippings/Archive/` is excluded — those were archived deliberately (junk, hype, superseded) and must not read as backlog.
- **Date** = the clipping's frontmatter `created:` field, which is what the Web Clipper writes. Files with no frontmatter fall back to filesystem birth time. Do **not** use `-mtime` here: iCloud rewrites mtimes on sync, so nearly every file looks modified in the last 24 hours and the window becomes meaningless.

Output: the new-since-yesterday titles (usually none), plus the backlog count and its 5 most recent entries so the queue stays visible.

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
**New Clippings:** [new-since-yesterday titles or "none"] — backlog: [N] unprocessed
**Open questions:** [list or "none"]
**Vault delta:** [summary or "no changes"]
```
