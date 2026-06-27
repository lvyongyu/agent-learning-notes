# 28 · 上线工程:可观测 / 重试 / 成本控制 / Productionizing an Agent

> 实战篇 · 第 3 篇(全系列大结局)/ Hands-on track · Note 3 (the finale)

[26 篇](26-build-minimal-agent.md) 的小 Agent 能在你电脑上跑。但要给**真实用户**用,还得加一堆"工程保险"。这篇讲从 demo 到产品差的那一截。
The toy Agent from [Note 26](26-build-minimal-agent.md) runs on your laptop. But to serve *real users*, you need engineering rails. This note covers demo → product.

## demo 和产品的差距 / Demo vs Product

```
demo:能跑通一次就行
      "works once" is enough

产品:要 7×24 稳、不超预算、出事能查、坏了能恢复
      24/7 stable, on-budget, debuggable, recoverable
```

## 四大支柱 / Four Pillars

### ① 可观测 Observability —— 出事能查 / See what happened

> Agent 是个"黑盒循环",不记录就**完全不知道它干了啥**。必须把每一步留痕。
> An Agent is a black-box loop; without logs you've *no idea what it did*. Log every step.

```
每次运行都记录 / log every run:
  - 用户输入 / the input
  - 每一圈:想了啥、调了哪个工具、参数、结果
    each loop: thought, tool, args, result
  - 用了多少 token、花了多少钱、多久 / tokens, cost, latency
  - 最终输出 / final output
```

这其实是 [13 篇"留痕可审计"](13-safety.md) 的放大版,也是做 [12 篇评估](12-evaluation.md) 的原料。
This is [Note 13's "logging"](13-safety.md) scaled up, and the raw material for [Note 12 evals](12-evaluation.md).

### ② 可靠性 Reliability —— 坏了能扛 / Survive failures

> 工具会超时、模型会偶发报错、网络会抖。**别一出错就崩**,要能重试、能兜底。
> Tools time out, the model errors, networks flake. *Don't crash on the first error* — retry & fall back.

| 招 / Tactic | 做法 / How |
|-------------|------------|
| 🔁 **重试 Retry** | 失败了等一下再试(指数退避)/ retry with backoff |
| ⏱️ **超时 Timeout** | 工具卡住就掐掉,别无限等 / cut off stuck tools |
| 🛟 **兜底 Fallback** | 实在不行给个保底回复 / a safe default reply |
| 🚧 **熔断 Circuit-break** | 某工具一直挂就暂时停用 / disable a failing tool |
| 🔒 **循环上限** | [26 篇](26-build-minimal-agent.md) 的"最多转 N 圈" / cap the loops |

### ③ 成本控制 Cost —— 不烧钱 / Don't burn money

> Agent 每转一圈都在花 [token](07-context-memory.md)。一个失控的循环能瞬间烧掉很多钱。
> Every loop spends [tokens](07-context-memory.md). A runaway loop can torch money fast.

| 招 / Tactic | 做法 / How |
|-------------|------------|
| 🧠 **挑对模型** | 简单任务用小/便宜模型,难的才上大模型 / cheap model for easy tasks |
| 💾 **缓存 Caching** | 重复的提示词/结果缓存起来,不重算 / cache repeated prompts |
| ✂️ **精简上下文** | 历史太长就压缩(见 [07](07-context-memory.md))/ compact history |
| 📊 **设预算上限** | 单次请求设 token/费用上限,超了就停 / cap per-request budget |
| 🚪 **能不用 Agent 就别用** | 简单问题直接答,别启动整套循环 / skip the loop when overkill |

### ④ 安全与质量 Safety & Quality —— 不出格 / Stay in bounds

> 上线前要有"护栏"挡住有害输入/输出,还要持续用 [评估集](12-evaluation.md) 盯着质量别下滑。
> Add guardrails for bad input/output, and keep watching quality with [evals](12-evaluation.md).

```
输入端:挡住恶意/注入(见 13 篇)
        block malicious / injected input
输出端:过滤有害内容、检查格式
        filter harmful output, check format
持续:  上线后定期重跑 Eval,模型/提示词改动后看分数
        re-run evals regularly & after changes
```

## 一张上线检查表 / A Go-Live Checklist

```
□ 每一步都有日志吗?(可观测)
□ 工具失败会重试/兜底吗?(可靠)
□ 有循环上限和超时吗?(可靠)
□ 设了成本/token 上限吗?(成本)
□ 危险操作要人确认吗?(安全)
□ 有一套 Eval 在盯质量吗?(质量)
□ 上线后能监控/告警吗?(运维)
```

## 🏁 全 28 篇,完结 / The Complete Series

```
理解原理(1阶段)         深入(2阶段)              实战(3阶段)
01-05 入门              16-19 设计模式            26 动手建 Agent
06-10 核心              20-22 提示词工程          27 多模态
11-13 进阶              23-25 底层原理            28 上线工程(本篇)
14-15 扩展
```

> 一句话收束整套笔记 / The one-line wrap-up:
> **Agent = [模型] + [工具] + [循环];把它做好 = 理解模型的长短板,再用工具、记忆、提示词、模式、工程,一层层把它包装成一个可靠的系统。**
> Agent = [model] + [tools] + [loop]; doing it well = understand the model's strengths & limits, then wrap it — with tools, memory, prompts, patterns, and engineering — into a reliable system.

恭喜你走完全程!🎉 从"Agent 是什么",到能看懂代码、理解模型脾气、知道怎么上线。
Congratulations on finishing! 🎉 From "what is an Agent" to reading the code, understanding the model, and shipping it.

➡️ 回到 / Back to: [README 目录](../README.md)
