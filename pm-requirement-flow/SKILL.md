---
name: pm-requirement-flow
description: "PM 工作流。需求澄清 → 派发 → 验收。Yi 平时派需求给 Claude Code 开发的流程，已经跑通了，记录下来方便复用。依赖 claude-code-dispatch。"
metadata: {"openclaw": {"emoji": "📋", "always": true}}
---

# PM Requirement Flow 📋

从模糊需求到代码上线的完整流程。

## 依赖

必须安装 `clawdhub install claude-code-dispatch`

## 核心理念

不澄清不派发。需求不清楚的时候多问几句，比开发到一半发现理解错了再返工要快得多。

## 流程

### 第一步：听需求

听用户说什么，不要急着给建议。先理解清楚再动手。

### 第二步：追问

持续追问几个关键点：

- **背景**：为什么做？解决什么问题？
- **用户**：谁用？痛点是什么？
- **范围**：必须包含什么？可以不包含？
- **验收**：怎么算完成？有什么标准？

每次问 2-3 个，不要一次性问完。

### 第三步：写 SPEC

把需求整理成结构化文档：

```
# [功能名]

## 背景
为什么做

## 用户
谁用 + 痛点

## 功能
1. [功能1] - 验收标准
2. [功能2] - 验收标准

## 边界
- 包含：...
- 不包含：...

## 完成标准
怎么验证
```

### 第四步：确认

把 SPEC 发给用户确认：
- "是这样吗？"
- "有没有理解错的？"

### 第五步：派发

用 `claude-code-dispatch` 派给 Claude Code 开发：

```bash
nohup bash ~/.openclaw/workspace/skills/claude-code-dispatch/scripts/dispatch.sh \
  -p "需求：<SPEC内容>" \
  -n "功能名" \
  --workdir /项目路径 \
  --permission-mode bypassPermissions \
  > /tmp/dispatch.log 2>&1 &
```

### 第六步：验收

Claude Code 完成后，独立验收：
- 检查实际产出
- 对照 SPEC 逐项核对
- 运行验证
- 不轻信"完成了"

通过后告知用户。

## 触发词

需求、开发、做个东西、帮我做XX、开始项目

---

*Yi 自用流程，感觉有用就拿去。*
