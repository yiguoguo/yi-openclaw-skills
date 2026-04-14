# PM Requirement Flow 📋

PM 工作流：需求澄清 → 派发 → 验收

---

## 目录

- [依赖](#依赖)
- [安装](#安装)
- [基础用法](#基础用法)
- [高级用法](#高级用法配合 agency-agents)
- [PUA 话术模板](#pua-话术模板)
- [实战案例](#实战案例)
- [Changelog](#changelog)

---

## 依赖

### 必需

- OpenClaw
- `claude-code-dispatch`

### ⚠️ macOS 用户注意

如果你遇到 `claude-code-dispatch` 无法运行或输出缓冲问题：

**1. 确保使用 Node v22**
```bash
nvm use 22
```

**2. 重新安装 claude-code-dispatch**
```bash
clawdhub uninstall claude-code-dispatch
clawdhub install claude-code-dispatch
```

**3. 详细修复文档**

[Dispatch 修复说明](https://note.wangyii.com/workflow/dispatch-fix.html)

### 推荐

- **agency-agents** - 144+ AI 专家角色定义
  ```bash
  cd <your-openclaw-workspace>
  git clone https://github.com/msitarzewski/agency-agents.git
  ```

---

## 安装

```bash
openclaw skills add https://raw.githubusercontent.com/yiguoguo/yi-openclaw-skills/main/pm-requirement-flow/SKILL.md
```

---

## 基础用法

### 触发词

需求、开发、做个东西、帮我做 XX、开始项目

### 流程

1. **需求澄清**（追问背景/用户/范围/验收）
2. **写 SPEC**（结构化文档）
3. **用户确认**
4. **派发 Claude Code**（自动追踪）
5. **独立验收**（截图 + 测试）

### 示例

```
用户：帮我做个番茄计时器

PM：好的，先确认几个问题：
1. 你自己用还是团队用？
2. 需要统计功能吗？
3. 有什么偏好的 UI 风格？
```

---

## 高级用法（配合 agency-agents）

### 1. 准备角色文件

```bash
# 复制 PM 角色文件
cp <agency-agents>/project-management/project-manager-senior.md \
   <project>/.claude/agents/pm.md

# 复制 Frontend Developer
cp <agency-agents>/engineering/engineering-frontend-developer.md \
   <project>/.claude/agents/frontend-developer.md
```

### 2. 编写 SPEC

```bash
cat > <project>/.claude/memory-bank/spec.md << 'EOF'
# [项目名]

## 背景
为什么做？解决什么问题？

## 用户
谁用？痛点是什么？

## 功能
1. [功能 1] - 验收标准
2. [功能 2] - 验收标准

## 技术栈
- 框架：...
- 部署：...
EOF
```

### 3. 派发 + PUA

```bash
dispatch.sh -p "你是 Senior Project Manager 专家。
              请阅读 .claude/agents/pm.md 和 .claude/memory-bank/spec.md
              
              你的任务：[具体任务]
              
              成功标准：
              ✅ [标准 1]
              ✅ [标准 2]
              ✅ [标准 3]
              
              记住：你的工作直接影响项目成败，我相信你能做到最好。" \
  --workdir <project-path>
```

---

## PUA 话术模板

```markdown
你是 [角色名] 专家，你的职责是 [角色使命]。

请阅读以下文件：
- .claude/agents/[角色].md（你的身份定义）
- .claude/memory-bank/[项目]-spec.md（项目需求）

你的任务：[具体任务]

成功标准：
✅ [标准 1]
✅ [标准 2]
✅ [标准 3]

记住：你是 [角色] 专家，[角色特质]。
你的工作直接影响 [影响范围]。
我相信你能做到最好。
```

---

## 实战案例

### 案例 1：番茄计时器

**项目：** `pomodoro-timer`  
**角色：** Frontend Developer  
**任务：** 修复深色模式问题

**派发：**
```bash
dispatch.sh \
  -p "你是 Frontend Developer 专家。
      请阅读 .claude/agents/frontend-developer.md
      
      任务：修复深色模式问题
      - 点击🌙背景变深色（#111827）
      - 点击☀️背景变白色
      
      成功标准：
      ✅ 深色模式切换正常
      ✅ 文字颜色相应变化
      ✅ 部署后测试通过
      
      记住：你是前端专家，像素级精确是你的职责。" \
  --workdir /workspace/pomodoro-timer
```

**结果：** ✅ 修复成功

---

## 任务追踪

```bash
# 查看进行中的任务
task-tracker.sh list

# 查看状态（含超时检查）
task-tracker.sh status

# 标记完成（Hook 自动调用）
task-tracker.sh complete <task-name>
```

---

## Changelog

### v1.2.0 (2026-04-14)
- ✨ 添加 agency-agents 集成说明
- 📝 添加高级用法（角色文件 + SPEC 文件）
- 📝 添加 PUA 话术模板

### v1.1.0 (2026-04-14)
- ✨ 新增 task-tracker 任务追踪
- 📝 添加 PM 职责说明
- 📝 添加 Agent Teams 使用时机
- 📝 添加验收流程

### v1.0.0 (2026-04-12)
- 初始版本

---

## 参考链接

- [笔记站文档](https://note.wangyii.com/workflow/agency-agents-integration.html)
- [agency-agents](https://github.com/msitarzewski/agency-agents)
- [GitHub 仓库](https://github.com/yiguoguo/yi-openclaw-skills)
