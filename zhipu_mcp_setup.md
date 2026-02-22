# Zhipu MCP Setup Guide

**Setup Date:** 2026-02-22
**Setup for:** Ryan (tencentmeetings)

---

## What is Zhipu MCP?

**Zhipu Visual Understanding MCP Server** is a Model Context Protocol (MCP) server developed by Z.AI that provides powerful visual capabilities including:
- 🖼️ Image analysis and understanding
- 🎥 Video understanding
- Screenshot text extraction
- Technical diagram analysis
- UI component recognition
- Data visualization interpretation

**Key Features:**
- Advanced OCR and text recognition
- Code generation from UI screenshots
- Diagram structure extraction
- Design system analysis
- Error diagnosis from screenshots

---

## Prerequisites

### System Requirements
- **Node.js** >= v18.0.0
- **MCP-compatible client** (Claude Code, Cline, etc.)

### Required: Zhipu API Key
You already have this saved in: `/root/.zhipu-config.json`

---

## Installation Methods

### Option A: One-Command Installation (Recommended)

```bash
# Replace YOUR_API_KEY with your actual key
claude mcp add -s user zai-mcp-server --env Z_AI_API_KEY=YOUR_API_KEY -- npx -y "@z_ai/mcp-server@latest"
```

**Steps:**
1. The command will:
   - Download and install the latest version
   - Create MCP configuration
   - Add it to your user settings

2. Verify installation:
   ```bash
   claude mcp list
   ```

---

### Option B: Manual Configuration

**Step 1:** Edit your Claude Code config file
```json
{
  "mcpServers": {
    "zai-mcp-server": {
      "type": "stdio",
      "command": "npx",
      "args": [
        "-y",
        "@z_ai/mcp-server@latest"
      ],
      "env": {
        "Z_AI_API_KEY": "YOUR_API_KEY",
        "Z_AI_MODE": "ZHIPU"
      }
    }
  }
}
```

**Step 2:** Replace `YOUR_API_KEY` with your actual key:
```
"2089f766b091405486ebcecc7bc31e61.qm73eLPh5zQJtcQV"
```

**Step 3:** Save the file at:
- Windows: `%USERPROFILE%\.claude.json` or `%APPDATA%\.claude.json`
- macOS: `~/.claude.json`
- Linux: `~/.claude.json`

**Step 4:** Restart Claude Code (or Cline)

---

## Available Tools

Once installed, you'll have access to these tools:

| Tool Name | Description | Use Case |
|-----------|-------------|----------|
| `ui_to_artifact` | Convert UI screenshots to code, prompts, design specs | Extracting button layouts, form structures |
| `extract_text_from_screenshot` | OCR text extraction from screenshots | Reading code from terminal, extracting text from documents |
| `diagnose_error_screenshot` | Analyze error dialogs, stack traces | Debugging failed deployments, understanding errors |
| `understand_technical_diagram` | Architecture diagrams, flowcharts, UML, ER | Understanding system designs, database schemas |
| `analyze_data_visualization` | Dashboard, charts, graphs | Extracting insights from data visualizations |
| `ui_diff_check` | Compare two UI screenshots | QA testing, design verification |
| `image_analysis` | General image understanding | Analyzing product images, screenshots, photos |
| `video_analysis` | Video scene understanding | Analyzing video content, extracting events |

---

## Usage Examples

### Example 1: Convert UI Design to Code

**You:** "Can you convert this Figma design into React components?"

**MCP Server will:**
- Analyze the image
- Extract component structure
- Generate React code with proper styling
- Suggest component libraries

---

### Example 2: Extract Code from Screenshot

**You:** "What's in this screenshot of the error?"

**MCP Server will:**
- Use OCR to read the error message
- Identify the error type and line number
- Provide suggestions for fixing it

---

### Example 3: Understand Architecture Diagram

**You:** "Can you explain this system architecture diagram?"

**MCP Server will:**
- Analyze the diagram structure
- Explain data flow between components
- Identify patterns and suggest optimizations

---

## How It Works

### Client-Server Communication

1. **You send request** to Claude Code:
   ```
   "Can you analyze this image?"
   ```

2. **Claude Code** checks if MCP tool is available:
   ```
   Does "image_analysis" match the request?
   ```

3. **Claude Code** sends image to MCP Server:
   ```
   POST to MCP Server with image data
   ```

4. **MCP Server** processes with Zhipu GLM-4.6V:
   - Analyzes image
   - Returns structured response
   - Extracts text, detects objects, understands context

5. **Response flows back** to you

---

## Configuration Options

### Environment Variables

| Variable | Value | Description |
|----------|-------|-------------|
| `Z_AI_API_KEY` | Your API key | Required for authentication |
| `Z_AI_MODE` | `ZHIPU` | Use Zhipu platform (default) |
| `Z_AI_ENDPOINT` | (Optional) | Custom API endpoint if needed |

---

## Troubleshooting

### Installation Issues

**Issue:** "Cannot install module @z_ai/mcp-server"

**Solution:**
```bash
# Force latest version
npx -y "@z_ai/mcp-server@latest"
```

---

### Configuration Not Working

**Issue:** MCP server not showing up in Claude Code

**Solutions:**
1. Check `~/.claude.json` syntax is correct
2. Verify API key is valid
3. Try restarting Claude Code completely
4. Check MCP server logs if available

---

### API Key Errors

**Issue:** "Authentication failed"

**Solutions:**
1. Verify your API key is correct
2. Check if key has expired
3. Try refreshing the key in Zhipu console

---

## Best Practices

### 1. Security
- ⚠️ Never commit your API key to version control
- 🔒 Store sensitive keys in environment variables only
- 📝 Use config files with restricted permissions

### 2. Usage
- 📊 Use for complex visual tasks
- 🖼️ Not needed for simple image descriptions (native tools work fine)
- 🎯 Save MCP server usage for when it's truly valuable

### 3. Performance
- ⚡ MCP server calls take 1-3 seconds
- 💡 Combine with native tools when possible
- 📱 Test with different image types before relying on it

---

## Quick Start Commands

```bash
# Check if MCP server is installed
claude mcp list

# Verify API key is loaded (check logs)
claude mcp logs

# Test image analysis (once installed)
# Send an image in Claude Code and ask it to analyze
```

---

## Resources

- **Official Docs:** https://open.bigmodel.cn/docs/ai/visual_mcp
- **NPM Package:** https://www.npmjs.com/package/@z_ai/mcp-server
- **Zhipu Console:** https://open.bigmodel.cn/console
- **Model Info:** GLM-4.6V (latest)

---

**Status:** ✅ Ready to install
**Your API Key:** `2089f766b091405486ebcecc7bc31e61.qm73eLPh5zQJtcQV`

---

**Last Updated:** 2026-02-22
