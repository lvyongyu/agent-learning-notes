# 09 · 多 Agent 协作 / Multi-Agent Collaboration

一个 Agent 干不过来的大活，可以拆给**好几个 Agent 分工**。这一篇讲它们怎么配合。
For a big job one Agent can't handle, you can split it across **several Agents**. This note shows how they cooperate.

## 为什么要多个 / Why More Than One

| 单个 Agent 的痛点 / Pain | 多 Agent 的解法 / Fix |
|--------------------------|------------------------|
| 记忆窗口装不下整个大项目 | 每个子 Agent 只管自己那块 / each handles one slice |
| 又要写代码又要测试又要查资料，容易乱 | 分工，各做擅长的 / divide by specialty |
| 一条路走到黑 | 多个并行探索，再汇总 / explore in parallel, then merge |

## 最常见的模式:主管 + 工人 / The Boss + Workers Pattern

```
            你 / You
             │ 大任务 / big task
             ▼
        ┌─────────┐
        │ 主 Agent │  ← 拆任务、分派、汇总
        │  Boss    │     split, dispatch, merge
        └─────────┘
         /    |    \
        ▼     ▼     ▼
     ┌────┐ ┌────┐ ┌────┐
     │子A │ │子B │ │子C │  ← 各干一块子任务
     └────┘ └────┘ └────┘     each does a subtask
     查资料   写代码   写测试
     research  code    tests
        \     |     /
         ▼    ▼    ▼
        结果汇总给主 Agent / results back to Boss
             │
             ▼
        整理好回复你 / final answer to you
```

> 子 Agent（Sub-agent）= 主 Agent 临时派出去的"小弟"，它有**自己独立的上下文**，干完把结果交回来。
> A sub-agent is a temp "helper" with its *own separate context*; it does the job and hands back the result.

## 关键好处:省记忆 / The Key Win: Saving Memory

```
主 Agent 不需要看子 Agent 的全部过程，
只需要它的最终结论 ——

The Boss doesn't need the worker's whole process,
only its final conclusion —

子 Agent: 读了 50 个文件、试了 10 种写法……（一大堆细节）
          (50 files read, 10 attempts… tons of detail)
                    │ 只回传 / returns only
                    ▼
          "Bug 在 login.js 第 12 行" ✅
```

这样主 Agent 的 [记忆窗口](07-context-memory.md) 不会被细节撑爆。
This keeps the Boss's [context window](07-context-memory.md) from blowing up on details.

## 几种常见分工方式 / Common Ways to Split

| 方式 / Pattern | 例子 / Example |
|----------------|----------------|
| 按**专长**分 / by skill | 一个查资料、一个写码、一个审查 / researcher, coder, reviewer |
| 按**并行**分 / fan-out | 5 个 Agent 同时搜不同关键词，再汇总 / 5 search in parallel, then merge |
| 按**流水线**分 / pipeline | 草稿 → 校对 → 润色，一棒接一棒 / draft → check → polish |

> 小知识 / Note：Claude Code 里我可以派出 **subagent（子 Agent）** 去并行搜索/审查代码——你看到的"Agent / Task"就是这个。
> In Claude Code I can spawn **subagents** to search or review code in parallel — that's the "Agent / Task" you see.

➡️ 下一篇 / Next: [新手常见误区](10-pitfalls.md)
