# Temp Number plugin for Claude

Rent private phone numbers, read the SMS they receive and manage renewals from Claude, so your personal number stays private.

## What's inside

| Part | What it does |
| --- | --- |
| MCP connector `temp-number` | Connects to `https://mcp.temp-number.com/mcp`. You sign in to your Temp Number account once (OAuth); no key to copy. |
| Skill `get-sms-number` | Checks price, stock and balance, asks you before buying, then waits for your SMS and shows the code. |
| Skill `manage-numbers` | Lists your numbers, renews or cancels them, always asking before it spends or cancels. |
| Command `/temp-number:numbers` | Wallet balance and your numbers, expiring ones first. |
| Command `/temp-number:inbox` | Latest messages on your numbers. |

## Install

In Claude Code:

```
/plugin marketplace add temp-number-com/claude-plugin
/plugin install temp-number@temp-number
```

The first time a tool runs, your browser opens the Temp Number sign-in and consent page. Purchases stay off unless you tick **Allow purchases** there.

## Requirements

- A Temp Number account with wallet funds: https://temp-number.com
- Buying and renewing spend your wallet balance. Claude asks before each one.

## Support

support@temp-number.com · https://temp-number.com/mcp

## License

MIT
