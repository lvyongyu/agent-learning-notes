# 04 · Agent 的四大零件 / The 4 Building Blocks

```
        ┌──────────────────────────────────┐
        │            Agent                  │
        │                                   │
        │   🧠 大脑 (LLM)    ← 思考、决策      │
        │      Brain           think/decide  │
        │                                   │
        │   🛠️ 工具 (Tools)  ← 读写文件/跑命令/ │
        │      Tools           搜索/调用 API   │
        │                                   │
        │   📋 记忆 (Context) ← 记住对话和      │
        │      Memory          已知信息        │
        │                                   │
        │   🎯 目标 (Goal)    ← 你给的任务      │
        │      Goal            your task      │
        └──────────────────────────────────┘
```

## 逐个说 / One by One

| 零件 / Block | 作用 / Role | 没有它会怎样 / Without it |
|--------------|-------------|--------------------------|
| 🧠 **大脑 LLM** | 决定下一步做什么 / decide next step | 不会思考，只是死脚本 / just a dumb script |
| 🛠️ **工具 Tools** | 真正影响世界 / actually do things | 只能空谈 / all talk, no action |
| 📋 **记忆 Context** | 记得前面发生了什么 / remember history | 每步都"失忆" / forgets everything |
| 🎯 **目标 Goal** | 判断任务是否完成 / when to stop | 不知道何时停 / never stops |

> 小知识 / Note：记忆（Context）是有**容量上限**的，太长会被压缩或遗忘 —— 这就是 Agent 有时会"忘事"的原因。
> Context has a **size limit**; when it's too long it gets compressed — that's why Agents sometimes "forget".

➡️ 下一篇 / Next: [术语表](05-glossary.md)
