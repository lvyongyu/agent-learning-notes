# 03 · 一个真实例子：修 Bug / A Real Example: Fixing a Bug

任务 / Task：**「帮我修复登录失败的 bug」/ "Fix the login bug for me."**

Agent 脑子里其实是这样一圈圈转的 ——
Here's how the Agent actually loops through it:

```
你 / You: 帮我修复登录失败的 bug

  第1圈 / Loop 1
  ├─ 🧠 想 Think:  我得先看看代码长啥样 / Let me look at the code first
  ├─ 🛠️ 做 Act:    调用【读文件】打开 login.js / Read login.js
  └─ 👀 看 Observe: 哦，这里密码比较写错了 / Found a wrong password check

  第2圈 / Loop 2
  ├─ 🧠 想 Think:  我应该改这一行 / I should fix this line
  ├─ 🛠️ 做 Act:    调用【编辑文件】修改代码 / Edit the file
  └─ 👀 看 Observe: 改好了 / Done

  第3圈 / Loop 3
  ├─ 🧠 想 Think:  得验证一下修对没 / Let me verify the fix
  ├─ 🛠️ 做 Act:    调用【跑测试】/ Run the tests
  └─ 👀 看 Observe: 测试通过 ✅ / Tests pass

  → 任务完成，回复你 / Task done, reply to you
```

## 要记住的两点 / Two Takeaways

1. **每一圈都重新思考**，不是一口气写完。
   It **re-thinks each loop**, not all at once.
2. **会自己验证**（跑测试），结果不对就再来一圈。
   It **verifies itself** (runs tests); if wrong, it loops again.

➡️ 下一篇 / Next: [四大零件](04-components.md)
