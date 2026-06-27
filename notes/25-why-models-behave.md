# 25 · 为什么模型有这些"脾气" / Why Models Behave This Way

> 底层原理篇 · 第 3 篇(全系列收尾)/ Under-the-Hood track · Note 3 (grand finale)

学完 [训练](23-training.md) 和 [采样](24-sampling.md),很多"怪现象"其实都能解释了。这篇把它们串起来——理解了脾气,就知道怎么对付。
After [training](23-training.md) and [sampling](24-sampling.md), the "quirks" all make sense. This note connects them — understand the temperament, and you know how to handle it.

## 用一张表解释所有"怪现象" / One Table Explains the Quirks

| 现象 / Quirk | 根因 / Root cause | 对策 / What to do |
|--------------|-------------------|-------------------|
| 会 [一本正经地编](10-pitfalls.md) | 目标是"接得像",不是"说真话" / trained to be *plausible*, not *truthful* | 给 [工具](06-tools.md)/[RAG](14-rag.md),要出处 |
| 不知道最新消息 | 知识停在 [训练截止日](23-training.md) / frozen at cutoff | 用工具联网、喂资料 |
| 同一问题答不一样 | [温度](24-sampling.md) 带随机性 / sampling randomness | 要稳就把温度调 0 |
| 聊久了 [忘事](07-context-memory.md) | [上下文窗口](07-context-memory.md) 有上限 / finite window | 写文件、精简对话 |
| 数学/计数偶尔翻车 | 它"算"是靠语言模式,不是真计算 / pattern, not real math | 让它 [分步想](16-chain-of-thought.md) 或调计算工具 |
| 太顺着你说(讨好) | [RLHF](23-training.md) 偏好"让人满意" / aligned to please | 明确要它"指出我的错" |
| 换个说法结果差很多 | 对提示词措辞敏感 / sensitive to wording | [好好写提示词](22-prompt-tips.md) |

> 看出规律没?**几乎每个"毛病"都源于它的本质:一个按概率预测下一个词的系统。** 不是 bug,是它的工作原理。
> Spot the pattern? *Almost every "flaw" stems from its nature: a system that predicts the next token by probability.* Not bugs — how it works.

## 模型不是什么 / What a Model Is NOT

```
❌ 不是一个数据库     → 它不"查"事实,是"生成"听起来对的话
   not a database       it generates, doesn't look up

❌ 不是一个计算器     → 算数靠模式匹配,会错
   not a calculator     math is pattern-matched, can slip

❌ 不会真的"懂"或"想" → 没有意图、没有信念,只有概率
   doesn't truly think   no intent or beliefs, just probabilities

✅ 它是:一个超强的"下一个词预测器"
   it IS: an extremely good next-token predictor
```

理解这一条,前面 24 篇的所有设计——[工具](06-tools.md)、[记忆管理](07-context-memory.md)、[反思](18-reflection.md)、[RAG](14-rag.md)——本质上都是在**扬长补短**:放大它的语言能力,补上它不会算、会忘、会编的短板。
Grasp this and all 24 prior designs — [tools](06-tools.md), [memory](07-context-memory.md), [reflection](18-reflection.md), [RAG](14-rag.md) — are really about *amplifying its strengths and patching its weaknesses*.

## 🎓 第二阶段完结 / End of Stage Two

```
入门 01-05   核心 06-10   进阶 11-13   扩展 14-15
basics       core         advanced     extensions
模式 16-19   提示词 20-22  原理 23-25
patterns     prompting    under-the-hood
```

你已经从"Agent 是什么",一路走到了"模型为什么会这样"。最后一站(26–28)是实战:动手建、多模态、上线。
You've gone from "what is an Agent" to "why the model behaves like this". The last stop (26–28) is hands-on: build, multimodal, ship.

> 最后一句心法 / The final mindset:
> **Agent 工程的本质,就是"知道模型擅长什么、不擅长什么,然后用工具、记忆、提示词、流程把它包装成一个靠谱的系统"。**
> Agent engineering is: *know what the model is good and bad at, then wrap it with tools, memory, prompts, and process into a reliable system.*

恭喜你学完整套 🎉 接下来——去读真实的 Agent 代码、自己搭一个、或者用这些概念反过来观察你正在用的 Claude Code。
Congrats on finishing the whole thing 🎉 Next — read real Agent code, build one, or use these ideas to watch the Claude Code you're using.

➡️ 下一篇 / Next: [动手建一个最小 Agent](26-build-minimal-agent.md)
