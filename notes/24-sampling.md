# 24 · 采样参数:温度等 / Sampling Parameters

> 底层原理篇 · 第 2 篇 / Under-the-Hood track · Note 2

同一个问题,模型有时回答稳如老狗,有时天马行空——这由几个**采样参数**控制。最有名的是"温度"。
Same question, sometimes a steady answer, sometimes wild — controlled by a few **sampling parameters**. The famous one is "temperature".

## 先理解:模型不是"选答案",是"按概率掷骰子" / The Key Idea

> 每生成一个词,模型其实算出了**一堆候选词各自的概率**,然后从中"抽"一个。怎么抽,就是采样参数说了算。
> For each next word, the model computes *probabilities over many candidates*, then *samples* one. How it samples is what these parameters decide.

```
下一个词的候选 / candidates for next word:
  好   ████████ 70%
  不错 ███ 20%
  棒   █ 7%
  紫色 . 0.1%   ← 几乎不可能 / near-impossible
```

## 温度 Temperature:控制"放飞程度" / Creativity Dial

| 温度 / Temp | 效果 / Effect | 适合 / Good for |
|-------------|---------------|-----------------|
| **低(0~0.3)** | 保守,总挑最可能的词,稳定可复现 / safe, picks top words, reproducible | 事实问答、代码、抽取 / facts, code, extraction |
| **中(0.7 左右)** | 平衡 / balanced | 一般对话 / general chat |
| **高(1.0+)** | 放飞,敢选小概率词,有创意但易跑偏 / wild, creative but risky | 写诗、头脑风暴 / poetry, brainstorming |

```
温度低 / low temp:
  "今天天气真" → "好"(几乎每次都一样)

温度高 / high temp:
  "今天天气真" → "好/魔幻/像一首诗"(每次可能不同)
```

> 这就解释了 [10 篇](10-pitfalls.md) 的"同一问题每次答不一样"——温度 > 0 时本来就带随机性。要可复现就把温度调到 0。
> This explains [Note 10](10-pitfalls.md)'s "different answer each time" — temp > 0 is random by design. For reproducibility, set temp to 0.

## 其他几个常见参数 / Other Common Params

| 参数 / Param | 管什么 / Controls |
|--------------|-------------------|
| **Top-p(核采样)** | 只在"累计概率前 p%"的候选里抽,砍掉长尾怪词 / sample only from the top-p mass |
| **Top-k** | 只在概率最高的 k 个里抽 / sample only from top-k candidates |
| **Max tokens** | 最多生成多少词(防止啰嗦/超 [窗口](07-context-memory.md))/ cap output length |
| **Stop 停止词** | 遇到指定字符串就停 / halt when it hits a marker |

## 实战怎么设 / Practical Settings

```
要准确、要稳定(代码/数据/Agent 工具调用):
  温度 ≈ 0,top-p 低
  → 这也是为什么 Agent 干活通常用低温:要可靠,不要发挥
  Agents usually run cool: reliability over flair

要创意、要多样(起名/文案/头脑风暴):
  温度 ↑,top-p ↑
```

> 小知识 / Note:做 Agent 时,绝大多数场景**温度调低**。你要的是"它老老实实按工具结果办事",不是"它发挥想象"。
> When building Agents, keep temperature *low* in most cases — you want it to follow tool results faithfully, not improvise.

➡️ 下一篇 / Next: [为什么模型有这些"脾气"](25-why-models-behave.md)
