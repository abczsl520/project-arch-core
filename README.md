# project-arch-core

**Language-agnostic project architecture principles for AI-assisted development.**

Keep every file small enough for AI agents to read and edit without blowing the context window. This is the shared foundation — language-specific skills build on top.

## Core Principles

1. **Source file ≤ 400 lines** / entry ≤ 100 / templates ≤ 200
2. **Entry point = wiring only** — init, mount, listen. No logic.
3. **Config externalization** — tunable values in config files, hot-reloadable
4. **Layered separation** — Interface → Logic → Data (adapts to web/CLI/worker/desktop)
5. **Observability** — admin dashboard for web services; logging for CLIs
6. **Frontend splitting** — HTML skeleton + separate JS/CSS

📖 Full details in [SKILL.md](SKILL.md) | Splitting decision flow in [references/splitting-guide.md](references/splitting-guide.md)

## When to Apply / When NOT to

✅ Web services, APIs, full-stack apps with 500+ lines total, AI hitting context limits

❌ Scripts under 200 lines, prototypes, frameworks with strong conventions (follow the framework first), pure libraries

## Language-Specific Skills

| Language/Framework | Skill | Status |
|-------------------|-------|--------|
| **Node.js** (Express, H5 Games, Data Tools) | [nodejs-project-arch](https://github.com/abczsl520/nodejs-project-arch) | ✅ Available |
| **React** / Next.js | `react-project-arch` | 🔲 Planned |
| **Python** (FastAPI/Flask/Django) | `python-project-arch` | 🔲 Community welcome |
| **Go** | `go-project-arch` | 🔲 Community welcome |

## Installation

```bash
git clone https://github.com/abczsl520/project-arch-core.git
cp -r project-arch-core ~/.agents/skills/
```

## Contributing a Language Skill

Create a `<lang>-project-arch` skill with: concrete directory structures, entry point patterns, config loading + hot-reload, splitting rules table, and project type references.

See [nodejs-project-arch](https://github.com/abczsl520/nodejs-project-arch) as the reference implementation.

## License

MIT
