# 08 · 系统提示词 / The System Prompt

同一个大模型，为什么有的变成"写代码的助手"，有的变成"客服"?区别就在**系统提示词**。
Same LLM — why does one become a "coding assistant" and another a "customer-service bot"? The difference is the **system prompt**.

## 一句话 / In One Sentence

> 系统提示词 = Agent 的**"岗前说明书"**：你是谁、能干嘛、有什么规矩、用什么语气。
> The system prompt is the Agent's *job briefing*: who you are, what you can do, the rules, the tone.

它在对话最开头就放进 [上下文](07-context-memory.md)，而且**每一轮都跟着**，所以全程都管用。
It's placed at the very start of the [context](07-context-memory.md) and *rides along every turn*, so it applies the whole time.

## 三种提示词别搞混 / Don't Confuse the 3 Kinds

```
┌── System Prompt 系统提示词 ──┐   ← 开发者写，设定角色和规则
│  "你是一个严谨的代码助手，      │     written by the developer
│   回答用中文，不要瞎编"        │
└──────────────────────────────┘

┌── User Prompt 用户提示词 ────┐   ← 你写，具体任务
│  "帮我修复登录的 bug"          │     written by you (the user)
└──────────────────────────────┘

┌── Assistant 回复 ────────────┐   ← 模型写，它的输出
│  "好的，我先看看 login.js……"   │     written by the model
└──────────────────────────────┘
```

| 角色 / Role | 谁写的 / Who writes | 作用 / Purpose |
|-------------|---------------------|----------------|
| system | 开发者 / developer | 定角色、定规矩（全程生效）/ set role & rules |
| user | 你 / you | 提具体需求 / the actual request |
| assistant | 模型 / model | 它的回答和工具调用 / its reply & tool calls |

## 一个好的系统提示词通常包含 / A Good System Prompt Usually Has

- 🎭 **角色**：你是谁 / Role — who you are
- ✅ **能力边界**：能做、不能做什么 / What you can & can't do
- 📏 **规则**：格式、语气、禁忌 / Rules — format, tone, don'ts
- 🛠️ **工具说明**：有哪些工具、何时用 / Which tools exist & when to use them

> 小知识 / Note：提示词写得越清楚，Agent 越"听话"。很多"AI 不好用"其实是提示词没写好——这门手艺叫 **提示词工程 (Prompt Engineering)**。
> Clearer prompt = more reliable Agent. A lot of "the AI is bad" is really a weak prompt. This craft is called **Prompt Engineering**.

➡️ 下一篇 / Next: [多 Agent 协作](09-multi-agent.md)
