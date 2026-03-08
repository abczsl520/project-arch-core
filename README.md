# project-arch-core

**Language-agnostic project architecture principles for AI-assisted development.**

A foundation skill that defines universal rules for keeping codebases AI-friendly. Language-specific skills (Node.js, React, Python, etc.) build on top of these principles.

## 🧠 Core Principles

1. **Single file ≤ 400 lines** — AI context stays manageable
2. **Entry point ≤ 100 lines** — wiring only, zero business logic
3. **Config externalization** — all tunable values in config files, hot-reloadable
4. **Layered separation** — Entry → Routes → Services → Data
5. **Admin dashboard** — every project gets config editor + stats
6. **Frontend splitting** — HTML skeleton + separate JS/CSS files

## 📊 Why?

| Scenario | Tokens per read | Context usage (200K) |
|----------|----------------|---------------------|
| 3000-line monolith | ~40K | 20% |
| 200-line module | ~2.7K | 1.3% |

**Result:** 10-15 productive AI rounds vs 3-5 with monolithic files.

## 🌐 Language-Specific Skills

This is the **foundation**. For concrete patterns, use the language-specific skill:

| Language/Framework | Skill | Status |
|-------------------|-------|--------|
| **Node.js** (Express, H5 Games, Data Tools) | [nodejs-project-arch](https://github.com/abczsl520/nodejs-project-arch) | ✅ Available |
| **React** / Next.js | `react-project-arch` | 🔲 Planned |
| **Python** (FastAPI/Flask/Django) | `python-project-arch` | 🔲 Community welcome |
| **Go** | `go-project-arch` | 🔲 Community welcome |

## 🚀 Installation

```bash
# Clone
git clone https://github.com/abczsl520/project-arch-core.git
cp -r project-arch-core ~/.agents/skills/

# Or with clawhub (when published):
# clawhub install project-arch-core
```

## 🤝 Contributing a Language Skill

Want to add support for your language? Create a `<lang>-project-arch` skill that:

1. References these core principles
2. Provides concrete, copy-pasteable directory structures
3. Includes language-idiomatic config loading + hot-reload patterns
4. Has a splitting rules table ("monolith → modules" with max lines)
5. Covers common project types for that ecosystem

See [nodejs-project-arch](https://github.com/abczsl520/nodejs-project-arch) as the reference implementation.

## License

MIT
