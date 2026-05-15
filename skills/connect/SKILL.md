---
name: connect
description: Surface non-obvious cross-references between vault notes — connecting two concepts that aren't already explicitly linked. Use when /connect is invoked, when the user says "what does X have to do with Y", "is there a thread between these notes", "what connects these ideas", or when reviewing two superficially unrelated topics for shared structure. Do NOT use for direct backlinks (use /backlinks) or for surfacing patterns within a single topic (use /emerge).
---

# Skill: /connect [argument]

Surface the non-obvious bridges between two concepts the vault hasn't linked yet — the value is in connections that surprise, not the ones you'd expect.

**Don't:** use this to find existing links — that's `/backlinks`. Don't surface connections already stated in either note.

## Steps

1. Parse the argument/topic from Shane's request.
2. Follow [Qwen Protocol](_lib/qwen-protocol.md) with:
   - `task`: "Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md). Find non-obvious bridges between '[argument]' and other concepts in the vault. What unexpected connections exist? What synthesis hasn't been made yet? Reject obvious connections — the value is in the surprising ones. Present 3–5 non-obvious connections, each framed as: '[Concept A] connects to [Concept B] because [non-obvious bridge]. The unexplored synthesis is [new insight].'"
   - `skill`: "connect"
3. Review Qwen's result, synthesize if needed, and present to Shane.
4. Follow [Concept Save Protocol](_lib/concept-save.md).

## Fallback

If Qwen is unavailable:

1. Run `obsidian search query='[argument]' limit=10` via bash and cast a wide net into adjacent domains.
2. Look for: structural similarities, causal links, tensions that illuminate, synthesis opportunities.
3. Present 3–5 non-obvious connections in the format above.
4. Follow [Concept Save Protocol](_lib/concept-save.md).
