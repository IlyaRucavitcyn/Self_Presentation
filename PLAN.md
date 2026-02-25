# Yearly Catchup Preparation — Master Plan

## Purpose
Prepare a presentation for CTO (direct manager/mentor) to justify a rate increase (~10-15%) based on roles covered, 2025 results, market research, and future plans.

## Key Context
- **Company**: Sigli (https://www.sigli.com/) — IT services company, ~100 people worldwide
- **Location**: Poland
- **Departments managed**: JS, PHP, QA — ~31 people total
- **Roles covered**: Pre-sales Engineer (30%), VP of Engineering (25%), Resource Manager (25%), Project & Client Management (20%)
- **Target raise**: ~10-15% (research-dependent)
- **Current compensation**: 5,680 EUR/mo base + 760 EUR/mo bonus = 6,440 EUR/mo total (B2B)
- **Final deliverables**: PDF report + presentation (PowerPoint/Google Slides → PDF)
- **Working format**: All core content in .md files, final conversion at the end

## Research Job Titles (for market comparison)
Research each separately with responsibility summaries:
1. VP of Engineering
2. Engineering Manager
3. Head of Engineering
4. Staff Engineer

## Plan

### Step 1: Folder Structure Setup
- [x] Create folder structure
- [x] Create PLAN.md (this file)

### Step 2: Content Collection (interactive, section by section)

#### 2.1 Roles & Responsibilities
- [x] Review and refine role definitions from CLAUDE.md
- [x] Discuss with user — any updates for 2025
- [x] Write `01_roles_responsibilities/summary.md`
- **Status**: DONE

#### 2.2 Results of 2025
- [x] Collect existing documents from user (GPM reports, OKR reviews, project lists, etc.)
- [x] Discuss key achievements, metrics, deliverables
- [x] Write `02_results_2025/results.md`
- **Status**: DONE

#### 2.3 Market Research — Salaries
- [x] Research aggregation platforms (Glassdoor, Itentio, Oyster HR, WorldSalaries) for salary + bonus + benefits data
- [x] Research Polish job boards (JustJoinIT API + manual vacancy collection) — 14 B2B vacancies collected
- [x] Write `03_market_research/aggregated_market_data.md`
- [x] Write `03_market_research/local_boards.md`
- [x] Write `03_market_research/summary.md`
- **Status**: DONE

#### 2.4 Comparison
- [x] User provides current salary (5,680 EUR/mo base + 760 bonus = 6,440 total B2B)
- [x] Build comparison framework (salary vs market, responsibilities vs typical role scope)
- [x] Write `04_comparison/analysis.md`
- **Status**: DONE

#### 2.5 Plans & Proposals
- [x] Discuss next year goals and new responsibility ideas
- [x] Write `05_plans_proposals/proposals.md`
- **Status**: DONE

### Step 3: Final Deliverables
- [x] Choose presentation tool — **HTML (single-file) selected** (Canva MCP abandoned)
- [x] Create `output/presentation.md` — slide-by-slide content draft — DONE
- [x] Update `PRESENTATION_STYLE.md` — aligned to Sigli corporate brand (colors, typography, CSS classes)
- [x] Create `Finished Presentations/yearly-catchup-2026.html` — 12-slide interactive HTML presentation
- [ ] Create `output/executive_summary.md`
- **Status**: HTML PRESENTATION DONE & POLISHED — 12 slides, Sigli brand, UX-optimised layout, font sizes increased, all two-col anti-patterns removed

#### Canva MCP Setup — Troubleshooting Log

**Problem:** Canva MCP configured but tools not appearing in VSCode extension sessions.

**Root cause:** Two issues:
1. Original config used `type: "sse"` pointing directly to `https://mcp.canva.com/mcp` — this does NOT handle OAuth. Server returns 401.
2. VSCode extension requires `.mcp.json` in project root (separate from `~/.claude.json` CLI config). MCP tools are only injected at session start; existing sessions don't pick them up.

**What was done:**
- Created `.mcp.json` in project root with `mcp-remote` (stdio) transport — this handles OAuth correctly:
  ```json
  {
    "mcpServers": {
      "canva": {
        "type": "stdio",
        "command": "npx",
        "args": ["-y", "mcp-remote@latest", "https://mcp.canva.com/mcp"]
      }
    }
  }
  ```
- `~/.claude.json` project entry previously had old SSE config — **fixed in session 4**: removed SSE entry, added `"canva"` to `enabledMcpjsonServers`
- Trust dialog accepted (`hasTrustDialogAccepted: true`)

**To activate in VSCode:**
1. Reload VSCode window (Cmd+Shift+P → "Developer: Reload Window")
2. Start a **new conversation** — MCP tools are injected at session start only
3. On first Canva tool use → browser opens for OAuth login → complete it
4. Canva tools will then be active: `generate-design`, `search-designs`, `export-design`, etc.

**Known Canva MCP tool names:**
- `generate-design` — create new design from prompt
- `search-designs` — find existing designs
- `get-design`, `get-design-pages`, `get-design-content`
- `export-design`, `get-export-formats`
- `create-folder`, `move-item-to-folder`

#### Slide Plan (draft order)
1. **Title** — Name, title, date
2. **Role & Scope** — 4 functional roles, 31 people, 3 departments — source: `01_roles_responsibilities/summary.md`
3. **2025 Financial Results** — GPM +17.4%, team +24%, GPM% by dept — source: `02_results_2025/results.md`
4. **2025 Projects & Pre-sales** — SamTrack (low-code, GPM 60%), Fortuna, Stembridge pipeline, Adexin — source: `02_results_2025/results.md`
5. **New Services Launched** — Low-code, Odoo, AI for Dev/QA, QA Mobile, Typo3 — source: `02_results_2025/results.md`
6. **Team & People** — Headcount growth, Copaco hire, new mentors, retention — source: `02_results_2025/results.md`
7. **Market Data** — EM range 6,400-8,700, Head of Eng 8,300-11,300, benefits standard — source: `03_market_research/summary.md`
8. **Compensation Gap** — Current vs market table, role scope tier comparison — source: `04_comparison/analysis.md`
9. **2026 Plans** — Service lines, Adexin, smaller projects via AI, AI at company scale — source: `05_plans_proposals/proposals.md`
10. **Proposal** — 35→40 EUR/hr, current vs proposed table, conservative framing — source: `05_plans_proposals/proposals.md`

#### Instructions for next session
1. Check that Canva MCP tools are visible (canva_* tools should appear)
2. If OAuth needed — complete login flow
3. Draft `output/presentation.md` from slide plan above first
4. Then use Canva MCP to create the actual presentation from that draft
5. Keep slides concise — numbers and bullets, not paragraphs

## Input Materials Available
- `input_materials/GPM _JS - GPM Contractors .csv` — JS department GPM data (2021-2026)
- `input_materials/GPM _PHP - GPM Contractors.csv` — PHP department GPM data (2021-2026)
- `input_materials/GPM _Quality Assurance - GPM Contractors .csv` — QA department GPM data (2021-2026)
- `input_materials/GPM_file_structure_guide.md` — **READ THIS FIRST** — complete guide for parsing CSV files, includes validated extraction script and column detection strategy
- `input_materials/Tech_Management_Stats - Initial.csv` — User's manual vacancy research (12 postings, B2B and UoP)
- `input_materials/*.png` — Screenshots of JustJoinIT vacancies (TQLO x2, Blazity, Remodevs, Connectis, Worksuite)

## Key Findings So Far
- Official job title: "Head of JS, PHP and QA Departments"
- CLAUDE.md role names (Pre-sales Engineer, VP of Engineering, Resource Manager, Project & Client Management) are functional mappings to industry-standard roles, not official titles
- December 2025 active contractors: JS=22, PHP=2, QA=7, Total=31
- GPM file parsing requires "track last seen year" strategy for Row 1 (year headers are sparse)
- **Current compensation**: 5,680 EUR/mo base + 760 EUR/mo bonus (13.4%) = 6,440 EUR/mo total
- **Market EM range (B2B)**: 6,400 - 8,700 EUR/mo median band (14 vacancies)
- **Market benefits standard**: medical + multisport + equipment + 25-26 days vacation
- **User's benefits**: none (no medical, no sports, no equipment, 19 vacation days)
- **Key gap**: base salary below market floor for standard EM; role scope exceeds typical EM significantly

## Content Review — Improvement Points (2026-02-20)

### Bugs / Errors
- [x] **#1** `analysis.md` — Vacation math: "33-39" still appears on lines 42 and 77; line 91 already says "38-39". Need to unify to 38-39 everywhere. *(Session log claimed this was fixed but lines 42+77 still show 33-39)*
- [x] **#2** `results.md` — GPM figures have no currency label (e.g. "906,306" — EUR? PLN?). Add EUR explicitly.

### Gaps / Missing Content
- [-] **#3** `proposals.md` — Benefits ask absent. Comparison documents a major gap (medical, sports, equipment, ~20 fewer vacation days) but proposal only requests rate. **Decide: add benefits ask or keep as rate-only?** → *Rejected: rate-only, single clean ask.*
- [-] **#4** `results.md` — Pre-sales conversion rate unframed. "2 contracts signed / 12-15 engagements" = 13-17% — needs one sentence of context (B2B IT norms, effort value beyond just wins). → *Rejected.*
- [-] **#5** `analysis.md` or `roles/summary.md` — PHP dept context missing. PHP=2 people could undermine "Head of 3 departments" narrative. Add: Typo3 service growing, niche specialty, etc. → *Rejected.*

### Framing Improvements
- [-] **#6** `results.md` — "Majority were temporary contractors" is vague. Tighten: how many of the 6 departures were fixed-term? State it precisely. → *Rejected.*
- [-] **#7** `results.md` — Adexin partnership understated (it's a new revenue channel created, not just a project). Elevate framing. → *Rejected.*
- [-] **#8** `results.md` — "No mentor or critical role losses" is buried. Surface this explicitly as a retention headline, especially in slow market context. → *Rejected.*
- [-] **#9** `results.md` — Pre-sales count is "~12-15" (a range). Confirm and pin to one number if possible. → *Rejected.*

### Decision Status
`[ ]` Pending | `[x]` Approved + applied | `[-]` Rejected

---

## Counter-argument Review (2026-02-20)

**Purpose:** Stress-test the presentation by addressing likely CTO push-backs before the meeting.

### Counter-arguments identified

| # | Argument | Status | Rebuttal doc |
|---|---|---|---|
| CA-1 | GPM per head declined (team grew faster than GPM) | `[-]` Skipped — not relevant | — |
| CA-2 | Pre-sales win rate is low (13-17%) | `[x]` Addressed — wins opened new service lines (C); trailing pipeline converts in 2026 (D) | — |
| CA-3 | Market comparison is self-serving / B2B tax advantages negate benefit gap | `[-]` Skipped — not relevant | — |
| CA-4 | Slow market = wrong timing for a raise | `[x]` Addressed — SamTrack alone covers the raise cost (C); retention risk in slow market (B) | — |
| CA-5 | Turnover looks high (~19-24%) | `[x]` Addressed — all 6 were project-end exits from 2024 contracts; can be named individually; no mentor/senior losses | — |
| CA-6 | Role scope is self-declared, not formally restructured | `[-]` Not expected — verbal backup: CTO accepted all initiatives; value captured regardless of who proposed it | — |
| CA-7 | No urgency signal (no retention risk stated) | `[x]` Addressed — user knows how to handle verbally | — |
| CA-8 | 2026 plans are plans, not delivered results | `[-]` Skipped — not relevant | — |

`[ ]` Pending | `[~]` In progress | `[x]` Addressed | `[-]` Acknowledged / accepted as valid

---

## Session Log
- **2026-02-14**: Project initiated. Folder structure created. Plan established. Roles & responsibilities draft written (`01_roles_responsibilities/summary.md`). GPM CSV files added and validated. GPM file structure guide created with working extraction script. December 2025 contractor counts verified (30 active, matching ~30 in summary).
- **2026-02-16**: Steps 2.1 and 2.2 completed. Roles locked. Results of 2025 written (financial performance, projects, new services, team growth, public speaking, challenges). Market research started: aggregated platform data collected (Glassdoor, Itentio, Oyster HR), 14 B2B vacancies compiled from manual research + JustJoinIT API. Key finding: user's total comp (6,440 EUR/mo) sits at or below market floor for a standard EM with narrower scope.
- **2026-02-17**: Steps 2.3-2.5 completed. Market research summary written. Comparison analysis done (salary positioning, bonus, benefits with vacation/holidays clarification, role scope tiers, gap summary). Plans & proposals drafted (35→40 EUR/hr, +14.3%; strategic initiatives incl. smaller projects via AI/low-code). All content collection done. Next: Step 3 — final deliverables using Office-PowerPoint-MCP-Server.
- **2026-02-20**: Content improvements session. Fixed cross-file inconsistencies: (1) removed Director of Engineering row from summary.md (already removed from aggregated_market_data.md); (2) corrected vacation days from "20-26" to "25-26" in analysis.md — validated against sources (Motife, Kadromierz, ITCompare) confirming 25-26 is the B2B market norm, not the UoP statutory range; (3) fixed vacation total from "33-39" to "38-39" accordingly. Fixed placeholder vacancy links in local_boards.md: matched all 7 manually collected vacancies (#1-7) to screenshots and filled in real URLs + company names (#1: Netguru, #2: INNERGY, #3: Shelf, #4: Perfect Gym, #5: Yard Corporate, #6: Tidio, #7: LeoVegas). All 14 vacancies now have real links. All content files are in final state. Step 3 (final deliverables) not yet started.
- **2026-02-20** (session 2): Counter-argument review completed (8 CAs identified, all processed). Canva MCP configured for this project (`~/.claude.json`). Slide plan drafted (10 slides). **Next session**: restart Claude Code → verify Canva MCP tools active → OAuth login → create `output/presentation.md` → build Canva presentation.
- **2026-02-20** (session 3): `output/presentation.md` created (10 slides, ready for Canva). Canva MCP troubleshooting: original SSE config doesn't handle OAuth (401). Fixed: created `.mcp.json` in project root using `mcp-remote` stdio transport. **To activate**: reload VSCode + start new conversation. Canva tools injected at session start only.
- **2026-02-20** (session 4): Canva MCP still not loading. Root cause: `~/.claude.json` had old broken SSE config in project `mcpServers` (overriding `.mcp.json`) AND `enabledMcpjsonServers` was empty. Fix: cleared `mcpServers.canva` SSE entry, added `"canva"` to `enabledMcpjsonServers`. OAuth tokens confirmed valid. **Next**: reload VSCode → start new conversation → Canva tools should now appear.
- **2026-02-24** (session 5): Full slide-by-slide review and polish of `output/presentation.md`. Changes: Activities column added to Slide 2; AI initiatives separated from service lines on Slide 5; market bonus standard added to Slide 7; Slide 8 reworked (base-only comparison, benefits gap table, bonus norms, EM tier alignment); Slide 9 merged EM tiers to single column; Slide 10 retention framing updated; Slide 11 terminology aligned; Slide 12 (sources) added. Presentation now 12 slides, fully reviewed. **Next**: Canva generation.
- **2026-02-24** (session 6): Canva MCP path abandoned. Updated `PRESENTATION_STYLE.md` to Sigli corporate brand — added official brand colors (#75C133 green, #4d65ff blue, #ECEEF3/#F2F9FF backgrounds), Inter font spec, Sigli brand voice, updated CSS variables, badge/button classes, reframed audience and tone sections to B2B corporate context. Built `Finished Presentations/yearly-catchup-2026.html` — single-file HTML presentation with 12 slides, Sigli branding, color-coded compensation tables (red for below-market, green for market ranges, blue for current role scope column), metric cards, keyboard/swipe navigation, progress bar, fade-up animations. Small text sizes increased by 2px across the board.
- **2026-02-24** (session 7): UX pass on both `output/presentation.md` and `Finished Presentations/yearly-catchup-2026.html`. (1) Content tightening: Activities column shortened to keyword phrases; Slide 4/6/10 bullets trimmed; Slide 9 reduced from 9 to 7 rows; Slide 11 context bullets reduced from 4 to 3. (2) Layout fixes — eliminated all "two tables/sections side-by-side" anti-patterns: Slides 3/4/5/6 had two-col layouts removed; Slide 3 GPM% table replaced with 3 stat chips; Slide 4 Outcomes table replaced with 2 stat cards; Slide 5 AI initiatives moved below service table with divider; Slide 6/10 two-col bullet lists merged into single column. (3) Slide 7/8 restructured: Slide 7 bonus+benefits merged into single 2×2 table; Slide 8 now has Gap column in salary table, bonus shown as inline note, benefits compressed to 2-row table. (4) Font sizes bumped +2px globally: table, th, tbl-compact, badge, metric-label/delta, bullet, section-head, source links, inline chip labels. **Status: HTML presentation fully polished. Ready for delivery.**
- **2026-02-25** (session 8): Created v1 rebuild — `output/presentation-v1.md` (all tables replaced with bullet/list format) and `Finished Presentations/yearly-catchup-2026-v1.html`. Changes vs original: (1) All font sizes enforced ≥ 15px — badge/section-head/tbl-compact th/source h4 raised from 14px, c-muted 0.9em override removed; (2) Slide 2: roles table → 4 role cards with large % numbers, color-coded top borders (amber/blue/green); (3) Slide 3: redundant GPM summary table removed, dept GPM% chips promoted to full dept-cards; (4) Slide 5: services table → 4 service cards with status badges (green=Delivered, blue=In Progress, amber=Started) + AI chips; (5) Slide 7: salary table → 4 range cards + 2 benefit cards with left green accent border; (6) Visual polish: darker bg (#111827), card box-shadows, second radial glow on title, check-items as bordered cards, stage enlarged to 1400×820px. Slides 8, 9, 11 retain tables (essential comparative data). Navigation/animation JS unchanged.
