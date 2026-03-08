# Splitting Decision Guide

Language-agnostic guide for deciding when and how to split files.

## Quick Token Estimate

Before deciding, estimate how much context a file eats:

```
Tokens ≈ lines × 13   (average for code files)
Context % ≈ tokens / 200,000 × 100
```

| Lines | ~Tokens | Context % | Verdict |
|-------|---------|-----------|---------|
| 100 | 1.3K | 0.7% | ✅ Fine |
| 200 | 2.6K | 1.3% | ✅ Fine |
| 400 | 5.2K | 2.6% | ⚠️ Limit |
| 800 | 10.4K | 5.2% | ❌ Split |
| 2000 | 26K | 13% | 🔥 Urgent |

Rule of thumb: if reading one file costs >3% of context, split it.

## Step 1: Should I Split?

```
File > 400 lines (or >3% context)?
  ├─ YES → Split (proceed to Step 2)
  └─ NO
      ├─ File has 3+ unrelated responsibilities? → Split
      ├─ AI agent struggling to edit accurately? → Split
      └─ Otherwise → Leave it alone
```

**Don't split if:**
- File is under 200 lines and cohesive
- You're in prototype/POC phase (split when stabilizing)
- The framework expects a single file (e.g., migration files, config files)

## Step 2: Find the Boundaries

Look for these natural split points (in priority order):

### 2a. By Responsibility
The strongest signal. Ask: "If I describe what this code does, do I use the word 'and'?"

- "This file handles **auth** and **game logic** and **admin**" → 3 files
- "This file renders the **game board**" → 1 file, leave it

### 2b. By Dependency Direction
Code that depends on nothing else → extract first (utilities, config, constants).
Code that everything depends on → keep stable, extract into its own module.

### 2c. By Change Frequency
Code that changes every sprint vs. code that hasn't changed in months → separate files.
Stable code gets fewer AI reads = fewer wasted tokens.

### 2d. By Audience
Admin-only code vs. user-facing code → separate files.
Server-only vs. client-shared → separate files.

## Step 3: Name and Place

| What you extracted | Suggested location | Naming |
|---|---|---|
| HTTP handlers | `routes/` or `handlers/` or `controllers/` | By domain: `auth`, `user`, `game`, `admin` |
| Business logic | `services/` or `lib/` | By capability: `crawler`, `parser`, `notifier` |
| Data access | `db/` or `models/` or `data/` | By entity: `user`, `order`, `config` |
| Shared utilities | `utils/` or `helpers/` | By type: `format`, `validate`, `crypto` |
| Config/constants | Root or `config/` | `config.json`, `constants.js` |
| Frontend JS | `public/js/` or `src/` | By responsibility: `app`, `api`, `table`, `chart` |

## Step 4: Verify the Split

After splitting, check:

- [ ] **Each file ≤ 400 lines** (entry ≤ 100, templates ≤ 200)
- [ ] **No circular imports** — if A imports B and B imports A, extract shared code to C
- [ ] **Entry point is wiring only** — no business logic leaked back in
- [ ] **Config values externalized** — no magic numbers or hardcoded strings
- [ ] **It still works** — run the project, hit the main flows
- [ ] **AI can read any single file** and understand its purpose without reading others

## Anti-Patterns

| ❌ Don't | ✅ Do Instead |
|----------|--------------|
| Split a 150-line cohesive file into 3 tiny files | Leave it — small and focused is fine |
| Create `utils.js` as a dumping ground for everything | Split utils by type: `format.js`, `validate.js` |
| One function per file | Group related functions (same domain/responsibility) |
| Split mid-prototype | Finish the feature, then split when stabilizing |
| Rename everything during a split | Split first, rename in a separate step |
