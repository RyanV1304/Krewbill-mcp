# Krewbill MCP

Krewbill gives each client a shared AI memory: a space of notes that a person has approved. Claude, ChatGPT and Cursor read those notes over a remote MCP server, so your team stops re-explaining a client's tone, rules and facts in every new chat.

Website: https://krewbill.com

> This repository only describes the hosted Krewbill MCP service. The service itself is closed-source.

## What it does

- One **space** per client, holding notes a person has approved.
- Assistants can **read** a space's approved notes.
- Assistants can only **suggest** new notes. Nothing is saved to the space until a person approves it.
- Each connection key is limited to one space and can be revoked.
- Works with any MCP client that supports remote (HTTP) servers. Tested with Claude Code; use with other clients may need a different setup.

## Tools

| Tool | What it does |
|---|---|
| `get_space_context` | Returns the approved notes for the space your key is limited to. |
| `suggest_memory` | Proposes a new note. It waits in an approval queue until a person approves it. |

Keys can be read-only, or read-and-suggest. Read-only keys cannot call `suggest_memory`.

## Connect

1. Create a space and a connection key at https://krewbill.com (see https://krewbill.com/connect).
2. Krewbill shows your personal server address once, when you create the key. Copy it.
3. Add it to your assistant. For Claude Code:

```bash
claude mcp add --transport http krewbill <your-server-address>
```

If your tool asks for a header instead of a key in the address, use the plain server address and send `Authorization: Bearer <your-key>`.

Create one key per tool, so you can revoke each separately.

## Status

Krewbill is in free early access until December 30, 2026. Paid plans are planned, not live. Per-person sign-in is not built yet, and OAuth is not supported.

## Feedback

https://krewbill.com/feedback
