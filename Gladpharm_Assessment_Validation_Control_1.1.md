# Gladpharm Assessment Report — Audit Validation

**Validated against:** Analytics on Microsoft Azure Specialization, **V2.8.1** (active Jan 1 – Jun 30, 2026), Module B → **Control 1.1 Analytics Portfolio Assessment** (pp. 24–25).
**Document under review:** `Gladpharm Assessment Report_v4.docx` (Yuria-aligned).
**Date:** 2026-06-11.

## Why Control 1.1

An Assessment Report is the *Accepted Documentation* for Control 1.1, which requires the partner to demonstrate that **all** of the listed assessment areas were considered for the customer. Controls 2.1 (Solution Design), 2.3 (PoC/Pilot), 3.1 (Deployment), 4.1 (Testing) and 4.2 (Post-deployment docs) are separate deliverables; where the v4 report already contributes to them, that is noted at the end. This validation therefore scores the report content against every Control 1.1 sub-item.

**Legend:** ✅ Covered · ⚠️ Partial (present but thin / needs explicit framing) · ❌ Gap.

## Compliance matrix — Control 1.1

| # | Checklist sub-item | Status | Report section(s) | Notes / action |
|---|---|---|---|---|
| **Business need** | | | | |
| B1 | Current pain points, challenges, and end-user needs | ✅ | Business overview → Problem statement; Main business challenges and needs | Strong — challenge table with business + technical perspective. |
| B2 | Product fit and gaps (which product best serves the need) | ⚠️ | Single data repository → Microsoft Fabric Lakehouse concept (advantages/disadvantages); BI/ETL software modernization | Content exists but is not framed as "product fit and gaps." Add a short explicit subsection so the auditor can map it 1:1. |
| B3 | Data storage needs — volume, type, location, current vs future | ✅ | System landscape + data sources table; Performance requirements; Budget (volumes); Visual As-IS vs future landscape | Volume (44.5M rec/yr, 500 GB–1 TB), type, location, and current-vs-future all present. |
| B4 | Data governance and compliance | ✅ | Data quality policy and framework; Data classification and related risks; Security and compliance needs | Covered. |
| B5 | Budget | ✅ | Budget (capacity sizing, F4/F8/F16/F64 Azure consumption) | Covered. |
| **Application landscape** | | | | |
| A1 | Current infrastructure or greenfield physical infrastructure | ✅ | Applications infrastructure/networking components → As-Is landscape | Covered. |
| A2 | Logical architecture and migration requirements | ✅ | Data migration needs; Future landscape; System landscape | Covered. |
| A3 | All applications, services, and SaaS BI platforms (e.g. PowerBI.com, Tableau online) | ✅ | System landscape (systems table incl. Qlik Sense); BI/ETL modernization (Power BI) | Current BI (Qlik Sense) and target BI (Power BI) both identified. |
| **Performance benchmarks** | | | | |
| P1 | Application performance and data transfer requirements | ✅ | Performance requirements and data transfer requirements (schedule, volumes, SLA) | Covered. |
| **User personas** | | | | |
| U1 | User roles, how each uses and accesses the data | ⚠️ | Users and roles | Roles + descriptions present, but "how each **uses/accesses** the data" (access patterns per role) is thin. Add an access-pattern column or sentence per role. |
| U2 | Stakeholder engagement across BI, analytics, and data-science roles | ⚠️ | Data processing (three DWH stakeholder groups); Users and roles (members) | Three consumer groups are named, but the members table is largely **TBD** and data-science persona is absent. Populate contacts and confirm whether a data-science persona applies. |
| **Skilling plan** | | | | |
| S1 | Customer skilling requirements / top skills (guidance template) | ✅ | Skilling plan | Present (drafted; current levels flagged `[TO CONFIRM]`). |
| **Data needs (workload level)** | | | | |
| D1 | Type, volume, frequency, speed influencing technology choice | ✅ | Performance requirements; data sources loading table; Budget | Covered. |
| D2 | Data centralization | ✅ | Single data repository | Covered. |
| D3 | Classification and risk of data | ✅ | Data classification and related risks | Covered. |
| D4 | Identify data sources (on-prem / AWS / Google) and Azure destination | ✅ | System landscape → data sources table (placement + destination) | Sources + placement + Bronze destination mapped. No AWS/Google sources exist for this customer (correctly reflects on-prem + Azure). |
| D5 | Identify who/what should consume the data | ✅ | Data processing (consumer groups); Future landscape (Power BI) | Covered. |
| **Networking** | | | | |
| N1 | Existing infrastructure/networking components connecting to Azure | ✅ | Applications infrastructure/networking components (As-Is + Future) | Fortinet, hybrid, API gateway, Entra ID sync all documented. |
| **Security and compliance needs** | | | | |
| SC1 | Identity & access management, RBAC, encryption | ✅ | Security and compliance needs; Users and roles (RBAC) | Encryption at-rest/in-transit, RBAC, secure comms all present. |
| SC2 | Industry- and geography-centric compliance (if applicable) | ⚠️ | Security and compliance needs (Geography Optimization) | Geography (Ukraine, latency, data residency) covered; **industry/regulatory** compliance for pharma (e.g. GDPR, GMP/GDP, local data-protection law) is not explicitly stated. Add one explicit line. |
| **Availability, resiliency & DR** | | | | |
| R1 | Customer expectations once moved to Azure | ✅ | Resilience, availability, and disaster recovery requirements | Covered. |
| R2 | Expected demand and scalability | ✅ | Resilience… (peak +75%, elastic scaling); Scalability content | Covered. |
| R3 | Uptime and SLAs | ✅ | Resilience… (≥96% solution, ≥98% DWH, maintenance window) | Covered. |

### Score summary

- **Covered (✅):** 18 of 22 sub-items
- **Partial (⚠️):** 4 — B2 product fit/gaps framing, U1 access patterns, U2 stakeholder/members + data-science persona, SC2 industry/regulatory compliance
- **Gap (❌):** 0

The report **substantively satisfies Control 1.1** for a single customer; the four partials are wording/explicitness fixes, not missing analysis.

## Recommended actions (to close the partials)

1. **B2 — add an explicit "Product fit and gaps" subsection** (1 short paragraph) under Business overview or before the Fabric Lakehouse concept, stating why Microsoft Fabric is the selected product and what gaps it closes vs the current Qlik Sense / manual stack. Reuse the Lakehouse advantages/disadvantages already in the report.
2. **U1 — add per-role access patterns.** Extend the Users and roles table with a short "Data access / usage" note per role (e.g. Data Analyst → read Silver/Gold via Power BI + SQL endpoint; Support → read-only PROD).
3. **U2 — populate the members table** (replace `TBD`s with real contacts) and confirm whether a **data-science** persona is in scope; if not, state that explicitly so the auditor sees it was considered.
4. **SC2 — add one explicit regulatory line** to Security and compliance needs naming the applicable regimes (e.g. Ukrainian personal-data law, GDPR for any EU data, pharma GxP/GDP record-keeping), or state "no industry-specific regulatory constraints beyond data residency" if that is the finding.

## Audit-readiness notes (beyond report content)

These are **evidence/process** requirements the auditor checks (Top-10 auditor questions, Glossary), independent of whether the report's content is complete:

- **Three (3) unique customers**, completed analytics deployments within the **last 24 months**, are required for Control 1.1. Gladpharm is **one** example — two more completed-customer assessments are needed for the audit package.
- **Source-document traceability:** auditors ask who created the document, where it is stored, when, and how it is used in delivery. Keep this report in the delivery repository with authorship/version metadata.
- **Excerpts are not acceptable evidence** — the live source document must be shown. (The `.docx` itself is fine; screenshots/excerpts are not.)
- **Customer sign-off** is required for completed-project controls (2.3/3.1/4.1). Not required to *pass 1.1*, but plan for it.

## Adjacent-control coverage already present in v4 (bonus)

The v4 report goes beyond Control 1.1 and already provides material that supports later controls — useful to note, though each still needs its own evidence:

| Control | Supported by v4 section | Still needed for that control |
|---|---|---|
| 2.1 Solution Design | Future landscape; Proposed architecture; PoV storage/mapping; data security (RBAC) | Explicit ingestion/storage/encryption/security checklist per 2.1; architecture diagrams |
| 2.3 PoC / Pilot | Proof of Value (PoV) use case scope (problem, goal, success criteria) | PoC **results** + customer acceptance |
| 3.1 Deployment | Implementation roadmap (PoC + scaling phases) | Signed SOW, as-built docs, production evidence |
| 3.2 Skilling | Skilling plan | Customer-facing skilling plan with cert paths (PL-300/DP-700) |

Control 1.1 does **not** require diagrams, but adding the As-Is/Future network and ETL-flow diagrams (from `Gladpharm.drawio`) strengthens both 1.1 and 2.1.
