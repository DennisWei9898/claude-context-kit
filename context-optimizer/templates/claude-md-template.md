# {Project Name} — Dev Guide

> {one-line product description}

## Current Phase
{phase name and what's in scope — be specific, e.g. "Phase 1 MVP: restaurant search + verified reviews. No invoice verification yet."}

## Project Structure
```
{root}/
├── CLAUDE.md                   ← this file (dev guide)
├── {design-doc}.md             ← system design / SDD
├── {plan}.md                   ← current sprint / roadmap
├── docs/
│   └── {product-concept}.md   ← full product spec (not loaded every session)
├── .claude/
│   ├── rules/                  ← loaded on demand via @include
│   └── skills/                 ← invoked via /skill-name
└── {src}/                      ← code
```

## Tech Stack
| Layer | Choice | Why |
|-------|--------|-----|
| {Frontend} | {tech} | {one-line reason} |
| {Backend}  | {tech} | {one-line reason} |
| {DB}       | {tech} | {one-line reason} |

## Core Rules
1. {rule — non-obvious constraint, e.g. "Reviews publish immediately; ACR score accumulates in background"}
2. {rule}
3. {rule}
4. {rule}
5. {rule — max 5}

## Document Reference
| Need | Where |
|------|-------|
| Full product spec / business model | `docs/{product-concept}.md` |
| System architecture & API design | `{sdd}.md` |
| Points / scoring rules detail | `docs/{rules}.md` |
| Current sprint tasks | `{plan}.md` |

## Available Skills
| Command | Invoke when |
|---------|------------|
| `/{skill-1}` | {trigger description} |
| `/{skill-2}` | {trigger description} |
