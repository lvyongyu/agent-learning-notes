# 02 · Agent vs 普通聊天 / Agent vs Plain Chat

## 区别一张图 / The Difference in One Diagram

```
【普通 LLM 聊天 / Plain Chat】
你 ──提问──▶ 模型 ──直接回答──▶ 你
You ─question▶ Model ─answer──▶ You
            （只会动嘴，不会动手 / talks only, can't act）


【Agent】
你 ──任务──▶ 模型 ──▶ 调用工具 ──▶ 读文件 / 跑命令 / 搜网页
You ─task──▶ Model ─▶ use tool ─▶ read file / run cmd / search web
              ▲                          │
              │   （拿到结果再想 / re-think with results）
              └──────────────────────────┘
```

## 一句话对比 / One-line Comparison

| | 普通聊天 / Plain Chat | Agent |
|---|----------------------|-------|
| 能力 / Ability | 只能「说」/ Only talks | 能「说」也能「做」/ Talks **and** acts |
| 工具 / Tools | ❌ 没有 / none | ✅ 读写文件、跑命令、搜索… |
| 步骤 / Steps | 一次回答 / one reply | 多轮循环 / many loops |
| 会自我修正吗 / Self-correct? | ❌ | ✅ 看到结果不对会重试 / retries on bad results |

> 公式 / Formula：**Agent = 大模型 + 工具 + 循环**
> **Agent = LLM + Tools + Loop**

➡️ 下一篇 / Next: [一个真实例子：修 Bug](03-loop-example.md)
