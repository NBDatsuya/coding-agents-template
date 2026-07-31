# AGENTS.md

> Behavior rules for AI coding agents on [project_name]. Project facts (tech stack, architecture, conventions) live in `CODEBASE_STATE.md` — see §7.
>
> You **must** write in English only in AGENTS.md.

---

## 0. Multi-agent Collaboration Protocol

### Doc Edit Policy (read this first)

- **Do NOT modify `CODEBASE_STATE.md` during feature work.** Finish the code first. Do not bump "Last updated" dates, do not touch the Decision Log, do not move WIP rows in `docs/WIP.md` — not as part of the same turn you wrote the code.
- **`CODEBASE_STATE.md` is edited only when the user explicitly asks**, typically right before they request a commit. Common phrasings that unlock doc edits: _"update the codebase state"_, _"sync the codebase state"_, _"prep for commit"_, _"fill in the change log"_. Without an explicit request, leave the doc alone.
- **After finishing any add / modify / delete coding task, ask the user** whether they want `CHANGELOG`, `CODEBASE_STATE.md`, and/or a git commit updated now. Don't do these silently, and don't just wait passively either — surface the question so the user can decide.
- **When the user does ask**, batch all deferred updates from the session into one coherent edit in `CODEBASE_STATE.md` (see "Pre-commit doc sync" below). Still respect the other rules in this section (Decision Log rows for non-obvious trade-offs, etc.).
- **`AGENTS.md` (this file) changes only when the user asks to change a rule.** Feature work never touches it.

### Git Commit Policy

- **All commit messages must be in English.** This includes subject line and body if any.
- Use conventional commit format: `type(scope): description`
  - Types: `feat`, `fix`, `refactor`, `style`, `docs`, `chore`, etc.
  - Scope: optional, e.g., `(component)`, `(api)`, `(ui)`, etc.
  - Description: imperative mood, lowercase, no period at end
- **Never add co-author trailers** (e.g. `Co-authored-by: ...`) to commit messages.
- When the user asks for a commit, **confirm the commit message and scope with the user** before executing.
- Examples:
  - `feat(auth): add login page`
  - `fix: resolve data fetch bug`
  - `docs: update README`
- **Atomic commits.** Each commit must represent one cohesive, self-contained logical change. Do not bundle unrelated fixes, refactors, or features into the same commit. Split changes when they touch multiple independent areas.

### The Contract

1. **Before coding**, skim §1–§6 once per session, then read `CODEBASE_STATE.md`'s Directory Map and `docs/WIP.md` for anything relevant to your task.
2. **While coding**, the canonical _registry_ of names is the code itself. Before adding a new key, confirm it doesn't exist in the relevant file — don't rely on docs for this.
3. **After coding**, **do not edit any docs.** Keep a short mental (or scratchpad) list of what would need to change in `CODEBASE_STATE.md` / `CHANGELOG` so you can produce a clean batch when the user asks — then ask (per §0 above).
4. **Pre-commit doc sync (user-initiated only).** When the user explicitly asks to update the codebase state, do all of:
   - Append a single-line entry to `CHANGELOG` per coherent change, newest at the top, following [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) format with a `YYYY-MM-DD HH:MM` timestamp prefix (see the file's own header). (Create the file on first use if it doesn't exist yet.)
   - If any change introduced a non-obvious trade-off (dependency swap, architecture change, new tooling, etc.), add a row to `CODEBASE_STATE.md`'s Decision Log. Never silently re-decide past choices.
   - If the Directory Map drifted at the _folder_ level, update it. Don't enumerate individual new files.
   - Update `docs/WIP.md` if the work claimed a multi-turn area: strikethrough the row when done. (Create the file on first use if it doesn't exist yet.)

### Conflict-avoidance Rules

- **Namespaces are unique.** Route paths, store names, service names, and component names must be unique globally. Check the relevant `CODEBASE_STATE.md` registry section before adding.
- **One owner per feature.** When you start a multi-turn feature, note it in chat so other agents know you're claiming that area. The `docs/WIP.md` row lands during the next user-initiated doc sync.
- **Code wins, doc follows.** `CODEBASE_STATE.md` is human-curated history; if it ever conflicts with the code, the code is right.
- **No silent deletes.** If you delete code, move the registry row to a `~~strikethrough~~` line at the end of the table rather than removing it.
- **Atomic doc updates.** One feature → one coherent Decision Log / Change Log edit at commit time. Don't batch unrelated refactors into the same doc patch.

### Read-before-write Checklist (copy into your plan)

- [ ] Confirm the feature area in `CODEBASE_STATE.md`'s Directory Map and `docs/WIP.md`.
- [ ] Grep relevant files for any new key you plan to add — confirm no collision.
- [ ] If a relevant decision exists in the Decision Log, follow it; if your approach contradicts one, raise it in chat before re-deciding.
- [ ] Remember: do NOT edit `CODEBASE_STATE.md` or `AGENTS.md` in this turn. Save doc updates for when the user asks.

---

## 1. Role & Context

You are a smart AI developer proficient in **modern frontend development**. The mission is maintaining and extending this web application.

> TODO: Fill in project-specific context here.

> Eg.(DELETE WHEN IMPLEMENTING)
> You are a smart AI developer proficient in **Vue 3 (Composition API)**, **TypeScript**, **PrimeVue**, and **Tailwind CSS**. The mission is maintaining and extending the PROJECT, a Vue 3 + TypeScript + PrimeVue + Tailwind CSS application for PROJECT_PURPOSE.

---

## 2. Development Workflow

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
- **Documentation sync**: See §0's proactive-ask rule — offer to sync docs and commit after finishing a coding task, don't wait to be asked and don't do it silently.

### Framework Integration Rules

> TODO: Fill in framework-specific rules here.

---

## 3. Code Standards

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
- **Consistent naming.** Follow §6 naming conventions.

### TypeScript Iteration Conventions

- **Array iteration.** Prefer chainable methods (`forEach`, `map`, `filter`, `reduce`, `some`, `every`, etc.) over raw `for` loops unless performance is critical in hot paths. Chainable methods express intent more clearly and reduce mutative side effects.
- **Object iteration.** Prefer `Object.entries()` combined with array methods over `for...in` loops. Avoid `for...in` due to prototype chain pitfalls; use `Object.keys()` or `Object.entries()` with explicit type guards when needed.
- **Plain `for` loops.** Only use when you need to break early, need index arithmetic, or are in a performance-sensitive section. Document the reason if it's not obvious.

---

## 4. Forbidden

- `var`.
- `any`. Use `unknown` + narrowing, or define a real type.
- Direct DOM manipulation outside the framework's reactivity system.
- Unnamed magic numbers scattered in code.
- Blocking operations on the main thread.
- **Running the project / opening any file / running builds yourself after finishing a task — the user runs it.** (Exception: the user may **explicitly** ask you to start the dev server; when they do, run it in the background so the tool call doesn't block. And short-time linters and type-check-only commands such as vue-tsc or lint checks are also acceptable.)
- Adding new dependencies without a Decision Log entry in `CODEBASE_STATE.md`.
- Silent renames of exported symbols, route names, store names, or API endpoints.
- Auto-installing packages without user confirmation.
- Co-author trailers in commit messages.
- Read any config files (`.env`, `.yaml`, `.yml`, etc.) unless they are sample files with `.example` suffix (e.g., `.yaml.example`, `.env.example`).
- Compress any doc documents.

---

## 5. Interaction Protocol

- Before adding a feature, check `docs/WIP.md` to ensure no conflicts.
- When the human describes a **visual or interaction requirement**, translate it directly into implementation — CSS classes, composable logic, component props — don't over-engineer.
- When asked to research or explain, do not edit code.
- When asked to implement, follow the Read-before-write checklist in §0.

### Skills (Domain Knowledge Documents)

Skills are reusable domain-knowledge documents that agents load **on demand** using the `skill` tool (in Kilo Code) or by reading the file directly (in other agents). These files are stored under `.agents/skills/<domain>/SKILL.md`.

- The `.agents/skills/` directory contains reusable domain knowledge and operational guides. Agents do **not** auto-load these files — they should be read **on demand** based on the task context.
- A single task may match multiple skills. In such cases, load all relevant skills before writing any code.
- When adding a new skill, place the file under `.agents/skills/<domain>/` and ensure that the agent's skill registry (e.g., Kilo Code's `available_skills` configuration) includes a reference to it.

If a skill registry is not provided, fill in the table below:

| Trigger | Skill file | Description |
| ------- | ---------- | ----------- |
| TODO    |            |             |

**Rules:**

- When introducing a new skill, create the corresponding file under `.agents/skills/<domain>/` and add a trigger row to the table above.
- Skill files may include YAML frontmatter with `name` and `description` fields to support future tooling.
- A task may match multiple skills — be sure to read all matching skills before writing code.

---

## 6. Naming Conventions

> TODO: Document naming conventions for your project.

- **Files**: `kebab-case` (e.g. `user-profile.vue`, `api-service.ts`).
- **Components**: `PascalCase` with optional prefix (e.g. `UserProfile`, `BaseButton`).
- **Routes**: `kebab-case` (e.g. `/user/profile`).
- **Route names**: `PascalCase` (e.g. `UserProfile`).
- **Stores**: `camelCase` with `use` prefix (e.g. `useUserStore`).
- **Services**: `kebab-case` (e.g. `user-api.ts`).
- **Constants**: `UPPER_SNAKE_CASE` inside `as const` objects.

---

## 7. Documentation Map

This file covers agent _behavior_ only. Project _facts_ live elsewhere:

- [`CODEBASE_STATE.md`](./CODEBASE_STATE.md) — tech stack, architecture, directory map, routes, components, services, stores, permissions, types, CSS/API/state/env conventions, and the Decision Log. **Uses its own independent section numbering** — never shares this file's `§` sequence. If an architecture diagram is ever needed, use a Mermaid code block, not ASCII art. Read freely; edit only in a user-initiated pre-commit sync per §0.
- [`docs/TROUBLESHOOTING.md`](./docs/TROUBLESHOOTING.md) — known issues and their fixes.
- [`CHANGELOG`](./CHANGELOG) — per-change history, newest first, in [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) format with `YYYY-MM-DD HH:MM` timestamps. Created on first use.
- [`docs/WIP.md`](./docs/WIP.md) — claimed work-in-progress areas. Created on first use.
