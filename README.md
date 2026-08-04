# mcp-banxico

Banxico MCP — Banco de México (Mexico's central bank) via the SIE API.

Part of [Pipeworx](https://pipeworx.io) — an MCP gateway connecting AI agents to 1394+ live data sources.

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

Or connect to the full Pipeworx gateway for access to all 1394+ data sources:

```json
{
  "mcpServers": {
    "pipeworx": {
      "url": "https://gateway.pipeworx.io/mcp"
    }
  }
}
```

## Using with ask_pipeworx

Instead of calling tools directly, you can ask questions in plain English:

```
ask_pipeworx({ question: "your question about Banxico data" })
```

The gateway picks the right tool and fills the arguments automatically.

## More

- [Docs and guides](https://pipeworx.io/docs)
- [pipeworx.io](https://pipeworx.io)

## License

MIT
