---
name: manage-numbers
description: List, renew or cancel the private phone numbers the user rents from Temp Number, and read their messages. Use when the user asks which numbers they have, what is expiring, to renew or extend a number, to cancel one and get a refund, or to check messages on a number they already own.
---

# Manage rented numbers

Use the `temp-number` MCP server. Listing and reading are free. Renewing spends wallet money and cancelling cannot be undone, so both need the user's yes first.

## See what the user has

- `list-active-numbers` lists every number. Pass `status` to narrow it: `active`, `expiring_soon`, `expired` or `cancelled`.
- Show each number as one row: number, country, expiry date and its purchased number ID. Put numbers that expire within 3 days first.
- To read messages on one number, call `check-sms` with its `purchased_number_id`. Show the newest message first, with sender and time.

## Renew a number

1. Find the number with `list-active-numbers` and confirm it is the one the user means.
2. An **expired** number cannot be renewed. Say so and offer to rent a new number with the `get-sms-number` skill.
3. Check the renewal price with `get-pricing` for the number's country and `get-balance` for the wallet.
4. Pick the package: `oneWeek`, `oneMonth`, `threeMonths`, `sixMonths` or `oneYear`. A number rented by the week renews by `oneWeek` only.
5. Ask, for example: "Renew +1 555 0100 for 1 month for $X.XX? It will then expire on DATE." Call `renew-number` only after a clear yes.
6. If `renew-number` times out, call `list-active-numbers` and check the new expiry date before trying again, so the number is not renewed twice.

## Cancel a number

1. Confirm which number, and warn that cancelling is permanent: the number is released and its messages stop.
2. Call `cancel-number` only after a clear yes.
3. Report the refund exactly as the server returns it. Never promise one in advance.

## Rules

- One yes covers one action on one number. Ask again for the next one.
- If a write tool is refused for missing permission, tell the user to reconnect Temp Number and tick **Allow purchases**, or turn purchases on in Dashboard → MCP Server.
