# 15 · MCP:给 Agent 接外部工具的标准协议 / Model Context Protocol

[工具](06-tools.md) 那么好用,但每接一个新工具都要单独写一遍对接代码,太累。**MCP** 就是来统一这件事的。
[Tools](06-tools.md) are great, but wiring up each new one by hand is tedious. **MCP** exists to standardize that.

## 一句话 / In One Sentence

> MCP = 一个**统一的插头标准**,让 Agent 能用同一种方式接上各种外部工具和数据源——就像 USB 之于各种设备。
> MCP is a *universal plug standard* that lets an Agent connect to any external tool or data source the same way — like USB for devices.

## 它解决什么痛点 / The Pain It Solves

```
没有 MCP / Without MCP:
  Agent ──自定义对接──▶ GitHub
  Agent ──自定义对接──▶ 数据库
  Agent ──自定义对接──▶ Slack
  每个都要单独写、各不相同 / each wired differently, N×M mess

有 MCP / With MCP:
  Agent ──┐
          ├─统一接口 MCP─▶ GitHub 的 MCP 服务
          ├─统一接口 MCP─▶ 数据库 的 MCP 服务
          └─统一接口 MCP─▶ Slack 的 MCP 服务
  一种说法,接万物 / one protocol, plug into anything
```

## 两个角色 / Two Roles

| 角色 / Role | 是谁 / Who | 干嘛 / Does |
|-------------|-----------|-------------|
| **MCP 客户端 / Client** | Agent 这一侧(如 Claude Code) | 发起请求:"有哪些工具?帮我调一个" / asks for & calls tools |
| **MCP 服务端 / Server** | 某个工具/数据源的封装 | 对外宣布"我能做这些",并真正执行 / advertises & runs the tools |

```
┌──────────┐   "你有啥工具?"        ┌──────────────┐
│  Agent   │ ──── 列出能力 ───────▶ │  MCP Server   │
│ (Client) │ ◀─── 我有 A/B/C ────── │ (如 GitHub)   │
│          │                       │              │
│          │ ──── "调用 A,参数…" ──▶ │   真正执行    │
│          │ ◀─── 返回结果 ──────── │   actually do │
└──────────┘                       └──────────────┘
```

是不是很眼熟?这正是 [06 篇](06-tools.md) 的工具调用流程,只是用了**标准化的协议**包起来。
Look familiar? It's the tool-call flow from [Note 06](06-tools.md), just wrapped in a *standard protocol*.

## 为什么这是大事 / Why It Matters

| 好处 / Benefit | 说明 / Note |
|----------------|-------------|
| 🔌 **即插即用 / Plug-and-play** | 接新工具不用改 Agent,装个 MCP 服务就行 / add tools without touching the Agent |
| ♻️ **可复用 / Reusable** | 一个 MCP 服务,任何支持 MCP 的 Agent 都能用 / one server, any MCP-aware Agent |
| 🌍 **生态共享 / Shared ecosystem** | 大家都写 MCP 服务,工具越来越多 / a growing shared pool of tools |

> 小知识 / Note:Claude Code 支持连接 **MCP 服务器**——比如接上一个数据库 MCP,我就能直接帮你查数据,而不用你额外写对接代码。
> Claude Code can connect to **MCP servers** — hook up a database MCP and I can query your data directly, no glue code from you.

## 全系列完结 / End of the Series 🎉

```
入门:01-05  →  核心:06-10  →  进阶:11-13  →  扩展:14-15
basics       core           advanced        extensions
```

你现在已经走完一条完整路线:
**循环 → 工具 → 记忆 → 提示词 → 多 Agent → 规划 → 评估 → 安全 → RAG → MCP。**
You've now walked the full path:
**loop → tools → memory → prompts → multi-agent → planning → eval → safety → RAG → MCP.**

下一步最好的学习方式:**带着这些概念,回头观察你正在用的 Claude Code**——它每一个行为,都能对上其中一篇笔记。
Best next step: *re-watch the Claude Code you're using* with these concepts in mind — every behavior maps to one of these notes.

➡️ 回到 / Back to: [README 目录](../README.md)
