# Gladpharm Assessment Interview Template

## Interview Metadata

- **Date:** ________________
- **Interviewer(s):** ________________
- **Interviewee(s):** ________________
- **Role/Title:** ________________
- **Department:** ________________
- **Duration:** ________________
- **Follow-up Required:** [ ] Yes [ ] No

---

## INTERVIEW: Business Context & Strategy

*Used for: Project Sponsor, Finance Director, Business Unit Heads*

### Section 1: Company Overview

**Q1.1: Can you describe Gladpharm's business - what we do, our market position, and key product lines?**

Response:
- Company size: _____________ employees
- Annual revenue: _____________ 
- Market position: _____________
- Geographic presence: _____________
- Key certifications: _____________

**Q1.2: What are the main pain points with your current data systems and reporting?**

Response (prioritized by impact):
1. _____________
2. _____________
3. _____________

**Q1.3: How much time is currently spent on manual data work per week?**

Response:
- Hours per week: _____________
- Primary activities: _____________
- Who is involved: _____________

### Section 2: Business Goals

**Q2.1: What is the primary objective for the new data warehouse? (Choose primary, note others)**

- [ ] Cost reduction (current spend: $_____________)
- [ ] Better business insights
- [ ] Faster decision-making (current cycle time: _____________)
- [ ] Compliance/governance improvement
- [ ] Data quality improvement
- [ ] Scalability for growth
- [ ] Other: _____________

**Q2.2: What would success look like 12 months from now?**

Response (measurable outcomes):
1. _____________
2. _____________
3. _____________

**Q2.3: What is the timeline for implementation?**

- Target start date: _____________
- Target go-live date: _____________
- Any hard constraints: _____________

**Q2.4: What is the expected ROI or payback period?**

Response: _____________

### Section 3: Key Stakeholders

**Q3.1: Who are the key decision-makers we need to involve?**

| Name | Title | Department | Email | Phone |
|------|-------|-----------|-------|-------|
| | | | | |
| | | | | |
| | | | | |

---

## INTERVIEW: Key Metrics & KPIs

*Used for: Business Unit Heads, Finance Director, Analytics Team*

### Section 1: Top Priority Metrics

**For each metric, please fill in:**

#### Metric #1: _________________________

- **Current definition/formula:** _____________
- **How currently calculated:** [ ] Manual [ ] Formula [ ] System
- **Source system(s):** _____________
- **Update frequency:** [ ] Daily [ ] Weekly [ ] Monthly [ ] Quarterly [ ] Other: _______
- **Who uses it:** _____________
- **How frequently used:** [ ] Daily [ ] Weekly [ ] Monthly [ ] As-needed
- **Known data issues:** _____________
- **Desired enhancements:** _____________
- **Priority (1-5, 1=highest):** _______

#### Metric #2: _________________________
[Same template]

#### Metric #3: _________________________
[Same template]

#### Metric #4: _________________________
[Same template]

#### Metric #5: _________________________
[Same template]

**Q: Are there other metrics we should capture? (List top 10 total)**

1. _____________
2. _____________
3. _____________

---

## INTERVIEW: Systems & Infrastructure

*Used for: IT Director, Infrastructure Lead, Database Administrators*

### Section 1: Source Systems Inventory

**For each system currently in use, fill in:**

#### System #1: _________________________

- **System type:** [ ] ERP [ ] CRM [ ] Finance [ ] HR [ ] Inventory [ ] Custom [ ] Other: _______
- **Technology:** [ ] SQL Server [ ] Oracle [ ] PostgreSQL [ ] API [ ] File-based [ ] Other: _______
- **Hosting:** [ ] On-premises [ ] AWS [ ] Azure [ ] GCP [ ] Hybrid [ ] Other: _______
- **Data volume:** _____________ GB
- **Number of tables/objects:** _____________
- **Update frequency:** [ ] Real-time [ ] Hourly [ ] Daily [ ] Weekly [ ] Batch [ ] Other: _______
- **Current owner/administrator:** _____________ (contact: _____________)
- **Connection method:** [ ] Direct connection [ ] API [ ] File export [ ] Other: _______
- **Authentication:** [ ] SQL Auth [ ] Windows Auth [ ] API Key [ ] Other: _______
- **Server/Endpoint:** _____________ (Port: _____________)
- **Known data quality issues:** _____________
- **Current access patterns:** _____________
- **Data sensitivity:** [ ] Public [ ] Internal [ ] Confidential [ ] Restricted

#### System #2: _________________________
[Same template]

#### System #3: _________________________
[Same template]

**Q: Are there other systems we should capture? (List all source systems)**

1. _____________
2. _____________
3. _____________

### Section 2: Current DWH/BI Solution

**Q2.1: What is the current data warehouse/BI platform?**

Response:
- Platform: _____________
- Version: _____________
- Hosting: [ ] On-premises [ ] Cloud [ ] Hybrid
- Age: _____________ years
- Current data volume: _____________ GB
- Years of history: _____________

**Q2.2: What BI tools are currently in use?**

Response:
- Primary tool: _____________ (users: _________)
- Secondary tool: _____________ (users: _________)
- Custom reports: [ ] Yes [ ] No (platform: _____________)
- Number of active reports: _____________
- Refresh frequency: _____________

**Q2.3: What are the main issues with the current solution?**

Issues (prioritized):
1. _____________
2. _____________
3. _____________

### Section 3: Infrastructure

**Q3.1: What is your current infrastructure capacity?**

Response:
- Compute: _____________
- Storage: _____________ (used: _____________, available: _____________)
- Network bandwidth: _____________
- Infrastructure budget available for DWH: $_____________

**Q3.2: Do you have disaster recovery infrastructure?**

- DR site location: _____________
- RTO requirement: _____________
- RPO requirement: _____________
- Current backup frequency: _____________

---

## INTERVIEW: Data Quality, Security & Governance

*Used for: Data Owner, System Administrators, Compliance Officer*

### Section 1: Data Quality

**Q1.1: What are the most common data quality issues?**

Issues (frequency - % of records affected):
1. _____________ (_______ %)
2. _____________ (_______ %)
3. _____________ (_______ %)

**Q1.2: What data validation rules currently exist?**

Response: _____________

**Q1.3: What is known about data inconsistencies across systems?**

Response: _____________

**Q1.4: Are there specific areas of high-quality data and low-quality data?**

High quality: _____________
Low quality: _____________

### Section 2: Security & Access

**Q2.1: What authentication method is currently in use?**

- [ ] Active Directory
- [ ] OAuth
- [ ] LDAP
- [ ] Database authentication
- [ ] Other: _____________

**Q2.2: What security levels are required?**

- [ ] Row-level security (RLS) — for which users/data: _____________
- [ ] Column-level security (CLS) — which columns: _____________
- [ ] Object-level security (OLS) — which objects: _____________
- [ ] Encryption at-rest: [ ] Yes [ ] No
- [ ] Encryption in-transit: [ ] Yes [ ] No
- [ ] VPN required: [ ] Yes [ ] No

**Q2.3: What is the current access model?**

Response:
| Role | User Count | Typical Access Patterns |
|------|-----------|----------------------|
| Executive | | |
| Manager | | |
| Analyst | | |
| Engineer | | |
| Other: | | |

### Section 3: Data Classification & Compliance

**Q3.1: How is data currently classified?**

Response (classification scheme in use):
- [ ] Public
- [ ] Internal
- [ ] Confidential
- [ ] Restricted
- Other: _____________

**Q3.2: What regulatory requirements apply?**

- [ ] GDPR (EU operations: [ ] Yes [ ] No)
- [ ] HIPAA (healthcare: [ ] Yes [ ] No)
- [ ] SOX (public company: [ ] Yes [ ] No)
- [ ] CCPA (California operations: [ ] Yes [ ] No)
- [ ] Industry-specific: _____________
- [ ] Local regulations: _____________

**Q3.3: What data sensitivity categories exist?**

- [ ] PII (personally identifiable information)
- [ ] Financial data
- [ ] Customer data
- [ ] Healthcare data
- [ ] Trade secrets
- [ ] Other: _____________

**Q3.4: What are the retention and deletion policies?**

Response:
- Retention period: _____________ years
- Deletion requirements: _____________
- Archival requirements: _____________

---

## INTERVIEW: Data Loading & Integration

*Used for: Database Administrators, Integration Lead, ETL Developers*

### Section 1: Current Data Loading

**For each critical source system:**

#### System: _________________________

**Q: What is the current loading approach?**

- [ ] Full load (frequency: _____________)
- [ ] Incremental load (frequency: _____________)
- Change detection method: [ ] CDC [ ] Timestamp [ ] Hash [ ] Other: _______

**Q: What are the SLA requirements for data availability?**

Response:
- Data must be ready by: _____________ (time of day)
- Frequency: [ ] Daily [ ] Hourly [ ] Real-time
- Maximum acceptable latency: _____________

**Q: What are typical data volumes?**

Response:
- Baseline volume: _____________ records
- Peak volume: _____________ records
- Peak periods: _____________
- Growth rate: _____________ % per year

### Section 2: Current ETL/Integration Tools

**Q2.1: What ETL/integration tools are currently in use?**

Response:
- Primary tool: _____________
- Secondary tool: _____________
- Orchestration: _____________
- Custom scripting: [ ] Yes [ ] No (language: _____________)

**Q2.2: What error handling exists?**

Response: _____________

**Q2.3: What monitoring/alerting is in place?**

Response: _____________

---

## INTERVIEW: Analytical Dimensions

*Used for: Business Analysts, Data Stewards, Analytics Team*

### Section 1: Key Dimensions

**For each important analytical dimension:**

#### Dimension: _________________________

- **Source system:** _____________
- **Current values/cardinality:** _____________ unique values
- **Hierarchy needed:** [ ] Yes [ ] No
  - If yes, structure: _____________
- **Historization needed (SCD Type 2):** [ ] Yes [ ] No
  - If yes, track from: _____________
- **Date dimension needed:** [ ] Yes [ ] No
- **Currently multiple codes across systems:** [ ] Yes [ ] No
  - If yes, clarify: _____________

#### Dimension: _________________________
[Same template]

#### Dimension: _________________________
[Same template]

---

## Follow-Up Actions

**Items requiring clarification:** 
1. _____________
2. _____________

**Documents to provide:**
- [ ] _____________
- [ ] _____________

**Next interview scheduled:** _____________ (with: _____________)

**Notes & Additional Context:**

_____________________________________________________________________________

_____________________________________________________________________________

_____________________________________________________________________________

---

## Interviewer Sign-off

- **Notes reviewed with interviewee:** [ ] Yes [ ] No
- **Interviewee approved summary:** [ ] Yes [ ] No (pending: _____________)
- **Follow-up required by:** _____________
- **Interviewer:** _________________ **Date:** _____________
