# The Divine Commandments of mcp-streamablehttp-proxy

**🔥 Behold! The Sacred stdio-to-StreamableHTTP Bridge of Divine Protocol Transcendence! ⚡**

## The Sacred Purpose - Bridge of Divine Protocol Translation!

**⚡ This blessed proxy bridges stdio MCP servers to StreamableHTTP glory! ⚡**

The **mcp-streamablehttp-proxy** is the divine bridge that transforms humble stdio-based MCP servers into glorious HTTP endpoints! It channels the following sacred powers:

- **🌉 Protocol Bridging** - Converts stdio JSON-RPC to HTTP StreamableHTTP!
- **🔄 Session Management** - Each client blessed with isolated subprocess!
- **⚡ Subprocess Orchestration** - Spawns and manages MCP server children!
- **🎯 Request Correlation** - Maps async responses to their divine requests!

**⚡ Without this proxy, stdio servers remain trapped in terminal purgatory! ⚡**

## The Holy Architecture - Divine Separation of Concerns!

```
┌─────────────────────────────────────────────────────────────┐
│           HTTP Client (Claude.ai, IDE, etc.)                 │
│                    Speaks StreamableHTTP                      │
└──────────────────────────┬───────────────────────────────────┘
                           │ HTTP POST /mcp
                           │ Mcp-Session-Id: <uuid>
                           ↓
┌─────────────────────────────────────────────────────────────┐
│              mcp-streamablehttp-proxy (This Holy Service)    │
│  • Receives HTTP requests at sacred /mcp endpoint           │
│  • Manages sessions with divine UUID blessing               │
│  • Spawns stdio MCP server subprocess per session          │
│  • Translates HTTP ↔ stdio with protocol righteousness     │
│  • Correlates async responses via request IDs              │
└──────────────────────────┬───────────────────────────────────┘
                           │ stdin/stdout pipes
                           │ JSON-RPC 2.0
                           ↓
┌─────────────────────────────────────────────────────────────┐
│          stdio MCP Server (Official or Custom)               │
│    • mcp-server-fetch, mcp-server-filesystem, etc.          │
│    • Speaks only stdio JSON-RPC - knows not of HTTP!        │
│    • Blissfully unaware of the divine HTTP transformation!  │
└─────────────────────────────────────────────────────────────┘
```

**⚡ Each layer has its divine purpose! Violate not the sacred boundaries! ⚡**

## The Sacred CLI Invocation - Command Line Divinity!

**🔥 The blessed command structure that summons the proxy! ⚡**

```bash
# The Divine Invocation Pattern
mcp-streamablehttp-proxy [OPTIONS] <server_command> [server_args...]

# Sacred Options (All Optional with Divine Defaults!)
--host <host>        # Binding host (default: 127.0.0.1, env: MCP_BIND_HOST)
--port <port>        # Binding port (default: 3000, env: MCP_PORT)
--timeout <seconds>  # Session timeout (default: 300)
--log-level <level>  # Logging verbosity: debug/info/warning/error (default: info)
```

**⚡ The server command is MANDATORY - without it, the proxy has nothing to bridge! ⚡**

### Divine Examples of Righteous Invocation

```bash
# Python module invocation - The blessed pattern!
mcp-streamablehttp-proxy python -m mcp_server_fetch

# Direct executable with sacred arguments!
mcp-streamablehttp-proxy /usr/bin/mcp-server --config /etc/mcp.conf

# Custom port with extended timeout blessing!
mcp-streamablehttp-proxy --port 8080 --timeout 600 npx @modelcontextprotocol/server-memory

# Debug mode for divine troubleshooting!
mcp-streamablehttp-proxy --log-level debug python -m mcp_server_filesystem --root /data
```

## The Session Lifecycle - Sacred State Management!

**🌅 Birth, Life, and Death of Divine Sessions! 🌄**

### 1. Session Birth - The Initialize Blessing
```json
// Client sends sacred initialize request
POST /mcp
{
  "jsonrpc": "2.0",
  "method": "initialize",
  "params": {
    "protocolVersion": "2025-06-18",
    "capabilities": {},
    "clientInfo": {"name": "client", "version": "1.0"}
  },
  "id": 1
}

// Proxy responds with session blessing
Response Headers: Mcp-Session-Id: <sacred-uuid>
{
  "jsonrpc": "2.0",
  "result": {
    "protocolVersion": "2025-06-18",
    "capabilities": {},
    "serverInfo": {"name": "server", "version": "1.0"}
  },
  "id": 1
}
```

**⚡ The session ID is thy divine key! Guard it with thy life! ⚡**

### 2. Session Life - The Operational Glory
```json
// All subsequent requests must bear the sacred session ID!
POST /mcp
Headers: Mcp-Session-Id: <sacred-uuid>
{
  "jsonrpc": "2.0",
  "method": "tools/list",
  "id": 2
}
```

### 3. Session Death - The Timeout Judgment
- **Default lifetime**: 300 seconds of divine existence!
- **Cleanup cycle**: Every 60 seconds, the reaper visits!
- **Graceful termination**: Subprocess receives SIGTERM blessing!

**⚡ Abandoned sessions are purged to prevent resource damnation! ⚡**

## The Sacred Environment Variables

**⚙️ Divine configuration through the blessed environment! ⚡**

```bash
# Binding Configuration
MCP_BIND_HOST=0.0.0.0     # Override default localhost binding
MCP_PORT=8080             # Override default 3000 port

# Logging Configuration
LOG_FILE=/var/log/mcp-proxy.log  # Enable file logging blessing
```

**⚡ Environment variables override CLI args - this is the divine precedence! ⚡**

## The Protocol Translation Mysteries

**🔄 How stdio becomes HTTP - The divine transformation! ⚡**

### The Request Flow - Downstream Divine Journey
1. **HTTP POST arrives** at `/mcp` endpoint with JSON-RPC body
2. **Session validation** - New or existing via Mcp-Session-Id
3. **Write to subprocess** - JSON + newline to stdin pipe
4. **Correlation setup** - Request ID mapped to Future

### The Response Flow - Upstream Blessed Return
1. **Read from subprocess** - Line-by-line from stdout pipe
2. **JSON parsing** - Each line is complete JSON-RPC message
3. **ID matching** - Response correlated via request ID
4. **HTTP response** - Returned to waiting client

**⚡ Notifications (no ID) are logged but not returned - one-way divine messages! ⚡**

## The Sacred Feature Matrix

**✅ Implemented Divine Powers:**
- Session management with UUID blessing
- Full MCP protocol lifecycle support
- Request-response correlation via ID
- Subprocess lifecycle management
- Configurable timeouts and cleanup
- Multiple concurrent sessions
- Protocol version forwarding
- Tool discovery support

**❌ Not Implemented (By Divine Design!):**
- Authentication (SWAG's job!)
- CORS handling (SWAG's job!)
- SSL/TLS (SWAG's job!)
- Rate limiting (SWAG's job!)

**⚡ The proxy focuses on protocol translation - all else is delegated! ⚡**

## The Debugging Commandments

**🔍 When sessions fail and responses timeout! ⚡**

### Enable Debug Logging - The Sight Beyond Sight!
```bash
# See all divine communications!
mcp-streamablehttp-proxy --log-level debug <server>

# Or via environment
export LOG_FILE=/tmp/mcp-debug.log
mcp-streamablehttp-proxy --log-level debug <server>
```

### Common Debugging Patterns
- **Session not found**: Client using expired or invalid session ID
- **Timeout errors**: Server taking >30s to respond
- **Subprocess died**: Check stderr output in logs
- **Protocol mismatch**: Client/server version negotiation failed

**⚡ Debug logs reveal all - but beware the verbosity demon! ⚡**

## The Integration Patterns

### Docker Deployment - The Containerized Glory!
```dockerfile
FROM python:3.11-slim
# Install via pixi (blessed!) or pip
RUN pip install mcp-streamablehttp-proxy
ENV MCP_BIND_HOST=0.0.0.0
CMD ["mcp-streamablehttp-proxy", "--host", "0.0.0.0", "python", "-m", "mcp_server_fetch"]
```

### With SWAG - The Divine Gateway Integration!
```nginx
# /config/nginx/proxy-confs/mcp-service.subdomain.conf
server {
    listen 443 ssl;
    server_name mcp-service.${BASE_DOMAIN};

    location = /_oauth_verify {
        internal;
        proxy_pass http://auth:8000/verify;
        proxy_set_header Authorization $http_authorization;
    }
    location /mcp {
        auth_request /_oauth_verify;
        proxy_pass http://mcp-fetch:3000;
    }
}
```

**⚡ Always bind to 0.0.0.0 in containers - localhost is container prison! ⚡**

## The Sacred Warnings and Divine Prohibitions

**⚡ FORBIDDEN: Running without proper server command! ⚡**
```bash
# This brings instant death!
mcp-streamablehttp-proxy  # No server = No purpose!
```

**⚡ FORBIDDEN: Exposing to public internet without auth! ⚡**
- Always deploy behind SWAG with auth_request for ForwardAuth!
- Never bind to 0.0.0.0 without protection!
- Session IDs are not authentication!

**⚡ FORBIDDEN: Infinite timeouts! ⚡**
- Sessions must expire or resources leak!
- Dead subprocesses must be reaped!
- Memory is not infinite!

## The Performance Revelations

**⚡ Sacred truths about proxy performance! ⚡**

- **One subprocess per session** - Isolation requires resources!
- **30s request timeout** - Long operations may timeout!
- **Async throughout** - Non-blocking divine glory!
- **No request queuing** - Parallel requests within session supported!

**⚡ For heavy loads, scale horizontally with divine load balancing! ⚡**

## The Testing Commandments

**🧪 Test with real MCP servers or face protocol chaos! ⚡**

```bash
# Test with echo server
mcp-streamablehttp-proxy python -m mcp_echo_server

# Verify with curl
curl -X POST http://localhost:3000/mcp \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","method":"initialize","params":{"protocolVersion":"2025-06-18","capabilities":{},"clientInfo":{"name":"test","version":"1.0"}},"id":1}'

# Use returned session ID for subsequent requests!
```

**⚡ Mock servers hide protocol sins - use real implementations! ⚡**

---

**🔥 May your stdio servers speak HTTP, your sessions stay alive, and your subprocesses terminate cleanly! ⚡**

**Remember: This proxy is but one component in the greater MCP OAuth Gateway divine architecture!**
