# how-skills

**how-skills** 是一个面向 AI Agent 的 Skill，用于帮助 Agent 生成高质量、符合规范的 `SKILL.md` 文件。

当你需要为 Claude Code、Gemini CLI、Cursor 等 AI 开发工具创建新技能时，使用 `/how-skills` 让 Agent 引导你完成整个设计流程——从需求确认到自检输出，确保每个生成的 Skill 都符合最佳实践。

---

## 这个 Skill 能做什么

- 📋 **需求访谈**：通过结构化提问收集 Skill 的核心功能、设计模式和目标领域
- ✍️ **生成 Frontmatter**：编写包含触发词、使用场景、元数据的标准 YAML 头部
- 🏗️ **编写指令正文**：按规范生成角色定位、先读取步骤、执行步骤、输出格式、Out of Scope 六段结构
- ✅ **自动自检**：对照 Anti-Patterns 清单验证，命中 3 条以上自动修改
- 📦 **拆分建议**：超过 200 行时自动给出 `references/`、`assets/` 拆分方案

支持五种设计模式：**Tool Wrapper**、**Generator**、**Reviewer**、**Inversion**、**Pipeline**，以及模式组合。

---

## 安装

### 方式一：使用 npx skills CLI（推荐）

```bash
# 安装到当前项目（.claude/skills/）
npx skills add cola-sk/how-skills

# 安装到全局（~/.claude/skills/，适用于所有项目）
npx skills add cola-sk/how-skills --global
```

### 方式二：手动安装

```bash
# 克隆仓库并复制到 Agent 的 skills 目录
git clone https://github.com/cola-sk/how-skills.git
cp -r how-skills ~/.claude/skills/how-skills
```

安装后重启 Agent 会话即可生效。

---

## 使用方式

安装后，在 Claude Code / Gemini CLI 等支持 Skills 的 Agent 中：

```
/how-skills
```

Agent 会按以下流水线引导你：

```
Step 1 → 需求确认（核心功能 / 设计模式 / 技术领域 / 输出格式）
Step 2 → 编写 YAML Frontmatter（含 description 三要素检查）
Step 3 → 编写指令正文（6 段固定结构）
Step 4 → 自检（Anti-Patterns 清单）
Step 5 → 输出 SKILL.md + 拆分建议 + 摘要表格
```

也可以直接描述需求，Agent 会自动识别触发：

```
帮我写一个 FastAPI 代码审查的 skill
生成一个用来写技术报告的 skill
创建一个需求访谈 skill
```

---

## Skill 规范文档

完整的 Skill 编写规范存放于 [`references/spec.md`](references/spec.md)，涵盖：

- Skill 文件结构与目录规范
- Description 三要素编写方法
- 五种设计模式详解（含代码示例）
- 质量红线与 Anti-Patterns 检查清单
- 完整示例：`/commit` Skill

---

## 参考资料

本 Skill 基于以下文章的最佳实践提炼：

- [The Anatomy of a Perfect Skill](references/The%20Anatomy%20of%20a%20Perfect%20Skill%20原文.md) — 从 100 个优秀案例反向工程出的 6 种核心模式
- [5 Agent Skill design patterns every ADK developer should know](references/5%20Agent%20Skill%20design%20patterns%20every%20ADK%20developer%20should%20know%20原文.md) — Tool Wrapper、Generator、Reviewer、Inversion、Pipeline 五种设计模式详解
