# 23 · 模型是怎么训练出来的 / How a Model Is Trained

> 底层原理篇 · 第 1 篇 / Under-the-Hood track · Note 1

Agent 的"[大脑](04-components.md)"是个大模型。它不是写出来的,是**喂海量数据"练"出来的**。这篇讲它怎么诞生。
The Agent's [brain](04-components.md) is an LLM. It isn't coded — it's *trained* on massive data. Here's how it's born.

## 三个阶段 / Three Stages

```
① 预训练 Pre-training
   读海量文本,学会"猜下一个词"
   read a huge pile of text, learn to predict the next word
        │
        ▼
② 微调 Fine-tuning (SFT)
   用"问→好答案"的范例,教它好好回答
   show "question → good answer" pairs, teach it to respond well
        │
        ▼
③ 对齐 RLHF
   用人的偏好打分,教它"什么样的回答更受欢迎"
   use human preference scores to make answers helpful & safe
```

## ① 预训练:学语言 / Pre-training: Learn Language

> 把互联网级别的文本喂进去,目标只有一个:**给前半句,猜下一个词**。猜亿万次后,它"顺带"学会了语法、常识、推理。
> Feed it internet-scale text with one goal: *given the start, predict the next word*. After billions of guesses, it "incidentally" learns grammar, facts, reasoning.

```
"今天天气真___" → 模型学会大概率是"好/不错"
"The sky is ___" → learns it's likely "blue"
```

这一步最贵、最耗算力,练出一个"什么都懂一点、但不太会聊天"的**原始模型**。
This is the costly, compute-heavy step, yielding a *raw model* that knows a lot but doesn't chat well.

## ② 微调:学好好说话 / Fine-tuning: Learn to Respond

> 给它大量**"问题 + 理想回答"**的范例,它学会"哦,被提问时应该这样组织答案",而不是续写一段网页。
> Show it many *"question + ideal answer"* pairs; it learns to *answer* rather than continue a webpage.

这就是为什么同一个底座,能调成助手、客服、代码专家——靠的是不同的微调数据(呼应 [08 系统提示词](08-system-prompt.md) 之外的另一层定制)。
That's how one base becomes an assistant / agent / coder — different fine-tuning data (a layer beneath the [system prompt](08-system-prompt.md)).

## ③ RLHF:学人类喜好 / Align to Human Preference

> 让模型对同一问题给几个答案,**人来排序"哪个更好"**,再用这些偏好训练它。结果:回答更有用、更礼貌、更少说有害内容。
> The model gives several answers; *humans rank which is better*; those preferences train it further. Result: more helpful, polite, and safe.

```
RLHF = Reinforcement Learning from Human Feedback
       从人类反馈中做强化学习
```

这一步也叫**对齐 (Alignment)**——让模型的行为"对齐"人类期望,和 [13 安全篇](13-safety.md) 是一条线。
This is **alignment** — making behavior match human expectations; same thread as [Note 13 on safety](13-safety.md).

> 小知识 / Note:训练好后,模型的知识就**"冻结"在那个时间点**了(叫知识截止日期 / knowledge cutoff)。这就是为什么它不知道最新的事——也是 [RAG](14-rag.md) 和 [工具](06-tools.md) 要补的洞。
> Once trained, knowledge is *frozen* at a point in time (the "knowledge cutoff") — why it doesn't know recent events, and what [RAG](14-rag.md) and [tools](06-tools.md) patch.

➡️ 下一篇 / Next: [采样参数:温度等](24-sampling.md)
