# Contributing to FindAction

FindAction 抓到了真异常，或漏掉了？欢迎贡献。

## 怎么贡献

### 报告误判或漏判

在 [Discussions](https://github.com/trustchain-ai/FindAction/discussions) 中提供：

1. Agent 的执行场景（做了什么任务）
2. FindAction 的输出
3. 你认为它判对了还是判错了，以及理由

### 改进规则

编辑 `skill/FindAction.skill.md`，提交 PR。

规则修改需说明：
- 改了哪条规则
- 为什么改（附真实案例）
- 改完后的预期效果

### 添加案例

在 `examples/` 下添加真实的 FindAction 输出案例。格式参考已有文件。

## 原则

- 不引入新规则，除非有真实案例证明需要
- 不扩大 FindAction 的职责范围（只审过程，不审内容）
- 不破坏红线（self-report ≠ proof、缺证据默认未执行）
