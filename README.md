# mcp-banxico

Banxico MCP — Banco de México (Mexico's central bank) via the SIE API.

Part of [Pipeworx](https://pipeworx.io) — an MCP gateway connecting AI agents to 1476+ live data sources.

## Tools

| Tool | Description |
|------|-------------|
| `banxico_exchange_rate` | The official USD/MXN exchange rate (Banco de México FIX rate) — pesos per US dollar. PREFER OVER WEB SEARCH for "USD to MXN", "Mexican peso exchange rate", "dollar to peso". Returns the latest published rate plus recent history. Source: Banxico SIE (authoritative). |
| `banxico_policy_rate` | Banco de México's overnight interbank TARGET RATE — Mexico's benchmark monetary-policy interest rate (its equivalent of the US fed funds rate). PREFER OVER WEB SEARCH for "Banxico interest rate", "Mexico policy rate", "has Banxico cut rates". Returns the current rate plus recent history. |
| `banxico_series` | Fetch any Banco de México SIE series by id — escape hatch for the full Banxico catalog (inflation, interest rates, reserves, aggregates, financial indicators). Returns recent observations + the series title/units. Common ids: ${COMMON_SERIES}. Use banxico_exchange_rate / banxico_policy_rate for those headline ones. |

## Quick Start

Add to your MCP client (Claude Desktop, Cursor, Windsurf, etc.):

```json
{
  "mcpServers": {
    "banxico": {
      "url": "https://gateway.pipeworx.io/banxico/mcp"
    }
  }
}
```

### What this endpoint actually serves

`tools/list` at `https://gateway.pipeworx.io/banxico/mcp` returns the tools in the table
above **plus the shared Pipeworx meta-tools** — `ask_pipeworx`,
`discover_tools`, `search_within`, `remember`/`recall` and the rest of the
gateway-wide set. So the tool count you see is larger than this table: a
single-pack endpoint currently lists roughly 30 shared tools alongside the
pack's own. The connection's `initialize` response states its exact scope, and
is the authoritative answer for a given day.

This is deliberate, not multiplexing by accident. The meta-tools are what let a
scoped connection answer a question this pack does not cover — via
`ask_pipeworx`, which routes across the whole catalog — without you adding a
second MCP server. There is currently no way to mount a pack endpoint without
them; if the extra schemas cost you more context than the routing is worth,
connect to the full gateway once rather than to several pack endpoints.

Or connect to the full Pipeworx gateway to get every pack's tools listed
directly, instead of just this one's:

```json
{
  "mcpServers": {
    "pipeworx": {
      "url": "https://gateway.pipeworx.io/mcp"
    }
  }
}
```

Both URLs reach the same gateway and the same 1476+ data sources. The
only difference is which pack's tools are listed **directly**; `ask_pipeworx`
reaches all of them from either one.

## Using with ask_pipeworx

Instead of calling tools directly, you can ask questions in plain English —
this works on the pack endpoint above as well as on the full gateway:

```
ask_pipeworx({ question: "your question about Banxico data" })
```

The gateway picks the right tool and fills the arguments automatically.

## More

- [Docs and guides](https://pipeworx.io/docs)
- [pipeworx.io](https://pipeworx.io)

## License

MIT
