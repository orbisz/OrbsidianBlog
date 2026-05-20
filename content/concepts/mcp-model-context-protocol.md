---
title: MCP (Model Context Protocol)
category: concepts
tags: [AI, AI-Agent, MCP, protocol]
sources: ["F:/blog/my-blog/blogs/AI/MCP.md"]
summary: MCP（模型上下文协议）是规范 LLM 与外部工具/系统集成的开放协议，基于 SSE 数据传输和 JSON-RPC 2.0 消息格式，实现 Agent 开发与工具开发的解耦。
created: 2026-05-20
updated: 2026-05-20
base_confidence: 0.70
lifecycle: draft
lifecycle_changed: 2026-05-20
tier: supporting
provenance:
  extracted: 0.75
  inferred: 0.20
  ambiguous: 0.05
---

# MCP (Model Context Protocol)

MCP 是规范应用程序向大语言模型提供上下文的开放协议，本质上是 MCP Client 和 MCP Server 之间的通信协议。

## 核心组件

- **MCP Client**: 发送请求/接收响应，集成在 MCP Host 中
- **MCP Server**: 处理请求并返回上下文数据（如高德地图、GitHub MCP 工具）
- **MCP Host**: 协议执行者，接受用户问题 → 选择工具 → 构建参数 → 调用 Server → 解析结果

## MCP 解决的核心问题

1. **统一接口上下文**: 有了统一协议，各平台 AI 客户端内置 MCP Client，只需将接口封装成 MCP Server 即可接入 ^[inferred]
2. **Agent 开发与工具开发解耦**: 工具按 MCP Server 标准发布，Agent 直接调用，类似 Type-C 统一充电接口 ^[inferred]

## 技术原理

### SSE (Server-Sent Events) — 数据传输方式

基于 HTTP 的长连接技术，服务端通过 `text/event-stream` 响应持续推送数据。

**协议格式**: 固定四种字段 `data` | `id` | `event` | `retry`

**实现方式**:
- Spring MVC: `SseEmitter` 同步阻塞模式
- Spring WebFlux: `Flux<ServerSentEvent<String>>` 响应式模式

### JSON-RPC 2.0 — 消息格式

无状态、轻量级远程过程调用协议，定义四字段消息结构：
- `jsonrpc`: 协议版本
- `method`: 要执行的方法名
- `params`: 入参
- `id`: 请求匹配符

### MCP 协议 — 通信协议

在 SSE + JSON-RPC 2.0 之上定义完整生命周期：

**两通道**:
- SSE 长连接（服务端 → 客户端推送）
- HTTP POST（客户端 → 服务端请求）

**四步骤**:
1. 连接: 发送 `GET /sse` 建立 SSE 长连接
2. 获取: 服务端返回 POST 端点 URI
3. 握手: `initialize` → `notifications/initialized`
4. 使用: `tools/list` / `tools/call`
5. 断开: 关闭 SSE 结束会话

## 相关页面
- [[concepts/rag]] — Agent 工具调用与知识检索
- [[concepts/context-engineering]] — Prompt/Context 工程
- [[concepts/agent-context-memory]] — Agent 上下文管理
