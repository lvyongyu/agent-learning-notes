# 18 · 反思与自我纠错 / Reflection & Self-correction

> 进阶模式篇 · 第 3 篇 / Patterns track · Note 3

让 Agent **回头检查自己刚才做得对不对**,发现问题就改——这就是反思 (Reflection)。它能明显减少错误。
Have the Agent *look back and check its own work*, then fix what's wrong — that's Reflection. It cuts errors a lot.

## 一句话 / In One Sentence

> 第一遍先做出草稿,再让模型**当自己的批评家**审一遍,挑毛病、改进。
> Make a draft first, then have the model act as *its own critic* — find flaws and improve.

就像写完作文再通读一遍找错别字,而不是写完直接交。
Like re-reading your essay for typos before handing it in, instead of submitting blind.

## 流程图 / The Flow

```
        ┌─────────────┐
        │  ① 生成草稿   │  先做出一个版本
        │  Draft       │  produce a first attempt
        └─────────────┘
               │
               ▼
        ┌─────────────┐
        │  ② 自我批评   │  "哪里不对?哪里能更好?"
        │  Critique    │  "what's wrong? what's better?"
        └─────────────┘
               │
        有问题?/ issues?
         ┌─────┴─────┐
         ▼           ▼
       有 yes        没 no
         │           │
         ▼           ▼
   ③ 改进重做     ✅ 交付
   revise & retry   ship
   (回到②再审)
   (loop back)
```

## 两种反思 / Two Kinds

| 类型 / Kind | 怎么做 / How | 例子 / Example |
|-------------|--------------|----------------|
| 🪞 **自省 / Self** | 自己审自己 / critiques itself | "我这段代码有没有漏掉边界情况?" |
| 🔍 **靠外部信号 / Grounded** | 用真实反馈来纠错 / use real feedback | 跑测试报错 → 照报错改 |

> 靠外部信号的反思**更可靠**:因为有"客观裁判"(测试、编译器、运行结果),不是模型自己说了算。这也呼应了 [12 篇评估](12-evaluation.md) 的思路。
> Grounded reflection is *more reliable* — there's an objective judge (tests, compiler, runtime), not just the model's opinion. Echoes [Note 12 on evaluation](12-evaluation.md).

## 一个例子 / An Example

任务:**写一个"判断闰年"的函数**
Task: *write an "is leap year" function*

```
① 草稿:if year % 4 == 0: 是闰年
② 批评:等等,整百年要能被 400 整除才算,
        我漏了这个规则
        (1900 不是闰年,但我会判成是)
③ 改进:加上 % 100 和 % 400 的判断
✅ 再审:这次 1900→否、2000→是,正确
```

看到没?**第一遍就是会漏**,反思这一步把它救了回来。
See? The first pass *does* miss things — reflection rescues it.

## 代价 / The Cost

> 反思 = 多跑几轮 = 更慢、更费 [token](07-context-memory.md)。所以一般**只对重要/容易错的任务**开反思,简单任务不必。
> Reflection = extra rounds = slower & more [tokens](07-context-memory.md). Use it for *important or error-prone* tasks, skip it for easy ones.

> 小知识 / Note:Claude Code 改完代码会**主动跑测试**,失败了照报错再改——这就是"靠外部信号的反思"在实战。
> When Claude Code edits code it *runs the tests*, and fixes from the errors — grounded reflection in action.

➡️ 下一篇 / Next: [常见 Agent 模式对比](19-agent-patterns.md)
