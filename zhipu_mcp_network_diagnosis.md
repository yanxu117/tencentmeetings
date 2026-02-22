# Zhipu MCP 网络连接诊断报告

**诊断日期：** 2026-02-22
**诊断者：** Yanxu11 (AI Assistant)

---

## 诊断结果总览

### ✅ 网络连接测试

| 测试项 | 结果 | 详情 |
|--------|------|------|
| DNS 解析 | ✅ 成功 | open.bigmodel.cn → 129.227.65.212 |
| Ping 测试 | ✅ 成功 | 平均延迟 2.10 ms，无丢包 |
| HTTP 连接 | ✅ 成功 | HTTP 200 OK |

### ❌ MCP 连接测试

| 测试项 | 结果 | 详情 |
|--------|------|------|
| Web Search MCP | ❌ 失败 | Accept header 错误 |
| 错误信息 | Header 格式不正确 | 必须同时包含 `application/json` 和 `text/event-stream` |

---

## 问题分析

### 主要问题：MCP Server Accept Header 错误

**错误详情：**
```
Accept header must include both application/json and text/event-stream
```

**可能原因：**

1. **客户端兼容性**
   - Zhipu MCP Server 可能对不同客户端有不同的要求
   - 某些客户端可能需要特定的 Accept header 格式

2. **协议版本**
   - MCP 协议可能不同版本有不同的 header 要求
   - 建议查看官方文档确认正确的格式

3. **服务端配置**
   - Zhipu 服务端可能对某些请求类型有特殊要求

---

## 建议解决方案

### 方案 1：使用官方推荐的安装方式

按照 Zhipu 官方文档，使用一键安装命令：

```bash
claude mcp add -s user zai-mcp-server --env Z_AI_API_KEY=YOUR_API_KEY -- npx -y "@z_ai/mcp-server@latest"
```

**原因：**
- 官方命令会自动处理所有 header 配置
- 避免手动配置错误

---

### 方案 2：等待官方修复

如果这是服务端的问题，建议：

1. **查看最新文档**
   - 访问：https://open.bigmodel.cn/docs/ai/visual_mcp
   - 查看是否有更新或修复说明

2. **联系支持**
   - 通过 Zhipu 官方渠道反馈问题

3. **监控修复进度**
   - 关注 Zhipu 社区或更新日志

---

### 方案 3：尝试其他 MCP 服务

如果 Zhipu MCP Server 连接持续有问题，可以考虑：

1. **切换平台模式**
   - 尝试从 `ZHIPU` 切换到 `ZAI`
   - 配置命令：`--env Z_AI_MODE=ZAI`

2. **使用代理或 VPN**
   - 如果网络环境需要特殊配置

---

## 网络环境评估

### 当前状态

- **DNS 解析：** ✅ 正常
- **Ping 延迟：** ✅ 2.10ms（优秀）
- **网络质量：** ✅ 稳定

### 结论

**网络连接完全正常**，问题出在 MCP Server 的 API 协议层面，不是网络问题。

---

## 后续建议

### 对于 Ryan

1. **短期建议**
   - 暂缓安装 Zhipu MCP Server
   - 等待官方更新或修复

2. **中长期方案**
   - 关注 Zhipu 社区动态
   - 考虑使用其他视觉理解服务
   - 继续使用已有的工具（Jina.ai、DuckDuckGo 等）

3. **项目优先级**
   - 继续完善 tencentmeetings 仓库的其他内容
   - 专注于当前可用的稳定工具

---

## 文件位置

```
/root/.openclaw/workspace/tencentmeetings/zhipu_mcp_network_diagnosis.md
```

---

**诊断人：** Yanxu11 (AI Assistant)
**最后更新：** 2026-02-22
**状态：** ✅ 诊断完成
