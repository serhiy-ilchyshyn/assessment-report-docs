# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is a **documentation / consulting-deliverable repository**, not a software project. There is no build system, package manager, test suite, or lint config — work here is editing Markdown, the draw.io diagram, and the exported Office documents. All content concerns a single engagement: a **data warehouse assessment for "Gladpharm"**, a pharmaceutical company.

The whole package is modeled on a reference deliverable, the **Yuria-Pharm Assessment Report v6.3** (55 pages, 15 sections). That report is the structural template the Gladpharm report aims to replicate; it is referenced throughout but is not itself in the repo.

## Two distinct document sets — keep them separate

The files fall into two groups that serve opposite purposes. Know which you are editing.

1. **The data-gathering toolkit** — reusable interview/planning artifacts used *before* the report exists:
   - `Gladpharm_Assessment_Package_Index.md` — master guide to the toolkit (read first).
   - `Gladpharm_QUICK_START.md` — week-by-week kickoff guide.
   - `Gladpharm_Data_Gathering_Strategy.md` — 6-phase collection plan, stakeholder matrix.
   - `Gladpharm_Interview_Template.md` — 6 interview templates with fill-in fields.
   - `Gladpharm_Assessment_Data_Gathering_Checklist.md` — 10-section completion tracker.
   - `Gladpharm_Progress_Tracker.md` — project status dashboard.
   - `Gladpharm_Assessment_ADJUSTED_FOR_DWH.md` — priority-ordered open questions reverse-engineered from the Silver-layer design (the gap list driving remaining data collection).

2. **The deliverable report** — the actual output:
   - `Gladpharm_Assessment_Report_v3_CONSOLIDATED.md` — **the current, authoritative report** (~900 lines, 15 sections). Edit report content here.
   - `Gladpharm Assessment Report_v2.docx` / `.pdf` — exported Office versions. **Note the version skew: the exports are v2, the Markdown is v3.** Treat the v3 Markdown as the source of truth; the docx/pdf are stale exports that must be regenerated after substantive report edits.
   - `Gladpharm.drawio` — architecture diagram (draw.io / diagrams.net format), referenced by the report's Appendix A.

## Domain model — needed to edit the report coherently

The report's technical sections assume a specific target architecture. Cross-references between sections will break if these aren't kept consistent:

- **Medallion architecture on Microsoft Fabric** — Bronze (raw) → Silver (modeled) → Gold (aggregated) layers.
- The Silver layer centers on a single fact table **`fct_spends`** (financial/budget spend tracking) with dimensions like `DimBudgetItems`, `DimCompanyStructure`, `DimEmployees`, `DimPlannedBudgetItems`. The measures `AC`, `PC`, `PN` and the fact grain are still partly open questions — see `ADJUSTED_FOR_DWH.md` before asserting definitions.
- Delivery is two-phase: **Phase 1 Proof of Value (PoV/PoC)** then **Phase 2 Scaling (6 months)**. Budget, roadmap, and capacity-sizing sections all reference this phasing — change one and reconcile the others.

## Working conventions

- **Regenerating exports:** there is no automated pipeline. After editing `Gladpharm_Assessment_Report_v3_CONSOLIDATED.md`, the `.docx`/`.pdf` must be re-exported (e.g. via pandoc or a manual export) and ideally renamed to v3 to end the version skew. Do not hand-edit the binary `.docx`/`.pdf` to keep content in sync — edit the Markdown and re-export.
- **Consistency is the main correctness concern.** These documents heavily cross-reference each other (the Index, Quick Start, and Strategy all enumerate the same file list, timeline, and report-section structure). When you rename a file, change the 4-week timeline, or add/remove a report section, search the other documents for the same list and update every copy.
- Dates in this package use the engagement's "today" of **2026-06-11**; relative phrasing ("this week", "Week 1") is anchored to that.
