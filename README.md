# Agent 学习笔记 / Agent Learning Notes

> 从零开始理解 AI Agent（智能体）的工作原理 —— 以 Claude / Claude Code 为例。
> Understanding how AI Agents work from scratch — using Claude / Claude Code as the example.

这是一份**新手向**的学习笔记。每篇都尽量「一图一概念」，中英对照，方便日后查阅和面试复习。
A **beginner-friendly** study log. One diagram per concept, bilingual (CN/EN), handy for review and interviews.

---

## 一句话总结 / In One Sentence

> **Agent = 大模型(LLM) + 工具(Tools) + 循环(Loop)**
> An Agent is a Large Language Model that can **use tools** and **runs in a loop** until the task is done.

```
   ┌─────────────────────────────────────┐
   │                                     │
   ▼                                     │
[ 想一想 ]  →  [ 动手做 ]  →  [ 看结果 ]──┘
  Think          Act           Observe
```

---

## 目录 / Table of Contents

| # | 笔记 / Note | 一句话 / TL;DR |
|---|-------------|----------------|
| 01 | [Agent 是什么](notes/01-what-is-an-agent.md) | 核心是「思考→行动→观察」循环 |
| 02 | [Agent vs 普通聊天](notes/02-agent-vs-chat.md) | 聊天只会动嘴，Agent 会动手 |
| 03 | [一个真实例子：修 Bug](notes/03-loop-example.md) | 看 Agent 一圈圈是怎么转的 |
| 04 | [四大零件](notes/04-components.md) | 大脑 / 工具 / 记忆 / 目标 |
| 05 | [术语表](notes/05-glossary.md) | 中英对照速查 |
| 06 | [工具是怎么调用的](notes/06-tools.md) | 模型只"填表单"，执行靠外部程序 |
| 07 | [上下文与记忆](notes/07-context-memory.md) | 为什么 Agent 会"忘事" |
| 08 | [系统提示词](notes/08-system-prompt.md) | Agent 的"岗前说明书" |
| 09 | [多 Agent 协作](notes/09-multi-agent.md) | 主管 + 工人,拆活分工 |
| 10 | [新手常见误区](notes/10-pitfalls.md) | 幻觉、记忆、验证心法 |

### 进阶篇 / Advanced

| # | 笔记 / Note | 一句话 / TL;DR |
|---|-------------|----------------|
| 11 | [规划长任务](notes/11-planning.md) | 大活先列计划,再一项项打勾 |
| 12 | [怎么评估 Agent](notes/12-evaluation.md) | 看正确性、成本、稳不稳 |
| 13 | [安全与权限](notes/13-safety.md) | 假设它会犯错,提前关小破坏范围 |

### 扩展篇 / Extensions

| # | 笔记 / Note | 一句话 / TL;DR |
|---|-------------|----------------|
| 14 | [RAG 检索增强](notes/14-rag.md) | 回答前先查资料,开卷考试 |
| 15 | [MCP 工具协议](notes/15-mcp.md) | 接外部工具的"USB 标准" |

---

## 还想学的（TODO）/ Want to Learn Next

- [x] 工具（Tool）是怎么定义和调用的 / How tools are defined & called → [06](notes/06-tools.md)
- [x] 上下文 / 记忆是怎么管理的（为什么 Agent 会"忘事"）/ Context & memory management → [07](notes/07-context-memory.md)
- [x] 多个 Agent 怎么协作分工 / Multi-agent collaboration → [09](notes/09-multi-agent.md)
- [x] 工具调用之外:Agent 怎么"规划"长任务 / Planning long tasks → [11](notes/11-planning.md)
- [x] 怎么评估一个 Agent 好不好（Evaluation）/ How to evaluate an Agent → [12](notes/12-evaluation.md)
- [x] 安全与权限:Agent 会不会乱来 / Safety & permissions → [13](notes/13-safety.md)
- [x] RAG 检索增强:怎么让 Agent 查资料再回答 / Retrieval-Augmented Generation → [14](notes/14-rag.md)
- [x] MCP:给 Agent 接外部工具的标准协议 / Model Context Protocol → [15](notes/15-mcp.md)

> 🎉 核心 + 进阶 + 扩展全部完结。下一步:带着这些概念回头观察你正在用的 Claude Code。
> All notes complete. Next step: re-watch the Claude Code you're using with these concepts in mind.

---

*笔记作者 / Author: lvyongyu · 学习中 / Work in progress 🚧*
