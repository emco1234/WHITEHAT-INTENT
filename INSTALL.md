# Quick Install Guide

## One-Line Install (Linux/macOS/Git Bash on Windows)

```bash
# Clone the repo
git clone https://github.com/emco1234/WHITEHAT-INTENT.git /tmp/whitehat-intent

# Back up existing config
cp ~/.config/opencode/opencode.json ~/.config/opencode/opencode.json.backup 2>/dev/null

# Done! WHITEHAT-INTENT auto-creates .intent/specs/ on first use.
# Now merge the agent definitions into your opencode.json
# See README.md "Step 3" for details
```

## What You Need to Merge

### 1. Add agents to `opencode.json`

Copy the 5 agent entries from `config/opencode/agents.json` into your `~/.config/opencode/opencode.json` under the `"agent"` key.

Replace `"CHANGE_ME_TO_YOUR_MODEL"` with your actual model (e.g., `"anthropic/claude-sonnet-4-5"`, `"openai/gpt-4o"`, etc.).

### 2. Set default agent

In your `opencode.json`, set:
```json
{
  "default_agent": "WHITEHAT-INTENT"
}
```

### 3. Add Context7 MCP (required)

In your `opencode.json`, under `"mcp"`, add:
```json
{
  "context7": {
    "type": "local",
    "command": ["npx", "-y", "@upstash/context7-mcp", "--transport", "stdio"],
    "enabled": true,
    "timeout": 20000
  }
}
```

### 4. Restart OpenCode

```bash
opencode
```

WHITEHAT-INTENT is now your default agent.
