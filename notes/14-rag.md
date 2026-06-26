# 14 · RAG 检索增强 / Retrieval-Augmented Generation

模型 [记不住](07-context-memory.md) 太多东西,也不知道你公司内部的资料。**RAG** 就是让它"先查再答"。
The model can't [remember](07-context-memory.md) much, and doesn't know your private docs. **RAG** lets it *look things up before answering*.

## 一句话 / In One Sentence

> RAG = 回答前,先去**资料库里搜出相关片段**,塞进上下文,再让模型基于这些片段回答。
> RAG = before answering, *search a knowledge base for relevant snippets*, put them in the context, then let the model answer based on them.

就像开卷考试:不靠死记,而是**先翻书找到那一页,再答题**。
Like an open-book exam: don't rely on memory — *find the right page first, then answer.*

## 为什么需要它 / Why We Need It

| 不用 RAG / Without | 用 RAG / With |
|--------------------|----------------|
| 只能答模型"记得"的 / only what the model memorized | 能答最新的、私有的资料 / fresh & private data |
| 容易 [编造](10-pitfalls.md) / prone to hallucination | 有出处,可核对 / grounded, checkable |
| 想更新知识要重训模型 / retrain to update | 改资料库即可 / just update the docs |

## 流程图 / The Flow

```
你的问题 / Your question
   "我们公司的报销上限是多少?"
        │
        ▼
① 去资料库搜相关片段 / search the knowledge base
        │
        ▼
   找到:"差旅报销单次上限 2000 元……"
   found: "travel reimbursement cap: ¥2000…"
        │
        ▼
② 把片段 + 问题一起给模型 / snippet + question → model
        │
        ▼
③ 模型基于片段回答 / model answers from the snippet
   "根据公司规定,上限是 2000 元。"
        │
        ▼
   (可附出处 / can cite the source)
```

## 它是怎么"搜"到相关的 / How It "Finds" Relevant Bits

> 关键不是关键词匹配,而是**按"意思"找**。把文字变成一串数字(叫**向量 / embedding**),意思相近的向量距离也近。
> The trick isn't keyword matching — it's matching by *meaning*. Text is turned into numbers (**embeddings**); similar meanings sit close together.

```
"报销上限"  ─┐
            ├─ 意思相近 → 向量距离近 → 被搜到
"花销额度"  ─┘   close meaning → close vectors → retrieved

"今天天气"  ──── 意思无关 → 距离远 → 不会被搜到
                unrelated → far → ignored
```

存这些向量、并快速找最近的,用的是 **向量数据库 (Vector DB)**。
Storing those vectors and finding the nearest ones is the job of a **vector database**.

## 三步建一个 RAG / Build a RAG in 3 Steps

```
准备阶段(一次)/ Setup (once):
  资料 → 切成小段 → 转成向量 → 存进向量库
  docs → chunk → embed → store

提问阶段(每次)/ Per query:
  问题 → 转向量 → 找最近的几段 → 连同问题给模型
  question → embed → top-k nearest → feed with question
```

> 小知识 / Note:RAG 和 [工具](06-tools.md) 是两条增强路线——工具让 Agent **动手做事**,RAG 让 Agent **查到资料**。真实 Agent 常常两个都用。
> RAG and [tools](06-tools.md) are two augmentation paths — tools let an Agent *act*, RAG lets it *know*. Real Agents often use both.

➡️ 下一篇 / Next: [MCP 工具协议](15-mcp.md)
