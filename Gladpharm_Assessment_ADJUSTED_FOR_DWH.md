# Gladpharm Assessment - Adjusted for DWH Fabric Silver Architecture

## Executive Context

Gladpharm has designed a **Silver Layer** data model focused on financial and budget analytics. The model includes:
- Central **Fact Table**: `fct_spends` (expense transactions)
- **4 Dimension Tables**: Date, Budget Items, Company Structure, Employees, Planned Budget Items
- **Star Schema** optimized for budget variance analysis (Actual vs Planned)

This assessment should validate and complete the architecture by identifying:
1. Source systems and Bronze layer transformations
2. Data quality requirements and SLA
3. Gold layer analytics and reporting needs
4. User requirements and access patterns
5. Implementation timeline and resources

---

## What We Know (From Silver Layer Design)

### Primary Use Case
**Actual vs Planned Budget Analysis** with drill-down capability by:
- Time period (daily → monthly → quarterly → fiscal year)
- Cost level (2-level hierarchy: Level1 → Level2 → Cost)
- Organizational structure (hierarchical)
- Employee/Responsible party
- Cost center

### Key Metrics (Implied)
- AC (Actual Costs) - measure in fct_spends
- PC (Planned Costs?) - measure in fct_spends
- PN (?) - measure in fct_spends
- Budget Variance = Planned - Actual
- Achievement % = Actual / Planned

### Data Grain
- **Fact Table**: Line-item level (document + line number = transaction grain)
- **Dimensions**: Master record level

### Technical Stack
- **Platform**: Microsoft Fabric (Lakehouse/Warehouse)
- **Schema Style**: Star schema with role-playing dimension (dim_date)
- **Source System**: Likely 1C (Ukrainian terminology in diagram indicates 1C accounting system)

---

## What We Need to Gather (Priority Order)

### PRIORITY 1: Source System → Bronze Layer (Critical for Implementation)

#### Q1.1: What is the primary source system?
- System name: _____________
- Is it 1C ERP? If so, which version: _____________
- Other ERP systems: _____________
- Data extraction method: ☐ Direct DB ☐ API ☐ File Export ☐ Other: _______

**Key tables/documents to extract:**
```
- Budget/Plan documents (source for DimPlannedBudgetItems)
- Actual expense transactions (source for fct_spends)
- Cost center master (source for cost_center dimension)
- Chart of accounts/Cost hierarchy (source for DimBudgetItems)
- Organizational structure (source for DimCompanyStructure)
- Employee master (source for DimEmployees)
- Transaction date ranges and current volumes
```

#### Q1.2: What is the current volume of transactions?
- Current year transactions (fct_spends): _________ records
- Years of historical data needed: _________ years
- Total estimated volume: _________ GB
- Peak periods: _____________
- Growth rate: _________ % annually

#### Q1.3: What transformations are needed from Bronze → Silver?
- Data validation rules: _____________
- Deduplication logic: _____________
- Hierarchical conformance (Cost structure mapping): _____________
- Date transformation needs: _____________
- Currency conversion: ☐ Yes ☐ No (if yes, which currencies: _____________)

---

### PRIORITY 2: Fact Table Details (Critical for Analytics)

#### Q2.1: What do AC, PC, and PN represent?
- AC = _________________________
- PC = _________________________
- PN = _________________________
- Are there other measures needed? _____________

#### Q2.2: What is the definition of each measure?
For each measure, document:
- Calculation formula: _____________
- Aggregation method (SUM, AVG, COUNT?): _____________
- Units (currency? quantity?): _____________
- Precision/decimals required: _____________

#### Q2.3: What are the grain-level keys for fct_spends?
- Primary key: document_id + line_no? Or another combination? _____________
- Is there a surrogate key needed? (sk_fct_spends is in design): ☐ Yes ☐ No
- What identifies uniqueness? _____________

#### Q2.4: Are there multiple types of spends?
- `spends_type` values in fct_spends — what are valid values? _____________
- How are they used in reporting? _____________
- Should they be a separate dimension? _____________

---

### PRIORITY 3: Dimensional Requirements (Critical for Usability)

#### Q3.1: DimBudgetItems — Cost Structure Detail
**Current Design:** Has ParentID (indicates 2-level hierarchy)
- Level 1 categories: _____________
- Level 2 subcategories: _____________
- Are there more levels needed?: ☐ Yes ☐ No (if yes, how many: _______)
- Does this hierarchy change over time (need SCD Type 2)?: ☐ Yes ☐ No
- How many total cost items: _________ (current), expected growth: _____________

#### Q3.2: DimCompanyStructure — Organization Hierarchy
**Current Design:** Hierarchical structure with Code and Name (Ukrainian + English)
- How many levels in org structure: _________ (typically 3-5)
- Is this organization stable or changes frequently: _____________
- Need to track historical changes (SCD Type 2)?: ☐ Yes ☐ No
- Total entities: _________ (current)

#### Q3.3: DimEmployees — Responsibility Tracking
**Current Design:** Id, Name, IsActive
- Do employees have department/cost center assignment?: ☐ Yes ☐ No
- Do they have manager/reporting relationships?: ☐ Yes ☐ No
- Separation of duties needed (role-based access)?: ☐ Yes ☐ No
- Need to track historical employee changes?: ☐ Yes ☐ No
- Total employees: _________ (active)

#### Q3.4: DimPlannedBudgetItems — Budget Master
**Current Design:** Id, Name, Code
- What is the grain? (By year? By period? By cost item?)
- Multiple budget scenarios?: ☐ Yes ☐ No (if yes, how many: ______)
- Budget status tracking (draft, approved, final?)?: ☐ Yes ☐ No
- Total planned budget items: _________

#### Q3.5: Dimension Conformation
- Can any dimensions be role-playing? (e.g., responsible_party_id as FK to DimEmployees): _____________
- Any slowly-changing dimensions (need version tracking)?: _____________
- Any dimensions that need effective-dating?: _____________

---

### PRIORITY 4: Reporting & Gold Layer (Critical for ROI)

#### Q4.1: What are the top 5 reports/dashboards needed?

**Report 1: ____________________**
- Audience: _____________
- Frequency: ☐ Daily ☐ Weekly ☐ Monthly ☐ On-demand
- Dimensions to drill: _____________
- Filters needed: _____________
- Expected users: _________

**Report 2: ____________________**
[Same template]

**Report 3: ____________________**
[Same template]

**Report 4: ____________________**
[Same template]

**Report 5: ____________________**
[Same template]

#### Q4.2: Ad-Hoc Analysis Patterns
- Most common analysis performed: _____________
- Typical time to answer a business question: _____________
- What data drill-paths are most common: _____________
- Any export/integration to other tools needed: _____________

#### Q4.3: Gold Layer Aggregations Needed
**The Silver layer supports detailed analysis. What summary layers are needed?**

```
Example aggregations:
- Actual vs Planned by Cost Level1 + Month
- Actual vs Planned by Department + Month
- Top 10 Over-budget Cost Centers
- Year-over-year budget variance
- Forecast remaining vs budget
```

List your required aggregations:
1. _____________
2. _____________
3. _____________
4. _____________
5. _____________

---

### PRIORITY 5: Data Quality & SLA (Critical for Operationalization)

#### Q5.1: Data Freshness Requirements
- How often does fct_spends need to refresh?: ☐ Daily ☐ Weekly ☐ Monthly ☐ Near-real-time
- Acceptable latency (e.g., "data ready by 8am each day"): _____________
- When are budgets updated?: ☐ Monthly ☐ Quarterly ☐ Annually
- Do dimensions need to refresh?: ☐ Daily ☐ Weekly ☐ Monthly

#### Q5.2: Data Quality Metrics
**What data quality issues exist today?**
- Known duplicates in expense data?: ☐ Yes ☐ No (estimate: ______%)
- Missing/null values?: ☐ Yes ☐ No (which fields: _____________%)
- Incorrect cost center assignments?: ☐ Yes ☐ No (estimate: ______%)
- Unreconciled transactions?: ☐ Yes ☐ No (estimate: ______%)
- Other data quality issues: _____________

#### Q5.3: SLA Requirements
- Maximum acceptable downtime: _____________
- Backup/recovery RTO (Recovery Time Objective): _____________
- Backup/recovery RPO (Recovery Point Objective): _____________
- Query performance target (e.g., "typical report runs <5 seconds"): _____________

---

### PRIORITY 6: Users & Access Control (Critical for Security)

#### Q6.1: User Groups & Access Levels
**Who will use this data warehouse?**

| Role | Count | Data Access Level | Tools Used | Frequency |
|------|-------|-------------------|-----------|-----------|
| CFO/Finance Director | | All | Power BI | Daily |
| Budget Managers | | Their departments | Power BI | Daily |
| Cost Center Owners | | Their cost center | Power BI | Weekly |
| Finance Analysts | | All | SQL/Power BI | As-needed |
| Auditors | | Subset (sensitive) | Power BI/SQL | Monthly |
| IT/Admins | | Technical | SQL | As-needed |

#### Q6.2: Row-Level Security (RLS) Needed?
- Should Budget Managers see only their department data?: ☐ Yes ☐ No
- Should Cost Center Owners see only their cost center?: ☐ Yes ☐ No
- Are there compliance/audit restrictions?: ☐ Yes ☐ No
- Need to restrict by legal entity?: ☐ Yes ☐ No

#### Q6.3: Data Sensitivity
- Is budget data confidential?: ☐ Yes ☐ No
- Are employee names/assignments sensitive?: ☐ Yes ☐ No
- Any compliance requirements (GDPR for employee data?)?: ☐ Yes ☐ No
- Data classification level: ☐ Public ☐ Internal ☐ Confidential ☐ Restricted

---

### PRIORITY 7: Implementation Constraints (Critical for Planning)

#### Q7.1: Infrastructure & Platform
- Current hosting: ☐ On-premises ☐ Azure Cloud ☐ Hybrid
- Azure subscription already exists?: ☐ Yes ☐ No
- Microsoft Fabric capacity available?: ☐ Yes ☐ No
- Budget constraints on cloud spend?: _____________

#### Q7.2: Integration & Orchestration
- Current ETL/pipeline tool: _____________
- Can use Fabric Data Factory?: ☐ Yes ☐ No
- Need to integrate with existing orchestration?: ☐ Yes ☐ No (which tool: _____________)
- Source system accessibility: ☐ Direct DB ☐ APIs ☐ Exports (restricted to _______ per day)

#### Q7.3: Timeline & Resources
- Target go-live date: _____________
- Internal FTE available for implementation: _________ hours/week
- External consulting needed?: ☐ Yes ☐ No (estimated hours: _______)
- Phased approach preferred?: ☐ Yes ☐ No (phases: _____________)

---

## Mapping Silver Layer to Source Data

### DimBudgetItems ← Budget Master Data
**Question:** Which source table contains the cost code hierarchy?
- Source table name: _____________
- Field for Level 1: _____________
- Field for Level 2: _____________
- Any additional hierarchy levels: _____________
- How often updated: _____________

### DimCompanyStructure ← Org Structure Data
**Question:** Which source contains the organization hierarchy?
- Source table name: _____________
- Fields for hierarchy: _____________
- How many levels in your org: _____________
- How often updated: _____________

### DimEmployees ← HR/Personnel Data
**Question:** Which source contains employee master data?
- Source table name: _____________
- Is this from HR system, 1C, or another source: _____________
- How often updated: _____________

### DimPlannedBudgetItems ← Budget Documents
**Question:** Which source contains the planned budget?
- Source table/document name: _____________
- Is this from planning system or 1C: _____________
- How is budget structure organized: _____________
- Multiple years of budget history: ☐ Yes ☐ No

### fct_spends ← Expense Transactions
**Question:** Which source contains the detailed expense transactions?
- Source table name: _____________
- Document type: _____________
- How are transactions identified uniquely: _____________
- Historical data available: _________ years
- Current record count: _________

---

## Validation Questions (To Confirm Design)

### Q1: Is the star schema correct?
- Are all necessary fact table measures captured (AC, PC, PN, others)? _____________
- Are all necessary dimensions represented? _____________
- Should any dimensions be split further? _____________
- Should any dimensions be combined? _____________

### Q2: Are there additional facts/dimensions needed?
- Any other analytical requirements not in current design? _____________
- Any performance optimization dimensions needed? _____________
- Any degenerate dimensions to add to fact table (e.g., document_type)? _____________

### Q3: Is the data grain appropriate?
- Is line-item grain (document + line_no) appropriate for all analysis? ☐ Yes ☐ No
- Do you need higher-level summaries (document level)?: ☐ Yes ☐ No
- Do you need lower-level detail (sub-line)?:☐ Yes ☐ No

### Q4: Are there missing dimensions?
- Product/Service dimension: ☐ Needed ☐ Not needed
- Vendor dimension: ☐ Needed ☐ Not needed
- Project dimension: ☐ Needed ☐ Not needed
- Customer/Department dimension: ☐ Needed ☐ Not needed
- Other: _____________

### Q5: Multi-version dimensions?
- Does the cost hierarchy change and need versioning?: ☐ Yes ☐ No
- Does the org structure change and need versioning?: ☐ Yes ☐ No
- Do employee assignments change and need versioning?: ☐ Yes ☐ No

---

## Next Steps to Complete This Assessment

1. **Data Source Validation** — Confirm source systems and data availability
2. **Bronze Layer Design** — Document transformations from source → Silver
3. **Gold Layer Design** — Define aggregations, reports, dashboards
4. **Data Quality Baseline** — Profile current data quality
5. **SLA Definition** — Confirm performance and availability targets
6. **Security & Access Control** — Design RLS and role-based access
7. **Implementation Roadmap** — Create phased delivery plan

---

## Assumed Gladpharm Context (To Validate)

✓ Focus: **Financial/Budget Analytics**
✓ Primary Use Case: **Actual vs Planned Cost Variance Analysis**
✓ Source System: **1C ERP (based on Ukrainian terminology)**
✓ Cloud Platform: **Microsoft Fabric**
✓ Data Model: **Star Schema with Budget & Org Hierarchies**
✓ Users: **Finance, Budget Managers, Cost Center Owners**

**Confirm these assumptions are correct:**
- [ ] Yes, this accurately describes Gladpharm's need
- [ ] Partial - need to revise (which areas: _____________)
- [ ] No - different focus (actual focus: _____________)

---

**Next Step:** Fill this form with Gladpharm stakeholders to complete the assessment foundation.
