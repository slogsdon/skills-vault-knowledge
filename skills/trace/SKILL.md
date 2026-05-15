---
name: trace
description: Map the chronological evolution of an idea across vault notes. Use when /trace is invoked or when Shane asks "how has my thinking on X changed", "when did I first write about X", "trace the evolution of X". Do NOT use to find connections between two separate ideas — that's /connect.
---

# Skill: /trace [argument]

Map the arc of how Shane's thinking on a topic evolved — not the current position, but the path that led there and the inflection points along the way.

**Don't:** use this for cross-concept bridging — that's `/connect`. Don't present a settled position without showing the inflection points that led there.

## Steps

1. Parse the argument/topic from Shane's request.
2. Follow [Qwen Protocol](_lib/qwen-protocol.md) with:
   - `task`: "Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md). Map the chronological evolution of Shane's thinking about '[argument]'. What was the earliest framing? What shifted, and what triggered each shift? What's the current settled position (if any), or what remains unresolved? Highlight inflection points — moments where thinking meaningfully changed direction."
   - `skill`: "trace"
3. Review Qwen's result, synthesize if needed, and present to Shane.
4. Follow [Concept Save Protocol](_lib/concept-save.md).

## Fallback

If Qwen is unavailable:

1. Run `obsidian search query='[argument]' limit=10` via bash; read notes paying attention to dates.
2. Sort chronologically. Identify: earliest framing, inflection points, current position.
3. Present a chronological narrative with specific note references and dates.
4. Follow [Concept Save Protocol](_lib/concept-save.md).
