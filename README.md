# claude-context-kit

A Claude Code skill that upgrades your project from a single large `CLAUDE.md` to a modular, token-efficient context system — in one conversation.

```
npx skills add DennisWei9898/claude-context-kit@context-optimizer
```

---

## The problem

Most Claude Code projects start with a single `CLAUDE.md` that grows over time. Product specs, business logic, competitor analysis, tech stack docs, and coding rules all land in the same file. This causes three problems:

1. **Token waste** — everything loads every session, even when you're doing something simple
2. **Rule compliance drops** — Claude's attention dilutes across 300+ lines
3. **No separation of concerns** — product docs and dev instructions are tangled together

## The solution

This skill walks you through the [5 Levels of Claude Code](https://codelove.tw/@tony/post/aWYABx) Level 2 → Level 3 upgrade:

```
Before                          After
──────────────────────          ──────────────────────────────────
CLAUDE.md (300+ lines)    →    CLAUDE.md (~80 lines, dev only)
                          →    docs/product-concept.md
                          →    .claude/rules/product.md
                          →    .claude/rules/tech-stack.md
                          →    .claude/rules/coding-style.md
                          →    .claude/skills/research/SKILL.md
                          →    .claude/skills/qa-review/SKILL.md
```

Rules load only when referenced. Skills inject only when invoked. Token cost drops 60–80% per session.

---

## Install

```bash
npx skills add DennisWei9898/claude-context-kit@context-optimizer
```

Or manually copy to your skills directory:

```bash
cp -r context-optimizer ~/.claude/skills/context-optimizer
```

---

## Usage

Just describe what you need:

```
/context-optimizer
```

Or the skill auto-triggers when you say things like:
- "my CLAUDE.md is too big"
- "help me organize my Claude Code project"
- "set up .claude/rules directory"
- "CLAUDE.md 太大了"
- "幫我整理 Claude 專案文件"

The skill will **ask for your confirmation** before touching any file. Nothing is deleted or committed automatically.

---

## What gets created

| File | What it is |
|------|-----------|
| `CLAUDE.md` | Rewritten as a lean dev guide (50–120 lines) |
| `docs/{topic}.md` | Your extracted product/business content (nothing deleted) |
| `.claude/rules/product.md` | Non-obvious product constraints that affect code decisions |
| `.claude/rules/tech-stack.md` | Stack table, API endpoints, local dev commands |
| `.claude/rules/coding-style.md` | Code conventions, naming rules, API response format |
| `.claude/skills/*/SKILL.md` | 2–4 starter skill templates for your project's workflows |

---

## Safety

- Asks for explicit confirmation before any file is created or modified
- Never deletes files — extracted content is preserved in `docs/`
- Never runs git commands or makes commits
- Never modifies `settings.json` or `settings.local.json`
- No routing rules injected into your CLAUDE.md
- Passed [claude-skill-safety-kit](https://github.com/DennisWei9898/claude-skill-safety-kit) security audit: all 7 categories 🟢 (Category 4 🟡 — CLAUDE.md modification is the stated purpose, with full user consent at each step)

---

## Repo structure

```
claude-context-kit/
└── context-optimizer/
    ├── SKILL.md                        ← main skill
    └── templates/
        └── claude-md-template.md       ← CLAUDE.md target structure reference
```

---

## Contact

Open to collaboration, consulting, or any questions about this skill.

- LinkedIn: https://www.linkedin.com/in/dennis-wei-47393a14a/
- Email: dennis.xd.wei@gmail.com

## License

MIT

---
---

# claude-context-kit（中文說明）

一個 Claude Code skill，幫你把龐大的 `CLAUDE.md` 升級為模組化、低 token 消耗的專案 context 架構 — 在一個對話中完成。

```
npx skills add DennisWei9898/claude-context-kit@context-optimizer
```

---

## 問題背景

大多數 Claude Code 專案的 `CLAUDE.md` 會隨著時間越長越大 — 產品規格、商業邏輯、競品分析、技術棧說明、程式碼規範全部塞在同一個檔案裡。這帶來三個問題：

1. **Token 浪費** — 每次 session 全部載入，即使你只是在改一行 CSS
2. **規則遵守率下降** — Claude 的注意力被稀釋在 300+ 行文件裡
3. **關注點混雜** — 產品文件和開發指引纏在一起

## 解法

這個 skill 帶你完成 [Claude Code 5 個熟練層級](https://codelove.tw/@tony/post/aWYABx) 的 Level 2 → Level 3 升級：

```
升級前                            升級後
──────────────────────────        ──────────────────────────────────────
CLAUDE.md（300+ 行）        →    CLAUDE.md（約 80 行，只含開發指引）
                            →    docs/product-concept.md（產品規格）
                            →    .claude/rules/product.md
                            →    .claude/rules/tech-stack.md
                            →    .claude/rules/coding-style.md
                            →    .claude/skills/research/SKILL.md
                            →    .claude/skills/qa-review/SKILL.md
```

Rules 只在被引用時載入。Skills 只在被呼叫時注入。每次 session 的 token 消耗降低 60–80%。

---

## 安裝

```bash
npx skills add DennisWei9898/claude-context-kit@context-optimizer
```

或手動複製到 skills 目錄：

```bash
cp -r context-optimizer ~/.claude/skills/context-optimizer
```

---

## 使用方式

直接呼叫：

```
/context-optimizer
```

或在對話中說出觸發詞，skill 會自動啟動：
- 「我的 CLAUDE.md 太大了」
- 「幫我整理 Claude 專案文件」
- 「設定 .claude/rules 目錄」
- "my CLAUDE.md is too big"
- "organize my Claude Code project"

Skill 會**先詢問你的確認**，才會動任何檔案。不會自動刪除或 commit。

---

## 會產生什麼

| 檔案 | 說明 |
|------|------|
| `CLAUDE.md` | 重寫為精簡開發指引（50–120 行） |
| `docs/{topic}.md` | 萃取出的產品/商業內容（不刪除原始內容） |
| `.claude/rules/product.md` | 影響程式碼決策的非顯而易見產品規則 |
| `.claude/rules/tech-stack.md` | 技術棧表、API 端點、本地開發指令 |
| `.claude/rules/coding-style.md` | 程式碼規範、命名規則、API 回傳格式 |
| `.claude/skills/*/SKILL.md` | 2–4 個針對你專案工作流的 skill 起始模板 |

---

## 安全性

- 每步都詢問明確確認，才會建立或修改任何檔案
- 不刪除任何檔案 — 萃取的內容保存在 `docs/`
- 不執行 git 指令，不自動 commit
- 不修改 `settings.json` 或 `settings.local.json`
- 不向你的 CLAUDE.md 注入任何 routing 規則
- 通過 [claude-skill-safety-kit](https://github.com/DennisWei9898/claude-skill-safety-kit) 安全審查：7 項全 🟢（第 4 項 🟡 — CLAUDE.md 修改是本 skill 的明確目的，每步都有完整用戶同意流程）

---

## Repo 結構

```
claude-context-kit/
└── context-optimizer/
    ├── SKILL.md                        ← 主要 skill 檔案
    └── templates/
        └── claude-md-template.md       ← CLAUDE.md 目標結構參考模板
```

---

## 聯絡方式

歡迎商業合作、諮詢邀約或任何關於此 skill 的問題。

- LinkedIn：https://www.linkedin.com/in/dennis-wei-47393a14a/
- Email：dennis.xd.wei@gmail.com

## 授權

MIT
