# Changelog

Every release of the didlogic MCP server. Versions match the server version
reported at <https://mcp.didlogic.com/health>.

## [4.7.3] - 2026-10-29

- The setup page now starts with OAuth sign-in, the quickest way to connect
  your assistant.

## [4.7.2] - 2026-10-28

- Links to the server now show a preview card when shared in chats and
  social networks.

## [4.7.1] - 2026-10-28

- Some operations are now available only on the main endpoint.

## [4.7.0] - 2026-10-28

- Added an explicit mode at `https://mcp.didlogic.com/mcp/explicit` for
  assistants that need every API operation as its own tool.

## [4.6.2] - 2026-10-27

- Fixed bugs and improved reliability.

## [4.6.0] - 2026-10-19

- Fixed bugs and improved reliability.

## [4.5.2] - 2026-10-15

- Fixed bugs and improved reliability.

## [4.5.1] - 2026-10-14

- Fixed bugs and improved reliability.

## [4.5.0] - 2026-10-14

- New setup page at <https://mcp.didlogic.com>: what the server does, the
  server URL, a link to the setup guide and a one-step Claude Desktop install.
- Claude Desktop extension: download it from
  <https://mcp.didlogic.com/didlogic.mcpb>, open it, paste your API key, done.
- AI agents can set the server up on their own: handed only the address, they
  get setup instructions for Claude, ChatGPT, Cursor and VS Code
  (`/llms.txt`).
- `/health` shows the version currently running.

## [4.4.0] - 2026-10-14

- Upload KYC documents from the conversation: attach a passport or a proof of
  address and ask the assistant to submit it.

## [4.3.1] - 2026-10-14

- Fixed bugs and improved reliability.

## [4.3.0] - 2026-10-14

- When your API key is revoked or your sign-in expires, your client now asks
  you to sign in again, instead of every request failing with an error.

## [4.2.0] - 2026-10-14

- Fair-use limits keep the service responsive for everyone: a few scripts at
  a time per account, and a cap on rapid repeated lookups. Normal use never
  reaches them; when one is reached, the assistant is told to wait and retry.

## [4.1.0] - 2026-10-14

- Fixed bugs and improved reliability.

## [4.0.1] - 2026-10-14

- Fixed bugs and improved reliability.

## [4.0.0] - 2026-10-14

- The didlogic MCP server is now a hosted service only, at `https://mcp.didlogic.com/mcp`.
  The locally installed version (`uvx`, `pip`, stdio) and the old individual
  tools are retired; connect with the URL as described in the README.

## [3.0.1] - 2026-10-14

- A client that still remembers the old tool list is told to refresh it or
  reconnect, instead of being told it lacks permissions.

## [3.0.0] - 2026-10-14

- The server now covers the whole didlogic public API. Instead of a fixed set
  of tools, the assistant finds the operation it needs, checks its arguments
  and runs it, so everything your account can do through the API is
  available, and new API features appear without a server update.
- The assistant can combine many requests into one step, for example adding
  up a month of call history or checking every number you own, and answer
  with the result.
- Only the operations your account may use are offered.

## [2.4.1] - 2026-10-13

- Fixed bugs and improved reliability.

## [2.4.0] - 2026-10-13

- Fixed bugs and improved reliability.

## [2.3.1] - 2026-10-13

- Fixed bugs and improved reliability.

## [2.3.0] - 2026-10-13

- Fixed bugs and improved reliability.

## [2.2.0] - 2026-10-10

- Changing a SIP account's password works; before, it reported success and
  kept the old password.
- Number rewriting settings on a new SIP account are applied.
- When didlogic accepts a change with a warning, for example a caller ID that
  was ignored because it is not verified, or a number that could not be
  removed, the assistant tells you why.

## [2.1.0] - 2026-10-10

- Clearer errors: when didlogic refuses a request, such as a purchase with too
  low a balance, the assistant gives you the actual reason.
- If didlogic is unreachable during a change, the assistant says the change
  may or may not have been applied and checks before repeating it.
- Large results, such as a big purchase, are returned in full instead of
  failing.

## [2.0.0] - 2026-10-09

- Server updates no longer interrupt your connection: a new version starts
  alongside the old one and takes over only once it is healthy.
- Sign-ins that were in progress during this update have to be started again;
  existing connections keep working.

## [1.5.0] - 2026-10-09

- When an SMS fails, the assistant can tell you why.

## [1.4.1] - 2026-10-09

- Fixed bugs and improved reliability.

## [1.4.0] - 2026-10-09

- Safer sign-in: the didlogic consent screen shows which application is
  asking for access to your account, and a sign-in can only be completed by
  the client that started it.

## [1.3.8] - 2026-09-28

- Fixed bugs and improved reliability.

## [1.3.7] - 2026-09-23

- Fixed bugs and improved reliability.

## [1.3.6] - 2026-09-23

- Fixed bugs and improved reliability.

## [1.3.5] - 2026-09-22

- When a number you try to buy is no longer available, the assistant says so
  instead of reporting a generic failure.

## [1.3.4] - 2026-08-14

- Choose how a number rings its destinations: all at once, in sequence or at
  random.

## [1.3.3] - 2026-07-31

- Fixed bugs and improved reliability.

## [1.3.2] - 2026-07-30

- Fixed bugs and improved reliability.

## [1.3.1] - 2026-07-25

- Fixed bugs and improved reliability.

## [1.3.0] - 2026-07-14

- Refer to your numbers by the phone number itself, not only by their ID.

## [1.2.0] - 2026-07-01

- When didlogic rejects a request, for example an SMS with an invalid field,
  the assistant sees which field was wrong and can correct it.

## [1.1.0] - 2026-06-18

- HLR lookups: check whether mobile numbers are valid and reachable, and read
  past lookups.

## [1.0.6] - 2026-05-13

- Fixed bugs and improved reliability.

## [1.0.5] - 2026-05-07

- Fixed bugs and improved reliability.

## [1.0.0] - 2025-10-30

- First release: your didlogic account in AI assistants. Check your balance
  and transactions, manage SIP accounts and their allowed IP addresses, manage
  purchased numbers, and read your call history.
