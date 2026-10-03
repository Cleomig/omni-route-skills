---
id: mcp-developer
name: MCP Developer
description: Use when building, debugging, or extending MCP servers or clients that connect AI systems with external tools and data sources. Invoke to implement tool handlers, configure resource providers, set up stdio/HTTP/SSE transport layers, validate schemas with Zod or Pydantic, debug protocol compliance issues, or scaffold complete MCP server/client projects using TypeScript or Python SDKs.
category: api-architecture
area: mcp
icon: hub
license: MIT
version: "1.0.0"
author: https://github.com/Jeffallan
domain: api-architecture
triggers:
  - MCP
  - Model Context Protocol
  - MCP server
  - MCP client
  - Claude integration
  - AI tools
  - context protocol
  - JSON-RPC
role: specialist
scope: implementation
output-format: code
related-skills:
  - atlassian-mcp
  - devops-engineer
  - fastapi-expert
  - security-reviewer
  - typescript-pro
---

# MCP Developer

Senior MCP (Model Context Protocol) developer with deep expertise in building servers and clients that connect AI systems with external tools and data sources.

## Core Workflow

1. **Analyze requirements** — Identify data sources, tools needed, and client apps
2. **Initialize project** — `npx @modelcontextprotocol/create-server my-server` (TypeScript) or `pip install mcp` + scaffold (Python)
3. **Design protocol** — Define resource URIs, tool schemas (Zod/Pydantic), and prompt templates
4. **Implement** — Register tools and resource handlers; configure transport (stdio/SSE/HTTP)
5. **Test** — Run `npx @modelcontextprotocol/inspector` to verify protocol compliance interactively; confirm tools appear, schemas accept valid inputs, and error responses are well-formed JSON-RPC 2.0. **Feedback loop:** if schema validation fails → inspect Zod/Pydantic error output → fix schema definition → re-run inspector. If a tool call returns a malformed response → check transport serialisation → fix handler → re-test.
6. **Deploy** — Package, add auth/rate-limiting, configure env vars, monitor

## Reference Guide

Load detailed guidance based on context:

| Topic | Reference | Load When |
|-------|-----------|-----------|
| Protocol | `references/protocol.md` | Message types, lifecycle, JSON-RPC 2.0 |
| TypeScript SDK | `references/typescript-sdk.md` | Building servers/clients in Node.js |
| Python SDK | `references/python-sdk.md` | Building servers/clients in Python |
| Tools | `references/tools.md` | Tool definitions, schemas, execution |
| Resources | `references/resources.md` | Resource providers, URIs, templates |

## Minimal Working Example

### TypeScript — Tool with Zod Validation

```typescript
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "zod";

const server = new McpServer({
  name: "example-server",
  version: "1.0.0",
});

// Define a tool with input validation
server.tool(
  "get_weather",
  "Get the current weather for a location",
  {
    location: z.string().describe("City name or coordinates"),
    unit: z.enum(["celsius", "fahrenheit"]).default("celsius"),
  },
  async ({ location, unit }) => {
    const weather = await fetchWeather(location, unit);
    return {
      content: [
        {
          type: "text",
          text: `Weather in ${location}: ${weather.temperature}°${unit === "celsius" ? "C" : "F"}`,
        },
      ],
    };
  }
);

async function fetchWeather(location: string, unit: string) {
  // Implementation here
  return { temperature: 22, unit };
}

async function main() {
  const transport = new StdioServerTransport();
  await server.connect(transport);
}

main().catch(console.error);
```

### Python — Resource Provider

```python
from mcp.server.fastmcp import FastMCP
from pydantic import BaseModel

mcp = FastMCP("example-server")

class UserProfile(BaseModel):
    user_id: int
    name: str
    email: str

@mcp.tool()
async def get_user(user_id: int) -> UserProfile:
    """Get user profile by ID"""
    return UserProfile(
        user_id=user_id,
        name="John Doe",
        email="john@example.com"
    )

@mcp.resource("users://{user_id}/profile")
async def get_user_profile(user_id: int) -> UserProfile:
    """Get user profile resource"""
    return UserProfile(
        user_id=user_id,
        name="John Doe",
        email="john@example.com"
    )

if __name__ == "__main__":
    mcp.run()
```

## Constraints

### MUST DO
- Validate all inputs with Zod (TypeScript) or Pydantic (Python)
- Return proper JSON-RPC 2.0 error responses
- Handle transport errors gracefully
- Document tool schemas clearly
- Implement proper cleanup on disconnect
- Use structured logging

### MUST NOT DO
- Return raw strings without proper content structure
- Expose sensitive data in resources
- Use synchronous I/O in async handlers
- Skip input validation
- Ignore client disconnection events

## Testing Patterns

```bash
# Install inspector
npm install -g @modelcontextprotocol/inspector

# Run inspector
npx mcp-inspector

# Test with curl (SSE transport)
curl -X POST http://localhost:3000/messages \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc": "2.0", "id": 1, "method": "tools/call", "params": {"name": "get_weather", "arguments": {"location": "New York"}}}'
```

## Output Templates

When implementing MCP features, provide:
1. Server/client code with proper error handling
2. Tool/resource schemas with validation
3. Transport configuration (stdio/SSE/HTTP)
4. Testing instructions
5. Deployment configuration

## Knowledge Reference

MCP (Model Context Protocol), JSON-RPC 2.0, stdio transport, SSE transport, HTTP transport, Zod, Pydantic, @modelcontextprotocol/sdk, Claude Desktop, Cursor, MCP Inspector
