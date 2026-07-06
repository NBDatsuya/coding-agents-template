# AI Agents Template — Full Guide

> Everything you need to know about using and customizing this template.

## Table of Contents

1. [What is This?](#what-is-this)
2. [Quick Start](#quick-start)
3. [Customization](#customization)
4. [Multi-Agent Workflow](#multi-agent-workflow)
5. [Tech Stack Templates](#tech-stack-templates)
6. [Tools & Integrations](#tools--integrations)
7. [Contributing](#contributing)

---

## What is This?

This is a **universal template** for AI coding agents. It provides:

### Core Components

| Component | Purpose |
|-----------|---------|
| `AGENTS.md` | Agent behavior rules (doc/commit policy, code standards, forbidden patterns) |
| `CODEBASE_STATE.md` | Living map of project facts — tech stack, architecture, conventions, registries |
| `docs/TROUBLESHOOTING.md` | Known issues and their fixes |
| `.agents/skills/` | Domain-specific knowledge for common tasks |

### Key Features

- **Tech-agnostic** — Works with Vue, React, Svelte, Node, Python, or any stack
- **Multi-agent ready** — Protocols for when multiple AI agents collaborate
- **Convention-driven** — Consistent patterns across your codebase
- **Quality enforced** — Built-in rules prevent common mistakes

---

## Quick Start

### For New Projects

```bash
# 1. Clone this template
git clone https://github.com/NBDatsuya/coding-agents-template.git your-project
cd your-project

# 2. Remove git history (start fresh)
rm -rf .git
git init

# 3. Customize for your project
# Edit AGENTS.md — fill in your tech stack, naming conventions, etc.
```

### For Existing Projects

```bash
# Copy just the AGENTS.md file
curl -O https://raw.githubusercontent.com/NBDatsuya/coding-agents-template/main/AGENTS.md
```

The AI agent will automatically read `AGENTS.md` when working in your project.

### Next Steps

1. **Fill in the Tech Stack** section in `CODEBASE_STATE.md`
2. **Define naming conventions** for your project in `AGENTS.md`
3. **Configure state management** rules in `CODEBASE_STATE.md`
4. **Set API conventions** if applicable in `CODEBASE_STATE.md`
5. **Note known issues or fixes** in `docs/TROUBLESHOOTING.md`

---

## Customization

### 1. Tech Stack

Update the **Tech Stack** table in `CODEBASE_STATE.md`:

```markdown
## 2. Tech Stack

| Layer        | Choice | Notes |
|------------|--------|-------|
| UI framework | Vue 3 | SFCs with Composition API |
| Language     | TypeScript | Strict mode, no `any` |
| Bundler      | Vite 5 | `@` → `./src` |
| Styling      | Tailwind CSS | Utility-first |
| State        | Pinia | With persistence |
| HTTP Client  | Axios | With interceptors |
```

### 2. Naming Conventions

Define your project's naming standards in `AGENTS.md`:

```markdown
## 6. Naming Conventions

- **Files**: `kebab-case` (e.g., `user-profile.vue`)
- **Components**: `PascalCase` (e.g., `UserProfile`)
- **Routes**: `kebab-case` (e.g., `/user/profile`)
- **Route names**: `PascalCase` (e.g., `UserProfile`)
- **Stores**: `camelCase` with `use` prefix (e.g., `useUserStore`)
```

### 3. Code Standards

Set quality rules in `AGENTS.md`:

```markdown
## 3. Code Standards

### TypeScript Basics

- No `var` — use `const` and `let`
- No `any` — use `unknown` + narrowing
- All props and emits must be typed

### Component Rules

- Components render UI only — no business logic
- All API calls go through services
- Cross-component state goes in stores
```

### 4. State Management

Document your state approach in `CODEBASE_STATE.md`:

```markdown
## 12. State Management

Stores are in `src/store/`:

- **Pinia** for cross-component state
- **Vue reactive** for component-local state
- **Persisted** via `pinia-plugin-persistedstate`
```

---

## Multi-Agent Workflow

When multiple AI agents collaborate, follow these protocols:

### 1. Read Before Write

Before starting any feature:

```
- [ ] Read AGENTS.md §0–§7
- [ ] Check CODEBASE_STATE.md's Directory Map for existing work
- [ ] Check docs/WIP.md for claimed areas
```

### 2. Claim Ownership

When working on a multi-turn feature:

```
Starting work on [feature-name]. Claiming a WIP row in docs/WIP.md for [feature].
```

This prevents other agents from working on the same area.

### 3. Document on Commit

When the user asks for a commit:

```
- Update CHANGELOG
- Add a Decision Log row in CODEBASE_STATE.md if needed
- Update CODEBASE_STATE.md's Directory Map if structure changed
```

### 4. Conflict Resolution

| Situation | Rule |
|-----------|------|
| Namespace collision | Check registry first; no silent renames |
| Deleted code | Move to strikethrough, don't remove |
| Doc vs Code | Code wins — docs follow code |

---

## Tech Stack Templates

This repository contains templates for different technologies:

| Stack | Location | Features |
|-------|----------|----------|
| **Vue 3** | `./templates/vue3/` | Vue 3 + TypeScript + Vite + Pinia + PrimeVue |
| **React** | `./templates/react/` | 🔜 Coming soon |
| **Svelte** | `./templates/svelte/` | 🔜 Coming soon |
| **Node.js** | `./templates/nodejs/` | 🔜 Coming soon |

### Using a Tech Stack Template

```bash
# Clone the full repo
git clone https://github.com/NBDatsuya/coding-agents-template.git
cd coding-agents-template

# Copy a specific template
cp -r templates/vue3 /path/to/your-project/
```

---

## Tools & Integrations

### Claude Code

This template is designed for Claude Code. The agent will:

1. Read `AGENTS.md` at project start
2. Follow conventions in §0–§7
3. Update `CODEBASE_STATE.md` only when asked
4. Respect WIP claims from other agents

### Cursor

Add to `.cursor/rules/`:

```
@import: ../AGENTS.md
```

### GitHub Copilot

Create `.cursorrules`:

```
# AI Agent Conventions

Follow the rules in AGENTS.md for this project.
```

---

## Contributing

Have a template to share? PRs welcome!

### Adding a New Template

1. Create a folder under `templates/`
2. Add `AGENTS.md` customized for that stack
3. Include any tech-specific conventions
4. Update this README with your template

### Template Structure

```
templates/
└── your-template/
    ├── AGENTS.md          # Required
    ├── README.md          # Optional
    └── example/           # Optional example code
```

---

## FAQ

### Q: Do I need all sections in AGENTS.md?

**A:** No. Only fill in what's relevant to your project. The template is modular.

### Q: Can I use this with GitHub Copilot?

**A:** Yes. Create a `.cursorrules` file referencing AGENTS.md.

### Q: How do I update conventions mid-project?

**A:** Edit AGENTS.md directly. Changes take effect immediately for new AI agent sessions.

### Q: What about security-sensitive conventions?

**A:** Add them to AGENTS.md with clear labels. The AI agent will respect them.

---

## License

MIT — Use freely, modify as needed, no attribution required.
