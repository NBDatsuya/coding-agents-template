# AI Agents Template — 完整使用指南

> 关于如何使用和定制本模板的一切你需要知道的。

## 目录

1. [这是什么？](#这是什么)
2. [快速开始](#快速开始)
3. [自定义配置](#自定义配置)
4. [多智能体协作](#多智能体协作)
5. [技术栈模板](#技术栈模板)
6. [工具集成](#工具集成)
7. [参与贡献](#参与贡献)

---

## 这是什么？

这是一个面向 AI 编程智能体的**通用模板**。它提供：

### 核心组件

| 组件 | 用途 |
|------|------|
| `AGENTS.md` | 智能体行为规则（文档/提交策略、代码标准、禁止事项） |
| `CODEBASE_STATE.md` | 项目事实的实时地图 —— 技术栈、架构、规范、注册表 |
| `docs/TROUBLESHOOTING.md` | 已知问题及其修复方案 |
| `.agents/skills/` | 领域知识库，用于常见任务 |

### 核心特性

- **技术无关** — 适用于 Vue、React、Svelte、Node、Python 或任何技术栈
- **多智能体就绪** — 包含多 AI 协作协议
- **规范驱动** — 代码库风格一致
- **质量保证** — 内置规则防止常见错误

---

## 快速开始

### 新项目

```bash
# 1. 克隆模板
git clone https://github.com/NBDatsuya/coding-agents-template.git your-project
cd your-project

# 2. 清除 git 历史（全新开始）
rm -rf .git
git init

# 3. 为你的项目定制
# 编辑 AGENTS.md — 填写你的技术栈、命名规范等
```

### 已有项目

```bash
# 仅复制 AGENTS.md 文件
curl -O https://raw.githubusercontent.com/NBDatsuya/coding-agents-template/main/AGENTS.md
```

AI 智能体工作时将自动读取项目根目录的 `AGENTS.md`。

### 下一步

1. **填写技术栈** — 在 `CODEBASE_STATE.md` 中填写 Tech Stack 部分
2. **定义命名规范** — 在 `AGENTS.md` 中为你的项目设置命名规则
3. **配置状态管理** — 在 `CODEBASE_STATE.md` 中设置状态管理规则
4. **设置 API 规范** — 如有需要，在 `CODEBASE_STATE.md` 中定义 API 约定
5. **记录已知问题** — 在 `docs/TROUBLESHOOTING.md` 中记录已知问题或修复方案

---

## 自定义配置

### 1. 技术栈

更新 `CODEBASE_STATE.md` 中的 **Tech Stack** 表格：

```markdown
## 2. Tech Stack

| 层级 | 选择 | 备注 |
|------|------|------|
| UI 框架 | Vue 3 | SFC + Composition API |
| 语言 | TypeScript | 严格模式，禁止 `any` |
| 构建工具 | Vite 5 | `@` → `./src` |
| 样式方案 | Tailwind CSS | 工具类优先 |
| 状态管理 | Pinia | 支持持久化 |
| HTTP 客户端 | Axios | 拦截器配置 |
```

### 2. 命名规范

在 `AGENTS.md` 中定义项目的命名标准：

```markdown
## 6. Naming Conventions

- **文件**：`kebab-case`（如 `user-profile.vue`）
- **组件**：`PascalCase`（如 `UserProfile`）
- **路由路径**：`kebab-case`（如 `/user/profile`）
- **路由名称**：`PascalCase`（如 `UserProfile`）
- **状态库**：`camelCase` + `use` 前缀（如 `useUserStore`）
```

### 3. 代码标准

在 `AGENTS.md` 中设置质量规则：

```markdown
## 3. Code Standards

### TypeScript 基础

- 禁止 `var` — 使用 `const` 和 `let`
- 禁止 `any` — 使用 `unknown` + 类型收窄
- 所有 props 和 emits 必须类型化

### 组件规则

- 组件只负责渲染 UI — 不含业务逻辑
- 所有 API 调用必须通过 services
- 跨组件状态放入 stores
```

### 4. 状态管理

在 `CODEBASE_STATE.md` 中文档化你的状态管理方案：

```markdown
## 12. State Management

状态库位于 `src/store/`：

- **Pinia** 用于跨组件状态
- **Vue reactive** 用于组件内部状态
- **持久化** 通过 `pinia-plugin-persistedstate`
```

---

## 多智能体协作

当多个 AI 智能体协作时，请遵循以下协议：

### 1. 编码前阅读

开始任何功能前：

```
- [ ] 阅读 AGENTS.md §0–§7
- [ ] 查看 CODEBASE_STATE.md 的目录地图了解现有工作
- [ ] 查看 docs/WIP.md 了解已声明的区域
```

### 2. 声明所有权

当处理多轮对话的功能时：

```
开始处理 [功能名]。在 docs/WIP.md 中声明一行 WIP 用于 [功能]。
```

这可以防止其他智能体同时处理同一区域。

### 3. 提交时文档同步

当用户要求提交时：

```
- 更新 CHANGELOG
- 如有需要在 CODEBASE_STATE.md 中添加决策日志
- 如结构变更则更新 CODEBASE_STATE.md 的目录地图
```

### 4. 冲突解决

| 情况 | 规则 |
|------|------|
| 命名空间冲突 | 先查注册表；不静默重命名 |
| 删除代码 | 移到删除线，不移除 |
| 文档 vs 代码 | 代码优先 — 文档跟随代码 |

---

## 技术栈模板

本仓库包含不同技术的模板：

| 技术栈 | 位置 | 特性 |
|--------|------|------|
| **Vue 3** | `./templates/vue3/` | Vue 3 + TypeScript + Vite + Pinia + PrimeVue |
| **React** | `./templates/react/` | 🔜 即将推出 |
| **Svelte** | `./templates/svelte/` | 🔜 即将推出 |
| **Node.js** | `./templates/nodejs/` | 🔜 即将推出 |

### 使用技术栈模板

```bash
# 克隆完整仓库
git clone https://github.com/NBDatsuya/coding-agents-template.git
cd coding-agents-template

# 复制特定模板
cp -r templates/vue3 /path/to/your-project/
```

---

## 工具集成

### Claude Code

本模板专为 Claude Code 设计。智能体将：

1. 项目开始时读取 `AGENTS.md`
2. 遵循 §0–§7 中的规范
3. 仅在用户要求时更新 `CODEBASE_STATE.md`
4. 尊重其他智能体的 WIP 声明

### Cursor

添加到 `.cursor/rules/`：

```
@import: ../AGENTS.md
```

### GitHub Copilot

创建 `.cursorrules`：

```
# AI 智能体规范

遵循本项目 AGENTS.md 中的规则。
```

---

## 参与贡献

有模板想分享？欢迎提交 PR！

### 添加新模板

1. 在 `templates/` 下创建文件夹
2. 添加针对该技术栈定制的 `AGENTS.md`
3. 包含任何特定于技术的规范
4. 在本 README 中更新你的模板

### 模板结构

```
templates/
└── your-template/
    ├── AGENTS.md          # 必需
    ├── README.md          # 可选
    └── example/           # 可选示例代码
```

---

## 常见问题

### Q: AGENTS.md 中是否需要填写所有部分？

**A:** 不需要。只填写与你的项目相关的部分。模板是模块化的。

### Q: 可以配合 GitHub Copilot 使用吗？

**A:** 可以。创建一个引用 AGENTS.md 的 `.cursorrules` 文件。

### Q: 项目进行中如何更新规范？

**A:** 直接编辑 AGENTS.md。更改对新 AI 智能体会话立即生效。

### Q: 安全敏感的规范如何处理？

**A:** 在 AGENTS.md 中添加明确标注。AI 智能体会遵守它们。

---

## 许可证

MIT — 自由使用，自由修改，无需署名。
