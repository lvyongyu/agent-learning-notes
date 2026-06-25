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

---

## 还想学的（TODO）/ Want to Learn Next

- [ ] 工具（Tool）是怎么定义和调用的 / How tools are defined & called
- [ ] 上下文 / 记忆是怎么管理的（为什么 Agent 会"忘事"）/ Context & memory management
- [ ] 多个 Agent 怎么协作分工 / Multi-agent collaboration

---

*笔记作者 / Author: lvyongyu · 学习中 / Work in progress 🚧*
