# 01 · Agent 是什么 / What Is an Agent

## 最核心的一句话 / The Core Idea

Agent 的本质就是一个**循环（loop）**：它一直转圈，直到任务完成。
At its core, an Agent is just a **loop** that keeps running until the task is done.

```
   ┌─────────────────────────────────────┐
   │                                     │
   ▼                                     │
[ 想一想 ]  →  [ 动手做 ]  →  [ 看结果 ]──┘
  思考          调用工具       观察反馈
 (Think)       (Act)         (Observe)
```

这就是大名鼎鼎的 **「思考 → 行动 → 观察」循环**。
This is the famous **Think → Act → Observe loop**.

| 阶段 / Stage | 在做什么 / What happens |
|--------------|------------------------|
| 🧠 思考 Think | 大模型决定「下一步该干嘛」/ The LLM decides the next step |
| 🛠️ 行动 Act | 调用一个工具（读文件、跑命令…）/ Call a tool (read a file, run a command…) |
| 👀 观察 Observe | 看工具返回了什么，作为下一轮的输入 / Read the tool's result, feed it back |

## 为什么要循环？ / Why a Loop?

因为真实任务**没法一步到位**。就像人做事：做一点 → 看效果 → 再决定下一步。
Because real tasks can't be done in one shot. Like a human: do a bit → check → decide the next move.

> 关键点 / Key point：每转一圈，Agent 都会**重新思考**，而不是一开始就把所有步骤写死。
> Each loop, the Agent **re-thinks** — it doesn't hard-code all steps upfront.

➡️ 下一篇 / Next: [Agent vs 普通聊天](02-agent-vs-chat.md)
