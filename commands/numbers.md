---
description: Show your Temp Number wallet balance and the numbers you rent, expiring ones first
---

Use the `temp-number` MCP server:

1. Call `get-balance` and show the balance on one line.
2. Call `list-active-numbers` and show each number as a row: number, country, expiry date, purchased number ID. Put any that expire within 3 days first and mark them.
3. If a number expires within 3 days, offer to renew it (follow the `manage-numbers` skill, which asks before spending).

Do not buy, renew or cancel anything in this command without asking first.
