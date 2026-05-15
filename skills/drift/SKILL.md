---
name: drift
description: Analyze gaps between stated priorities (OKRs, focus statements) and actual session behavior to surface drift. Use when /drift is invoked, when the user says "am I doing what I said I would", "where am I off-track", "do my actions match my goals", "am I avoiding something", or during weekly retrospectives. Reads accountability.md, patterns.md, and recent daily notes. Do NOT use for surfacing patterns within a topic — use /emerge for that.
---

# Skill: /drift [argument]

Surface the gap between Shane's stated intentions and actual behavior — where he's drifting from his own goals and values, with vault evidence for each.

**Don't:** use this for topic pattern analysis — that's /emerge. Don't soften drift findings — this is accountability analysis, not cheerleading.

## Steps

1. Parse the argument/topic from Shane's request.
2. Follow [Qwen Protocol](_lib/qwen-protocol.md) with:
   - `task`: "Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md), `obsidian read file='Context/accountability'`, `obsidian read file='Context/patterns'`. Analyze the gap between Shane's stated intentions and actual behavior patterns in the vault around '[argument]' (or broadly). Where is he drifting from his own stated values or goals?"
   - `skill`: "drift"
3. Review Qwen's result, synthesize if needed, and present to Shane.

## Fallback

If Qwen is unavailable:

1. Search for stated intentions via bash: `obsidian search query='want to' limit=10`, `obsidian search query='goal' limit=10`, `obsidian search query='intend' limit=10`, `obsidian search query='commit' limit=10`, `obsidian search query='value' limit=10`
2. Also read `Context/accountability.md` and `Context/patterns.md` by running `obsidian read file='Context/accountability'` and `obsidian read file='Context/patterns'` via bash
3. If `[argument]` is provided, scope the search to that domain; otherwise cast broadly
4. Compare stated intentions against observable behavior:
   - What does Shane say he values? What does the vault show him actually spending time/attention on?
   - What goals appear repeatedly without progress?
   - What beliefs does he state vs. what his decisions imply?
5. Surface 2–4 specific drift patterns, each framed as: "You say [X], but the evidence shows [Y]"
6. Be direct — this is accountability analysis, not cheerleading
7. Present findings with vault evidence for each drift identified
