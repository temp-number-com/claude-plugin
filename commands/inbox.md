---
description: Show the latest SMS on your Temp Number numbers
argument-hint: "[number or purchased number ID]"
---

Use the `temp-number` MCP server to show recent messages.

- If the user gave a number or ID ($ARGUMENTS), find it with `list-active-numbers` and call `check-sms` for it.
- Otherwise call `list-active-numbers` with status `active` and call `check-sms` for each number (at most 10).

Show the newest messages first: number, sender, time and the text. If a message contains a one-time code, repeat the code on its own line so it is easy to copy. Say plainly when a number has no messages yet.
