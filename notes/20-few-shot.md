# 20 · few-shot 与示例的力量 / Few-shot Prompting

> 提示词工程篇 · 第 1 篇 / Prompt Engineering track · Note 1

想让模型按你要的方式回答,最有效的一招往往不是"解释",而是**给它几个例子**。这叫 few-shot。
The most effective way to get the output you want is often not *explaining* — it's *showing a few examples*. That's few-shot.

## 三个词先分清 / Three Words First

| 叫法 / Name | 给几个例子 / Examples | 例子 / Example |
|-------------|----------------------|----------------|
| **Zero-shot 零样本** | 0 个 | "把这句翻成英文:你好" |
| **One-shot 单样本** | 1 个 | 先给 1 个翻译示范,再让它翻 |
| **Few-shot 少样本** | 几个(2~5) | 给几个示范,它照葫芦画瓢 |

## 为什么例子比解释强 / Why Examples Beat Explanations

> 与其用一大段文字描述"我要什么格式",不如直接**摆几个成品给它看**。模型超擅长"找规律、照着学"。
> Instead of a paragraph describing the format you want, just *show finished samples*. Models are great at spotting patterns and mimicking.

```
❌ 光解释 / Explain only:
   "请提取人名,用 JSON,key 叫 name,要数组……"
   (模型可能理解偏)/ model may misread

✅ 给例子 / Show examples:
   输入:张三和李四去爬山
   输出:["张三","李四"]
   输入:王五一个人在家
   输出:["王五"]
   输入:小明和小红打球     ← 让它接
   输出:?                  ← 它会照格式输出 ["小明","小红"]
```

## 一个对比例子 / A Before/After

任务:**判断评论情绪**
Task: *classify sentiment*

```
Few-shot 提示词 / prompt:
  "好吃极了"   → 正面
  "难吃死了"   → 负面
  "还行吧"     → 中性
  "太棒了!"    →            ← 模型补:正面 ✅

给了三个例子,模型立刻 get 到"只回三选一的标签"
With 3 examples, it instantly gets "answer one of three labels"
```

## 用好 few-shot 的要点 / Tips for Good Few-shot

| 要点 / Tip | 说明 / Why |
|------------|------------|
| 📐 **格式一致** | 例子格式要和你想要的输出**一模一样** / match the exact format you want |
| 🌈 **覆盖多样** | 例子要包含不同情况(正/负/边界)/ cover varied cases incl. edge ones |
| 🎯 **2~5 个够了** | 太多会挤占 [上下文](07-context-memory.md)、变贵 / too many waste context & cost |
| ⚖️ **别偏** | 例子别全是同一类,否则模型会偏 / don't make all examples one class |

> 小知识 / Note:few-shot 也是触发 [思维链 CoT](16-chain-of-thought.md) 的好办法——给的例子里**带上推理过程**,模型就会跟着"想出声"。
> Few-shot is also a great way to trigger [CoT](16-chain-of-thought.md): put the *reasoning* in your examples and the model will think aloud too.

➡️ 下一篇 / Next: [结构化输出](21-structured-output.md)
