# 12 · 怎么评估一个 Agent 好不好 / How to Evaluate an Agent

写出一个 Agent 不难,难的是知道它**到底靠不靠谱**。这一篇讲怎么衡量。
Building an Agent is easy; knowing whether it's *actually reliable* is hard. This note is about measuring that.

## 为什么评估很难 / Why It's Tricky

> 普通程序:输入固定 → 输出固定,对就是对。
> Agent:同一个问题,**每次回答可能不一样**(有随机性),而且常常"没有唯一正确答案"。
> Normal code: same input → same output. An Agent: the *same question can give different answers*, and often there's no single "correct" one.

所以不能只看"跑没跑通",得有一套打分办法。
So you can't just check "did it run" — you need a way to score quality.

## 评什么 / What to Measure

| 维度 / Dimension | 问题 / The question |
|------------------|---------------------|
| ✅ **正确性 / Correctness** | 答案/结果对不对? / is the result right? |
| 🎯 **完成度 / Task success** | 任务真做完了吗? / did it finish the job? |
| 💰 **成本 / Cost** | 花了多少 token / 多少钱? / how many tokens / how much $? |
| ⏱️ **速度 / Latency** | 多久出结果? / how long did it take? |
| 🔁 **稳定性 / Consistency** | 跑 10 次有几次成功? / how many of 10 runs succeed? |
| 🛡️ **安全性 / Safety** | 会不会乱删东西、说错话? / does it do harmful things? |

> 关键心法:别只看"它答得好不好",还要看 **"成本"和"稳不稳"**。一个答得对但跑 10 次错 4 次的 Agent,不能用。
> Key mindset: don't only judge answer quality — weigh *cost* and *consistency* too. An Agent that's right but fails 4 of 10 runs isn't usable.

## 三种打分办法 / Three Ways to Score

```
① 标准答案对比 / Golden answers
   准备一批"题目+正确答案",自动比对
   prepare Q&A pairs, auto-compare
   👍 客观、能自动化   👎 很多任务没有唯一答案
   objective, automatable | many tasks have no single answer

② 人工打分 / Human review
   人来看输出,按标准评分
   humans rate the output
   👍 最贴近真实质量   👎 慢、贵、主观
   closest to real quality | slow, costly, subjective

③ 用 AI 当裁判 / LLM-as-judge
   让另一个模型按标准给输出打分
   a second model grades the output
   👍 快、可规模化     👎 裁判自己也可能出错
   fast, scalable | the judge can be wrong too
```

## 一个最小例子 / A Minimal Example

```
任务集 / Test set:
  题1:1+1=?        期望:2
  题2:法国首都?     期望:巴黎
  题3:修复这个 bug  期望:测试通过

跑 Agent → 对答案 → 算通过率
run Agent → check → compute pass rate

结果:3 题对 2 题 → 通过率 67%
Result: 2/3 correct → 67% pass rate
```

> 小知识 / Note:这套"题目集 + 打分"在业界叫 **Eval(评估集)**。改了提示词或换了模型,就重跑一遍 Eval,看分数有没有变高——这是做 Agent 的核心工作流。
> This "test set + scoring" is called an **Eval**. After changing the prompt or model, you re-run the Eval to see if the score went up — it's the core workflow of building Agents.

➡️ 下一篇 / Next: [安全与权限](13-safety.md)
