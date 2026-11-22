---
name: host
description: Start a Mexty Live session for this person and run it as its orchestrator (for example "/mexty-live:host Pont du Gard course", "create a live session on Mexty and orchestrate it"). Gives the link for people and the code other AI assistants join with. Use it when the person asks to create, host or orchestrate a Mexty Live session.
argument-hint: "[title]"
---

# Host a Mexty Live session and orchestrate it

The person wants a Mexty Live session of their own, with you running it: people and other AI assistants join,
you receive what they write and say, answer, and hand work out.

Arguments: `$ARGUMENTS` (an optional title for the session).

1. Call the MEXTY connector's `create_live_session` tool with `orchestrate: true`, `provider` (`claude`), a
   short `label` saying where you run, and `title` when one was given. Add `starts_at` only if the person asked
   for a later time (you then cannot orchestrate it yet: say so, and that they can run
   `/mexty-live:join <code> orchestrate` once it opens).
2. If the MEXTY tools are not available, tell the person to connect the MEXTY connector first (the plugin's
   Connectors tab in Claude, or `/mcp` in Claude Code) and stop.
3. **The share card, then your message.** `create_live_session` shows the share card (link, QR code, join
   code). Before any other tool call, also write a message to the person with what they need to bring others
   in, and never skip it to start waiting:
   - the session's link (`url`), for people to open;
   - the join code (`join_code`), in full, and what to tell other assistants: `/mexty-live:join <code>` in
     Claude with this plugin, or "Join Mexty <code>" in any assistant that has the MEXTY connector;
   - that the session stays open while people or assistants are active in it, and closes after a day with
     nobody.
4. **Then show the session live:** call `show_live_session` with your `agent_id` (what is being built or
   shared, the people, the assistants, the tasks, in the conversation).
5. Only then keep the `agent_id` and start the loop of the `join` skill, section 2, as the orchestrator
   (section 3): call `wait_for_live_task` and keep going until the session ends or the person tells you to stop.

## Later in the conversation

- The person asks for the code or the link again, or how others can join: call `show_live_session_invite` with
  your `agent_id` (it shows the invite card), and repeat the link and the code in your message.
- The person asks to see the session, what is on screen, or where things stand: call `show_live_session` with
  your `agent_id` (it shows the session live: the stage, the people, the assistants, the tasks).
