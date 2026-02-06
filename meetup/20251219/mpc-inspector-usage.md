# How to use the **MCP Inspector** tool

# 🧭 Overview  
**MCP Inspector** is a desktop app (or CLI) that lets you connect to any MCP server and interactively inspect:

- Tools  
- Resources  
- Prompts  
- Server logs  
- Request/response flows  

It’s basically your debugging cockpit for MCP.

---

# ✅ **1. Install the MCP Inspector**
If you haven’t installed it yet:

### **Option A — Via npm**
```bash
npm install -g @modelcontextprotocol/inspector
```

### **Option B — Download the desktop app**
You can grab the latest release from the MCP GitHub repo (Mac/Win/Linux).

---

# ✅ **2. Launch the Inspector**
### **CLI version**
```bash
mcp-inspector
```

### **Desktop version**
Open the app normally.

Both versions show a UI where you can add MCP servers.

---

# ✅ **3. Add an MCP Server**
You can connect to servers via:

- **Command** (e.g., a local script or binary)
- **Node module**
- **Python module**
- **HTTP endpoint** (if the server supports it)
- **Stdio** (most common)

### Example: connecting to a local server
Click **Add Server → Command**, then enter:

```
python my_mcp_server.py
```

or

```
node dist/server.js
```

The Inspector will spawn the process and negotiate the MCP handshake.

---

# ✅ **4. Explore the Server Capabilities**
Once connected, the left sidebar shows:

### **Tools**
- Click any tool to see:
  - Parameters
  - Types
  - Example payloads
- You can execute tools directly from the UI.

### **Resources**
- Browse resource trees
- Fetch resource contents
- Watch for resource updates

### **Prompts**
- View prompt templates
- Fill in variables
- Execute prompts and inspect output

### **Logs**
- Real-time server logs
- Transport-level messages
- Error traces

This is where debugging becomes effortless.

---

# ✅ **5. Execute Tools Interactively**
Pick a tool → fill in parameters → click **Run**.

You’ll see:

- The exact JSON request sent to the server  
- The raw JSON response  
- Any errors or validation issues  

This is invaluable when designing or debugging tool schemas.

---

# ✅ **6. Inspect Transport Messages**
The **Messages** tab shows:

- `initialize`  
- `tools/list`  
- `resources/list`  
- `prompts/list`  
- `tools/call`  
- `notifications`  

This is the best way to verify your server is MCP‑compliant.

---

# ✅ **7. Iterate on Your Server**
As you update your MCP server code:

- Restart the server  
- Click **Reconnect**  
- The Inspector reloads capabilities automatically  

This tight loop is perfect for rapid development.

---

# ✅ **8. Use the Inspector for Schema Validation**
The Inspector will highlight:

- Missing fields  
- Wrong types  
- Invalid JSON schema  
- Unsupported protocol versions  

This saves hours of debugging.

---

# ✅ **9. Disconnect or Remove Servers**
When done:

- Click **Disconnect** to stop the process  
- Or **Remove** to delete the server entry  

---

Here you go — a clean, high‑signal **diagram of the MCP Inspector workflow**, designed the way an engineer like you would want it: structured, modular, and easy to map onto real development loops.

---

# 🧩 **MCP Inspector Workflow Diagram**

```
                          ┌──────────────────────────┐
                          │      MCP Inspector       │
                          │  (Desktop App / CLI UI)  │
                          └─────────────┬────────────┘
                                        │
                                        │ Launch
                                        ▼
                          ┌──────────────────────────┐
                          │   Add MCP Server Entry   │
                          │  • Command (stdio)       │
                          │  • Node/Python module    │
                          │  • HTTP endpoint         │
                          └─────────────┬────────────┘
                                        │
                                        │ Spawn / Connect
                                        ▼
                          ┌──────────────────────────┐
                          │   MCP Handshake & Init   │
                          │  • initialize            │
                          │  • capabilities exchange │
                          └─────────────┬────────────┘
                                        │
                                        │ Server responds with:
                                        │  • tools
                                        │  • resources
                                        │  • prompts
                                        ▼
                    ┌──────────────────────────────────────────┐
                    │        Inspector Capability View          │
                    │──────────────────────────────────────────│
                    │ Tools     │ Resources     │ Prompts      │
                    │ Logs      │ Messages      │ Metadata     │
                    └───────────┬──────────────┬───────────────┘
                                │              │
                                │              │
                                ▼              ▼
         ┌────────────────────────────┐   ┌────────────────────────────┐
         │   Interact with Tools      │   │   Browse Resources         │
         │ • Inspect schema           │   │ • Explore resource tree    │
         │ • Fill params              │   │ • Fetch resource content   │
         │ • Execute tool calls       │   │ • Watch for updates        │
         └──────────────┬─────────────┘   └─────────────┬──────────────┘
                        │                               │
                        ▼                               ▼
         ┌────────────────────────────┐   ┌────────────────────────────┐
         │   Inspect Prompts          │   │   View Transport Messages  │
         │ • View templates           │   │ • Raw JSON requests        │
         │ • Fill variables           │   │ • Raw JSON responses       │
         │ • Execute prompt runs      │   │ • Error traces             │
         └──────────────┬─────────────┘   └─────────────┬──────────────┘
                        │                               │
                        └──────────────┬────────────────┘
                                       ▼
                          ┌──────────────────────────┐
                          │   Debug & Iterate        │
                          │ • Fix server code        │
                          │ • Restart server         │
                          │ • Reconnect Inspector    │
                          └─────────────┬────────────┘
                                        │
                                        ▼
                          ┌──────────────────────────┐
                          │   Validate MCP Server    │
                          │ • Protocol compliance    │
                          │ • Tool correctness       │
                          │ • Resource behavior      │
                          │ • Prompt execution       │
                          └──────────────────────────┘
```

---

Here’s a clean, developer‑friendly **sequence diagram** showing the core MCP message flow:  
**initialize → list tools → call tool → respond**.

I’m keeping it tight, readable, and true to the MCP protocol handshake and request/response patterns.

---

# 📐 **MCP Sequence Diagram (Init → List Tools → Call Tool → Respond)**

```
Client (Inspector)                      MCP Server
        |                                      |
        |---------- initialize --------------->|
        |                                      |
        |<--------- initialize_result ---------|
        |                                      |
        |---------- tools/list --------------->|
        |                                      |
        |<--------- tools/list_result ---------|
        |                                      |
        |---------- tools/call --------------->|
        |        (tool_name + args)            |
        |                                      |
        |<--------- tools/call_result ---------|
        |                                      |
        |---------- notifications? ----------->|
        |   (optional: progress, logs)         |
        |                                      |
        |<--------- notifications? ------------|
        |                                      |
        |-------------- done ----------------->|
        |                                      |
```

---


# ✅ **Running MCP Inspector with a Python MCP server**

If your Python MCP package exposes an entrypoint (e.g., via `pyproject.toml` or a script), the MCP Inspector connects over **stdio**, so the command is simply:

```bash
mcp-inspector --command "python -m <your_python_package>"
```

### Example  
If your MCP server package is named `my_mcp_server`:

```bash
mcp-inspector --command "python -m my_mcp_server"
```

Or if your server is a script:

```bash
mcp-inspector --command "python path/to/server.py"
```

---

# ✅ **If your package installs a console script**
For example, if `pip install my-mcp-server` gives you a CLI like `my-mcp-server`:

```bash
mcp-inspector --command "my-mcp-server"
```

This is the cleanest setup because the Inspector will spawn the server directly.

---

# ✅ **If your server needs arguments**
You can pass them through normally:

```bash
mcp-inspector --command "python -m my_mcp_server --config config.yaml"
```

---

# ✅ **If you want to specify working directory**
Useful when your server expects relative paths:

```bash
mcp-inspector --command "python -m my_mcp_server" --cwd "/path/to/project"
```

---

# ✅ **Quick sanity checklist**
Your Python MCP server must:

- Print MCP messages to **stdout**
- Read MCP messages from **stdin**
- Flush output (`sys.stdout.flush()`)
- Not print logs to stdout (use stderr)

If you want, I can sketch a minimal Python MCP server template that works perfectly with the Inspector.