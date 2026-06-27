# 17 · ReAct 详解 / ReAct in Depth

> 进阶模式篇 · 第 2 篇 / Patterns track · Note 2

[术语表](05-glossary.md) 里提过 ReAct,这篇讲透。它是当今绝大多数 Agent 的"基本盘"。
We mentioned ReAct in the [glossary](05-glossary.md); here's the full story. It's the backbone of most Agents today.

## 一句话 / In One Sentence

> ReAct = **Rea**soning + **Act**ing:把"[想出声](16-chain-of-thought.md)"和"[调工具](06-tools.md)"**交替进行**,边想边做,边做边想。
> ReAct = **Rea**soning + **Act**ing: *interleave* "thinking aloud" with "calling tools" — think a bit, act a bit, repeat.

其实你早就见过它了——[01 篇](01-what-is-an-agent.md) 的"思考→行动→观察"循环,正式名字就叫 ReAct。
You've already met it — the "Think → Act → Observe" loop from [Note 01](01-what-is-an-agent.md) is formally called ReAct.

## 三个关键词轮流出现 / Three Keywords Take Turns

```
Thought(想):我需要先查天气
   │
Action(做):调用 weather(city="北京")
   │
Observation(看):返回 "晴,28°C"
   │
Thought(想):有了数据,可以回答了
   │
Action(做):给出最终答案
```

> 关键:**每次"想"都基于上一次"看"到的真实结果**,所以不会脱离现实瞎编(比纯 [CoT](16-chain-of-thought.md) 更靠谱)。
> Key: each *Thought* is grounded in the last real *Observation*, so it doesn't drift into fiction (more reliable than pure [CoT](16-chain-of-thought.md)).

## CoT vs ReAct 一图分清 / Tell Them Apart

```
CoT(只想不做)/ think only:
   想 → 想 → 想 → 答
   全靠脑补,碰不到真实世界
   all in-head, never touches reality

ReAct(想+做)/ think + act:
   想 → 做 → 看 → 想 → 做 → 看 → 答
   每步都能拿真实结果来校正
   each step corrected by real results
```

| 对比 / Aspect | CoT | ReAct |
|---------------|-----|-------|
| 用工具吗 / Tools? | ❌ 不用 | ✅ 用 |
| 能拿实时信息吗 / Live data? | ❌ 不能 | ✅ 能 |
| 适合 / Best for | 纯推理题 / pure reasoning | 要查/要动手的任务 / look-up & action |

## 一个完整例子 / A Full Example

任务:**"现在北京适合穿什么?"**
Task: *"What should I wear in Beijing right now?"*

```
Thought:我不知道当前天气,得查
Action: weather(city="北京")
Observation:晴,3°C,有风
Thought:3°C 还有风,挺冷的
Action: 回答
最终:建议穿厚外套加围巾 🧣
```

没有工具,模型只能瞎猜温度;有了 ReAct,它**先查到真实数据再建议**。
Without tools the model would guess the temperature; with ReAct it *fetches real data first*.

> 小知识 / Note:Claude Code 就是个 ReAct Agent——你看到我"先说要干嘛、再调工具、再根据结果继续",就是 Thought→Action→Observation 在转。
> Claude Code *is* a ReAct Agent — me saying what I'll do, calling a tool, then continuing from the result is exactly Thought→Action→Observation.

➡️ 下一篇 / Next: [反思与自我纠错](18-reflection.md)
