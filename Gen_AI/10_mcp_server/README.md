# MCP Server

Enkel MCP-server (Model Context Protocol) som exponerar verktyg till AI-assistenter.

## Vad är MCP?

MCP är Anthropics öppna standard för att koppla AI-assistenter till externa verktyg och datakällor. En MCP-server kan exponera:

- **Tools** - Funktioner som AI:n kan anropa
- **Resources** - Data som AI:n kan läsa
- **Prompts** - Fördefinierade promptmallar

## Installation

```bash
pip install mcp
```

## Användning

### Alternativ 1: Kör direkt

```bash
mcp run server.py
```

### Alternativ 2: Claude Desktop

Lägg till i `claude_desktop_config.json`:

**Windows:** `%APPDATA%\Claude\claude_desktop_config.json`
**Mac:** `~/Library/Application Support/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "demo": {
      "command": "python",
      "args": ["C:/full/path/to/server.py"]
    }
  }
}
```

Starta om Claude Desktop efter ändring.

## Tillgängliga verktyg

| Verktyg | Beskrivning |
|---------|-------------|
| `add(a, b)` | Adderar två tal |
| `multiply(a, b)` | Multiplicerar två tal |
| `get_weather(city)` | Hämtar väder (mock) |
| `reverse_string(text)` | Vänder på en sträng |

## Skapa egna verktyg

```python
from mcp.server.fastmcp import FastMCP

mcp = FastMCP("Min Server")

@mcp.tool()
def my_function(param: str) -> str:
    """Beskrivning av vad funktionen gör."""
    return f"Resultat: {param}"
```

## Länkar

- [MCP Documentation](https://modelcontextprotocol.io/)
- [MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk)
