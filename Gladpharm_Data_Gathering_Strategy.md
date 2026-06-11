# Gladpharm Assessment Data Gathering Strategy

## Overview
This document provides a phased approach to systematically collect all Gladpharm data needed to populate the assessment report (modeled on Yuria-Pharm Assessment Report v6.3).

---

## Phase 1: Stakeholder Identification & Kickoff (Week 1)

### Primary Stakeholders to Identify

| Role | Responsibility | Interview Priority | Timeline |
|------|-----------------|-------------------|----------|
| **Project Sponsor** | Business case, budget, timeline | 1 (kickoff) | Day 1 |
| **IT Director/CTO** | Infrastructure, systems, security | 1 (kickoff) | Day 1-2 |
| **Finance Director/CFO** | Current costs, budget, ROI | 2 (business) | Day 3-4 |
| **Data Owner** | Data inventory, quality, governance | 2 (technical) | Day 5-7 |
| **Business Unit Heads** | KPIs, metrics, pain points | 2 (business) | Day 5-7 |
| **IT Infrastructure Lead** | Current systems, hosting, networking | 2 (technical) | Day 5-7 |
| **System Administrators** | Access patterns, compliance, security | 3 (detailed) | Week 2 |
| **Data Stewards/Analysts** | Current reports, usage patterns | 3 (detailed) | Week 2 |

### Kickoff Meeting Agenda (2-3 hours)
1. Project objectives and scope (30 min)
2. Assessment report structure overview (20 min)
3. Data gathering timeline and expectations (20 min)
4. Roles and responsibilities clarification (20 min)
5. Schedule individual interviews (30 min)

---

## Phase 2: Business Context Gathering (Week 1-2)

### Interview 1: Project Sponsor & Finance Director

**Objective:** Understand business drivers, constraints, and success criteria

**Questions & Topics:**

#### Business Overview
- Company background (founding, size, market position)
- Current annual revenue and growth trajectory
- Number of employees by function (IT, Finance, Operations, etc.)
- Geographic presence and expansion plans
- Key industry certifications (GMP, ISO, regulatory compliance)

#### Current Pain Points
- Primary frustration with current data systems (quantify impact)
- Time spent on manual data work per week/month
- Delayed decision-making due to data latency
- Cost concerns with current infrastructure
- Specific incidents or near-misses due to poor data visibility

#### Business Goals for DWH
- Primary objective: cost reduction, better insights, faster decisions?
- Expected business outcomes (list top 5)
- Timeline for implementation (start/go-live dates)
- Success metrics and how they'll be measured
- Expected ROI and payback period

#### Budget & Resources
- Total project budget allocated
- Budget breakdown: Azure services, licenses, personnel, consulting
- Internal team availability (% FTE commitment)
- Need for external vendor/consulting support

---

### Interview 2: Business Unit Heads

**Objective:** Understand key metrics, KPIs, and analytical needs

**Questions & Topics:**

#### Key Metrics & KPIs (collect top 5-10 per unit)
For each metric, capture:
- Metric name and definition
- Current calculation method (manual, formula, system)
- Who currently uses it and how often
- Frequency of review (daily, weekly, monthly)
- Known data quality issues
- Desired future state

**Typical Pharmaceutical Metrics:**
- Sales volume and value (by product, region, customer)
- Inventory turnover and stock levels
- Margin analysis by product/line
- Production efficiency and yield
- Supply chain metrics
- Regulatory compliance tracking
- Customer satisfaction/retention

#### Business Processes
- Key monthly/quarterly business cycles
- Peak data demand periods (month-end, quarter-end, year-end)
- Critical decision points that need data support
- Reporting frequency and audience
- Current reporting tools and limitations

#### User Groups
- How many analysts per business unit?
- Decision makers who need data access
- Type of access needed (drill-down, top-level summary, etc.)
- Training needs and current skill levels

---

## Phase 3: Technical Infrastructure Gathering (Week 2-3)

### Interview 3: IT Director & Infrastructure Lead

**Objective:** Complete systems inventory and infrastructure assessment

**Questions & Topics:**

#### Source Systems Inventory
For each system, document:
- System name and purpose (ERP, CRM, Finance, etc.)
- Technology: SQL Server, Oracle, PostgreSQL, API, File-based?
- Hosting: On-premises, AWS, Azure, GCP, or hybrid?
- Data volume (GB), number of tables/objects
- Update frequency (hourly, daily, batch, real-time)
- Owner/administrator contact
- Connection details (server, port, authentication method)
- Known data quality issues

**Systems to identify:**
1. Primary ERP system (SAP, Oracle, Microsoft Dynamics?)
2. Financial systems (GL, AR, AP, Fixed Assets)
3. Inventory/Supply Chain systems
4. Manufacturing/Production systems
5. CRM system (customer data, sales)
6. HR/Payroll system
7. Any legacy or specialized systems
8. API-based data sources
9. File-based sources (Excel, CSV, FTP)

#### Current Data Warehouse/BI Solution
- Current DWH platform (SQL Server, Oracle, Snowflake, etc.)
- Hosting location and infrastructure
- Current data volume stored (GB, years of history)
- Age of current solution and refresh cycles
- Main issues with current solution
- BI tools used (Power BI, Tableau, Qlik, custom reports?)
- Number of active users and frequency of use
- Current report portfolio (list of critical reports)

#### Infrastructure Capabilities
- Current compute capacity (servers, processing power)
- Storage capacity and growth trends
- Network bandwidth (on-prem to cloud if applicable)
- Disaster recovery site(s) and RTO/RPO targets
- Infrastructure budget available for DWH

#### Hosting Strategy
- On-premises data center(s): location, capacity, constraints
- Cloud adoption status: AWS/Azure/GCP presence?
- Preference for on-prem, cloud, or hybrid?
- Any cloud governance policies or restrictions?

---

### Interview 4: Data Owner & System Administrators

**Objective:** Detailed data quality, security, and governance assessment

**Questions & Topics:**

#### Data Quality
- Known data inconsistencies across systems (document specific examples)
- Data profiling done? (if yes, share results)
- Data validation rules currently in place?
- Data quality metrics tracked?
- Most common data issues and their frequency

#### Security & Access Patterns
- Current authentication method (AD, OAuth, LDAP?)
- Row-level security (RLS) needed? For which data/users?
- Column-level security (CLS) needs?
- Object-level security (OLS) needs?
- Access patterns by role (finance, operations, executives)
- Audit logging requirements
- VPN or network restrictions for data access?

#### Data Classification & Compliance
- Data classification levels in place (Public, Internal, Confidential, Restricted)
- Regulatory requirements (GDPR, HIPAA, local compliance?)
- PII handling and protection requirements
- Financial data classification and requirements
- Data retention policies (how many years of history required?)
- Data deletion/archival requirements
- Compliance frameworks (ISO, SOC2, GxP?)

#### Master Data Management
- Master data domains (Product, Customer, Vendor, Cost Center, GL Account)
- Current master data quality and governance
- Need for master data integration/consolidation?
- Currently multiple customer/product codes across systems?

---

### Interview 5: Database Administrators & Integration Lead

**Objective:** Data loading and integration architecture

**Questions & Topics:**

#### Data Loading Strategy
For each source system:
- Full load or incremental load?
- If incremental: change detection method (CDC, timestamp, hash?)
- Current loading frequency (real-time, hourly, daily, weekly, batch?)
- Required SLA (when must data be ready by?)
- Data freshness requirements
- Peak load periods and volume surges

#### Current ETL/Integration Tools
- Current ETL tool (SSIS, Informatica, Talend, custom scripts?)
- Current data integration platform
- Orchestration tool (Azure Data Factory, Orchestrator, Airflow, cron jobs?)
- Error handling and retry mechanisms
- Monitoring and alerting capabilities

#### Data Transformation Needs
- Business rules that need to be applied
- Dimension conformance (standardize product codes, customer IDs?)
- Calculations and derived metrics
- Historical tracking requirements (SCD Type 2 needs?)
- Deduplication and record matching requirements

---

## Phase 4: Requirements & Design Alignment (Week 3-4)

### Interview 6: Business Analysts & Analytics Team

**Objective:** Analytical requirements and design validation

**Questions & Topics:**

#### Analytical Dimensions
For each dimension, identify:
- Dimension name (Product, Customer, Region, etc.)
- Source system(s) and master system
- Current value domain and hierarchies
- Need for historization (track changes over time - SCD Type 2?)
- Role-playing dimensions needed?
- Slowly Changing Dimension (SCD) type needed

**Typical Dimensions:**
- Product/SKU (with hierarchy: Category → Subcategory → Product)
- Customer/Counterparty (with hierarchy: Region → Country → City)
- Geography (with hierarchy: Continent → Country → Region → City)
- Business Unit/Department/Cost Center
- Time/Period/Date dimensions
- Legal Entity/Company
- Channel (Direct, Distributor, etc.)
- Promotional calendar
- Organizational structure

#### Reporting Requirements
- Most frequently requested reports (top 10)
- Report audience and access frequency
- Report performance requirements (refresh time)
- Drill-through capabilities needed?
- Ad-hoc analysis patterns
- Dashboard vs. detailed report balance
- Export/scheduling requirements

#### Advanced Analytics
- Time-series analysis needed?
- Forecasting requirements?
- Predictive modeling needs?
- Data science team engagement needed?

---

## Phase 5: Documentation Collection (Ongoing)

### Request the Following Documents

**Architecture & Design:**
- [ ] Current system architecture diagram
- [ ] Current data flow diagram
- [ ] Network topology diagram
- [ ] Database schema documentation

**Data & Metadata:**
- [ ] Existing data dictionary/metadata
- [ ] Entity relationship diagrams (ERDs)
- [ ] Data lineage documentation (if exists)
- [ ] Sample data export from source systems

**Reports & Metrics:**
- [ ] Current reports list and usage statistics
- [ ] Report ownership matrix
- [ ] Current report templates
- [ ] KPI definitions and dashboards

**Operations:**
- [ ] SLAs and performance baselines
- [ ] Incident/issue logs (data-related)
- [ ] Current runbooks/procedures
- [ ] User access matrix/RACI matrix

**Compliance & Security:**
- [ ] Current security policies
- [ ] Data classification scheme
- [ ] Compliance audit reports
- [ ] DLP/data governance policies

---

## Phase 6: Data Synthesis & Gap Analysis (Week 4)

### Mapping Collected Data to Report Sections

Organize findings into Yuria-Pharm report structure:

1. **Executive Summary** — Key findings from all interviews
2. **Business Context** — Company overview, pain points, goals
3. **Current State Assessment** — Systems, infrastructure, processes
4. **Data Landscape** — Sources, volume, quality, classification
5. **KPIs & Metrics** — Detailed metric specifications
6. **Analytical Dimensions** — Dimension inventory and hierarchy
7. **Data Quality Assessment** — Issues, gaps, remediation needs
8. **Security & Governance** — Current state, requirements, gaps
9. **Infrastructure Assessment** — Capabilities, constraints, recommendations
10. **Recommended Solution Architecture** — Medallion/Fabric design
11. **Disaster Recovery & Resilience** — Strategy and requirements
12. **Implementation Roadmap** — Phased approach with timeline
13. **Cost & Budget Analysis** — Sizing and ROI
14. **Next Steps & Action Items** — Executive action list

### Identify Gaps

After synthesizing data:
- What information is still missing?
- What needs clarification or follow-up?
- What trade-offs need business decision?
- What technical validation is needed?

---

## Timeline Summary

| Week | Deliverable | Status |
|------|-------------|--------|
| Week 1 | Kickoff, stakeholder identification, Phase 1-2 interviews | |
| Week 2 | Phase 2 completion, Phase 3 interviews | |
| Week 3 | Phase 3-4 completion, document collection | |
| Week 4 | Data synthesis, gap analysis, report outline | |
| Week 5+ | Report writing and validation | |

---

## Interview Preparation Checklist

For each interview:

- [ ] Confirm attendees and send prep materials 1 day before
- [ ] Share interview objectives and expected duration
- [ ] Request relevant documents in advance
- [ ] Set up recording (if permission granted)
- [ ] Prepare specific examples/scenarios for discussion
- [ ] Have Yuria-Pharm sample sections available for reference
- [ ] Send follow-up summary within 24 hours
- [ ] Schedule follow-up for clarifications within 1 week

---

## Next Actions

1. **Identify Gladpharm contacts** for each stakeholder role
2. **Schedule kickoff meeting** (Week 1)
3. **Prepare interview guides** (customize each for specific audience)
4. **Create feedback loops** (share drafts of assessment sections with stakeholders)
5. **Build assessment report document** (start populating as data arrives)
