# 22 · 提示词调优实用技巧 / Prompt Tuning Tips

> 提示词工程篇 · 第 3 篇(收尾)/ Prompt Engineering track · Note 3 (wrap-up)

[08 篇](08-system-prompt.md) 讲了提示词是什么,这篇是**实操手册**:几招立刻能用、让模型更听话的技巧。
[Note 08](08-system-prompt.md) covered what a prompt is; this is the *hands-on cheat sheet* — quick tricks that make the model behave.

## 七招 / Seven Tricks

| # | 技巧 / Trick | 怎么做 / How |
|---|--------------|--------------|
| 1 | 🎯 **说清楚要什么** | 别含糊。"写函数"→"写一个 Python 函数,输入年份,返回是否闰年" |
| 2 | 🧩 **给上下文/背景** | 告诉它读者是谁、用在哪 / who's the audience, where it's used |
| 3 | 📋 **给例子** | 用 [few-shot](20-few-shot.md) 示范期望输出 |
| 4 | 🪜 **让它分步想** | 加"[一步步想](16-chain-of-thought.md)",难题更准 |
| 5 | 🚧 **划边界** | 明说"不要做什么":别瞎编、别超过 100 字 |
| 6 | 🎭 **给角色** | "你是资深医生"→语气和深度都会变 / set a persona |
| 7 | 📐 **定输出格式** | 要 [JSON / 表格 / 列表](21-structured-output.md) 就明说 |

## 一个"烂→好"的改写 / A Bad→Good Rewrite

```
❌ 烂提示词 / Bad:
   "讲讲狗"
   → 模型不知道要多长、给谁看、什么角度

✅ 好提示词 / Good:
   "你是宠物医生。用 3 条要点,向第一次养狗的新手
    解释幼犬日常照顾的注意事项,每条一句话,中文。"
   → 角色✓ 受众✓ 格式✓ 长度✓ 语言✓
```

效果天差地别——**信息量越足,模型猜得越少,结果越稳。**
Night and day — *the more you specify, the less it guesses, the steadier the result.*

## 结构化你的提示词 / Structure It

长提示词建议**分块**,用标题/分隔符,让模型看得清:
For long prompts, *break into blocks* with headers/separators so the model can parse them:

```
# 角色 / Role
你是……

# 任务 / Task
请……

# 规则 / Rules
- 不要……
- 必须……

# 输出格式 / Output
用 JSON,字段为……

# 例子 / Examples
输入… 输出…
```

> 用清晰的分隔(标题、`---`、`<标签>`)能明显降低模型"理解偏差"。这是工业级提示词的标准做法。
> Clear delimiters (headers, `---`, `<tags>`) noticeably reduce misreads — standard practice in production prompts.

## 调试心法 / Debugging Mindset

> 模型没按预期做时,**先别怪模型,先看提示词**:是不是没说清?缺例子?没划边界?
> 改提示词 → 再试 → 比较,就是 [12 篇评估](12-evaluation.md) 的小循环。
> When output is off, *blame the prompt first*: unclear? no examples? no boundaries? Tweak → retry → compare — the mini-loop from [Note 12](12-evaluation.md).

> 小知识 / Note:别指望一次写完美。好提示词都是**试出来、改出来的**——这正是"提示词工程"是门手艺的原因。
> Don't expect a perfect prompt first try. Good prompts are *iterated* — that's why prompt engineering is a craft.

➡️ 下一篇 / Next: [模型是怎么训练出来的](23-training.md)
