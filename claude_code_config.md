# Claude Code 配置指南

**创建日期：** 2026-02-22
**目的：** 配置 Zhipu MCP Server 到 Claude Code

---

## 检查结果

**当前状态：** ❌ Claude Code 配置文件不存在

检查位置：
- `~/.claude.json` - ❌ 不存在
- `%APPDATA%\.claude.json` - ❌ 不存在
- `$HOME/.claude.json` - ❌ 不存在

---

## 配置步骤

### 步骤 1：查找配置文件

**Windows:**
```powershell
# Claude Code 默认位置
$claudercPath = "$env:APPDATA\Claude"

# 检查文件是否存在
if (Test-Path $claudercPath\claude.json) {
    Write-Host "配置文件找到：$claudercPath\claude.json"
} else {
    Write-Host "配置文件不存在，需要创建"
}
```

**macOS:**
```bash
# Claude Code 默认位置
claudercPath="$HOME/.claude.json"

# 检查文件是否存在
if [ -f "$claudercPath/claude.json" ]; then
    echo "配置文件找到：$claudercPath/claude.json"
else
    echo "配置文件不存在，需要创建"
fi
```

**Linux:**
```bash
# Claude Code 默认位置
claudercPath="$HOME/.claude.json"

# 检查文件是否存在
if [ -f "$claudercPath/claude.json" ]; then
    echo "配置文件找到：$claudercPath/claude.json"
else
    echo "配置文件不存在，需要创建"
fi
```

---

### 步骤 2：创建配置文件

**Windows:**
```powershell
# 创建配置目录（如果不存在）
New-Item -ItemType Directory -Force -Path "$env:APPDATA\Claude" -ErrorAction SilentlyContinue | Out-Null

# 创建配置文件
$config = @{
    "mcpServers": @{
        "zai-mcp-server" = @{
            "type" = "stdio"
            "command" = "npx"
            "args" = @("-y", "@z_ai/mcp-server@latest")
            "env" = @{
                "Z_AI_API_KEY" = "YOUR_API_KEY"
                "Z_AI_MODE" = "ZHIPU"
            }
        }
    }
}

# 保存到文件
$config | ConvertTo-Json -Depth 100 | Out-File "$env:APPDATA\Claude\claude.json"
```

**macOS/Linux:**
```bash
# 创建配置目录（如果不存在）
mkdir -p "$HOME/.claude"

# 创建配置文件
cat > "$HOME/.claude.json" << 'EOF'
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
EOF

# 显示结果
echo "配置文件已创建：$HOME/.claude.json"
```

---

### 步骤 3：重启 Claude Code

**重要：** 创建配置文件后，必须重启 Claude Code 才能生效！

**Windows:**
- 关闭 Claude Code 应用
- 重新打开 Claude Code

**macOS/Linux:**
- 重启 Claude Code

---

## 配置文件内容示例

完整的 `~/.claude.json` 配置：

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

**重要：** 将 `YOUR_API_KEY` 替换为你的实际 API key：

```
2089f766b091405486ebcecc7bc31e61.qm73eLPh5zQJtcQV
```

---

## 验证配置

创建配置文件后，运行以下命令验证：

```bash
# 检查配置文件
cat ~/.claude.json

# 检查 npx 是否可用
npx -y "@z_ai/mcp-server@latest" --help

# 测试 MCP 连接
# 在 Claude Code 中输入：hello
```

---

## 集成到仓库

配置文件创建后，上传到你的 tencentmeetings 仓库：

```bash
git add ~/.claude.json
git commit -m "Add Claude Code config for Zhipu MCP"
git push
```

---

## 快速配置脚本

如果你希望一键创建配置，我可以帮你运行：

```bash
# macOS/Linux
cat > ~/.claude.json << 'EOF'
{
  "mcpServers": {
    "zai-mcp-server": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@z_ai/mcp-server@latest"],
      "env": {
        "Z_AI_API_KEY": "2089f766b091405486ebcecc7bc31e61.qm73eLPh5zQJtcQV",
        "Z_AI_MODE": "ZHIPU"
      }
    }
  }
}
EOF
```

---

**创建人：** Yanxu11 (AI Assistant)
**最后更新：** 2026-02-22
