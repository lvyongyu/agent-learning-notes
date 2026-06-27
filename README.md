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

> 🎉 以上 01–15 = **第一阶段:理解 Agent 完整原理**。下面 16–25 是第二阶段进阶。
> Notes 01–15 = **Stage One: how an Agent works**. Notes 16–25 below are Stage Two.

### 进阶模式篇 / Patterns（设计套路）

| # | 笔记 / Note | 一句话 / TL;DR |
|---|-------------|----------------|
| 16 | [思维链 CoT](notes/16-chain-of-thought.md) | 让模型想出声,答得更准 |
| 17 | [ReAct 详解](notes/17-react.md) | 边想边用工具,Agent 基本盘 |
| 18 | [反思与自我纠错](notes/18-reflection.md) | 做完自审再改,少出错 |
| 19 | [常见模式对比](notes/19-agent-patterns.md) | CoT/ReAct/反思/规划/路由 怎么选 |

### 提示词工程篇 / Prompt Engineering

| # | 笔记 / Note | 一句话 / TL;DR |
|---|-------------|----------------|
| 20 | [few-shot 示例](notes/20-few-shot.md) | 给例子比讲道理管用 |
| 21 | [结构化输出](notes/21-structured-output.md) | 让程序能直接读的 JSON |
| 22 | [提示词调优技巧](notes/22-prompt-tips.md) | 七招让模型更听话 |

### 底层原理篇 / Under the Hood

| # | 笔记 / Note | 一句话 / TL;DR |
|---|-------------|----------------|
| 23 | [模型怎么训练出来的](notes/23-training.md) | 预训练→微调→RLHF |
| 24 | [采样参数:温度等](notes/24-sampling.md) | 控制"稳定 vs 放飞" |
| 25 | [为什么模型有这些脾气](notes/25-why-models-behave.md) | 一表解释所有"怪现象"(总收尾) |

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
- [x] 设计模式:CoT / ReAct / 反思 / 路由 / Agent design patterns → [16–19](notes/16-chain-of-thought.md)
- [x] 提示词工程进阶:few-shot / 结构化输出 / 技巧 / Prompt engineering → [20–22](notes/20-few-shot.md)
- [x] 底层原理:训练 / 采样参数 / 模型脾气 / Under the hood → [23–25](notes/23-training.md)
- [ ] (未来 / future) 动手建一个最小 Agent / Build a minimal Agent from code
- [ ] (未来 / future) 多模态:让 Agent 看图听声 / Multimodal agents
- [ ] (未来 / future) 上线工程:可观测、重试、成本控制 / Productionizing agents

> 🎉 **25 篇全部完结**——从"Agent 是什么"到"模型为什么会这样"。
> 下一步:带着这些概念回头观察你正在用的 Claude Code,每个行为都能对上一篇笔记。
> All 25 notes complete — from "what is an Agent" to "why the model behaves this way".

---

*笔记作者 / Author: lvyongyu · 学习中 / Work in progress 🚧*
