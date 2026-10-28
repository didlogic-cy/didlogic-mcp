# Tools

The didlogic MCP server exposes three tools. Together they give an assistant
the whole didlogic public API without one tool per operation.

## `search`

Finds the API operations that match a task.

| Argument | Type | Description |
|----------|------|-------------|
| `query` | string | What to look for, e.g. `balance`, `sms`, `buy number` |

Returns the matching operations by name with a short description. An
operation your account cannot use is not listed.

## `get_schema`

Returns the exact arguments of chosen operations.

| Argument | Type | Description |
|----------|------|-------------|
| `tools` | array of strings | Operation names from `search`, e.g. `["balance_show"]` |

An argument an operation does not declare is refused rather than ignored, so
a filter is never silently dropped.

## `execute`

Runs a short Python script that calls operations and returns one answer.

| Argument | Type | Description |
|----------|------|-------------|
| `code` | string | The script |

Inside the script, `await call_tool(name, params)` calls an operation with the
arguments from `get_schema`. Only the value the script returns reaches the
assistant, so it can page through results, combine calls and aggregate
without sending every page back.

```python
spent = 0
page = 1
while True:
    reply = await call_tool("calls_show", {"from": "2026-10-01", "to": "2026-10-31", "page": page})
    spent += sum(call["amount"] for call in reply["calls"])
    if page >= reply["pagination"]["total_pages"]:
        break
    page += 1
return round(spent, 2)
```

The script runs in a restricted sandbox: no file or network access other than
`call_tool`, a subset of Python, and limits on the number of calls, run time,
memory and reply size, which the tool's description states.

Writes take effect immediately. If a script stops part-way, the writes it
already made stay in place.

### Uploading files

Operations that take a file, such as uploading a KYC document, accept it as:

```json
{
  "content_base64": "<the file's bytes, base64-encoded>",
  "filename": "passport.pdf",
  "content_type": "application/pdf"
}
```

## Explicit mode

`https://mcp.didlogic.com/mcp/explicit` serves the same API as one tool per
operation instead of the three tools above, for assistants that need each
operation as a tool of its own. Each tool takes the operation's arguments
directly and says whether it only reads, may change or remove something, and
whether it reaches a phone number outside your account. Every operation is
listed; one your account cannot use is refused when called. Sign-in and API
keys work the same on both endpoints.

## Errors

A refused or failed call returns a message that says what happened and what
to do next. A message saying the key was not accepted means you need to sign
in again or replace the API key; retrying will not help.
