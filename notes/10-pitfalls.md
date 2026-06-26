# 10 · 新手常见误区 / Common Beginner Pitfalls

学到这里，把最容易踩的坑和"它到底有多聪明"理清楚，避免对 Agent 有错误期待。
Now let's clear up the easy traps and "how smart is it really", so you don't get the wrong expectations.

## 误区清单 / The Myth List

| 你以为 / You think | 实际上 / Reality |
|--------------------|------------------|
| 它真的"懂"了我的意思 | 它在**预测下一个最可能的词**，不是真理解 / it *predicts the next likely token*, not true understanding |
| 它说的都是对的 | 它会**一本正经地编**（叫"幻觉"）/ it can confidently make things up ("hallucination") |
| 它记得我们之前所有对话 | 超出 [窗口](07-context-memory.md) 就忘 / it forgets past the context window |
| 它能自己上网/读文件 | 没给 [工具](06-tools.md) 它啥也干不了 / no tools = it can only talk |
| 它越大就越不会错 | 更强 ≠ 不会错，仍要**你来验证** / stronger ≠ infallible, still verify |

## 什么是"幻觉" / What Is "Hallucination"

> 幻觉 = 模型**编出听起来很真、其实是假**的内容。比如编一个不存在的函数名、假的 API、错的引用。
> Hallucination = the model produces *plausible-sounding but false* content — a fake function name, a non-existent API, a wrong citation.

```
为什么会这样? / Why?

模型的目标是"接一个最像样的下文"，
而不是"说真话"。
The model aims to continue text *plausibly*,
not to be *truthful*.

→ 所以不确定时，它也可能硬接一个
→ So when unsure, it may still confidently fill in
```

**怎么防 / How to defend:**
- ✅ 让它**给出处**、能验证 / ask for sources you can check
- ✅ 关键结果**自己跑一遍/对一遍** / run or double-check critical results yourself
- ✅ 给它真实资料([RAG](05-glossary.md)),少靠它"记得" / feed it real data instead of trusting memory

## 一句话心法 / The Mindset

> 把 Agent 当成一个**很能干、但偶尔会自信地犯错的实习生**：
> 给清楚的任务、给工具、给资料，然后**验收结果**。
> Treat the Agent like a *capable intern who sometimes confidently errs*:
> give clear tasks, tools, and data — then *check the work*.

## 回顾:你已经学完的地图 / Recap: The Map You've Learned

```
01 是什么(循环) → 02 vs 聊天 → 03 修 bug 例子 → 04 四大零件
                                                      │
05 术语表  06 工具  07 记忆  08 系统提示词  09 多 Agent  10 误区(本篇)
```

恭喜!你已经把 Agent 的核心拼图凑齐了 🎉
Congrats — you've assembled the core picture of how Agents work! 🎉

➡️ 回到 / Back to: [README 目录](../README.md)
