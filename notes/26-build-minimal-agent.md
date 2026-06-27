# 26 · 动手建一个最小 Agent / Build a Minimal Agent

> 实战篇 · 第 1 篇 / Hands-on track · Note 1

前 25 篇都在讲原理。这篇用**几十行伪代码**把它落地——你会发现:一个 Agent 的核心,真的就是 [一个循环](01-what-is-an-agent.md)。
The first 25 notes were theory. This one *lands it in ~40 lines* — you'll see an Agent's core really is just [a loop](01-what-is-an-agent.md).

## 先看全貌:5 个零件 / The Big Picture: 5 Parts

```
① 系统提示词  → 告诉模型它是谁、有哪些工具
② 工具清单    → 每个工具:名字+说明+参数+真正执行的函数
③ 对话历史    → 一个不断追加的列表(就是"记忆")
④ 调用模型    → 把历史发给 LLM,拿回它的决定
⑤ 主循环      → 想→(调工具→看结果)→再想……直到给出答案
```

对应的正是 [04 篇的四大零件](04-components.md) + [01 篇的循环](01-what-is-an-agent.md)。
This maps to [the 4 building blocks](04-components.md) + [the loop](01-what-is-an-agent.md).

## ② 定义工具 / Define a Tool

工具 = 给模型看的"说明书" + 真正执行的函数。
A tool = a "spec" the model sees + a real function that runs.

```python
# 真正执行的函数 / the real function
def get_weather(city):
    # 这里真去调天气 API / actually call a weather API
    return f"{city}：晴,3°C"

# 给模型看的说明书 / the spec the model sees (见 06 篇)
weather_tool = {
    "name": "get_weather",
    "description": "查询某城市当前天气 / get a city's current weather",
    "input_schema": {
        "type": "object",
        "properties": {"city": {"type": "string"}},
        "required": ["city"],
    },
}

# 名字 → 函数 的对照表,方便按名字调用
TOOLS = {"get_weather": get_weather}
```

## ⑤ 主循环 / The Main Loop

这是整个 Agent 的心脏——和 [ReAct](17-react.md) 一模一样:
This is the Agent's heart — exactly [ReAct](17-react.md):

```python
def run_agent(user_input):
    # ③ 对话历史 = 记忆 / the conversation history = memory
    messages = [{"role": "user", "content": user_input}]

    while True:                                   # ← 就是这个循环 / the loop
        # ④ 调模型,带上工具清单 / call the LLM with the tools
        reply = call_llm(
            system="你是助手,可以用工具。/ You are an assistant with tools.",
            messages=messages,
            tools=[weather_tool],
        )
        messages.append(reply)                    # 把模型的话记进历史

        # 模型想调工具吗? / did it ask for a tool?
        if reply.wants_tool:
            name = reply.tool_name                 # 例:get_weather
            args = reply.tool_args                 # 例:{"city":"北京"}
            result = TOOLS[name](**args)           # 🛠️ 真正执行 / actually run it
            # 把结果塞回历史,进入下一圈 / feed result back, loop again
            messages.append({"role": "tool", "content": result})
            continue

        # 没调工具 = 它给出最终答案了 / no tool = final answer
        return reply.text
```

> 看懂这段,你就懂了 Agent 的 90%。剩下的工程(重试、并发、记忆压缩…)都是给**这个循环**加保险。
> Get this and you get 90% of Agents. The rest (retries, concurrency, memory compaction…) just hardens *this loop*.

## 跑起来会发生什么 / What a Run Looks Like

```
user:  北京今天穿什么?
 └─ 第1圈:模型想调 get_weather(city="北京")
           执行 → "晴,3°C"  → 塞回历史
 └─ 第2圈:模型看到 3°C,这次不调工具了
           直接答:"挺冷,建议厚外套 🧥"
return → "挺冷,建议厚外套"
```

是不是和 [03 篇修 bug 的例子](03-loop-example.md) 一个节奏?只是工具换了。
Same rhythm as [the bug-fixing example in Note 03](03-loop-example.md) — just different tools.

## 从"玩具"到"能用"还差什么 / Toy → Usable

| 缺的东西 / Missing | 为什么要 / Why | 哪篇讲过 / Where |
|--------------------|---------------|------------------|
| 循环上限 | 防止无限转圈 / avoid infinite loops | (下一段) |
| 错误处理 | 工具报错别崩 / tools may fail | [28 上线工程](28-production.md) |
| 记忆管理 | 历史太长会爆 [窗口](07-context-memory.md) | [07](07-context-memory.md) |
| 危险操作确认 | 别让它乱删 / guard risky acts | [13 安全](13-safety.md) |

```python
# 一个最起码的保险:限制最多转 N 圈
for step in range(10):     # 最多 10 圈 / cap the loops
    ...
else:
    return "转太多圈了,放弃 / gave up after too many steps"
```

> 小知识 / Note:你正在用的 Claude Code,内核就是这个循环的"加强版"——多了几十种工具、权限确认、记忆压缩、并发子 Agent。但骨架没变。
> Claude Code is a beefed-up version of this very loop — dozens of tools, permission gates, compaction, concurrent sub-agents. Same skeleton.

➡️ 下一篇 / Next: [多模态:让 Agent 看图听声](27-multimodal.md)
