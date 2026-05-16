# AGENTS.md

> Project conventions and shared codebase state for AI coding agents on [project_name].
>
> **Multi-agent source of truth.** Sections 1–12 are the _rules_. Section **13 (Codebase State)** is the _living map_ of everything that currently exists in the project.
>
> You **must** write in English only in AGENTS.md.

---

## 0. Multi-agent Collaboration Protocol

### Doc Edit Policy (read this first)

- **Do NOT modify `CODEBASE_STATE.md` during feature work.** Finish the code. Do not bump `Last updated` dates, do not append to §13.9 / §13.10 / §14, do not move "WIP" rows — not as part of the same turn you wrote the code.
- **`CODEBASE_STATE.md` is edited only when the user explicitly asks**, typically right before they request a commit. Common phrasings that unlock doc edits: _"update the codebase state"_, _"sync the codebase state"_, _"prep for commit"_, _"fill in the change log"_. Without an explicit request, leave the doc alone.
- **When the user does ask**, batch all deferred updates from the session into one coherent edit in `CODEBASE_STATE.md` (see "Pre-commit doc sync" below). Still respect the other rules in this section (decision log rows for non-obvious trade-offs, etc.).
- **`AGENTS.md` (this file) changes only when the user asks to change a rule.** Feature work never touches it.

### Git Commit Policy

- **All commit messages must be in English.** This includes subject line and body if any.
- Use conventional commit format: `type(scope): description`
  - Types: `feat`, `fix`, `refactor`, `style`, `docs`, `chore`, etc.
  - Scope: optional, e.g., `(component)`, `(api)`, `(ui)`, etc.
  - Description: imperative mood, lowercase, no period at end
- When the user asks for a commit, **confirm the commit message and scope with the user** before executing.
- Examples:
  - `feat(auth): add login page`
  - `fix: resolve data fetch bug`
  - `docs: update README`

### The Contract

1. **Before coding**, skim §1–§12 once per session, then read `CODEBASE_STATE.md` §13.1 and §16 (WIP claims) for anything relevant to your task.
2. **While coding**, the canonical _registry_ of names is the code itself. Before adding a new key, confirm it doesn't exist in the relevant file — don't rely on docs for this.
3. **After coding**, **do not edit any docs.** Keep a short mental (or scratchpad) list of what would need to change in §13.10 / §14 so you can produce a clean batch when the user asks.
4. **Pre-commit doc sync (user-initiated only).** When the user explicitly asks to update the codebase state, do all of:
   - Append a single-line entry to §14 (Change Log) per coherent change, newest at the top, with date prefix.
   - If any change introduced a non-obvious trade-off (dependency swap, architecture change, new tooling, etc.), add a row to §13.10 (Decision Log). Never silently re-decide past choices.
   - If §13.1 (directory map) drifted at the _folder_ level, update it. Don't enumerate individual new files.
   - Update §16 (WIP) if the work claimed a multi-turn area: strikethrough the row when done.

### Conflict-avoidance Rules

- **Namespaces are unique.** Route paths, store names, service names, and component names must be unique globally. Check §13.2 / §13.4 / §13.5 / §13.6 before adding.
- **One owner per feature.** When you start a multi-turn feature, note it in chat so other agents know you're claiming that area. The §16 WIP row lands during the next user-initiated doc sync.
- **Code wins, doc follows.** `CODEBASE_STATE.md` is human-curated history; if it ever conflicts with the code, the code is right.
- **No silent deletes.** If you delete code, move the registry row to a `~~strikethrough~~` line at the end of the table rather than removing it.
- **Atomic doc updates.** One feature → one coherent §13.10 / §14 edit at commit time. Don't batch unrelated refactors into the same doc patch.

### Read-before-write Checklist (copy into your plan)

- [ ] Confirm the feature area in `CODEBASE_STATE.md` §13.1 and §16 (WIP).
- [ ] Grep relevant files for any new key you plan to add — confirm no collision.
- [ ] If a relevant decision exists in §13.10, follow it; if your approach contradicts one, raise it in chat before re-deciding.
- [ ] Remember: do NOT edit `CODEBASE_STATE.md` or `AGENTS.md` in this turn. Save doc updates for when the user asks.

---

## 1. Role & Context

You are a smart AI developer proficient in **modern frontend development**. The mission is maintaining and extending this web application.

> TODO: Fill in project-specific context here.

> Eg.(DELETE WHEN IMPLEMENTING)
> You are a smart AI developer proficient in **Vue 3 (Composition API)**, **TypeScript**, **PrimeVue**, and **Tailwind CSS**. The mission is maintaining and extending the PROJECT, a Vue 3 + TypeScript + PrimeVue + Tailwind CSS application for PROJECT_PURPOSE.

---

## 2. Tech Stack (hard constraints)

> TODO: Document your project's tech stack here.

| Layer        | Choice | Notes |
| ------------ | ------ | ----- |
| UI framework |        |       |
| Language     |        |       |
| Bundler      |        |       |
| Styling      |        |       |
| Routing      |        |       |
| State        |        |       |
| HTTP Client  |        |       |
| Testing      |        |       |

**Do not add new top-level dependencies without appending a §13.10 decision log row.**

> Eg.(DELETE WHEN IMPLEMENTING)
>
> | Layer                | Choice                                  | Notes                                      |
> | -------------------- | --------------------------------------- | ------------------------------------------ |
> | UI framework         | Vue 3 SFC, `<script setup lang="ts">`   | No Options API                             |
> | Language             | Strict TypeScript                       | `any` is forbidden                         |
> | Bundler              | Vite 5                                  | `@` alias → `./src` (see `vite.config.ts`) |
> | UI Component Library | PrimeVue 4                              | `@primevue/themes` for theming             |
> | Styling              | Tailwind CSS 3 + `tailwindcss-primeui`  | Atomic-first; see §9                       |
> | Routing              | `vue-router@4` with `createWebHistory`  | Routes in `src/router/`                    |
> | State                | Pinia (+ `pinia-plugin-persistedstate`) | Stores in `src/store/`                     |
> | HTTP Client          | Axios                                   | Configured in `src/request/axios/`         |
> | Maps                 | `vue3-baidu-map-gl`                     | Baidu Maps Vue 3 wrapper                   |
> | Charts               | Chart.js                                | Data visualization                         |
> | Icons                | PrimeIcons                              | Included with PrimeVue                     |
> | Date Utils           | dayjs                                   | Lightweight date handling                  |
> | i18n                 | primelocale                             | Chinese localization                       |

---

## 3. Architecture Overview

> TODO: Document your project architecture here.

```
┌─────────────────────────────────────────┐
│              Frontend App               │
│                                         │
│  Components, Pages, Routing, State     │
└─────────────────────────────────────────┘
                    │
                    │ HTTP Request
                    ▼
             Backend API Server
```

> Eg.(DELETE WHEN IMPLEMENTING)
>
> ```
> ┌─────────────────────────────────────────────────────────┐
> │                    Vue SPA (router + layout)           │
> │                                                         │
> │  Pages: home, login, device management, station, etc.  │
> │  Layouts: main (sidebar + header), blank (login)       │
> └─────────────────────────────────────────────────────────┘
>            ▲                                    │
>            │         HTTP Request               │
>            │            (Axios)                 │
>            └────────────────────────────────────┘
>                           │
>                           ▼
>                    Backend API Server
> ```
>
> - **Vue owns**: routing, layouts, pages, components, state management
> - **Pinia stores**: user auth, dict cache, device status drafts, geo info
> - **Axios**: HTTP request handling with interceptors
> - **PrimeVue**: UI component library with custom theme
>
> For detailed directory structure, see `CODEBASE_STATE.md` §13.

---

## 4. Development Workflow

### Scope of Responsibilities

Current mode is limited to:

- **confirming** — clarify requirements before coding
- **coding** — feature implementation
- **boilerplating** — scaffolding and template code
- **first-glimpse review** — initial code review

Do not proactively refactor or optimize unrelated code.

### Operational Standards

- **Communicate before modifying**: Before changing existing files, inform the user what you're about to change.
- **Confirm dependencies**: Do not auto-install packages. List the required packages and wait for user confirmation.
- **Verification approach**: Let the user manually verify. Do not run dev/build/test for verification since HMR is assumed to be running.
- **Requirement clarification**: When requirements are unclear, ask before writing code.
- **Documentation sync**: After completing a workflow, update relevant documentation when user asks.

### Framework Integration Rules

> TODO: Fill in framework-specific rules here.

---

## 5. Code Standards

### TypeScript Basics

- **No `var`.** Always `const`, `let` only when reassignment is real.
- **No `any`.** Use `unknown` + narrowing, or define a real type.
- **Typed props and emits.** All props typed with TypeScript; all events typed.
- **Typed events.** When a payload becomes non-trivial, define a named type and use it at both ends.

### Component Rules

- **Strict UI separation.** Components render UI **only**. No business logic in component files except for component-local state.
- **Services are canonical.** All API calls go through services.
- **Stores for shared state.** Cross-component state goes in state management stores.

### Code Quality

- **No magic numbers.** Define constants with meaningful names.
- **Loop hygiene.** Avoid heavy logic in tight loops. Pre-compute when possible.
- **Modularity.** Separate concerns: data fetching, rendering, UI controls.
- **Consistent naming.** Follow §8 naming conventions.

---

## 6. Forbidden

- `var`.
- `any`. Use `unknown` + narrowing, or define a real type.
- Direct DOM manipulation outside the framework's reactivity system.
- Unnamed magic numbers scattered in code.
- Blocking operations on the main thread.
- **Running the project / opening any file yourself after finishing a task — the user runs it.** (Exception: the user may **explicitly** ask you to start the dev server; when they do, run it in the background so the tool call doesn't block.)
- Adding new dependencies without a §13.10 decision entry.
- Silent renames of exported symbols, route names, store names, or API endpoints.
- Auto-installing packages without user confirmation.

---

## 7. Interaction Protocol

- Before adding a feature, check anything listed in §16 (WIP) to ensure no conflicts.
- When the human describes a **visual or interaction requirement**, translate it directly into implementation — CSS classes, composable logic, component props — don't over-engineer.
- When asked to research or explain, do not edit code.
- When asked to implement, follow the Read-before-write checklist in §0.

### Skills (domain knowledge documents)

`.agents/skills/` contains reusable domain knowledge and operational guides. Agents do **not** auto-load these files — read them **on demand** based on task context.

| Trigger | Skill file | Description |
| ------- | ---------- | ----------- |
| TODO    |            |             |

**Rules:**

- When adding a new skill, create the file under `.agents/skills/<domain>/` and register a trigger row in this table.
- Skill files may include YAML frontmatter (`name` / `description`) for future tooling.
- A task may match multiple skills — read all matching ones before writing code.

---

## 8. Naming Conventions

> TODO: Document naming conventions for your project.

- **Files**: `kebab-case` (e.g. `user-profile.vue`, `api-service.ts`).
- **Components**: `PascalCase` with optional prefix (e.g. `UserProfile`, `BaseButton`).
- **Routes**: `kebab-case` (e.g. `/user/profile`).
- **Route names**: `PascalCase` (e.g. `UserProfile`).
- **Stores**: `camelCase` with `use` prefix (e.g. `useUserStore`).
- **Services**: `kebab-case` (e.g. `user-api.ts`).
- **Constants**: `UPPER_SNAKE_CASE` inside `as const` objects.

---

## 9. CSS

> TODO: Document CSS conventions for your project.

- Use utility classes or component-scoped styles as per project conventions.
- Follow BEM naming for custom class names when needed.
- Keep styles modular and maintainable.

---

## 10. API Conventions

> TODO: Document API conventions for your project.

All API calls go through services in the services directory.

Example API prefixes:

- `/api/v1/` - Public query interfaces
- `/api/admin/` - Admin operation interfaces

---

## 11. State Management

> TODO: Document state management approach for your project.

Stores are in the store directory.

- Use framework-specific state management (Pinia, Vuex, Zustand, Redux, etc.)
- **When to use global state**: cross-component or cross-page state that must persist or be shared.
- **When to use local state**: local UI state that doesn't need sharing.

> Eg.(DELETE WHEN IMPLEMENTING)
>
> Stores are in `src/store/`:
>
> All stores use `pinia-plugin-persistedstate` for persistence.
>
> - **Pinia**: installed and mounted (`src/main.ts`), persisted-state plugin enabled.
> - **Vue reactive**: in-component `ref` / `reactive` only (no shared reactive singletons outside Pinia).
> - **When to use Pinia**: cross-component or cross-page state that must persist or be shared.
> - **When to use component state**: local UI state that doesn't need sharing.

---

## 12. Environment Variables

Environment variables are defined in `.env` files and referenced in the configuration.

> TODO: Document your environment variable conventions.
> Eg. `src/properties/env.ts` and `.env`. (DELETE THIS LINE WHEN IMPLEMENTING)

---

## 13. Troubleshooting

> TODO: Add common troubleshooting steps for your project or link to a specified file.

---

## 14. Codebase State

[`CODEBASE_STATE.md`](./CODEBASE_STATE.md) at the repo root holds the project's _history_: §13.1 directory map, §13.2 routes, §13.3 components, §13.4 services, §13.5 stores, §13.6 permissions, §13.7 types, §13.9 WIP claims, §13.10 decision log, §14 change log.

Read the sibling freely; edit it only in a user-initiated pre-commit sync per §0.

---

## 15. Change Log

See [`CHANGELOG`](./CHANGELOG) for the per-change history.

---

## 16. WIP

See [`docs/WIP.md`](./docs/WIP.md) for reference.
