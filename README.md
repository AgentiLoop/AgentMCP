# AgentMCP

A lightweight Swift MCP (Model Context Protocol) client for macOS. Connect to any MCP server via stdio or HTTP — no external SDK required.

## Features

- **Stdio & HTTP** transport support
- **JSON-RPC 2.0** protocol implementation
- **Tool discovery** — auto-discover tools from connected servers
- **Tool execution** — call tools with typed arguments
- **Resource reading** — read resources from MCP servers
- **Multi-server** — manage connections to multiple servers simultaneously
- **Zero dependencies** — pure Swift, no external packages
- **macOS 14+** / Swift 6.4

## Installation

Add to your `Package.swift`:

```swift
dependencies: [
    .package(url: "https://github.com/AgentiLoop/AgentMCP.git", from: "1.6.10"),
]
```

Then add `MCPClient` to your target:

```swift
.target(name: "YourApp", dependencies: [
    .product(name: "MCPClient", package: "AgentMCP"),
]),
```

## Usage

```swift
import MCPClient

// Create client and connect to an MCP server via stdio
let client = MCPClient()
let serverId = try await client.connect(
    name: "my-server",
    command: "/path/to/mcp-server",
    arguments: []
)

// Discover available tools
let tools = try await client.listTools(serverId: serverId)

// Call a tool
let result = try await client.callTool(
    serverId: serverId,
    name: "my_tool",
    arguments: ["key": .string("value")]
)
```

## Architecture

| File | Purpose |
|------|---------|
| `MCPClient.swift` | Main client API — connect, list tools, call tools |
| `MCPConnection.swift` | Base connection protocol |
| `StdioConnection.swift` | Stdio transport (launches process) |
| `HTTPConnection.swift` | HTTP/SSE transport |
| `ServerManager.swift` | Multi-server connection manager |
| `JSONValue.swift` | Type-safe JSON encoding/decoding |
| `MCPClientError.swift` | Error types |

## Part of AgentiLoop Agent!

AgentMCP is one of the open-source building blocks of **[AgentiLoop Agent!](https://github.com/AgentiLoop/Agent)**, the native AI agent for macOS 14.6+ on Apple Silicon and Intel. Agent! codes in Xcode, drives any Mac app, runs shell as you or as root, and works with 23 LLM providers plus on-device Apple Intelligence.

🌐 [agentiloop.ai](https://agentiloop.ai/) · ⬇️ [Download Agent!](https://github.com/AgentiLoop/Agent/releases/latest) · 🍺 `brew install --cask agentiloop-agent` · 💻 CLIs: [Rust](https://github.com/AgentiLoop/AgentiLoopCLI) / [Go](https://github.com/AgentiLoop/AgentiLoopGo)

**More Agent! packages:** [AgentAccess](https://github.com/AgentiLoop/AgentAccess) · [AgentAudit](https://github.com/AgentiLoop/AgentAudit) · [AgentColorSyntax](https://github.com/AgentiLoop/AgentColorSyntax) · [AgentD1F](https://github.com/AgentiLoop/AgentD1F) · [AgentEventBridges](https://github.com/AgentiLoop/AgentEventBridges) · [AgentLLM](https://github.com/AgentiLoop/AgentLLM) · [AgentSwift](https://github.com/AgentiLoop/AgentSwift) · [AgentTerminalNeo](https://github.com/AgentiLoop/AgentTerminalNeo) · [AgentTools](https://github.com/AgentiLoop/AgentTools) · [AgentScripts](https://github.com/AgentiLoop/AgentScripts)

## License

MIT

---

Copyright © 2026 AgentiLoop.ai, a Logos InkPen LLC company. All rights reserved.
