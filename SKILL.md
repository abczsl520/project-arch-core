---
name: project-arch-core
description: Language-agnostic project architecture principles for AI-assisted development. Enforces file splitting (<400 lines), config externalization, entry-point minimalism, layered separation, and admin dashboards. Use as a foundation when no language-specific arch skill exists, or when creating new arch skills for other languages/frameworks.
---

# Project Architecture Core — AI-Friendly Development

Language-agnostic architecture principles that keep codebases small enough for AI agents to read and edit efficiently.

## Core Principles

These apply to **any** language or framework:

### 1. File Size Limits
- **Source file ≤ 400 lines** — beyond this, AI context usage spikes and edit accuracy drops
- **Entry point ≤ 100 lines** — only wiring/mounting, zero business logic
- **HTML templates ≤ 200 lines** — skeleton only, logic in separate files

### 2. Entry Point = Wiring Only
The main entry file does exactly three things:
1. Initialize dependencies (DB, middleware, plugins)
2. Mount routes / register handlers
3. Start listening

No business logic, no route handlers, no data processing.

### 3. Config Externalization
- All tunable values in a config file (`config.json`, `.env`, `config.yaml`, etc.)
- Loaded at runtime, never hardcoded
- Admin-editable without code changes or restarts (hot-reload preferred)
- Secrets stripped before exposing to frontend/clients

### 4. Layered Separation
```
Entry (wiring) → Routes/Handlers (HTTP) → Services (logic) → Data (DB/API)
```
- **Routes/Handlers**: request parsing, validation, response formatting
- **Services**: reusable business logic, shared across routes
- **Data**: database queries, external API calls, file I/O

### 5. Admin Dashboard
Every project gets an admin interface:
- Auth-protected config editor with hot-reload
- Runtime stats (uptime, memory, request counts)
- Key business metrics
- Operation log

### 6. Frontend Splitting
- HTML = structure only (no inline JS/CSS beyond minimal bootstrap)
- CSS in separate files
- JS split by responsibility (each ≤ 400 lines)

## Why This Matters for AI

| Scenario | Tokens per read | Context usage (200K) |
|----------|----------------|---------------------|
| 3000-line monolith | ~40K | 20% |
| 200-line module | ~2.7K | 1.3% |

Splitting files → **10-15 productive AI rounds** vs 3-5 with monoliths. **70-93% token savings** per file read.

## Language-Specific Skills

This skill provides the universal foundation. For concrete directory structures, code patterns, and framework-specific rules, use the appropriate language skill:

| Language/Framework | Skill | Status |
|-------------------|-------|--------|
| Node.js (Express) | [nodejs-project-arch](https://github.com/abczsl520/nodejs-project-arch) | ✅ Available |
| React / Next.js | `react-project-arch` | 🔲 Planned |
| Python (FastAPI/Flask) | `python-project-arch` | 🔲 Community welcome |
| Go | `go-project-arch` | 🔲 Community welcome |

## Creating a New Language Skill

If you're building a `<lang>-project-arch` skill, follow these core principles and add:

1. **Concrete directory structure** — not abstract, copy-pasteable
2. **Entry point pattern** — actual code showing wiring-only entry
3. **Config pattern** — language-idiomatic config loading + hot-reload
4. **Splitting rules table** — "this monolith → these modules" with max lines
5. **Project type references** — separate files for different project types (game/tool/API/etc.)

Keep the same naming convention: `<lang>-project-arch` with `references/` subdirectory.
