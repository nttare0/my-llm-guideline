# my-llm-guideline

LLM rule files that force your coding agent to **build only with three
allowlisted tools — and never invent its own tools**.

| # | Tool | Source |
|---|------|--------|
| 1 | **Astryx** (Meta design system) | https://github.com/meta/astryx |
| 2 | **Modern Web Guidance** (Google Chrome) | https://github.com/GoogleChrome/modern-web-guidance-src |
| 3 | **shadcn/ui** | https://ui.shadcn.com |

> **Start with [`AGENTS.md`](AGENTS.md)** — it is the single entry point for
> every agent. Detailed rules live in [`rules/`](rules/README.md).

## What's in this repo

```
AGENTS.md                          ← canonical entry point (read this first)
CLAUDE.md                          ← shim for Claude Code (points to AGENTS.md)
.github/copilot-instructions.md    ← shim for GitHub Copilot
.cursor/rules/*.mdc                ← Cursor mirrors (00-core, 01-astryx, 02-mwg, 03-shadcn, 04-decision-tree)
rules/
  README.md                        ← index
  00-core-allowlist.md             ← the allowlist: sources, installs, discovery commands
  01-astryx.md                     ← Astryx usage rules
  02-modern-web-guidance.md        ← Modern Web Guidance usage rules
  03-shadcn.md                     ← shadcn/ui usage rules
  04-decision-tree.md              ← which tool wins for which task
  05-forbidden-patterns.md         ← banned patterns (before/after)
  06-workflow-checklist.md         ← before/during/after checklist + response template
  07-how-to-add-a-rule.md          ← template + steps for adding the next rule
  08-site-essentials.md            ← required site essentials: favicon, privacy, terms, sitemap, share preview
  09-real-images.md                ← real images only — Unsplash & Pinterest, never AI-generated
  10-prebuild-plugins.md           ← pre-build plugins: Ponytail + Agent Skills install gate
  11-security-checklist.md         ← security gate: 32 checks required before shipping
  12-launch-checklist.md           ← launch gate: 20 website essentials required before launch
```

## How to use these rules

1. **Copy `AGENTS.md` + `rules/` into your project** (or point your agent at this repo).
2. Keep the compatibility shims (`CLAUDE.md`, `.github/copilot-instructions.md`,
   `.cursor/rules/`) if you use those agents — they all point to the same rules.
3. Your agent must run the discovery commands before writing code:
   - Astryx: `npx @astryxdesign/cli search …` / `component …`
   - Modern Web Guidance: `npx modern-web-guidance@latest search …` / `retrieve …`
   - shadcn: `npx shadcn@latest search …` / `add …`
4. If the allowlist can't do something, the agent must **stop and ask** — not invent.

## How to add more rules (step by step)

See [`rules/07-how-to-add-a-rule.md`](rules/07-how-to-add-a-rule.md). In short:

1. Get explicit user approval for the new tool/rule.
2. Copy the template from `07-how-to-add-a-rule.md` → save as `rules/08-<name>.md`.
3. Add a row to `rules/README.md` and `AGENTS.md` §6.
4. Update `00-core-allowlist.md` / `04-decision-tree.md` / `05-forbidden-patterns.md` if affected.
5. Mirror in `.cursor/rules/` if you use Cursor. Bump the version in `AGENTS.md`.

## Design principles

- **One file = one concern.** Rules are modular so they can grow step by step.
- **Command-first.** Every rule names its source of truth + discovery command.
- **Strict by default.** No invented tools, no hand-rolled replacements, no new libraries.
- **One system per screen.** Astryx (default) or shadcn — never mixed without approval.
- **Modern platform first.** Modern Web Guidance governs all CSS/JS decisions.

---

*Version 1.7 — 2026-11-17 · Allowlist: Astryx, Modern Web Guidance, shadcn/ui only · Images: Unsplash, Pinterest (real photos only) · Plugins: Ponytail, Agent Skills · Gates: security (32) + launch (20).*
