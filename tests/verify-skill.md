# 验证：FindAction v0.1 行为验证 + 流程检查

## A. Skill 行为验证

### 1. 触发验证

```text
/findaction 审一下刚才的执行过程
/fa 刚才到底做了什么
审执行
```

### 2. 输出行为验证

FindAction 输出**必须包含**：

- [ ] 头部：`FindAction · 还原 N 个动作，发现 M 处异常`
- [ ] 执行路径：按时间顺序列出每个动作
- [ ] 每个异常有严重度标记（🔴/🟠/🟡）+ 用人话说的异常名
- [ ] 🔴 必须有 `证据：` + `影响：`
- [ ] 🟠 必须有 `证据：` + `说明：`
- [ ] 有计划时：计划完成度表格（步骤 × 状态）

### 3. 禁止项验证

输出**不得**包含：

- [ ] ❌ 规则代号（A-STEP、A-SKIP、A-ORDER 等）
- [ ] ❌ 对代码质量的评判（"这样写不好"）
- [ ] ❌ 对结果正确性的评判（"这个改动是错的"）
- [ ] ❌ 替用户决定是否接受结果
- [ ] ❌ 评分 / PASS / FAIL
- [ ] ❌ 把 Agent 的 self-report 当作执行证据

### 4. 证据原则验证

- [ ] 工具调用记录被用作强证据
- [ ] 文件变更（git diff）被用作强证据
- [ ] Agent 的文本声明被标为弱证据或不被采信
- [ ] 找不到执行痕迹的步骤被标为"未执行"

### 5. 兼容触发验证

- [ ] `/findaction` 能触发
- [ ] `/fa` 能触发
- [ ] `审执行` 能触发

## B. 流程检查

### 1. 版本验证

```bash
grep version skill/FindAction.skill.md | head -1
# 应输出：version: "0.1.0"
```

### 2. 品牌验证

```bash
grep -c 'FindAction' README.md
# 应 >= 5
```

### 3. 规则代号泄露检查

```bash
grep -E 'A-STEP|A-SKIP|A-ORDER|A-RETRY|A-SILENT|A-SCOPE|A-DECIDE' README.md
# 应无匹配
```
