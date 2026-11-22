---
name: get-sms-number
description: Rent a private phone number from Temp Number and read the SMS it receives, such as a sign-up code for the user's own account. Use when the user asks for a phone number to receive a text, a virtual or temporary number in a country, or a code sent to a number they rented.
---

# Get a private number and read its SMS

The user wants a private number so their personal number stays out of a sign-up, or wants to read a text sent to a number they rent. The `temp-number` MCP server does the work. Its tools spend real wallet money, so follow these steps in order.

## 1. Find out what the user needs

Ask only for what is missing:

- **Country**: turn it into an ISO 3166-1 alpha-2 code (United States = `US`, United Kingdom = `GB`).
- **How long**: a short rental for one code, or a longer one they will keep. Use the duration keys the server returns; never invent one.
- **Number type** (optional): `non_voip` numbers are mobile-style lines that more services accept; `voip` numbers are cheaper. If the user does not care, leave it out.

## 2. Check price, stock and balance

1. `get-pricing` with `country_code` to list the durations and prices for that country.
2. `get-inventory` with `country_code` (plus `duration` and `number_type` if known) to confirm a number is in stock.
3. `get-balance` to confirm the wallet covers the price.

If there is no stock, say so and offer nearby options from the pricing list (another duration or number type). If the balance is too low, tell the user how much is missing and point them to https://temp-number.com/Dashboard to top up. Never try to buy anyway.

## 3. Ask before buying

Show the user one line, for example:

> United States, non-VoIP, 1 month: $X.XX from your $Y.YY balance. Buy it?

Call `purchase-number` only after a clear yes in this conversation. One yes covers one number.

If `purchase-number` times out or returns an unclear error, do **not** call it again. Call `list-active-numbers` first: the purchase may have gone through, and a second call would buy a second number.

If the server says purchases are not allowed for this connection, tell the user to reconnect Temp Number and tick **Allow purchases** on the consent screen, or turn purchases on in Dashboard → MCP Server.

## 4. Hand over the number and wait for the SMS

1. Give the user the full number in international format and its purchased number ID.
2. Tell them to enter it on the service and request the code.
3. Call `check-sms` with `purchased_number_id`. If nothing has arrived, wait about 20 to 30 seconds and check again, up to about 5 minutes, then ask the user whether to keep waiting.
4. When the message arrives, show the sender, the time and the code on its own line so it is easy to copy.

## Rules

- Only help the user receive messages for their own accounts and their own use. Decline requests to impersonate someone or to get around a service's limits or bans.
- Report prices, refunds and errors exactly as the server returns them. Never promise a refund in advance.
- For renewals, cancellations and listing numbers, use the `manage-numbers` skill.
