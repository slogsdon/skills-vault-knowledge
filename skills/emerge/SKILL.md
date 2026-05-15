---
name: emerge
description: Use when asked to surface hidden patterns or implicit ideas in the vault, or when /emerge is invoked. Do NOT use to find connections between two specific concepts — use /connect for that.
---

# Skill: /emerge [argument]

Surface what Shane is circling in the vault without stating directly — the implicit beliefs, unspoken assumptions, and ideas approached from multiple angles but never synthesized.

**Don't:** surface obvious or labeled themes — the value is in what's implicit. Don't use this for cross-concept bridging — that's /connect.

## Steps

1. Parse the argument/topic from Shane's request.
2. Follow [Qwen Protocol](_lib/qwen-protocol.md) with:
   - `task`: "Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md). Search the vault for implicit patterns, unspoken assumptions, and emergent ideas around '[argument]' (or across the full vault if no argument given). Surface what Shane is circling without stating directly."
   - `skill`: "emerge"
3. Review Qwen's result, synthesize if needed, and present to Shane.

## Fallback

If Qwen is unavailable:

1. If `[argument]` is provided, run `obsidian search query='[argument]' limit=15` via bash; otherwise run broad searches via bash: `obsidian search query='goals' limit=10`, `obsidian search query='beliefs' limit=10`, `obsidian search query='habits' limit=10`, `obsidian search query='work' limit=10`
2. Read 10–15 notes spanning different topics and time periods by running `obsidian read file='[note name]'` via bash for each
3. Look for what's implicit — not stated conclusions, but:
   - Topics that recur without being labeled as important
   - Assumptions embedded in how questions are framed
   - Ideas approached from multiple angles but never synthesized
   - Things written around but never directly about
4. Surface 3–5 emergent patterns, each framed as: "You keep circling [X] without naming it directly — the implicit belief seems to be [Y]"
5. Present the findings to Shane with specific note evidence for each pattern
