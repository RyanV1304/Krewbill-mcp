# Krewbill MCP

Krewbill gives each client a shared AI memory: a space of notes that a person has approved. Claude, ChatGPT and Cursor read those notes over a remote MCP server, so your team stops re-explaining a client's tone, rules and facts in every new chat.

Website: https://krewbill.com

> This repository only describes the hosted Krewbill MCP service. The service itself is closed-source.

## What it does

- One **space** per client, holding notes a person has approved.
- Assistants can **read** a space's approved notes.
- Assistants can only **suggest** new notes. Nothing is saved to the space until a person approves it.
- Each connection key is limited to the spaces you choose, can be read-only, and can be revoked.
- Accounts, workspaces, roles and invitations are available in the web app.
- Works with any MCP client that supports remote (HTTP) servers. Tested with Claude Code; use with other clients may need a different setup.

## Tools

| Tool | What it does |
|---|---|
| `list_spaces` | Lists the spaces your key may read. |
| `get_space_context` | Returns a space's approved notes (voice and rules, key facts, decisions). Assistants call it first, before drafting for a client or project. |
| `search_memory` | Searches approved notes by keyword, in one space or in all spaces your key can read. |
| `suggest_memory` | Proposes a new note. It waits in an approval queue until a person approves it, and never changes shared memory by itself. |
| `flag_stale` | Flags an approved note as possibly out of date for a person to review. It never edits or removes the note. |

A key can cover one space, several, or all of them, and can be read-only. Read-only keys cannot suggest notes.

## Connect

1. Create a space and a connection key at https://krewbill.com (see https://krewbill.com/connect).
2. Krewbill shows your personal server address once, when you create the key. Copy it.
3. Add it to your assistant. For Claude Code:

```bash
claude mcp add --transport http krewbill <your-server-address>
```

If your tool asks for a header instead of a key in the address, use the plain server address `https://www.krewbill.com/api/mcp` and send `Authorization: Bearer <your-key>`.

Create one key per tool, so you can revoke each separately.

## Status

Krewbill is free during early access, until December 30, 2026. Connections authenticate with keys.

## Feedback

https://krewbill.com/feedback
