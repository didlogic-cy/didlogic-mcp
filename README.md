# MCP server for didlogic

The official [Model Context Protocol](https://modelcontextprotocol.io) server
for [didlogic](https://didlogic.com). It connects Claude, ChatGPT, Cursor,
VS Code and any other MCP client to your didlogic account, so you can manage
phone numbers, SIP accounts, routing, SMS, calls and billing by asking in
plain language.

- **Endpoint:** `https://mcp.didlogic.com/mcp` (Streamable HTTP)
- **Auth:** OAuth sign-in, or a didlogic API key
- **Coverage:** the full didlogic public API v1 and v2, within your account's
  permissions and settings

This is a hosted service: there is nothing to install or run. This
repository holds its documentation and registry metadata.

## What you can do

Everything the [didlogic public API](https://docs.didlogic.com/docs/openapi-spec)
offers, including:

- **Phone numbers** — browse countries, cities and regions, search available
  numbers, buy them, change their settings and release them
- **Inbound routing** — add, change and remove the destinations a number
  forwards to
- **SIP accounts** — create, update and delete SIP accounts and manage their
  allowed IP addresses
- **Calls** — call history and statistics, recordings, call price quotes and
  ASR reports
- **Click2Call** — place, check and cancel click-to-call calls
- **SMS** — send messages and read the history
- **Billing** — balance and transaction history
- **Compliance** — KYC documents and identities, number risk checks and HLR
  lookups

What is available to you is exactly what your account and its API key allow.
Every request acts as your account and on its balance: buying a number,
sending an SMS or placing a call is charged at once. Assistants are instructed
to describe a paid or destructive action and wait for your confirmation before
they run it.

## How it works

The server does not expose one tool per API operation. It gives the assistant
three tools and the API's own specification:

1. `search` finds the operations that match a task
2. `get_schema` returns the exact arguments of the ones chosen
3. `execute` runs a short script that calls them and returns only the answer

So the assistant can loop over pages, combine several calls and add up the
results in one step, and the server always covers the API as it is today.
See [docs/tools.md](docs/tools.md) for details.

## Setup

You need a didlogic account. If your client uses an API key rather than OAuth,
create one in the customer portal under
[API & Webhooks](https://app.didlogic.com/app/api-webhooks).

### Claude Desktop

Either:

- download the extension from
  [mcp.didlogic.com/didlogic.mcpb](https://mcp.didlogic.com/didlogic.mcpb)
  (also attached to each [release](../../releases)), open it, and paste your
  API key, or
- go to **Settings → Connectors → Add custom connector**, enter
  `https://mcp.didlogic.com/mcp`, and sign in with didlogic.

### Claude Code

```bash
claude mcp add --transport http didlogic https://mcp.didlogic.com/mcp
```

Then run `/mcp` and sign in.

### ChatGPT

Add a custom connector (developer mode) with the URL
`https://mcp.didlogic.com/mcp` and OAuth authentication, then sign in.

### Cursor and other `mcpServers` clients

```json
{
  "mcpServers": {
    "didlogic": {
      "url": "https://mcp.didlogic.com/mcp"
    }
  }
}
```

If the client does not support OAuth, send your API key instead:

```json
{
  "mcpServers": {
    "didlogic": {
      "url": "https://mcp.didlogic.com/mcp",
      "headers": { "Authorization": "Bearer YOUR_API_KEY" }
    }
  }
}
```

### VS Code

In `.vscode/mcp.json`:

```json
{
  "servers": {
    "didlogic": {
      "type": "http",
      "url": "https://mcp.didlogic.com/mcp"
    }
  }
}
```

## Example prompts

- "What's my balance, and how much did I spend on calls last month?"
- "Find me a London number and tell me what it costs before buying it."
- "Forward my US number to my SIP account `office`."
- "Show yesterday's missed calls on my German numbers."
- "Create a SIP account for the Berlin office and allow only 203.0.113.10."
- "Send an SMS to +44 7700 900123 saying the meeting moved to 3 pm."
- "Which countries have the worst answer rate this week?"

More in [docs/examples.md](docs/examples.md).

## Security

- The server holds no credentials of its own. It forwards your OAuth token or
  API key with each request, and didlogic decides what it may do.
- Treat the API key like a password: it can spend your balance. Revoke it in
  [API & Webhooks](https://app.didlogic.com/app/api-webhooks) at any time.
- To report a vulnerability, write to [support@didlogic.com](mailto:support@didlogic.com).

## Known limitations

- Uploading KYC documents needs the assistant to send the file's contents.
  Claude can do this with files you attach; ChatGPT currently cannot, so upload
  documents in the customer portal there.

## Links

- Server and setup page: <https://mcp.didlogic.com>
- MCP server guide: <https://docs.didlogic.com/docs/guides/apps-developer-tools/mcp-server>
- API getting started: <https://docs.didlogic.com/docs/api/get-started>
- OpenAPI specification: <https://docs.didlogic.com/docs/openapi-spec>
- Changelog: [CHANGELOG.md](CHANGELOG.md)

## Support

Questions and problems: [support@didlogic.com](mailto:support@didlogic.com), or the chat in the
[didlogic customer portal](https://app.didlogic.com).

## License

The contents of this repository are released under the [MIT License](LICENSE).
The didlogic service itself is subject to the didlogic terms of service.
