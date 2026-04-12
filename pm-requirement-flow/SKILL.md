---
name: pm-requirement-flow
description: PM 需求澄清 → 派发开发完整流程。从模糊需求开始，追问澄清到足够清晰，然后派发给 Claude Code 开发，最后独立验收。Requires: claude-code-dispatch (for task dispatching to Claude Code)
metadata: {"openclaw": {"emoji": "📋", "always": true}}
---

# PM Requirement Flow 📋

从模糊需求到完成开发的完整 PM 流程。

## 依赖

**必须安装：** `claude-code-dispatch`

```bash
# 安装依赖
clawdhub install claude-code-dispatch
```

## 核心原则

> **不澄清不派发。** 需求不清晰时，宁可多问几句，也不要让开发返工。

## 工作流

### Phase 1: 接收需求

用户给出模糊需求。

**不要立刻动手，先理解清楚。**

### Phase 2: 追问澄清

持续追问，直到没有模糊点：

| 追问维度 | 示例问题 |
|---------|---------|
| **背景** | 为什么做这个？解决什么问题？ |
| **用户** | 谁会用？他们的痛点是什么？ |
| **范围** | 必须包含什么？可以不包含什么？ |
| **验收** | 怎么算完成？你怎么验证？ |
| **优先级** | 核心是哪个功能？ |
| **约束** | 有没有技术限制？时间限制？ |

**停止追问的条件：**
- 用户明确说"清楚了，就这样做"
- 你能把需求写成完整的 SPEC

### Phase 3: 写 SPEC/PRD

输出结构化的需求文档：

```
# [功能名] SPEC

## 背景
[为什么做]

## 用户
[谁用 + 痛点]

## 功能清单
1. [功能1] - [验收标准]
2. [功能2] - [验收标准]

## 边界
- 包含：[...]
- 不包含：[...]

## 技术约束
[如果有]

## 完成标准
[如何验证]
```

### Phase 4: 用户确认

把 SPEC 给用户确认：
- "是这样的吗？"
- "有没有遗漏或理解错的？"

**得到明确确认后再派发。**

### Phase 5: 派发开发

用 `claude-code-dispatch` 派发给 Claude Code：

```bash
nohup bash ~/.openclaw/workspace/skills/claude-code-dispatch/scripts/dispatch.sh \
  -p "需求：<SPEC内容>" \
  -n "功能名" \
  --workdir /项目路径 \
  --permission-mode bypassPermissions \
  > /tmp/dispatch.log 2>&1 &
```

### Phase 6: 独立验收

Claude Code 完成后，**我独立验收**：

- 检查实际产出（代码/文件）
- 对照 SPEC 逐项核对
- 运行验证命令
- **不轻信 Claude Code 的"完成了"**

通过后告知用户。

## 触发词

需求、做个东西、开发、想加个功能、帮我做个XX、开始项目

## 注意事项

- 追问要精准，一次 2-3 个问题
- 不要问可以自己判断的问题
- 目标是清晰，不是完美
- 派发后保持跟踪直到验收
