# 19 · 常见 Agent 模式对比 / Agent Patterns Compared

> 进阶模式篇 · 第 4 篇(收尾)/ Patterns track · Note 4 (wrap-up)

前几篇讲了 [CoT](16-chain-of-thought.md)、[ReAct](17-react.md)、[反思](18-reflection.md)。这篇把常见"套路"放一起对比,帮你以后看到名词不犯怵。
We covered [CoT](16-chain-of-thought.md), [ReAct](17-react.md), [Reflection](18-reflection.md). This note lines up the common patterns so the jargon stops scaring you.

## 五个常见模式 / Five Common Patterns

| 模式 / Pattern | 一句话 / TL;DR | 啥时候用 / When |
|----------------|----------------|-----------------|
| **CoT** | 想出声,不动手 / reason out loud | 纯推理题 / pure reasoning |
| **ReAct** | 边想边用工具 / think + act | 要查/要动手 / look-up & action |
| **Reflection 反思** | 做完自我审查再改 / self-critique | 重要、易错的任务 / high-stakes |
| **Plan-and-Execute 先规划后执行** | 先列完整计划,再一项项做 / plan all, then do | 步骤多的长任务 / long multi-step |
| **Router 路由** | 先判断类型,再分给合适的处理 / classify, then dispatch | 输入种类多 / many input types |

## ReAct vs Plan-and-Execute / 两种"干活节奏"

这俩最容易混。区别在**什么时候做计划**:
These two get confused most. The difference is *when planning happens*:

```
ReAct(走一步看一步)/ step-by-step:
  想→做→看→想→做→看……
  灵活,但可能绕路
  flexible, but may wander

Plan-and-Execute(先画地图再上路)/ plan-first:
  ①先列完整计划 [1][2][3][4]
  ②再埋头一项项执行
  高效有条理,但中途变化时要重规划
  efficient & orderly, but must re-plan if things change
```

> 实战里常常**混用**:先 Plan 出大步骤,每个步骤内部再用 ReAct 灵活应对。这正是 [11 篇规划](11-planning.md) 说的"计划+循环配合"。
> In practice they're *combined*: Plan the big steps, then use ReAct inside each step. Exactly the "plan + loop" combo from [Note 11](11-planning.md).

## Router 路由模式 / The Router Pattern

```
用户输入 / input
     │
     ▼
 ┌────────┐  这是啥类型的问题?
 │ 路由器  │  what kind of request?
 │ Router │
 └────────┘
   /  |  \
  ▼   ▼   ▼
退款  技术  闲聊      ← 各自交给专门的处理/Agent
refund tech chat       each to a specialist
```

> 好处:每个分支可以用**更专、更便宜**的处理方式,不用一个万能大 Agent 包打天下。和 [09 多 Agent](09-multi-agent.md) 思路相通。
> Upside: each branch can be *specialized & cheaper* — no single do-everything Agent. Same spirit as [Note 09](09-multi-agent.md).

## 怎么挑 / How to Choose

```
任务很简单、纯推理        → CoT
要用工具/查实时信息       → ReAct
结果很重要、不能错        → 加 Reflection
步骤多、要有条理          → Plan-and-Execute
输入五花八门             → Router 先分流
```

> 心法 / Mindset:这些不是互斥的"门派",而是**可以叠着用的积木**。真实系统常常是"Router → Plan → 每步 ReAct → 关键处 Reflection"。
> These aren't rival "schools" — they're *stackable building blocks*. Real systems often chain "Router → Plan → ReAct per step → Reflection at key points".

➡️ 下一篇 / Next: [few-shot 与示例的力量](20-few-shot.md)
