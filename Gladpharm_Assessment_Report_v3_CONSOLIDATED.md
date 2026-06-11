# GLADPHARM ASSESSMENT REPORT
## Version 3.0 - Consolidated

**Confidential**

---

## TABLE OF CONTENTS

1. [Introduction](#introduction)
   - Purpose
   - Scope
   - Out of Scope
   - Definitions

2. [Business Overview](#business-overview)
   - Business Background
   - Problem Statement
   - Main Business Challenges and Needs
   - Business Goals

3. [Current State Assessment](#current-state-assessment)
   - Applications Infrastructure
   - System Landscape
   - Data Processing
   - Users and Roles
   - Data Classification and Risks

4. [Technical Infrastructure](#technical-infrastructure)
   - Network Architecture
   - Security and Compliance Needs
   - Resilience, Availability, and Disaster Recovery
   - Scalability Requirements

5. [Proposed Architecture](#proposed-architecture)
   - Data Warehouse Design (Medallion Architecture)
   - Silver Layer Model
   - Gold Layer Requirements

6. [Proof of Value](#proof-of-value)
   - Use Case Scope
   - Data Processing
   - Success Criteria

7. [Implementation Roadmap](#implementation-roadmap)
   - PoC Phases
   - Scaling Phases
   - Timeline and Milestones

8. [Budget and Resource Planning](#budget-and-resource-planning)
   - Azure Consumption Estimates
   - Resource Requirements

9. [Recommendations](#recommendations)

10. [Next Steps](#next-steps)

---

## INTRODUCTION

### Purpose

The purpose of this document is to present the comprehensive findings from the assessment conducted for Gladpharm Ltd. The report defines the project's boundaries across various dimensions, including business requirements, technical architecture, approach, and implementation roadmap. It serves as an agreement between the project team, the project sponsor, and key stakeholders.

This assessment evaluates both business and technical contexts, emphasizing how technical system implementation benefits the organization's strategic goals. The report includes business challenges, technical recommendations, and a phased implementation plan to guide future teams in implementing Gladpharm's future state data platform based on Microsoft Fabric.

### Scope

- Data consolidation from multiple sources (ERP, MS SQL, APIs, Excel, and more)
- Main business challenges in the data ecosystem
- System landscape and infrastructure assessment
- Performance requirements and data transfer specifications
- Users, roles, and access control
- Applications infrastructure and networking components
- Security and compliance needs
- Recommended improvements and migration strategy
- Proof of Value use case for budget analytics
- Implementation roadmap and cost projections

### Out of Scope

- Detailed analysis of current business processes (beyond data impacts)
- Complete system implementation
- Post-go-live support and optimization
- Employee change management beyond data team training

### Definitions and Abbreviations

| # | Term | Description |
|---|------|-------------|
| 1 | DWH | Data Warehouse |
| 2 | REST | Representational State Transfer |
| 3 | API | Application Programming Interface |
| 4 | ETL | Extract, Transform, Load |
| 5 | ELT | Extract, Load, Transform |
| 6 | PoV | Proof of Value |
| 7 | BI | Business Intelligence |
| 8 | CDC | Change Data Capture |
| 9 | SQL | Structured Query Language |
| 10 | DB | Database |
| 11 | EoM | End of Month |
| 12 | EoQ | End of Quarter |
| 13 | EoY | End of Year |
| 14 | SLA | Service-Level Agreement |
| 15 | RBAC | Role Based Access Control |
| 16 | ODS | Operational Data Store |
| 17 | OData | Open Data Protocol |
| 18 | HTTPS | HyperText Transfer Protocol Secure |
| 19 | TLS | Transport Layer Security |
| 20 | OAuth | Open Authorization |
| 21 | VM | Virtual Machine |
| 22 | IaC | Infrastructure as Code |
| 23 | CI/CD | Continuous Integration/Continuous Deployment |
| 24 | CFR | Central Funding Source |

---

## BUSINESS OVERVIEW

### Business Background

**Gladpharm Ltd** is a Ukrainian pharmaceutical manufacturer established in 1996 that has grown into one of the leading domestic players in the healthcare industry. The company has developed a strong presence across multiple therapeutic areas and maintains international standards.

**Company Profile:**
- **Founded:** 1996
- **Location:** Ukraine (Kyiv-based)
- **Core Business:** Development, manufacturing, and supply of generic medicines
- **Key Therapeutic Areas:** Cardiology, Endocrinology, Gastroenterology
- **Certifications:** International GMP standards compliance
- **Market Position:** Leading domestic pharmaceutical manufacturer
- **Employee Base:** Significant operational and technical workforce

**Business Strategy:**
Gladpharm emphasizes building resilient local production capabilities, investing in modern infrastructure and quality-control systems, and positioning itself as a reliable partner in Ukraine's healthcare ecosystem. The company demonstrates strong social responsibility and commitment to national healthcare security.

### Problem Statement

The main disadvantages of Gladpharm's existing data ecosystem are:

1. **Manual Data Processing**: Part of the company's data processing and reporting workflows is still performed manually, which increases effort and limits the frequency of report updates.

2. **Fragmented Data Integration**: Data from multiple operational systems is not yet fully integrated, which complicates end-to-end analytics and consolidated reporting.

3. **High Data Volume Complexity**: The company manages over **44.5 million records annually** across numerous systems (ERP, OData, REST API, Excel, Dataverse, Azure DB, SharePoint), creating complexity in data handling and synchronization.

4. **Lack of Unified Platform**: The absence of a centralized data platform results in disconnected processes and repeated data preparation efforts across departments.

5. **Inconsistent Data Quality**: Data-quality control is not fully standardized, as validation processes differ between systems.

6. **Limited Scalability**: The current setup limits scalability, flexibility, and the ability to efficiently produce accurate and timely analytical outputs, especially during peak periods (EoM, EoQ, EoY).

### Main Business Challenges and Needs

#### Key Business Challenges

| Challenge | Business Perspective | Technical Perspective |
|-----------|----------------------|----------------------|
| **Decentralized Data Architecture** | Dispersed data across numerous operational systems leads to duplicated efforts and higher maintenance costs | Absence of centralized data platform and governance model limits integration, scalability, and agility |
| **Manual Reporting Processes** | Manual preparation of summary tables increases workload and slows down reporting cycles, limiting ability to make timely decisions | Existing internally developed solution lacks full automation and central orchestration, reducing efficiency |
| **Inconsistent Data Quality** | Incomplete or inconsistent data across reports reduces trust in analytics and decision-making accuracy | Data-quality checks are applied unevenly with no unified or automated validation framework |
| **System Scalability Limits** | Peak periods (EoM, EoQ, EoY) overwhelm current capacity, delaying critical reporting | Infrastructure cannot elastically scale to handle 75% baseline growth during peak times |

#### Business Needs and Goals

| # | Business Need | Description |
|---|---|---|
| 1 | **Ensure Business Continuity** | Implement a robust and resilient data platform capable of processing high workloads from multiple operational systems while maintaining stable performance and ensuring uninterrupted analytical and reporting activities |
| 2 | **Efficient Analytical Reporting** | Develop an automated reporting environment that minimizes manual effort, enables daily or on-demand report generation, and supports timely and accurate business decision-making |
| 3 | **Scalable and Integrated Solution** | Establish a scalable, centralized architecture that consolidates data from all key sources (ERP, Finance, Treasury, Logistics) and ensures consistent, high-performance data access |
| 4 | **Enhanced Data Quality** | Improve overall data quality by standardizing validation and control mechanisms, automating checks, and implementing unified governance procedures across the organization |

---

## CURRENT STATE ASSESSMENT

### Applications Infrastructure

#### System Landscape

Gladpharm operates a diverse ecosystem of internal and external systems. Most systems are internal, connected via REST API or OData interfaces, while several external services (document management, GPS tracking) exchange data through REST APIs.

**System Inventory:**

| # | System | Description | Access Method | Data Type | Location |
|---|--------|-------------|----------------|-----------|----------|
| 1 | **ERP System** | Core enterprise application providing financial planning, budgeting, treasury operations, and cost management data | OData REST API | Structured | Internal |
| 2 | **Accounting System** | Accounting records, general ledger, financial reporting, and management accounting | OData REST API | Structured | Internal |
| 3 | **Transport Management** | Fleet management, vehicle usage, routes, and logistics performance | OData REST API | Structured | Internal |
| 4 | **MS SQL Server** | Multiple data domains: Sales transactions, Visit activity (medical rep interactions), Market analytics | Direct DB / API | Relational | Internal |
| 5 | **Odoo CRM** | Customer relationship management and sales pipeline | OData REST API | Structured | Internal |
| 6 | **Odoo Retail** | Retail operations and point-of-sale data | OData REST API | Structured | Internal |
| 7 | **Excel** | Project management, task tracking, manual data entry, departmental reporting | Manual Upload | Flat Files | Local |
| 8 | **Azure DB** | Business documents, contracts, approval workflows | REST API (JSON) | Semi-structured | External |
| 9 | **SharePoint** | Collaboration, document storage, cross-departmental integration | OData Web API | Semi-structured | Internal |
| 10 | **Dataverse** | Cloud-based data service for structured data storage | OData Web API | Structured | Internal |
| 11 | **Vehicle Tracking (GPS)** | Vehicle locations, movement history, geofencing | REST API (JSON) | Semi-structured | External |
| 12 | **External Data Sources** | Market data (NIQ), Yield data (Yieldigo), Respos API | REST API | Semi-structured | External |
| 13 | **Qlik Sense** | BI and visualization platform for dashboards and analytics | Direct Query | Processed Data | Internal |

#### Data Processing

**Current Approach:**
Data processing is performed through an internally developed integration platform that manages ETL/ELT workflows. The system supports horizontal scalability to handle growing data volumes. Processed data is loaded into analytical environments (Qlik Sense) for reporting and monitoring.

**Data Sources and Volumes:**

| System | Access Approach | Protocol | Annual Records | Data Volume |
|--------|-----------------|----------|-----------------|------------|
| ERP | API Server | OData | 2,000,000 | 6 MB/day |
| Planning & Budgeting | API Server | OData | 1,000,000 | - |
| Treasury | API Server | OData | 1,000,000 | - |
| Accounting System | API Server | OData | 1,000,000 | 2 MB/day |
| Transport Management | API Server | OData | 1,000,000 | 3 MB/day |
| MS SQL (Operational) | Internal Network | SQL | 38,000,000 | 60 MB/day |
| Sales Operations | Internal Network | SQL | 30,000,000 | - |
| Visit Activity | Internal Network | SQL | 5,000,000 | - |
| Market Analytics | Internal Network | SQL | 3,000,000 | - |
| Project Activity | Excel | File Upload | 1,000,000 | 0.1 MB/day |
| Azure DB (Documents) | REST API | JSON | 500,000 | 0.5 MB/day |
| Vehicle Tracking (GPS) | REST API | JSON | 1,000,000 | 0.5 MB/day |
| SharePoint & Dataverse | API | OData | 300,000 | 0.3 MB/day |
| **Total** | | | **44,500,000** | **~72.4 MB/day** |

**Historical Data Volume:** 500 GB - 1 TB (preliminary estimate)

#### Data Processing Schedule

| Data Source | Processing Deadline | Average Time | Maximum Time |
|-------------|-------------------|--------------|--------------|
| Raw Data (ERP, External APIs) | 05:00 AM | 2 hours | 3 hours |
| Dimensions Data | 5:30 AM | 15 minutes | 1 hour |
| Fact Tables | 7:00 AM | 30 minutes | 1 hour |
| Data Marts | 8:00 AM | 20 minutes | 40 minutes |

#### Data Migration Requirements

Key considerations for data migration:
- **Database Size & Complexity**: Estimate size, schema complexity (tables, indexes, stored procedures)
- **Initial Data Loading**: Bulk transfer of historical data (~500GB-1TB)
- **Incremental Updates**: Change data capture and synchronization during migration
- **Data Validation**: Verify integrity and consistency post-migration
- **Performance Baseline**: Current performance metrics needed for comparison

### Users and Roles

**Current User Groups:**

| # | Role | Description | Count | Primary Responsibilities | Access Level |
|---|------|-------------|-------|------------------------|--------------|
| 1 | **Administrator** | Manages infrastructure, user access, and security settings | TBD | Platform ops, user mgmt, security | Full |
| 2 | **Support** | Monitors solutions, handles deployments, ETL/ELT processes | TBD | PROD environment monitoring | Read-only |
| 3 | **Power BI Developer** | Develops reports and dashboards | TBD | Report creation, visualization | Read-only |
| 4 | **Developer** | Manages development processes, modifies codebase | TBD | DEV environment full control | Dev: Full / Prod: Read-only |
| 5 | **DevOps** | Automates deployment processes, IaC implementation | TBD | Deployment, infrastructure provisioning | Terraform access |
| 6 | **Data Owner** | Manages data, access permissions, usage policies | R. Khomenko | Data governance, compliance | Full |
| 7 | **Data Analyst** | Develops data marts, optimizes processes, analysis | R. Khomenko | Analytics, optimization | Full |
| 8 | **Finance Manager** | Budget review, financial analysis, reporting | Multiple | Analysis, decision-making | Read-only |
| 9 | **CFO / Finance Director** | Executive reporting, strategic analysis | 1 | Strategic decisions | Read-only |

**Key Contacts:**
- **Data Owner:** khomenko.r@gladpharm.com
- **Data Analyst:** khomenko.r@gladpharm.com

### Data Classification and Risks

| Data Source | Classification | Risk Level | Key Sensitivity | Regulatory Impact |
|-------------|-----------------|-----------|-----------------|------------------|
| **ERP** | Restricted | High | Financial data, budgets, treasury | Regulatory compliance required |
| **Accounting System** | Restricted | High | GL entries, financial records | Financial audit trail required |
| **Transport Management** | Internal Use Only | Medium | Logistics operations, schedules | Minimal regulatory |
| **MS SQL Operational** | Confidential | High | Sales, customer, competitive data | Privacy (GDPR if applicable) |
| **Excel (Projects)** | Internal Use Only | Medium | Project timelines, deliverables | Minimal regulatory |
| **Azure DB (Documents)** | Internal Use Only | Medium | Contracts, approvals | Legal/contract requirements |
| **Vehicle Tracking (GPS)** | Internal Use Only | Medium | Location data, routes | Employee privacy considerations |
| **SharePoint & Dataverse** | Internal Use Only | Medium | Internal docs, integration data | Minimal regulatory |

---

## TECHNICAL INFRASTRUCTURE

### Network Architecture

**Infrastructure Overview:**
Gladpharm operates a hybrid IT system with:

- **On-Premises:** Local data centers secured by Fortinet network appliances
- **Cloud:** Azure Environment with isolated network protected by Azure services
- **Connectivity:** Public internet (HTTPS, TLS) with IP allow lists and OAuth 2.0 authentication

**Current Network Components:**

1. **On-Premises Data Center**
   - Fortinet perimeter protection, traffic filtering, intrusion prevention
   - Active Directory for identity management
   - Network monitoring via Fortinet ecosystem
   - Direct database access for internal systems

2. **Azure Cloud Environment**
   - Network Security Groups for protection
   - No dedicated private channel (no ExpressRoute/VPN Gateway currently)
   - Synchronization between on-prem AD and Azure Entra ID

3. **API Gateway & Authentication**
   - Custom API Gateway for authenticated public endpoints
   - OAuth 2.0 security layer
   - TLS/HTTPS encryption for all data transmission

4. **Monitoring & Logging**
   - Security agent logs and system events
   - Sysmon data (process, file, DNS tracking)
   - Azure Defender audit logs
   - Fortinet network traffic logs
   - **Gap:** No centralized telemetry pipeline (Azure Monitor/Log Analytics not implemented)

### Security and Compliance Needs

**Required Security Measures:**

| Security Measure | Implementation | Objective |
|------------------|-----------------|-----------|
| **Data Encryption** | Encrypt-at-rest for sensitive data | Protect financial data and indicators |
| **Access Control** | Role-based access control (RBAC) | Restrict unauthorized access |
| **Secure Communication** | HTTPS/TLS for all data transmission | Prevent tampering during data exchange |
| **Geography Optimization** | Minimize latency for Ukrainian users | Optimize regional performance |
| **Data Integrity Checks** | Hash functions at processing stages | Detect unauthorized alterations |
| **Audit Trail** | Comprehensive audit logging | Compliance and security monitoring |
| **Identity Management** | Azure AD / OAuth 2.0 | Unified authentication |

**Compliance Requirements:**
- Financial data protection and audit trail requirements
- Potential GDPR compliance (if processing EU residents' data)
- Internal data governance policies
- Role-based access control enforcement

### Resilience, Availability, and Disaster Recovery

**Customer Expectations vs. Solution Requirements:**

| Requirement | Target SLA | Implementation |
|-------------|-----------|-----------------|
| **Solution Uptime** | ≥96% | Multi-region failover capability |
| **Data Warehouse Uptime (Weekdays)** | ≥98% | Automated backup and recovery |
| **Data Replication** | ≥2 data centers | Geo-redundant storage |
| **Automatic Backups** | Daily for DWH database | Daily snapshots with 24-hour retention |
| **Backup Replication** | ≥2 data centers | Cross-region replication |
| **Point-in-Time Recovery** | Supported | Full recovery < 24 hours |
| **VM Backups** | Automatic | All critical VMs protected |
| **Maintenance Window** | Saturday 4 PM - Sunday 4 PM | Outside business hours |

### Scalability Requirements

**Peak Time Demands:**
- Solution should handle **75% baseline growth** during peak periods (EoM, EoQ, EoY)
- Integrated monitoring system needed for auto-scaling decisions
- Elastic scaling for DWH and ETL components without recreation
- Minimal downtime during scaling

**Data Storage Optimization:**
- Raw data stored in low-cost storage
- Ability to re-process without source system access
- Compression ratio: 1:6 (160 GB for 1 TB uncompressed data)

---

## PROPOSED ARCHITECTURE

### Overview: Medallion Architecture with Microsoft Fabric

Gladpharm's proposed data warehouse follows the **Medallion (Bronze-Silver-Gold) Architecture** deployed in **Microsoft Fabric** on Azure cloud.

```
┌─────────────────────────────────────────────────────────┐
│ BRONZE LAYER                                            │
│ Raw data from all source systems (as-is)               │
│ • ERP, Accounting, Transport, MS SQL, APIs, Excel      │
│ • No transformations, minimal metadata added           │
└─────────────────────────────────────────────────────────┘
                          ↓ [Data Cleaning & Conformance]
┌─────────────────────────────────────────────────────────┐
│ SILVER LAYER                                            │
│ Cleaned, standardized, conformed data                   │
│ • Star schema structure                                 │
│ • Fact and dimension tables                             │
│ • Ready for analysis and integration                    │
└─────────────────────────────────────────────────────────┘
                          ↓ [Business Aggregations]
┌─────────────────────────────────────────────────────────┐
│ GOLD LAYER                                              │
│ Business-ready datasets for reporting                   │
│ • Aggregated fact tables                                │
│ • Summary dimensions                                    │
│ • Analytics and dashboard data                          │
└─────────────────────────────────────────────────────────┘
```

### Silver Layer Data Model

Gladpharm's analytical foundation is built on a **Star Schema** with one central fact table and supporting dimensions:

#### Fact Table: **fct_spends**

**Purpose:** Captures all expense transactions at line-item granularity

**Key Fields:**
- **sk_fct_spends** (Surrogate Key - Primary Key)
- **id** (Business Key - Transaction ID)
- **sk_date_id** (Foreign Key - Links to dim_date)
- **spends_type** (Transaction type - Actual vs Planned)
- **document_id** (Source document identifier)
- **line_no** (Line item number within document)
- **cost_level1** (First-level cost hierarchy)
- **cost_level2** (Second-level cost hierarchy)
- **cost** (Specific cost code)
- **cost_center** (Organizational cost center)
- **responsible** (Employee responsible for expense)
- **entity** (Legal entity/Organization)
- **cfr** (Central Funding Source)

**Measures:**
- **AC** (Actual Costs)
- **PC** (Planned Costs)
- **PN** (Pending Amounts)

**Metadata:**
- created_at, created_by (Data lineage)

**Data Grain:** Line-item level (Document + Line Number)

#### Dimension Tables

| Dimension | Purpose | Key Fields | SCD Type | Records |
|-----------|---------|-----------|----------|---------|
| **dim_date** | Time dimension for temporal analysis | sk_date_id (PK), calendar_date, day_of_month, month_name, quarter, fiscal_year, etc. | N/A (Static) | 3,650+/year |
| **DimBudgetItems** | Cost structure hierarchy | Id (PK), Name, ParentID (for hierarchy), NameEn | SCD 2 (track history) | TBD |
| **DimCompanyStructure** | Organization hierarchy | Id (PK), Name, Code, ParentID, NameEn | SCD 2 (track changes) | TBD |
| **DimEmployees** | Employee master | Id (PK), Name, IsActive | SCD 2 (track status) | ~TBD active |
| **DimPlannedBudgetItems** | Budget master data | Id (PK), Name, Code | Static | TBD |

### Silver Layer Characteristics

- **Schema Type:** Denormalized Star Schema
- **Optimization:** Optimized for analytical queries and drill-down analysis
- **Performance:** Supports fast aggregations and dimensional filtering
- **Historization:** Slowly Changing Dimensions (SCD 2) for tracking changes over time
- **Lineage:** Complete data lineage through technical fields

### Gold Layer Requirements

The Gold Layer will provide business-ready aggregations and reports:

**Planned Aggregations:**
1. **Actual vs Budget Analysis** - by Cost Level1, Month, and Organization
2. **Department Performance** - Budget variance by department and period
3. **Cost Center Analysis** - Top over-budget cost centers
4. **Year-over-Year Comparison** - Trend analysis and forecast
5. **Employee Responsibility Tracking** - Budget accountability by responsible party
6. **Organizational Roll-up** - Hierarchical budget analysis

---

## PROOF OF VALUE

### Use Case Scope

**Objective:** Demonstrate automation of a manual Excel-based budget reporting process using Microsoft Fabric and Power BI.

**Existing Process (Today):**
- Manual data extraction from ERP and budget system
- Excel consolidation and preparation
- Manual calculation of actuals vs planned
- Report "Бюджет наступного року по ЦФВ" (Budget Report by Central Funding Source)
- Email distribution to management

**Proposed PoV (Automated):**

| Aspect | Current State | Future State (PoV) |
|--------|---------------|------------------|
| **Data Source** | Manual ERP exports + Excel sheets | Automated API extraction from ERP |
| **Data Transformation** | Manual Excel formulas | Fabric notebooks + SQL transformations |
| **Report Update Frequency** | Manual (weekly/monthly) | Automated daily or on-demand |
| **Report Format** | Static Excel file | Interactive Power BI dashboard |
| **Refresh Time** | 2-4 hours manual work | 30 minutes automated pipeline |
| **Accuracy** | Manual entry errors (5-10%) | Automated validation (>99%) |
| **Distribution** | Email attachment | Shared portal with permissions |

### PoV Data Sources

**Primary Source:** ERP Database via OData API

**Dimensions Imported:**
- Статьи Бюджетов (Budget Items)
- Статьи Оперативних Бюджетів (Operational Budget Items)
- СтатьиОБ / Статьи Бюджета (Budget Articles)
- Користувачі (Users/Employees)
- Структура Підприємства (Company Structure)
- Організація (Organization)

**Fact Tables Imported:**
- Каз_БюдАдмін (Budget Master)
- Витрат_ОБ_Адмін (Administrative Expenses)

### PoV Processes

1. **Data Ingestion**
   - Daily extraction via ERP OData API (05:00 AM)
   - Automated authentication and error handling
   - Landing zone staging

2. **Data Transformation**
   - Bronze → Silver layer transformations
   - Hierarchy conformance (cost levels, organizational structure)
   - Dimension matching and validation

3. **Report Generation**
   - Automated aggregation and calculation
   - Power BI model refresh
   - Dashboard updates

### PoV Success Criteria

The PoV will be considered successful if:

✓ **Full Automation:** Microsoft Fabric automates 100% of previously manual data preparation  
✓ **Daily Refresh:** Fabric pipelines deliver automated daily or on-demand refresh  
✓ **Interactive Reports:** Power BI dashboard replicates existing Excel report structure with improved interactivity  
✓ **Significant Effort Reduction:** 80%+ reduction in manual effort (from 4 hours to 30 minutes)  
✓ **Data Accuracy:** Data validation shows >99% accuracy vs manual baseline  
✓ **Business Validation:** Finance team confirms report matches expectations  

---

## IMPLEMENTATION ROADMAP

### Phase 1: Proof of Value (PoC)

**Duration:** November 3 - December 9, 2025

#### Stage 1A: Data Analysis & Infrastructure Setup
- **Start:** Nov 3, 2025 | **End:** Nov 14, 2025
- **Activities:**
  - Deep-dive data source analysis (ERP structure, data lineage)
  - Infrastructure preparation in Azure
  - Network connectivity validation
  - OData API connectivity testing
- **Deliverables:**
  - Complete understanding of data sources
  - Connected Dev/Test environments
  - Ready-to-use Fabric workspace
  - API authentication configured

#### Stage 1B: Model & Report Development
- **Start:** Nov 14, 2025 | **End:** Nov 19, 2025
- **Activities:**
  - Develop initial data model (Bronze/Silver layers)
  - Create draft Power BI report
  - Data quality validation
  - Logic and structure verification
- **Deliverables:**
  - First working version of star schema
  - Draft Power BI report
  - Verified data structure and calculations

#### Stage 1C: Pipeline & Automation Development
- **Start:** Nov 19, 2025 | **End:** Dec 2, 2025
- **Activities:**
  - Develop Fabric data pipelines
  - Implement automated model refresh
  - Automate Power BI report updates
  - Deploy PoC to production environment
- **Deliverables:**
  - Fully automated ETL pipelines
  - Automated model refresh schedule
  - Deployed PoC solution
  - Testing environment validated

#### Stage 1D: UAT & Documentation
- **Start:** Dec 2, 2025 | **End:** Dec 9, 2025
- **Activities:**
  - User acceptance testing with Finance team
  - Issue resolution and refinement
  - Documentation and knowledge transfer
  - Sign-off from stakeholders
- **Deliverables:**
  - Validated PoC by business users
  - Complete PoC documentation
  - Knowledge transfer to team
  - Business sign-off

**PoC Expected Outcome:** Demonstrated feasibility, automation, and ROI potential

---

### Phase 2: Scaling Implementation (6 Months)

**Duration:** January 5 - April 5, 2026

#### Stage 2A: Architecture & Infrastructure Setup
- **Start:** Jan 5, 2026 | **End:** Jan 19, 2026
- **Fabric Capacity Provisioning:** F16/F32 based on projections
- **Environment Setup:** Dev/Test/Prod workspaces with RBAC
- **Gateway Configuration:** Secure connectivity to data sources
- **Lakehouse Structure:** Stage/Bronze/Silver/Gold layers
- **Security Implementation:** Encryption, access control, audit logging
- **Deliverables:**
  - Production-ready Fabric platform
  - All environments secured and configured
  - Automated RBAC implementation

#### Stage 2B: Data Ingestion & Integration Setup
- **Start:** Jan 19, 2026 | **End:** Feb 9, 2026
- **Onboarding All Sources:**
  - MS SQL (38M records)
  - ERP System (2M records)
  - Accounting System (1M records)
  - Transport Management (1M records)
  - CRM/Retail (Odoo)
  - External APIs (NIQ, Yieldigo, GPS)
- **Manual Data Process:** Templating for Excel/CSV files
- **Data Retention:** Automated retention policies
- **Deliverables:**
  - Unified data ingestion layer
  - Standardized manual upload process
  - Stable daily data collection (72.4 MB/day average)

#### Stage 2C: Modelling, Automation & CI/CD
- **Start:** Feb 9, 2026 | **End:** March 5, 2026
- **Bronze → Silver → Gold:** Complete transformations
- **Business Models:** ~500-550 dimensional tables, ~60-70% for DWH
- **Data Quality Framework:** Schema checks, load completeness, alerts
- **Pipeline Orchestration:** Dependency management, error handling
- **CI/CD Implementation:** Git versioning, environment promotion
- **Deliverables:**
  - End-to-end automated pipelines
  - Complete data quality monitoring
  - CI/CD-ready development lifecycle

#### Stage 2D: Reporting, Performance & Migration
- **Start:** March 5, 2026 | **End:** March 25, 2026
- **Historical Data Migration:** ~500GB-1TB legacy data
- **Existing Reports Migration:** Move current Power BI/Qlik reports
- **New Report Development:** Additional analytical dashboards
- **Performance Tuning:** EoM/EoQ/EoY peak load testing
- **SLA Verification:** Confirm 98% weekday, 96% overall uptime
- **Deliverables:**
  - Full historical data loaded
  - Migrated reports operational
  - Performance validated

#### Stage 2E: UAT, Documentation & Go-Live
- **Start:** March 25, 2026 | **End:** April 5, 2026
- **User Acceptance Testing:** Finance team comprehensive testing
- **Bug Fixes:** Issues resolved
- **Operational Documentation:** Runbooks, procedures, troubleshooting
- **Team Onboarding:** Training for support and analytics teams
- **Go-Live:** Production deployment and cutover
- **Deliverables:**
  - Production-ready solution
  - Fully trained support team
  - Complete operational documentation

**Full Implementation Timeline:** ~5 months from kickoff to go-live

---

## BUDGET AND RESOURCE PLANNING

### Azure Fabric Capacity Sizing

**Data Volume Estimates:**

| Component | Records/Year | Estimated Tables | Storage (Logical) | Storage (Compressed) |
|-----------|-------------|-----------------|-------------------|---------------------|
| ERP System | 2M | 130-200 | - | - |
| Accounting | 1M | 80-120 | - | - |
| Transport Mgmt | 1M | 50-70 | - | - |
| MS SQL (38M) | 38M | 150-200 | - | - |
| Other Sources | 3.5M | 15-25 | - | - |
| **Total Estimated** | **44.5M** | **425-615** | **1 TB** | **160 GB** |
| **Relevant for DWH (60-70%)** | | **255-430** | **~600 GB** | **100 GB** |

### PoV Scope Capacity

**PoV Data (ERP + Project Activity = 20% of total):**
- Logical Storage: 200 GB
- Compressed Storage: 35 GB

### Azure Consumption - Main Scope (Post-PoV)

**Option 1: Microsoft Fabric F16**
- **Monthly Cost:** $2,260.60
- **Annual Cost (1-year reserved):** $1,361.40/month ($16,337 annually)
- **Use Case:** Moderate analytical workloads, smaller user base

**Option 2: Microsoft Fabric F64**
- **Monthly Cost:** $8,876.80
- **Annual Cost (1-year reserved):** $5,280.00/month ($63,360 annually)
- **Benefit:** 100 free Power BI Pro licenses (~$1,400 savings)
- **Use Case:** Large-scale analytics, many concurrent users

### Azure Consumption - PoV Scope

**Option 1: Microsoft Fabric F4**
- **Monthly Cost:** $555.60
- **Annual Cost (1-year reserved):** $330.81/month ($3,970 annually)

**Option 2: Microsoft Fabric F8**
- **Monthly Cost:** $1,117.88
- **Annual Cost (1-year reserved):** $668.28/month ($8,019 annually)

### Resource Requirements

| Role | Phase | Effort | Notes |
|------|-------|--------|-------|
| **Fabric Architect** | PoC + Scaling | 200 hrs | Overall design, capacity planning |
| **ETL Developer** | PoC + Scaling | 300 hrs | Pipeline development, optimization |
| **Data Analyst** | PoC + Scaling | 150 hrs | Data modeling, quality rules |
| **Power BI Developer** | PoC + Scaling | 150 hrs | Report and dashboard development |
| **Data Engineer** | Scaling | 200 hrs | Infrastructure, CI/CD setup |
| **DevOps** | Scaling | 100 hrs | Terraform automation, deployment |
| **QA/Testing** | PoC + Scaling | 100 hrs | Testing, validation |
| **Business Analyst** | PoC + Scaling | 80 hrs | Requirements gathering, validation |
| **Total Internal Effort** | | **1,280 hrs** | ~8-10 months for 1 FTE team |

### Budget Summary

| Component | PoV Cost | Annual Cost (Full) |
|-----------|----------|------------------|
| **Fabric Capacity (F8 → F16/F32)** | $3,970 - $8,019 | $16,337 - $63,360 |
| **Other Azure Services** | $500 - $1,000 | $2,000 - $5,000 |
| **Professional Services** | $20,000 - $30,000 | - |
| **Internal Resources** | $64,000 - $96,000 | $64,000 - $96,000 (annual) |
| **Total Year 1** | **$88,470 - $135,019** | **$82,337 - $164,360** |

---

## RECOMMENDATIONS

### Immediate Priorities (Next 30 Days)

1. **Secure Executive Sponsorship**
   - Obtain CFO/Finance Director sign-off on approach
   - Secure budget allocation ($30K-$40K for PoC)
   - Establish steering committee

2. **Form Core Team**
   - Identify Fabric architect lead
   - Assign data engineer
   - Assign business analyst liaison

3. **Finalize PoV Scope**
   - Confirm budget report scope
   - Validate ERP data access
   - Sign off on timeline (Nov 3 start date)

### Short-Term Improvements (Months 1-2)

1. **Implement Data Quality Framework**
   - Establish validation rules for all sources
   - Automated data quality checks in pipelines
   - Daily quality metrics dashboard

2. **Establish Data Governance**
   - Define data ownership matrix
   - Create data stewardship roles
   - Document metadata standards

3. **Optimize Manual Data Processes**
   - Create Excel templates for manual entries
   - Implement file naming conventions
   - Standardize validation checks

### Long-Term Strategic Improvements (Months 3-6)

1. **Centralized Data Platform**
   - Consolidate all data sources into Fabric
   - Implement unified governance model
   - Enable self-service analytics

2. **CI/CD & DevOps**
   - Implement automated deployment pipelines
   - Git-based version control for all artifacts
   - Infrastructure-as-Code (Terraform) automation

3. **Advanced Analytics**
   - Predictive budgeting models
   - Anomaly detection in spending
   - Forecasting capabilities

4. **User Enablement**
   - Self-service BI training program
   - Advanced report development skills
   - Analytics center of excellence

---

## NEXT STEPS

### Immediate Actions (This Week)

- [ ] Schedule executive steering committee meeting
- [ ] Distribute this assessment to leadership for review
- [ ] Confirm budget allocation and resource commitment
- [ ] Identify primary PoV stakeholders and sign-off authority

### Pre-PoC Phase (Weeks 1-2)

- [ ] Finalize team assignments
- [ ] Set up development Azure subscription
- [ ] Establish secure communication channels
- [ ] Schedule detailed PoV kickoff meeting
- [ ] Begin detailed data source analysis
- [ ] Document ERP system architecture

### PoC Kick-off (Week 3)

- [ ] Deploy initial Fabric workspace
- [ ] Configure OData API connections
- [ ] Begin data exploration and profiling
- [ ] Create detailed project plan with deliverables
- [ ] Schedule weekly status reviews

### Success Indicators

**PoC Success Metrics:**
- Budget report fully automated by Dec 9
- 80%+ reduction in manual effort
- Report accuracy >99% vs manual baseline
- Daily refresh successfully executing
- Business stakeholder sign-off obtained

**Full Implementation Success (April 2026):**
- All 44.5M records successfully migrated
- 96% system uptime achieved
- 98% DWH uptime (weekdays)
- Zero SLA violations in first month
- All users trained and productive
- Cost optimization demonstrated

---

## APPENDICES

### A. Architecture Diagrams

[See accompanying draw.io and Lucidchart files]
- Gladpharm.drawio - Complete system architecture
- GladPharm of DWH Fabric Silver.json - Silver layer ER diagram

### B. Detailed Technical Specifications

**Data Model Specifications:**
- fct_spends: Line-item transaction detail
- dim_date: 3,650+ daily records
- DimBudgetItems: Multi-level hierarchy (SCD 2)
- DimCompanyStructure: Organizational hierarchy (SCD 2)
- DimEmployees: Employee master with status tracking
- DimPlannedBudgetItems: Budget master reference

**Processing Schedule:**
- 05:00 AM: Raw data extraction (2-3 hours)
- 05:30 AM: Dimension processing (15 min - 1 hour)
- 07:00 AM: Fact table processing (30 min - 1 hour)
- 08:00 AM: Data marts ready (20-40 minutes)

### C. Security & Compliance Checklist

- [ ] Data encryption at-rest implemented
- [ ] TLS/HTTPS for all data transmission
- [ ] RBAC configured and tested
- [ ] Audit logging enabled and monitored
- [ ] Backup and recovery procedures documented
- [ ] Disaster recovery plan tested
- [ ] Data classification applied to all tables
- [ ] Compliance requirements documented

### D. Risk Register

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|-----------|
| Data quality issues | High | High | Implement validation framework early |
| API connectivity problems | Medium | High | Redundant connections, error handling |
| Performance during peaks | Medium | Medium | Load testing, capacity planning |
| Resource availability | Medium | Medium | Cross-train team members |
| Scope creep | High | Medium | Strict change control process |

---

## DOCUMENT METADATA

| Property | Value |
|----------|-------|
| **Document Title** | Gladpharm Assessment Report - Consolidated |
| **Version** | 3.0 |
| **Date** | June 11, 2026 |
| **Classification** | Confidential |
| **Status** | Final |
| **Primary Author** | Data Architecture Team |
| **Review/Approval** | Pending |
| **Distribution** | Steering Committee, Project Sponsor, Key Stakeholders |

---

**End of Document**

---

## DOCUMENT SIGN-OFF

| Role | Name | Date | Signature |
|------|------|------|-----------|
| Project Sponsor | _________________ | __________ | _________________ |
| Finance Director | _________________ | __________ | _________________ |
| IT Director | _________________ | __________ | _________________ |
| Data Owner | R. Khomenko | __________ | _________________ |

---

*This assessment report is intended for use by authorized project team members and stakeholders only. Unauthorized distribution is prohibited.*

*For questions or clarifications, contact the Data Architecture and Analytics team.*
