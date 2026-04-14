# Yi OpenClaw Skills 🧰

个人 OpenClaw Skills 集合，可直接安装使用。

## Skills

| Skill | 说明 | 触发词 |
|-------|------|--------|
| **jargon-translator** 🎭 | 互联网黑话双向转换器 | 黑话、包装、人话 |
| **communication-coach** 🥊 | 苏格拉底式挑刺 + 降维表达 | 挑刺、对练、话术 |
| **pm-requirement-flow** 📋 | PM 工作流：需求澄清 → 派发 → 验收（集成 task-tracker + Agent Teams） | 需求、开发、做个东西 |

## 安装方式

```bash
# 安装单个 skill
openclaw skills add https://raw.githubusercontent.com/yiguoguo/yi-openclaw-skills/main/jargon-translator/SKILL.md
openclaw skills add https://raw.githubusercontent.com/yiguoguo/yi-openclaw-skills/main/pm-requirement-flow/SKILL.md

# 或下载后安装
cp -r jargon-translator ~/.openclaw/workspace/skills/
cp -r pm-requirement-flow ~/.openclaw/workspace/skills/
```

## pm-requirement-flow 使用

**触发词：** 需求、开发、做个东西、帮我做 XX、开始项目

**流程：**
1. 需求澄清（追问背景/用户/范围/验收）
2. 写 SPEC（结构化文档）
3. 用户确认
4. 派发 Claude Code（自动追踪）
5. 独立验收（截图 + 测试）

**示例：**
```
用户：帮我做个番茄计时器
PM：好的，先确认几个问题：
1. 你自己用还是团队用？
2. 需要统计功能吗？
3. 有什么偏好的 UI 风格？
```

## 来源说明

- **jargon-translator**: 原始来源不可考，来源于互联网社区分享
- **communication-coach**: 原始来源不可考，来源于互联网社区分享
- **pm-requirement-flow**: 原创（参考 agency-agents PM 角色定义）

## Changelog

### 2026-04-14

**pm-requirement-flow v1.1.0**
- ✨ 新增 task-tracker 任务追踪
- 📝 添加 PM 职责说明（不写代码）
- 📝 添加 Agent Teams 使用时机
- 📝 添加验收流程（含截图要求）
- 📝 添加 pm-agent-profile.md（完整角色定义）
- 🐛 修复 dispatch 输出缓冲问题

## License

MIT
