# CODEBASE_STATE.md

> Living map of everything that currently exists in the project — tech stack, architecture, and generated registries. Facts here are _project state_, not agent behavior; agent rules live in [`AGENTS.md`](./AGENTS.md).
>
> **Independent numbering.** Sections below use their own `1.`, `2.`, `3.` sequence. They do not share `AGENTS.md`'s `§` numbering — don't cross-reference a `§` number from this file into `AGENTS.md` or vice versa; use section titles instead.
>
> Edited only in a user-initiated pre-commit sync (see `AGENTS.md` §0). Read freely at any other time.

---

## 1. Directory Map

> TODO: Document the top-level directory structure here (folder-level only, not every file).

```text
src/
├── components/   # TODO
├── pages/        # TODO
├── router/       # TODO
├── store/        # TODO
├── services/     # TODO
└── ...
```

---

## 2. Tech Stack

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

**Do not add new top-level dependencies without appending a Decision Log row (§14).**

> Eg.(DELETE WHEN IMPLEMENTING)
>
> | Layer | Choice | Notes |
> | --- | --- | --- |
> | UI framework | Vue 3 SFC, `<script setup lang="ts">` | No Options API |
> | Language | Strict TypeScript | `any` is forbidden |
> | Bundler | Vite 5 | `@` alias → `./src` (see `vite.config.ts`) |
> | UI Component Library | PrimeVue 4 | `@primevue/themes` for theming |
> | Styling | Tailwind CSS 3 + `tailwindcss-primeui` | Atomic-first; see §10 |
> | Routing | `vue-router@4` with `createWebHistory` | Routes in `src/router/` |
> | State | Pinia (+ `pinia-plugin-persistedstate`) | Stores in `src/store/` |
> | HTTP Client | Axios | Configured in `src/request/axios/` |
> | Maps | `vue3-baidu-map-gl` | Baidu Maps Vue 3 wrapper |
> | Charts | Chart.js | Data visualization |
> | Icons | PrimeIcons | Included with PrimeVue |
> | Date Utils | dayjs | Lightweight date handling |
> | i18n | primelocale | Chinese localization |

---

## 3. Architecture Overview

> TODO: Document your project architecture here. If a diagram is needed, use a **Mermaid** code block (not ASCII art) so it renders on GitHub/GitLab and stays easy to edit.

> Eg.(DELETE WHEN IMPLEMENTING)
>
> ```mermaid
> flowchart TB
>     A["Vue SPA (router + layout)<br/>Pages: home, login, device management, station, etc.<br/>Layouts: main (sidebar + header), blank (login)"]
>     B[Backend API Server]
>     A -->|"HTTP Request (Axios)"| B
>     B -->|Response| A
> ```
>
> - **Vue owns**: routing, layouts, pages, components, state management
> - **Pinia stores**: user auth, dict cache, device status drafts, geo info
> - **Axios**: HTTP request handling with interceptors
> - **PrimeVue**: UI component library with custom theme

---

## 4. Routes

> TODO: Registry of route paths and route names. Check here before adding a new route to avoid collisions.

| Path | Name | Component | Notes |
| ---- | ---- | --------- | ----- |
|      |      |           |       |

---

## 5. Components

> TODO: Registry of shared/reusable components (not every page-local component).

| Component | Location | Purpose |
| --------- | -------- | ------- |
|           |          |         |

---

## 6. Services

> TODO: Registry of API service modules.

| Service | Location | Endpoints covered |
| ------- | -------- | ------------------ |
|         |          |                     |

---

## 7. Stores

> TODO: Registry of state stores.

| Store | Location | Purpose |
| ----- | -------- | ------- |
|       |          |         |

---

## 8. Permissions

> TODO: Registry of permission keys / roles, if the project has an authorization model.

| Key | Description |
| --- | ------------ |
|     |              |

---

## 9. Types

> TODO: Registry of shared/global TypeScript types (not component-local types).

| Type | Location | Purpose |
| ---- | -------- | ------- |
|      |          |         |

---

## 10. CSS Conventions

> TODO: Document CSS conventions for your project.

- Use utility classes or component-scoped styles as per project conventions.
- Follow BEM naming for custom class names when needed.
- Keep styles modular and maintainable.

---

## 11. API Conventions

> TODO: Document API conventions for your project.

All API calls go through services in the services directory.

Example API prefixes:

- `/api/v1/` - Public query interfaces
- `/api/admin/` - Admin operation interfaces

---

## 12. State Management

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

## 13. Environment Variables

Environment variables are defined in `.env` files and referenced in the configuration.

> TODO: Document your environment variable conventions.
> Eg. `src/properties/env.ts` and `.env`. (DELETE THIS LINE WHEN IMPLEMENTING)

---

## 14. Decision Log

> Non-obvious trade-offs: dependency swaps, architecture changes, new tooling. Append a row per decision; never silently re-decide a past entry — raise it in chat first if a new approach contradicts one.

| Date | Decision | Why | Alternatives considered |
| ---- | -------- | --- | ------------------------ |
|      |          |     |                          |
