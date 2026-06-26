# 06 · 工具是怎么定义和调用的 / How Tools Are Defined & Called

工具（Tool）就是 Agent「动手」的能力。这一篇讲清楚：工具长什么样、Agent 怎么调用、结果怎么回来。
A Tool is the Agent's ability to *act*. This note explains: what a tool looks like, how the Agent calls it, and how the result comes back.

## 一句话 / In One Sentence

> 工具 = 一份「功能说明书」。LLM 自己**不会**真读文件，它只是**填一张表单**说「我要用这个工具，参数是这些」，由外面的程序去执行。
> A tool is a *spec sheet*. The LLM doesn't actually read the file — it just *fills out a form* saying "use this tool with these arguments", and the surrounding program runs it.

这点超级重要:**模型只负责"决定调用"，真正执行的是外面的代码（harness）。**
Key idea: the model only *decides* to call; the real execution is done by outside code (the "harness").

## 工具长什么样 / What a Tool Looks Like

定义一个工具，就是告诉模型三件事：**名字、干嘛用的、要哪些参数**。
Defining a tool means telling the model three things: **name, what it does, what arguments it needs.**

```json
{
  "name": "read_file",
  "description": "读取一个文件的内容 / Read the contents of a file",
  "input_schema": {
    "type": "object",
    "properties": {
      "path": { "type": "string", "description": "文件路径 / file path" }
    },
    "required": ["path"]
  }
}
```

> `description` 写得好不好，直接决定模型会不会**在对的时机**选这个工具。它是模型唯一的判断依据。
> A good `description` is what makes the model pick the tool *at the right moment* — it's the only clue the model has.

## 一次完整的调用 / One Full Round-Trip

```
1. 你给任务 + 工具清单 ──▶ 模型
   You send task + tool list ──▶ Model

2. 模型回："我要调用 read_file，path=login.js"   ← 这叫 tool_call
   Model replies: "call read_file with path=login.js"   ← a tool_call

3. 外面的程序真去读文件，拿到内容            ← harness 执行
   The harness actually reads the file

4. 把内容塞回去 ──▶ 模型                      ← 这叫 tool_result
   Feed the content back ──▶ Model            ← a tool_result

5. 模型基于结果继续思考下一步……（回到第 2 步循环）
   Model thinks again based on the result… (loop back to step 2)
```

看出来了吗?第 2~5 步就是 [01 篇](01-what-is-an-agent.md) 讲的 **思考→行动→观察** 循环，工具调用正是「行动」那一环。
See it? Steps 2–5 are exactly the **Think → Act → Observe** loop from [Note 01](01-what-is-an-agent.md) — the tool call is the "Act".

## 新手最容易误会的 3 件事 / 3 Common Misconceptions

| 误会 / Myth | 真相 / Truth |
|-------------|--------------|
| 模型自己能读文件、上网 | ❌ 模型只输出"我想调用 X"，执行靠外部程序 / The model only *says* it wants X; outside code runs it |
| 工具是模型自带的 | ❌ 工具是**你**提供给它的清单，你给几个它才知道几个 / You supply the list; it only knows what you give |
| 参数是模型瞎填的 | ❌ 参数必须符合你定义的 `input_schema`，否则会报错重试 / Args must match your schema, or it errors & retries |

> 小知识 / Note：你现在用的 Claude Code，`read_file`、`run command`、`edit` 这些都是工具。我每次"读文件"其实就是发了一个 tool_call。
> The `read_file`, `run command`, `edit` actions in Claude Code *are* tools. Every time I "read a file", I'm sending a tool_call.

➡️ 下一篇 / Next: [上下文与记忆](07-context-memory.md)
