# Gladpharm Assessment Report - Data Gathering Checklist

## 1. BUSINESS OVERVIEW

### 1.1 Business Background
- [ ] Company history and founding date
- [ ] Current size (employees, revenue, offices)
- [ ] Industry position and market share
- [ ] Main business lines/divisions
- [ ] Geographic presence (countries, regions)
- [ ] Key certifications (ISO, GMP, etc.)

**Questions to ask:**
- Who should provide this? (CEO, CFO, Business Director)
- Any existing company profile or annual report?

---

### 1.2 Current Pain Points & Challenges
- [ ] Current data storage solution (on-premises/cloud/hybrid?)
- [ ] Data systems in use (list all systems)
- [ ] Current reporting/BI tools
- [ ] Main data-related challenges
- [ ] Performance issues
- [ ] Data quality issues
- [ ] Manual processes that need automation
- [ ] Cost concerns

**Questions to ask:**
- What is the biggest frustration with current data systems?
- How much time is spent on manual data work weekly?

---

### 1.3 Business Goals for DWH
- [ ] Primary objective (cost reduction, better insights, faster decisions?)
- [ ] Timeline for implementation
- [ ] Success metrics
- [ ] Expected ROI
- [ ] Business units involved
- [ ] Key stakeholders

---

## 2. APPLICATIONS INFRASTRUCTURE

### 2.1 Source Systems Inventory
For each system, document:

**System Name:**
- [ ] System type (ERP, CRM, Finance, etc.)
- [ ] Technology stack (SQL Server, Oracle, PostgreSQL, API, etc.)
- [ ] Hosting (On-premises, AWS, Azure, other cloud)
- [ ] Current data volume (GB)
- [ ] Number of tables/objects
- [ ] Update frequency
- [ ] Current owner/administrator contact
- [ ] Connection details (if available)

**List all systems Gladpharm uses:**
1. 
2. 
3. 
4. 
5. 

---

### 2.2 Current Data Warehouse/BI Solution
- [ ] Current DWH platform (SQL Server, Oracle, Snowflake, etc.)
- [ ] Hosting location
- [ ] Current data volume stored
- [ ] Age of current solution
- [ ] Main issues with current solution
- [ ] BI tools used (Power BI, Tableau, Qlik, custom reports)
- [ ] How many users/reports in use

---

## 3. DATA REQUIREMENTS

### 3.1 Key Metrics/KPIs
For each metric, document:
- [ ] Metric name
- [ ] Definition/formula
- [ ] Unit of measurement
- [ ] Calculation logic
- [ ] Source system(s)
- [ ] Required dimensions
- [ ] Business owner

**Examples to consider:**
- Sales volume/value
- Inventory turnover
- Margin metrics
- Production metrics
- Cost analysis

**List key metrics (prioritized):**
1. 
2. 
3. 
4. 
5. 

---

### 3.2 Analytical Dimensions
For each dimension:
- [ ] Dimension name
- [ ] Source system
- [ ] Current values/hierarchy
- [ ] Need for historization (track changes over time?)

**Common dimensions to consider:**
- [ ] Product/SKU
- [ ] Customer/Counterparty
- [ ] Geography (Country, Region, Location)
- [ ] Business Unit/Department
- [ ] Time/Period
- [ ] Cost Center
- [ ] Legal Entity
- [ ] Other business-specific dimensions

---

### 3.3 Data Volume & Growth
- [ ] Current total data volume (GB)
- [ ] Expected growth rate (% per year)
- [ ] Peak data load periods (month-end, quarter-end, year-end?)
- [ ] Peak volume surge (how much higher than baseline?)
- [ ] Data retention requirements (how many years of history?)

---

## 4. USERS & ROLES

### 4.1 User Groups
For each role, document:
- [ ] Role name
- [ ] Number of users
- [ ] Primary responsibilities
- [ ] Data access needs
- [ ] Tools used
- [ ] Key person contact info

**Typical roles:**
- [ ] Project Manager
- [ ] System Administrator
- [ ] Data Engineer
- [ ] Data Analyst
- [ ] Business Analyst
- [ ] BI Developer
- [ ] End-user/Manager
- [ ] C-level stakeholder

---

### 4.2 Stakeholder List
- [ ] Name, Title, Department
- [ ] Email, Phone
- [ ] Decision authority level
- [ ] Key concerns/priorities

**Critical stakeholders to identify:**
- [ ] CFO/Finance Director
- [ ] Data Director/CTO
- [ ] Business Unit Heads
- [ ] IT Director

---

## 5. DATA CLASSIFICATION & SECURITY

### 5.1 Data Classification
For each data source:
- [ ] Classification level (Public, Internal, Confidential, Restricted)
- [ ] Regulatory requirements (GDPR, HIPAA, financial compliance?)
- [ ] Data sensitivity (PII, financial, customer data?)
- [ ] Retention policy
- [ ] Deletion/archival requirements

---

### 5.2 Security Requirements
- [ ] Current authentication method (AD, OAuth, etc.)
- [ ] Row-level security (RLS) needed? For which data?
- [ ] Encryption requirements (at-rest, in-transit)
- [ ] VPN/network access requirements
- [ ] Audit logging needs
- [ ] Compliance frameworks (ISO, SOC2, etc.)

---

## 6. CURRENT INFRASTRUCTURE

### 6.1 Network & Hosting
- [ ] On-premises data centers (locations)
- [ ] Cloud providers in use (AWS, Azure, GCP?)
- [ ] Network architecture (VPN, direct connect?)
- [ ] Firewall rules/restrictions
- [ ] Disaster recovery site(s)

---

### 6.2 Infrastructure Capabilities
- [ ] Current compute capacity
- [ ] Storage capacity
- [ ] Network bandwidth
- [ ] Infrastructure budget for DWH

---

## 7. DATA LOADING & INTEGRATION

### 7.1 Loading Strategy
For each source system:
- [ ] Full load or incremental load?
- [ ] If incremental: change detection method (CDC, timestamp, hash?)
- [ ] Loading frequency (hourly, daily, weekly?)
- [ ] Required SLA (when must data be ready?)
- [ ] Data freshness requirements

---

### 7.2 Data Quality
- [ ] Current data quality issues documented?
- [ ] Data validation rules in place?
- [ ] Data profiling done?
- [ ] Known data inconsistencies?
- [ ] Data quality metrics tracked?

---

## 8. TIMELINE & SCOPE

### 8.1 Project Timeline
- [ ] Target start date
- [ ] Target go-live date
- [ ] Project phases/milestones
- [ ] Key dates/deadlines

---

### 8.2 Scope Decisions
- [ ] Phase 1 scope (which systems/metrics first?)
- [ ] Future phases planned?
- [ ] Out-of-scope items

---

## 9. BUDGET & RESOURCES

### 9.1 Budget Information
- [ ] Total project budget allocated
- [ ] Budget for Azure cloud services
- [ ] Budget for tools/licenses
- [ ] Budget for team/resources

---

### 9.2 Available Resources
- [ ] Internal team size
- [ ] Available time commitment
- [ ] Need for external vendor/consulting?

---

## 10. CONTACTS & NEXT STEPS

### 10.1 Key Contacts
| Role | Name | Email | Phone |
|------|------|-------|-------|
| Project Sponsor | | | |
| Data Owner | | | |
| IT Lead | | | |
| Business Owner | | | |

---

### 10.2 Document Collection Needed
- [ ] Current system architecture diagram
- [ ] Data flow diagram
- [ ] Existing data dictionary/metadata
- [ ] Current reports list
- [ ] Performance baseline data
- [ ] User access matrix
- [ ] Any existing assessment documents

---

## NOTES FOR GLADPHARM TEAM:

**Priority Actions:**
1. Schedule kickoff meeting with key stakeholders
2. Identify project sponsor and steering committee
3. Gather system inventory (which systems exist?)
4. List top 5-10 most important metrics
5. Define user groups and access patterns
6. Document current pain points

**Recommended Approach:**
- Interview business users (what metrics do they need?)
- Meet with IT (what systems are in place?)
- Review existing documentation
- Assess current infrastructure
- Understand compliance requirements

---

**Compiled by:** [Your Name]
**Date:** [Date]
**Version:** 1.0
