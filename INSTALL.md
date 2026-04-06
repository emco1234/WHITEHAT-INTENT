# Quick Install Guide

## One-Line Install (Linux/macOS/Git Bash on Windows)

```bash
# Clone the repo
git clone https://github.com/emco1234/WHITEHAT-INTENT.git /tmp/whitehat-intent

# Back up existing config
cp ~/.config/opencode/opencode.json ~/.config/opencode/opencode.json.backup 2>/dev/null
cp ~/.config/opencode/oh-my-opencode.json ~/.config/opencode/oh-my-opencode.json.backup 2>/dev/null

# Install spec template
mkdir -p ~/.intent/specs
cp /tmp/whitehat-intent/intent-specs/template.md ~/.intent/specs/template.md

# Done! Now merge the agent definitions into your opencode.json
# See README.md "Step 3" for details
```

## What You Need to Merge

### 1. Add agents to `opencode.json`

Copy the 5 agent entries from `config/opencode/agents.json` into your `~/.config/opencode/opencode.json` under the `"agent"` key.

Replace `"CHANGE_ME_TO_YOUR_MODEL"` with your actual model (e.g., `"anthropic/claude-sonnet-4-5"`, `"openai/gpt-4o"`, etc.).

### 2. Add categories to `oh-my-opencode.json`

Copy the 4 category entries from `config/oh-my-opencode/categories.json` into your `~/.config/opencode/oh-my-opencode.json` under the `"categories"` key.

### 3. Set default agent

In your `opencode.json`, set:
```json
{
  "default_agent": "WHITEHAT-INTENT"
}
```

### 4. Add Context7 MCP (required)

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

### 5. Restart OpenCode

```bash
opencode
```

WHITEHAT-INTENT is now your default agent.
