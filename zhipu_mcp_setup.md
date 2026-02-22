# Zhipu MCP Setup Guide - Complete Documentation

**Setup Date:** 2026-02-22
**Purpose:** Setup Zhipu Visual Understanding MCP Server for OpenClaw and other MCP-compatible clients

---

## Quick Install Commands

### Claude Code (Recommended)
```bash
claude mcp add -s user zai-mcp-server --env Z_AI_API_KEY=YOUR_API_KEY -- npx -y "@z_ai/mcp-server@latest"
```

### Cline
```json
// ~/.clauderc.json or project config
{
  "mcpServers": {
    "zai-mcp-server": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@z_ai/mcp-server@latest"],
      "env": {
        "Z_AI_API_KEY": "YOUR_API_KEY",
        "Z_AI_MODE": "ZHIPU"
      }
    }
  }
}
```

### Crush
```json
{
  "mcpServers": {
    "zai-mcp-server": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@z_ai/mcp-server@latest"],
      "env": {
        "Z_AI_API_KEY": "YOUR_API_KEY",
        "Z_AI_MODE": "ZHIPU"
      }
    }
  }
}
```

### Roo Code / Kilo Code
```json
{
  "mcpServers": {
    "zai-mcp-server": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@z_ai/mcp-server@latest"],
      "env": {
        "Z_AI_API_KEY": "YOUR_API_KEY",
        "Z_AI_MODE": "ZHIPU"
      }
    }
  }
}
```

**Important:** Replace `YOUR_API_KEY` with your actual Zhipu API key:
```
2089f766b091405486ebcecc7bc31e61.qm73eLPh5zQJtcQV
```

---

## Usage Examples

### Example 1: Image Analysis
**You:** "Analyze this image"

**Process:**
1. You send image to Claude Code
2. Claude Code calls `image_analysis` MCP tool
3. Zhipu GLM-4.6V analyzes image
4. Returns structured response with objects, text, insights

---

### Example 2: Screenshot to Code
**You:** "What does this UI component do?"

**Process:**
1. You send screenshot image to Claude Code
2. Claude Code calls `ui_to_artifact` or `extract_text_from_screenshot`
3. MCP Server extracts component structure, generates code
4. Returns React/Vue/HTML components with styling

---

### Example 3: Diagram Understanding
**You:** "Explain this architecture diagram"

**Process:**
1. You send diagram image to Claude Code
2. Claude Code calls `understand_technical_diagram`
3. MCP Server analyzes diagram structure
4. Returns explanation of components, data flow, relationships

---

## Available Tools

| Tool | Description | Input | Output |
|-------|-------------|--------|--------|
| `ui_to_artifact` | UI screenshot | Code, design specs, prompts |
| `extract_text_from_screenshot` | Screenshot/terminal image | Text content |
| `diagnose_error_screenshot` | Error dialog | Diagnosis, suggestions |
| `understand_technical_diagram` | Architecture diagram | Component explanation |
| `analyze_data_visualization` | Charts, dashboards | Insights, trends |
| `ui_diff_check` | Two UI screenshots | Differences, issues |
| `image_analysis` | General image | Objects, context, description |
| `video_analysis` | Video (MP4/MOV) | Scenes, events, text |

---

## Quota & Pricing

### Free Tier
- **Search & Web Read MCP:** 100 requests/month
- **Vision MCP:** 5 hours prompt pool, resets in 5 hours
- **After quota exhausted:** Cannot use until next billing cycle

### Pro Tier (¥29/month)
- **Search & Web Read MCP:** 1,000 requests/month
- **Vision MCP:** 5 hours prompt pool
- **After quota exhausted:** Cannot use until next billing cycle

### Max Tier (¥99/month)
- **Search & Web Read MCP:** 4,000 requests/month
- **Vision MCP:** 5 hours prompt pool
- **After quota exhausted:** Cannot use until next billing cycle

---

## Troubleshooting

### MCP Not Listed
1. Check config file syntax
2. Verify API key is valid
3. Restart client completely
4. Check MCP server logs

### Connection Failed
1. Verify API key
2. Check internet connection
3. Try using latest version

### Quota Exceeded
1. Check remaining quota in Zhipu Console
2. Upgrade plan if needed

---

## Best Practices

### 1. Security
- Never commit API keys to Git
- Store in environment variables only
- Use read-only permissions for config files

### 2. Performance
- Use MCP only when native tools insufficient
- Combine with existing tools when possible
- Batch visual tasks when appropriate

### 3. Cost Optimization
- Use cheaper native tools for simple tasks
- Reserve MCP for complex visual understanding
- Monitor usage in Zhipu Console

---

## Resources

- **Official Docs:** https://open.bigmodel.cn/docs/ai/visual_mcp
- **NPM Package:** https://www.npmjs.com/package/@z_ai/mcp-server
- **Zhipu Console:** https://open.bigmodel.cn/console
- **Your API Key:** Already configured in `/root/.zhipu-config.json`

---

**Last Updated:** 2026-02-22
**Status:** ✅ Documentation ready for installation
