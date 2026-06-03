---
name: obsidian
description: |
  General-purpose Obsidian vault skill — use this whenever the user wants to do anything with their vault or personal notes. Covers reading notes by name, searching vault content, creating new notes, appending to existing ones, checking backlinks, and working with daily notes. Trigger immediately on phrases like: "look up my note on X", "add this to my vault", "what does my note say about Y", "find notes about Z", "log this to my vault", "update my daily note", "create a note for...", "what links to X", "search my vault for...", "show me what I know about...", "check my notes on...", or any time the user mentions Obsidian, their vault, or personal notes. If the user is asking about something they might have written down, reach for this skill first.
---

# Obsidian Vault Skill

Use the `obsidian` CLI to interact with the Personal vault — read, search, create, append, backlink, and daily note operations — always via bash with single quotes.

**Don't:** use double quotes in obsidian CLI arguments — they silently fail. Don't use `daily:append` — it's unreliable; use `daily:read` to get the note name, then `obsidian append file='<name>'`.

## CLI reference

Run all commands via bash. Always use **single quotes** for argument values — double quotes cause a known parser issue and will silently fail.

```bash
# Read a note by its wikilink name (no path, no .md extension)
obsidian read file='Note Name'

# Search the vault
obsidian search query='search term' limit=10

# Create a new note (silent suppresses auto-open in Obsidian)
obsidian create name='Note Name' content='# Title\n\nContent here' silent

# Append to an existing note
obsidian append file='Note Name' content='New content to add'

# Get everything that links to a note
obsidian backlinks file='Note Name'

# Read today's daily note (to get its name/path)
obsidian daily:read

# Append to the daily note: read it first to get the note name, then use append
# daily:append is unreliable — use append file='...' with the actual note name instead
obsidian append file='2026-04-16' content='Entry text'

# List all tags or open tasks across the vault
obsidian tags
obsidian tasks
```

> Obsidian must be running for any CLI command to work. If you get a connection error, ask the user to open Obsidian first.

## Safety: the active-file fallback (read this before any delete)

The CLI **silently falls back to the active file** when a selector (`name=` / `file=`) doesn't resolve to a real note. It does not error — it acts on whatever note is currently focused in Obsidian. This makes a mistyped selector destructive:

- `obsidian delete name='Untitled' permanent` did **not** delete `Untitled.md` — it permanently deleted the *active* note (an unrelated draft), because `name=` failed to resolve and fell through to the active file.
- `obsidian read name='...'` can likewise return the active note's content instead of the note you named, making "verification" misleading.

Rules:

1. **Never delete (or run any destructive op) by `name=`.** Always target the exact relative path: `obsidian delete path='folder/Note.md'`. Exact paths don't fuzzy-match and won't fall back.
2. **Drop `permanent`** so deletes go to trash and stay recoverable. The vault is git-tracked, so a wrong delete of a *committed* note is also recoverable with `git -C "$VAULT" checkout -- 'path/Note.md'`.
3. **Verify by exact path, not `read name=`.** To confirm a write landed, check the file at its known path (`wc -l "$VAULT/Note.md"`) — don't trust `obsidian read name=`, which may show the active file.
4. **There is no `--help`.** `obsidian create --help` (or any unknown args) creates a stray `Untitled.md`. Use `obsidian help` for usage. Remove an accidental stray by its exact path.
5. **Bracket destructive ops with `git status`.** Run `git -C "$VAULT" status --porcelain` before and after, so an unintended deletion shows up immediately as a `D` line you can revert.

## Interpreting requests

The user's phrasing is often loose — your job is to figure out which operation(s) to run.

**Reading a specific note**: If the user gives you a note name or enough context to guess it, try `obsidian read` directly. If the exact name is unclear, search first then read the best match.

**Searching**: When the user wants to find notes about a topic, or isn't sure which note they mean, search with a short keyword query. Return the matching paths and briefly describe what each is, then offer to read any of them.

**Logging / capturing**: When the user wants to save something new ("log this", "capture this idea", "add a note about X"), use `obsidian create` with a clear, descriptive note name — think about how they'd search for it later.

**Updating an existing note**: When the user wants to add to something they already have, find it with search if needed, then `obsidian append`. Don't overwrite with `create` unless they explicitly ask to replace the note.

**Daily note**: Requests like "log to today", "add this to my daily", or "what's in my daily note" → first run `obsidian daily:read` to get today's note name, then use `obsidian append file='<note-name>' content='...'` to add to it. The `daily:append` command is unreliable and should be avoided.

**Tracing connections**: "What links to X" or "what references this note" → `obsidian backlinks file='Note Name'`.

## Common multi-step patterns

- **"What do I know about X?"** → search → read top result(s) → summarize key points
- **"Find my note on X and add Y to it"** → search → confirm which note → append
- **"Create a note summarizing our conversation about X"** → synthesize content → create with good name and structure
- **"What notes reference X?"** → backlinks
- **"Add this to today's note"** → daily:read to get the note name → append to it by name

## Output conventions

- **Reads**: Return the note content as-is, preserving headings and structure. No need to paraphrase.
- **Searches**: List matching paths. If names are ambiguous, add a one-line description of each.
- **Creates / appends**: Confirm what was written, the note name, and where in the vault it lives.
- **Backlinks**: One note per line. If none, say so.

## Note naming

When creating notes, use title case and be descriptive. Good names are searchable: `Qwen CLI Quoting Bug`, `Developer Advocacy 2026 OKRs`, `CatalystForms Launch Checklist`. Avoid generic names like `Ideas` or `Notes`.

## Post-write protocol

After any `create` or `append` operation, commit the change:

```bash
VAULT="$HOME/Library/Mobile Documents/iCloud~md~obsidian/Documents/Personal"
git -C "$VAULT" add -A && git -C "$VAULT" commit -m "docs: [brief description of what was written]"
```

Use conventional commit style. Examples:
- `docs: log session entry 14:32`
- `docs: write today's focus to 2026-04-17 daily note`
- `docs: append EOD audit to 2026-04-17`
- `docs: create note Qwen CLI Quoting Bug`
