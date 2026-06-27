# 21 · 结构化输出 / Structured Output

> 提示词工程篇 · 第 2 篇 / Prompt Engineering track · Note 2

让模型输出**程序能直接读的格式**(通常是 JSON),而不是一段大白话——这是把 Agent 接进真实系统的关键。
Make the model output a format *programs can parse directly* (usually JSON), not prose — key to wiring an Agent into real systems.

## 为什么需要 / Why

```
人看的输出 / for humans:
  "这条评论是正面的,置信度大概九成"
  → 程序很难自动处理 / hard for code to use

机器读的输出 / for machines:
  { "sentiment": "正面", "confidence": 0.9 }
  → 程序一行就取到值 / code reads it in one line
```

> Agent 的结果常常要**交给下一段程序**(存数据库、触发动作)。结构化输出就是它们之间的"标准接口"。
> An Agent's result often feeds the *next program* (save to DB, trigger an action). Structured output is the standard interface between them.

## 它和工具调用是亲戚 / Cousin of Tool Calls

还记得 [06 篇](06-tools.md) 说"模型只是填一张符合 schema 的表单"吗?结构化输出是同一个机制:**你定义好格式,模型按格式填。**
Remember [Note 06](06-tools.md) — "the model just fills a form matching a schema"? Structured output is the same mechanism: *you define the shape, the model fills it.*

```
你给的格式约定 / your schema:
  {
    "name":   字符串,
    "age":    数字,
    "vip":    true/false
  }

模型按格式输出 / model fills it:
  { "name": "张三", "age": 30, "vip": true }
```

## 三种实现强度 / Three Levels of Strength

| 方式 / Way | 怎么做 / How | 可靠度 / Reliability |
|------------|--------------|---------------------|
| 🗣️ **嘴上要求** | 提示词写"请用 JSON 回答" | 一般,偶尔跑偏 / okay, sometimes drifts |
| 📋 **给例子** | 配 [few-shot](20-few-shot.md) 示范格式 | 较好 / better |
| 🔒 **强制约束** | 用 schema 强制,不合格就重试 | 最稳 / strongest |

> 最稳的做法是**第三种**:在工具/接口层校验,格式不对就让模型重答,直到合格。很多平台(含 Claude 的工具调用)就是这么保证的。
> The strongest is #3: validate at the tool layer and make the model retry until valid. That's how many platforms (incl. Claude's tool calls) guarantee it.

## 常见坑 / Common Gotchas

```
⚠️ 模型在 JSON 前后加废话:
   "好的!这是结果:{...} 希望有帮助"
   → 程序解析失败 / parse fails
   解法:明确要求"只输出 JSON,不要别的字"
   fix: say "output ONLY the JSON, nothing else"

⚠️ 字段缺失或类型错(age 填成 "三十")
   → 用 schema 校验拦住、重试
   fix: schema validation + retry
```

> 小知识 / Note:结构化输出是 [多 Agent](09-multi-agent.md) 协作的润滑剂——子 Agent 回传**结构化结果**,主 Agent 才能可靠地接着用。
> Structured output is the glue for [multi-agent](09-multi-agent.md) work — workers return *structured results* the boss can reliably consume.

➡️ 下一篇 / Next: [提示词调优实用技巧](22-prompt-tips.md)
