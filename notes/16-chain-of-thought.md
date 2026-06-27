# 16 · 思维链 CoT / Chain-of-Thought

> 进阶模式篇 · 第 1 篇 / Patterns track · Note 1

让模型"一步步把推理过程写出来",答案会明显更准。这就是 **思维链 (Chain-of-Thought, CoT)**。
Making the model "show its reasoning step by step" noticeably improves accuracy. That's **Chain-of-Thought (CoT)**.

## 一句话 / In One Sentence

> 别让模型"一口报答案",让它**先想出声、再下结论**——就像数学题写步骤,比直接写答案更不容易错。
> Don't let the model blurt the answer — have it *think out loud first, then conclude* — like showing your work on a math problem.

## 对比:直接答 vs 想出声 / Direct vs Think-aloud

```
❌ 直接答 / Direct:
   问:小明有 3 个苹果,买了 2 袋每袋 4 个,共几个?
   答:9          ← 容易算错 / easy to slip

✅ 想出声 / CoT:
   问:同上
   答:先算买的 = 2×4 = 8
       再加原有 = 8 + 3 = 11
       所以是 11 ✅   ← 拆开后更稳 / steadier
```

## 为什么有效 / Why It Works

> 模型是**一个词一个词往外蹦**的。把推理写出来,等于给自己铺了"垫脚石",后面的词能踩着前面的结论走,而不是凭空猜一个最终答案。
> The model generates *token by token*. Writing the reasoning lays "stepping stones" — later tokens build on earlier conclusions instead of guessing a final answer from thin air.

```
没有 CoT:问题 ──────────────▶ 答案(一步跳过去,容易摔)
With none: question ─────────▶ answer (one big leap, may fall)

有 CoT:  问题 → 想1 → 想2 → 想3 → 答案(踩着走,稳)
With CoT: question → s1 → s2 → s3 → answer (stepping along)
```

## 几种触发方式 / Ways to Trigger It

| 方式 / Way | 怎么做 / How |
|------------|--------------|
| 🗣️ 一句咒语 | 在提示词里加"**让我们一步步想 / think step by step**" |
| 📝 给范例 | 给一个"带推理过程"的例子,模型会照着学(见 [few-shot](20-few-shot.md)) |
| 🧠 内置思考 | 新模型自带"思考"能力,会先在内部推理再作答 |

## 和 Agent 的关系 / Relation to Agents

CoT 是 [思考→行动→观察](01-what-is-an-agent.md) 里**"思考"那一环的放大镜**。下一篇的 ReAct,就是把 CoT 的"想"和工具的"做"**交替**起来。
CoT is a magnifier on the *"Think"* part of the [loop](01-what-is-an-agent.md). The next note, ReAct, *interleaves* CoT's thinking with tool actions.

> 小知识 / Note:CoT 让推理更准,但也更费 [token](07-context-memory.md)(想得多=输出多)。所以是"用成本换准确率"的取舍。
> CoT boosts accuracy but costs more [tokens](07-context-memory.md) (more thinking = more output) — a cost-for-accuracy trade-off.

➡️ 下一篇 / Next: [ReAct 详解](17-react.md)
