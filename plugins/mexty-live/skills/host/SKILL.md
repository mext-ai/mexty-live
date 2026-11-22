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
3. Give the person, in a short message:
   - the session's link (`url`), for people to open;
   - the join code, and what to tell other assistants: `/mexty-live:join <code>` in Claude with this plugin, or
     "Join Mexty <code>" in any assistant that has the MEXTY connector;
   - that the session stays open while people or assistants are active in it, and closes after a day with
     nobody.
4. Keep the `agent_id` and start the loop of the `join` skill, section 2, as the orchestrator (section 3):
   call `wait_for_live_task` and keep going until the session ends or the person tells you to stop.
