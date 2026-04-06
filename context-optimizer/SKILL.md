---
name: context-optimizer
description: Analyze and optimize your Claude Code project context structure. Use when user says "CLAUDE.md too big", "optimize CLAUDE.md", "reorganize Claude Code project", "set up .claude/rules", "upgrade to Level 3", "split CLAUDE.md", "CLAUDE.md 太大", "整理 CLAUDE.md", "優化 CLAUDE.md", "Claude Code 文件太長", "設定 rules 目錄", "拆分 CLAUDE.md", "幫我整理 Claude 專案文件"
---

# Claude Context Optimizer

Upgrades a Claude Code project from Level 2 (single large CLAUDE.md) to Level 3 (modular rules + on-demand skills).
Based on the [5 Levels of Claude Code](https://codelove.tw/@tony/post/aWYABx) framework.

**Result:** fewer tokens consumed per session, higher rule compliance, clean separation between product docs and dev instructions.

---

## Before touching anything — ask first

When triggered, always ask the user:

> "I can help split your CLAUDE.md into a lean dev guide + `docs/` folder, and scaffold `.claude/rules/` and `.claude/skills/`. Want me to start with an analysis? (yes / no)"

Stop if they say no.

---

## Analysis

Run these to understand the current state:

```bash
wc -l CLAUDE.md 2>/dev/null || wc -l claude.md
find .claude -type f 2>/dev/null | sort
```

Then read CLAUDE.md and the project root. Identify:
- How many lines, and what % is non-dev content (product specs, business model, market research, competitor analysis)
- Whether `.claude/rules/` and `.claude/skills/` exist
- What tech stack the project uses (read package.json, go.mod, etc.)

Present the diagnosis and a proposed structure. **Show the full plan and wait for explicit confirmation (yes / no / customize) before making any changes.**

The proposed structure should follow the template in `templates/claude-md-template.md`.

---

## What to produce

Once the user confirms, the goal is:

**CLAUDE.md** — 50–120 lines. Dev instructions only. No product specs, no business model, no market research. See `templates/claude-md-template.md` for the target structure.

**`docs/{topic}.md`** — All non-dev content moved here. Nothing is deleted; everything is preserved.

**`.claude/rules/`** — Three starter files, filled with content read from the project's existing docs (not placeholder text):
- `product.md` — Non-obvious product constraints that affect how code is written (e.g. "reviews publish immediately, ACR runs in background", "24h dedup on point deduction")
- `tech-stack.md` — Stack table, key API endpoints, local dev setup commands
- `coding-style.md` — Code conventions, API response format, DB rules

**`.claude/skills/`** — 2–4 starter `SKILL.md` files based on what the project actually needs. Common patterns: research, qa-review, feature-plan, doc-sync. Each starter has frontmatter + a short workflow outline for the user to fill in.

---

## Constraints

- Never overwrite existing `.claude/rules/` files without asking
- Never run git commands or make commits
- Never modify `settings.json` or `settings.local.json`
- If CLAUDE.md is already ≤ 100 lines, say it looks healthy and offer only the skills scaffold
- Rules files must use content from the actual project — don't write generic placeholders
- After finishing, tell the user which files to review and customize

---

## Gotchas

- CLAUDE.md and claude.md are the same file on macOS (case-insensitive FS) — don't create both
- If `.claude/rules/` already has files, list them and ask before overwriting
- Skills scaffolds are starting points — tell the user explicitly that they need to fill in the workflow details
- Some projects keep their tech stack only in a README or a plan.md — read all root-level markdown before writing tech-stack.md
- A CLAUDE.md that's long but already well-structured (pure dev instructions) may not need extraction — judge by content type, not just line count
- Rules files loaded via `.claude/rules/` are NOT automatically injected — the user needs to reference them via `@rules/product.md` syntax or the project's CLAUDE.md `@include` directive
