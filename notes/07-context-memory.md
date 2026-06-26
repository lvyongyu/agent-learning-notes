# 07 · 上下文与记忆 / Context & Memory

为什么 Agent 聊久了会"忘事"?因为它的记忆有**物理上限**。这一篇讲清楚记忆是怎么回事。
Why do Agents "forget" after a long chat? Because their memory has a *hard limit*. This note explains how memory actually works.

## 关键真相 / The Key Truth

> LLM **没有**长期记忆。它不会"记住"上次和你聊了啥。
> An LLM has **no** long-term memory. It doesn't "remember" your last chat.

那它为什么看起来记得?因为**每一轮，都会把整段对话重新发给它一遍**。
So why does it seem to remember? Because **every turn, the whole conversation is re-sent to it.**

```
第 3 轮时，模型收到的其实是这一整包：
On turn 3, the model actually receives this whole bundle:

┌─────────────────────────────┐
│ 系统提示词 / System prompt    │  ← 规则、角色
│ 你的第 1 句 / Your msg 1      │
│ 模型的回答 1 / Reply 1        │
│ 工具结果 1 / Tool result 1    │
│ 你的第 2 句 / Your msg 2      │
│ ……                          │
│ 你的第 3 句 / Your msg 3      │  ← 新的
└─────────────────────────────┘
         ↑
   这一整包 = 上下文 (Context)
   This whole bundle = the Context
```

所以"记忆"其实是**每次都把历史重新喂进去**装出来的。
So "memory" is faked by *re-feeding the whole history every time.*

## 上下文窗口 = 记忆的容量 / Context Window = Memory Capacity

这个"包"装不下无限内容，它有上限，按 **token（词元）** 算。
That bundle can't be infinite — it has a limit, measured in **tokens**.

| 概念 / Term | 解释 / Meaning |
|-------------|----------------|
| Token 词元 | 文本切成的小块，约等于 ¾ 个英文单词 / a text chunk, ~¾ of an English word |
| Context Window 上下文窗口 | 一次最多能装多少 token（如 20 万）/ max tokens per bundle (e.g. 200K) |
| 装满了会怎样 | 旧内容被**压缩或丢弃** → 这就是"忘事" / old stuff gets *compressed or dropped* → "forgetting" |

## 为什么会"忘事" / Why It "Forgets"

```
对话越来越长……
Conversation grows…

[█████████████████████] 窗口满了 / window full
        │
        ▼
把前面的旧对话压成一段摘要 / compress old turns into a summary
        │
        ▼
细节丢了，只剩大意 → "你刚才说的那个文件名我不记得了"
Details lost, only gist kept → "I forget the exact filename you mentioned"
```

## 怎么缓解 / How to Cope

| 办法 / Tactic | 说明 / Note |
|---------------|-------------|
| 📝 写进文件/记忆 | 重要信息存到外部（文件、数据库），别只靠对话 / save to files, don't rely on chat |
| 🔍 RAG 检索 | 需要时再去查资料，而不是全塞进窗口 / look it up when needed (see [glossary](05-glossary.md)) |
| ✂️ 精简对话 | 长任务里及时总结、丢掉没用的 / summarize & trim long sessions |

> 小知识 / Note：Claude Code 有 `/clear`（清空对话）和长对话**自动压缩**机制，本质都是在管理这个窗口。
> Claude Code's `/clear` and auto-compaction are both ways of managing this window.

➡️ 下一篇 / Next: [系统提示词](08-system-prompt.md)
