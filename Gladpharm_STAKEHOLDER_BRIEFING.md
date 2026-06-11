# Gladpharm DWH Assessment - Stakeholder Briefing

## What We've Discovered About Your Vision

Gladpharm has designed a **data warehouse for financial analytics** focused on answering critical budget questions:

> "How are we spending money vs. what we planned?"

Your Silver layer data model shows you want to track and analyze:
- **Actual expenses** vs **Planned budgets** (AC vs PC)
- Drill-down by **time period, cost structure, department, and responsible person**
- **Year-over-year and period-over-period variance analysis**
- Visibility at **transaction detail level** (down to individual expense line items)

---

## Your Architecture (What You've Designed)

### Three Data Layers

```
┌─────────────────────────────────────────────────────────┐
│ BRONZE LAYER                                            │
│ Raw data from source systems                            │
│ • Expense transactions from 1C accounting system        │
│ • Budget master data                                    │
│ • Organization structure                               │
│ • Employee master                                       │
│ • Cost center assignments                               │
└─────────────────────────────────────────────────────────┘
                          ↓ (Transformations)
┌─────────────────────────────────────────────────────────┐
│ SILVER LAYER (Your Design)                              │
│ Cleaned, conformed data in analytics-ready structure    │
│ • fct_spends (Fact Table - Transactions)               │
│ • dim_date (Time dimension)                             │
│ • DimBudgetItems (Cost hierarchy)                       │
│ • DimCompanyStructure (Organization hierarchy)          │
│ • DimEmployees (People master)                          │
│ • DimPlannedBudgetItems (Budget master)                 │
└─────────────────────────────────────────────────────────┘
                          ↓ (Aggregations)
┌─────────────────────────────────────────────────────────┐
│ GOLD LAYER (To Be Defined)                              │
│ Business-ready reports and dashboards                   │
│ • Actual vs Budget reports                              │
│ • Variance analysis                                     │
│ • Department drill-downs                                │
│ • Forecast vs Actual                                    │
│ • Custom management dashboards                          │
└─────────────────────────────────────────────────────────┘
```

### Your Star Schema (Silver Layer)

```
                    ┌───────────────┐
                    │   dim_date    │
                    │ (Time Master) │
                    └───────────────┘
                            ↑
                            │ sk_date_id
                            │
        ┌───────────────┐   │   ┌──────────────────┐
        │ DimBudgetItems│   │   │ DimCompanyStruct │
        │   (Costs)     │   │   │  (Organization)  │
        └───────────────┘   │   └──────────────────┘
              ↑             │             ↑
              │             │             │
              ├─────────────┼─────────────┤
                            │
              ┌─────────────▼─────────────┐
              │    fct_spends (Facts)     │
              │  • AC (Actual Cost)       │
              │  • PC (Planned Cost)      │
              │  • PN (?)                 │
              └───────────────┬───────────┘
              ↑               ↑
              │               │
        ┌─────────────┐  ┌────────────────┐
        │DimEmployees │  │DimPlannedBudget│
        │ (People)    │  │  (Budget Plan)  │
        └─────────────┘  └────────────────┘
```

---

## What We Need From You

### For Finance Leadership

**1. Confirm the Business Case**
- [ ] Is budget variance analysis the primary use case?
- [ ] Are there other analytics needs beyond budget tracking?
- [ ] What decisions will this data warehouse enable?
- [ ] What's the expected ROI and payback period?

**2. Define Success Metrics**
- [ ] What KPIs will show the warehouse is successful?
- [ ] How will you measure adoption?
- [ ] What's the target user base? (_____ people)

---

### For Finance Operations

**1. Source Data Inventory**
- [ ] Where does expense data come from? (1C? Other systems?)
- [ ] Where are budgets maintained? (Excel? System?)
- [ ] How often is this data updated?
- [ ] What's the historical data volume? (_____ years, _____ transactions)

**2. Current Reporting Needs**
- [ ] What reports do you produce today?
- [ ] How much time is spent on manual reporting?
- [ ] What insights are most critical to your decisions?
- [ ] What drill-paths do you use most? (By month? By cost center? By responsible person?)

---

### For IT & Data Management

**1. Source System Details**
- [ ] Primary ERP system: _________________
- [ ] Can we extract directly from database? ☐ Yes ☐ No
- [ ] Are there APIs available? ☐ Yes ☐ No
- [ ] Data refresh frequency needed: _________________
- [ ] Any constraints on data extraction: _________________

**2. Data Quality Baseline**
- [ ] What data quality issues exist in the source systems?
- [ ] Duplicate records: ☐ Yes ☐ No (estimate _____ %)
- [ ] Missing fields: ☐ Yes ☐ No (which ones: _______)
- [ ] Data reconciliation needed: ☐ Yes ☐ No
- [ ] Current data validation rules: _________________

**3. Infrastructure Requirements**
- [ ] Azure subscription status: ☐ Exists ☐ Needs setup
- [ ] Microsoft Fabric licensing: ☐ Available ☐ Needs purchase
- [ ] Network/security constraints: _________________
- [ ] Data residency requirements: _________________

---

### For Budget/Cost Center Managers

**1. Your Analytics Needs**
- [ ] What budget questions do you need answered weekly/monthly?
- [ ] What drill-paths are most important? (by subcost center? by employee? by time?)
- [ ] Do you need to see individual expense line items or summaries?
- [ ] What variance thresholds trigger investigation? (over ____% triggers review)

**2. Access & Security**
- [ ] Should you only see your department's data? ☐ Yes ☐ No
- [ ] Should employees see only their cost center? ☐ Yes ☐ No
- [ ] What sensitivity level is this data? (☐ Public ☐ Internal ☐ Confidential)

---

### For All Stakeholders

**Complete This Matrix:**

| Aspect | Stakeholder | Value | Notes |
|--------|-----------|-------|-------|
| **Actual Costs** | Who owns? | Who needs it? | |
| **Planned Budgets** | Who owns? | Who needs it? | |
| **Cost Center Assignment** | Who owns? | How structured? | |
| **Organizational Structure** | Who owns? | How many levels? | |
| **Employee/Responsible Party** | Who owns? | Active count? | |
| **Time Dimension** | Fiscal or Calendar? | Critical periods? | |
| **Currency** | Single or Multi? | Conversion needed? | |
| **Chart of Accounts** | Who owns? | How many codes? | |

---

## Questions About the Design

### About the Fact Table (fct_spends)

**Q: What do AC, PC, and PN mean?**
- AC = _________________________
- PC = _________________________
- PN = _________________________

**Q: Are there other amounts you need to track?**
- [ ] Amount without VAT
- [ ] Foreign currency amounts
- [ ] Approved vs Committed vs Actual
- [ ] Budget variance (Planned - Actual)
- [ ] Other: _________________

**Q: What identifies a unique transaction?**
- Is it: Document ID + Line Number + Date?
- Or something else: _________________

---

### About the Dimensions

**Q: Cost Structure (DimBudgetItems)**
- Your budget codes: How many levels deep? (☐ 2 levels ☐ 3 levels ☐ More)
- Example structure: Level1 → Level2 → Cost (please provide real examples)
- Do these codes change? (do old codes disappear and new ones appear?)
- How many unique codes: _________ (current), _________ (expected)

**Q: Organization (DimCompanyStructure)**
- Your org structure: How many levels? (typically 3-5)
- How many total units/departments: _________
- Does the structure change frequently?
- Do people need to see only their department? ☐ Yes ☐ No

**Q: Employees (DimEmployees)**
- Total active employees: _________
- Need to track which cost center each employee is assigned to? ☐ Yes ☐ No
- Need to track manager/reporting relationships? ☐ Yes ☐ No
- Need separation of duties/roles? ☐ Yes ☐ No

**Q: Planned Budget (DimPlannedBudgetItems)**
- Is this "budget by cost code" or "budget by cost code by month" or "budget by scenario"?
- How many budget versions do you maintain? (e.g., Initial, Revised1, Final, Forecast)
- Do you budget at the detail cost level or higher level?

---

## What Happens Next

### Phase 1: Data Gathering (Weeks 1-2)
✓ Review this briefing as a team
✓ Complete the assessment questions above
✓ Provide sample data from source systems
✓ Confirm the design meets your needs

### Phase 2: Design Validation (Weeks 2-3)
→ Map source systems to Silver layer tables
→ Define Bronze layer transformations
→ Confirm data quality rules
→ Validate security requirements

### Phase 3: Gold Layer Design (Week 3-4)
→ Define specific reports and dashboards
→ Specify aggregation requirements
→ Design drill-down paths
→ Plan BI layer implementation

### Phase 4: Implementation Planning (Week 4)
→ Create implementation roadmap
→ Define resource needs and timeline
→ Establish SLAs and support model

---

## Key Decision Points

### Decision 1: Data Granularity
**Question:** Should the warehouse store:
- ☐ **Detailed** (every transaction line item) — allows maximum drill-down, larger storage
- ☐ **Summarized** (daily/weekly summary level) — smaller storage, less drill-down
- ☐ **Hybrid** (detailed recent + summarized history) — balance of both

**Our recommendation:** Start with detailed, Fabric compression handles storage efficiently.

### Decision 2: Historical Data
**Question:** How much history should we load?
- ☐ **1 year** (current + prior year)
- ☐ **3 years** (typical for trend analysis)
- ☐ **5+ years** (if comparing long-term trends)
- ☐ **All available** (complete history)

**Our recommendation:** 3 years is typically sufficient for budget analysis.

### Decision 3: Real-Time vs Batch
**Question:** How fresh does the data need to be?
- ☐ **Daily overnight** (data ready by 8am next day)
- ☐ **Weekly** (refreshed once a week)
- ☐ **Monthly** (refreshed at month-end)
- ☐ **Real-time/Hourly** (continuous updates)

**Our recommendation:** Daily is standard for financial analytics; real-time is rare for budget data.

### Decision 4: Access Model
**Question:** Should budget/cost data be:
- ☐ **Public** (everyone sees all data)
- ☐ **By Role** (CFO sees all, managers see their dept, individual contributors see their budget)
- ☐ **Restricted** (only finance team sees sensitive data)

**Our recommendation:** By Role is typical; need to validate sensitivity.

---

## Timeline & Effort Estimate

| Phase | Week | Key Activity | Effort |
|-------|------|--------------|--------|
| **Discovery** | 1-2 | Gather requirements, validate design | 10-15 hrs/stakeholder |
| **Design** | 2-3 | Map source→silver, define gold layer | 20-30 hrs IT + Finance |
| **Build** | 3-6 | Create Bronze/Silver/Gold layers | 80-120 hrs engineering |
| **Test** | 6-7 | Data validation, user acceptance | 20-30 hrs |
| **Deploy** | 7 | Go-live, training, support | 10-15 hrs |
| **Stabilize** | 8+ | Monitor, optimize, iterate | 5-10 hrs/week ongoing |

**Total Effort: 150-250 hours** (depending on source system complexity)

---

## Success Criteria

By end of implementation, you should have:

✓ **Automated daily data refresh** — No manual Excel work
✓ **Single source of truth** — One version of budget vs actual (not multiple conflicting reports)
✓ **Self-service analytics** — Non-technical users can answer their own questions
✓ **Fast insights** — Reports run in seconds, not hours
✓ **Historical analysis** — Trends and forecasting capability
✓ **Audit trail** — Know who accessed what and when
✓ **Drill-down capability** — Explore from dashboard to line-item detail
✓ **Mobile-ready** — View reports on phone/tablet

---

## Next Step

**Please complete and return:**

1. **Stakeholder Briefing Feedback** — Confirm this matches your vision
2. **Assessment Questionnaire** — Answer priority questions above
3. **Source Data Sample** — Provide sample data from 1C and other systems
4. **Timeline Preference** — When do you want to start and go live?

**Expected Timeline:** 4 weeks from data gathering start to go-live readiness

---

## Questions?

Key contacts for this assessment:
- **Technical Architecture:** [Your Name]
- **Business Requirements:** [Finance Lead Name]
- **Source Systems:** [IT Lead Name]
- **Implementation:** [Project Manager Name]

**Next Meeting:** [Schedule within 1 week]
