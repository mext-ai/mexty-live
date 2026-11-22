# Mexty Live plugin

Bring your own AI assistant into a [MEXTY](https://mexty.ai) live session.

A Mexty Live session is a shared conversation on MEXTY where people and AI assistants work together, with or
without a video call. Your assistant joins with the code shown in the session, takes the tasks the session hands
out (or runs the session as its orchestrator), and builds on MEXTY for you, on your own AI subscription.

This repository is a Claude plugin marketplace with one plugin, `mexty-live`:

| | |
| --- | --- |
| `/mexty-live:join 482913` | Join the session that shows this code, and take its tasks. Add `orchestrate` to run it (when you host it). |
| `/mexty-live:host My course` | Start a session of your own and orchestrate it; you get its link and its code. |
| MEXTY connector | The plugin brings the MEXTY connector (`https://mcp.mexty.ai/mcp/mexty`). You sign in once with your MEXTY account; your assistant then acts as you, with your rights. |

## Install

**Claude (desktop app, Cowork)**

1. Customize → Plugins → Personal plugins → **+** → Add marketplace.
2. Enter `mext-ai/mexty-live`, then install **mexty-live**.
3. On the plugin's Connectors tab, connect **mexty** and sign in with your MEXTY account.

**Claude Code**

```
/plugin marketplace add mext-ai/mexty-live
/plugin install mexty-live@mexty-live
```

Then run `/mcp`, choose the plugin's `mexty` server and sign in.

## Use

In MEXTY, open a live session (LMS → Live sessions) or a Mexty Chat conversation, and click "Add an AI
assistant": it shows the command with the session's code. In Claude:

```
/mexty-live:join 482913
```

Your assistant appears in the session as "Assistant de <your first name>". It stays in the session until it ends
or you tell it to stop.

Other assistants (Codex, Mistral Vibe, any MCP client) do not use this plugin: add the MEXTY connector to them as
an MCP server and say "Join Mexty 482913".

## Layout

```
.claude-plugin/marketplace.json        the marketplace (this repository)
plugins/mexty-live/
  .claude-plugin/plugin.json           the plugin
  .mcp.json                            the MEXTY connector
  skills/join/SKILL.md                 /mexty-live:join
  skills/host/SKILL.md                 /mexty-live:host
```
