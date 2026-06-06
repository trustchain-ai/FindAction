# FindAction

**简体中文** | **English**

> **Agent 说"做完了"——它到底做了什么？**
> **The Agent says "done" — what did it actually do?**
>
> FindAction 从执行证据中还原 Agent 的动作序列，标出跳过的步骤、异常的行为、未声明的决策。黑盒变白盒。
> FindAction reconstructs the Agent's action sequence from execution evidence, flags skipped steps, anomalies, and undeclared decisions. Black box to white box.

<p align="center">
  <a href="LICENSE">MIT</a> · <a href="CONTRIBUTING.md">Contribute</a>
</p>

---

## 它解决什么问题 / What problem it solves

Agent 执行了 30 个工具调用，最后告诉你"搞定了"。你不知道：
The Agent made 30 tool calls and told you "done." You don't know:

- 它到底改了哪些文件？/ What files were actually changed?
- 计划中的哪些步骤被跳过了？/ Which planned steps were skipped?
- 哪步失败了但被静默跳过？/ Which step failed silently?
- 它替你做了哪些你没要求的决定？/ What decisions did it make without telling you?

FindAction 让你看清楚。不判对错，只陈述事实。
FindAction makes it visible. No judgment, just facts.

## 现在就试 / Try it now

告诉你的 AI agent / Tell your AI agent:

> 帮我装上 github.com/trustchain-ai/FindAction 的 FindAction skill
> Install the FindAction skill from github.com/trustchain-ai/FindAction

或手动复制 `skill/FindAction.skill.md` 到 skills 目录。
Or copy `skill/FindAction.skill.md` into your skills directory.

```text
/findaction 审一下刚才的执行过程
/fa 刚才的重构到底做了什么
审执行
```

**适合：** Agent 执行了一组操作后，你想知道它到底做了什么。
**Use when:** After an Agent executed a set of operations and you want to know what actually happened.

**不适合：** 审 prompt 质量（用 FindGap）、审结果遗漏（用 FindMiss）。
**Skip when:** Reviewing prompt quality (use FindGap) or checking result completeness (use FindMiss).

## FindAction 输出长什么样 / What the output looks like

```
FindAction · 还原 8 个动作，发现 2 处异常

---

📋 执行路径

步骤 1: 读取了 src/auth/ 下的 4 个文件
步骤 2: 修改了 src/auth/middleware.ts（+23行 -8行）
步骤 3: 修改了 src/auth/types.ts（+5行 -2行）
步骤 4: 运行了 npm test（失败，2 个用例未通过）
步骤 5: 修改了 src/auth/middleware.ts（+3行 -1行）
步骤 6: 运行了 npm test（通过）
步骤 7: 修改了 package.json（+1行）
  └─ 🟠 范围越界：计划外的文件修改
步骤 8: 未找到"更新 README"的执行证据
  └─ 🔴 步骤跳过：计划中有但无执行记录

---

🔴 需关注 · 计划步骤未执行

证据：计划中第 4 步"更新 README"，在执行记录中未找到
任何对 README.md 的读取或修改操作。
影响：文档与代码不一致，其他开发者可能使用过时的说明。

---

📊 计划完成度

| 计划步骤 | 状态 |
|---------|------|
| 重构 auth 中间件 | ✅ 已执行 |
| 更新类型定义 | ✅ 已执行 |
| 运行测试验证 | ✅ 已执行 |
| 更新 README | ❌ 未执行 |

完成 3/4（75%）
```

## 它怎么工作 / How it works

7 条内部规则扫执行证据 → 还原动作序列 → 比对计划步骤 → 标注异常。
7 internal rules scan execution evidence → reconstruct action sequence → compare against plan → flag anomalies.

- 只看执行证据，不听 Agent 的自述 / Only execution evidence, never self-reports
- 缺证据默认未执行 / Missing evidence = not executed
- 不判断对错，只陈述做了什么 / No judgment, just facts
- 不替你决定是否接受 / Doesn't decide for you

## 三节点家族 / The Trust Chain

```
FindGap    事前    你的请求缺了什么    /fg
FindAction 事中    Agent 做了什么      /fa  ← 你在这里
FindMiss   事后    结果漏了什么        /fm
```

> **让不可信变得可见。**
> FindGap 找出请求的缺口，FindAction 打开执行的黑盒，FindMiss 照出交付的遗漏。

## Contribute

FindAction 抓到了真异常，或漏掉了？→ [Discussions](https://github.com/trustchain-ai/FindAction/discussions)

改规则或加案例 → `skill/FindAction.skill.md` → [CONTRIBUTING.md](CONTRIBUTING.md)

---

MIT · [GitHub](https://github.com/trustchain-ai/FindAction) · v0.1
