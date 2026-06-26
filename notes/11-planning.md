# 11 · Agent 怎么规划长任务 / How an Agent Plans Long Tasks

短任务靠一圈圈 [循环](01-what-is-an-agent.md) 就够了。但"重构整个项目"这种大活,Agent 需要先**规划**,否则会走一半迷路。
Short tasks just need the [loop](01-what-is-an-agent.md). But a big job like "refactor the whole project" needs *planning first*, or the Agent gets lost halfway.

## 为什么光靠循环不够 / Why the Loop Alone Isn't Enough

```
没有计划 / No plan:
做一步 → 做一步 → 做一步 → ……走着走着忘了大目标
step → step → step → … loses sight of the big goal

有计划 / With a plan:
先列清单 → 一项项打勾 → 始终知道"还剩啥"
make a list → check items off → always knows what's left
```

> 大任务里,Agent 的记忆 [窗口](07-context-memory.md) 装不下所有细节。一份**写下来的计划**就是它的"外部记忆"。
> In a big task, the Agent's [context window](07-context-memory.md) can't hold every detail. A *written plan* is its "external memory".

## 三种常见规划方式 / Three Common Planning Styles

| 方式 / Style | 怎么做 / How | 适合 / Good for |
|--------------|--------------|-----------------|
| 📋 **待办清单 / To-do list** | 先拆成有序步骤,做完打勾 / split into ordered steps, tick them off | 步骤清楚的任务 / clear multi-step work |
| 🌲 **先粗后细 / Decompose** | 大目标→子目标→具体动作,逐层展开 / goal → subgoals → actions | 大而模糊的任务 / big fuzzy goals |
| 🔄 **边做边改 / Re-plan** | 发现计划不对,就改计划再继续 / revise the plan when reality differs | 充满未知的任务 / lots of unknowns |

## 计划 + 循环 怎么配合 / How Plan and Loop Work Together

```
            ┌─────────────┐
            │  先做计划     │  ① 拆步骤、列清单
            │  Make a plan │     break it down
            └─────────────┘
                   │
                   ▼
        ┌──────────────────────┐
        │  按清单一项项执行       │  ② 每一项 = 一轮
        │  do items one by one  │     思考→行动→观察
        └──────────────────────┘
                   │
          每做完一项就回头看：
          after each item, check back:
                   │
         ┌─────────┴─────────┐
         ▼                   ▼
   计划还对吗?           全做完了?
   plan still right?     all done?
   不对 → 改计划          是 → 结束
   no → re-plan          yes → finish
```

## 一个例子 / An Example

任务:**"把项目里所有 `var` 改成 `let`"**
Task: *"Replace every `var` with `let` in the project."*

```
计划 / Plan:
  [ ] 1. 找出所有用了 var 的文件
  [ ] 2. 逐个文件修改
  [ ] 3. 跑测试确认没改坏

执行 / Execute:
  ✅ 1. 搜到 8 个文件        ← 工具:搜索
  ✅ 2. 改完 8 个文件        ← 工具:编辑(循环 8 次)
  ✅ 3. 测试通过            ← 工具:跑测试
→ 清单清空,任务完成 / list empty, done
```

> 小知识 / Note:你在 Claude Code 里看到的 **todo 清单 / 计划模式 (Plan Mode)**,就是这种"先规划再执行"的体现。
> The **todo list / Plan Mode** you see in Claude Code is exactly this "plan before doing" idea.

➡️ 下一篇 / Next: [怎么评估一个 Agent](12-evaluation.md)
