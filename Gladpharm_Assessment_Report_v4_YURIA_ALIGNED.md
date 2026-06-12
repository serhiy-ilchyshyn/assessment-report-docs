gladpharm

Assessment

report

# Introduction

## Purpose

The purpose of this document is to present the main findings from the assessment conducted during the DWH Implementation. It also defines the project's boundaries across various dimensions, including approach and roadmap, and serves as an agreement between the project team, the project sponsor, and key stakeholders. This document is intended for both business and technical audiences and does not cover the actual system implementation or provide detailed technical guidelines, projections, or presumptions. The Assessment Report covers both business and technical contexts without focusing specifically on either, emphasizing how the technical system implementation benefits the business. This report includes business challenges and recommendations from the analysis phase, and complements the accompanying documentation, deliverables, and diagrams. It is designed to serve as a guide for future teams and resources in implementing Gladpharm's future state data platform.

## Scope

- Data from multiple sources (ERP, MS SQL, OData, REST API, Excel, Dataverse, Azure DB, SharePoint) and related objects
- Applications infrastructure/networking components
- System landscape design
- Data warehouse with medallion architecture
- Recommended changes and improvements
- Analysis for requirements preparation
- CI/CD for different environments
- Security and compliance needs
- Orchestration module
- Data quality module
- Users and roles
- Proof of Value (PoV) use case and scope
- Documentation to the developed system

## Out of scope

- Analysis of current business processes
- Network connectivity setup between on-premises network and Azure

## Definitions

Definitions and abbreviations

| Term | Description |
|---|---|
| GP | Gladpharm |
| DWH | Data Warehouse |
| REST | Representational State Transfer |
| API | Application Programming Interface |
| DB | Database |
| BI | Business Intelligence |
| ETL | Extract, Transform, Load |
| ELT | Extract, Load, Transform |
| POV | Proof of Value |
| BG | Business Goal |
| UC | Use Case |
| AD | Active Directory |
| ERP | Enterprise Resource Planning |
| GB | Gigabyte |
| SCD | Slowly Changing Dimension |
| CDC | Change Data Capture |
| VLAN | Virtual Local Area Network |
| VPN | Virtual Private Network |
| SaaS | Software as a Service |
| PaaS | Platform as a Service |
| HTTPS | Hypertext Transfer Protocol Secure |
| RBAC | Role Based Access Control |
| ODS | Operational Data Store |
| CSV | Comma-Separated Values |
| SQL | Structured Query Language |
| EoM | End of Month |
| EoQ | End of Quarter |
| EoY | End of Year |
| SLA | Service-Level Agreement |
| DEV | Development |
| PROD | Production |
| VM | Virtual Machine |
| CI | Continuous Integration |
| CD | Continuous Delivery / Continuous Deployment |
| DC | Data Center |

# Business overview

## Business background

Gladpharm Ltd is a Ukrainian pharmaceutical manufacturer established in 1996 that has grown into one of the leading domestic players. Its core business involves developing, manufacturing and supplying generic medicines across several therapeutic areas including cardiology, endocrinology and gastroenterology, while adhering to international GMP standards.

From the business perspective, Gladpharm places emphasis on building resilient local production capabilities, investing in modern infrastructure and quality-control systems, and positioning itself as a reliable partner in Ukraine's healthcare ecosystem. The company also shows strong social responsibility and national-service orientation, highlighting its role in the supply of medicines during challenging times in Ukraine's environment.

## Problem statement

Gladpharm operates a complex and fragmented analytics environment involving multiple data sources, manual processes, and partially integrated operational systems. The current reporting ecosystem spans numerous systems (ERP, MS SQL, OData, REST API, Excel, Dataverse, Azure DB, SharePoint) and manages over 44 million records annually, each playing a critical role in financial planning, sales, logistics, and operational decision-making.

The main disadvantages of the existing solution are:

- Part of the company's data processing and reporting workflows is still performed manually, which increases effort and limits the frequency of report updates.
- Data from multiple operational systems is not yet fully integrated, which complicates end-to-end analytics and consolidated reporting.
- The company manages over 44 million records annually across numerous systems (ERP, OData, REST API, Excel, Dataverse, Azure DB, SharePoint, etc.), creating complexity in data handling and synchronization.
- Lack of a unified data platform results in disconnected processes and repeated data preparation efforts.
- Data-quality control is not fully standardized, as validation processes differ between systems.
- The current setup limits scalability, flexibility, and the ability to efficiently produce accurate and timely analytical outputs.

To overcome these challenges, there is an urgent need to develop a modern, scalable, and secure DWH using a medallion architecture. This new platform must enable seamless data integration, provide high data quality, ensure compliance with regulatory standards, and serve as a single source of truth for business analytics and strategic decision-making.

## Main business challenges and needs

Key business challenges

| Key Business Challenges | Business Perspective | Technical Perspective |
|---|---|---|
| Decentralized data architecture and limited flexibility | Dispersed data across numerous operational systems leads to duplicated efforts and higher maintenance costs. | Absence of a centralized data platform and governance model limits integration, scalability, and agility in developing new analytical solutions. |
| Manual and time-consuming reporting processes | Manual preparation of summary tables increases workload and slows down reporting cycles, limiting the ability to update reports frequently and make timely business decisions. | The existing internally developed data-processing solution lacks full automation and central orchestration, which reduces efficiency and complicates maintenance across multiple data sources. |
| Inconsistent data quality and limited governance | Incomplete or inconsistent data across reports reduces trust in analytics and decision-making accuracy. | Data-quality checks are applied unevenly, with no unified or automated validation framework implemented across all systems. |

Business needs

| Business Needs | Description |
|---|---|
| Ensure Business Continuity | Implement a robust and resilient data platform capable of processing high workloads from multiple operational systems while maintaining stable performance and ensuring uninterrupted analytical and reporting activities. |
| Efficient Analytical Reporting | Develop an automated reporting environment that minimizes manual effort, enables daily or on-demand report generation, and supports timely and accurate business decision-making. |
| Scalable and Integrated Solution | Establish a scalable, centralized architecture that consolidates data from all key sources (ERP, finance, etc.) and ensures consistent, high-performance data access for all divisions. |
| Enhanced Data Quality | Improve overall data quality by standardizing validation and control mechanisms, automating checks, and implementing unified governance procedures across the organization. |
| Historical data tracking | Accumulate historical data for trend analysis and informed business decisions, with the ability to return to a given state of an object. |

## Business goals

Considering the existing business challenges the next business goals should be addressed.

| BG-ID | BG description | BG benefits |
|---|---|---|
| BG-01 | Data-driven decision-making | Transition to making faster, more accurate, and efficient decisions based on data. |
| BG-02 | Process transparency | Create a single source of truth across all users and divisions. |
| BG-03 | Cost optimization | Reduce reporting and analytics costs, minimize duplication and manual efforts. |
| BG-04 | Data quality improvement | By using advanced data management and analytics tools, Gladpharm will be able to create a single source of truth for its data, improve data-quality processes, and achieve consistent compliance throughout its governance process. |
| BG-05 | Scalability and business continuity | Support growing data volumes and additional sources while maintaining stable performance during peak periods (EoM/EoQ/EoY). |

The implementation of a modern DWH platform will provide Gladpharm with significant strategic and operational advantages. It will enhance data processing capabilities, reduce manual effort and operational costs, and modernize the company's approach to business processes and technology usage. With advanced data management and analytics tools, the DWH platform will help Gladpharm address key challenges in data governance, ensure data consistency across departments, and support compliance with internal and external regulations. This transformation will empower faster, data-driven decision-making and foster a culture of innovation and efficiency across the organization.

The following use cases, aligned with the business goals above, are addressed by the proposed solution.

| UC-ID | UC description | UC benefits | Priority |
|---|---|---|---|
| UC-01 | Enterprise Data Consolidation Platform | Build a unified data consolidation platform that integrates all operational systems (ERP, MS SQL, Finance, Treasury, Logistics, Projects, etc.) into a single, governed environment. This provides a single source of truth, enables cross-domain analytics, and reduces duplicated data processing across departments. | 1 |
| UC-02 | End-to-End Automation and Scalability | Implement automated data workflows and scalable pipelines to process large data volumes efficiently and reliably. This reduces manual interventions and improves performance during peak data processing periods. | 1 |
| UC-03 | Advanced Analytical Capabilities | Develop advanced dashboards and analytics powered by high-quality, consolidated data. Automation within Microsoft Fabric reduces the number of manually built reports and provides faster, insight-driven decision-making. | 1 |
| UC-04 | Data Governance and Quality Management | Introduce a standardized governance framework covering data validation, lineage, access control, and compliance. This ensures transparency, accuracy, and regulatory alignment across all data assets. | 2 |
| UC-05 | Operational Efficiency and Cost Optimization | Optimize infrastructure and data-processing resource utilization through scalable architecture, reducing total cost of ownership while maintaining performance. | 2 |
| UC-06 | Improved User Experience and Collaboration | Provide business users and analysts with a modern, accessible data environment that simplifies collaboration, accelerates report creation, and ensures consistent use of reliable data. | 2 |

## Product fit and gaps

To identify which product best serves Gladpharm's needs, the current stack (manual Excel-based preparation, partially integrated operational systems, and Qlik Sense reporting) was evaluated against the business goals above. **Microsoft Fabric** is the recommended product: it provides a unified Lakehouse with the Medallion (Bronze–Silver–Gold) architecture, native Power BI integration, built-in orchestration, and elastic capacity — directly closing the gaps in the current environment.

| Capability needed | Current state (gap) | Fit with Microsoft Fabric |
|---|---|---|
| Single source of truth | Data fragmented across ERP, MS SQL, Excel, and other systems; no central platform | OneLake + Lakehouse consolidates all sources into one governed environment |
| Automated reporting | Manual summary tables; infrequent refresh | Fabric pipelines + Power BI enable daily/on-demand automated refresh |
| Data quality & governance | Uneven, non-standardized validation | Built-in Data Quality framework + Microsoft Purview governance |
| Scalability for peaks (EoM/EoQ/EoY) | Limited elasticity | Fabric capacity scales elastically without re-provisioning |
| Historical analysis | Limited historization | Delta Lake time-travel + SCD Type 2 historization |

Residual gaps to manage during implementation: Delta tables lack native primary/foreign keys (integrity enforced in the DQ layer), and the team requires skilling in Fabric, PySpark, and Power BI (see *Skilling plan*).

# Applications infrastructure

## System landscape

Gladpharm operates a diverse ecosystem of internal and external systems. Most systems are internal, connected via REST API or OData interfaces, while several external services (document management, GPS tracking) exchange data through REST APIs. Data is primarily stored in MS SQL databases and complemented by Excel, Dataverse, Azure DB, and SharePoint for additional inputs and collaboration. Analytical reporting is currently supported through Qlik Sense, which consumes and visualizes data from these sources.

Systems and services

| # | System | Description |
|---|---|---|
| 1 | OData-based systems | Internal business applications (such as ERP, planning) that provide access to operational and financial data through OData REST APIs within the internal infrastructure. |
| 2 | BAF | Accounting and transport management systems that provide access to operational and financial data through OData REST APIs within the internal infrastructure. |
| 3 | MS SQL | Microsoft SQL Server includes several key data domains, which are accessed directly within the internal network or through API connections for analytical and reporting purposes. |
| 4 | Systems exposing data via RESTful APIs | A set of internal and external systems, including Azure DB and SharePoint, that exchange data through REST API endpoints. These integrations enable automated data retrieval, synchronization, and interaction with external services. |
| 5 | Excel | Used as an internal data source for manual input, local data storage, and departmental reporting. Excel files are shared within the organization and can be integrated into analytical workflows through connectors or automated import processes. |
| 6 | Dataverse | A cloud-based data service used for structured data storage and integration with other business applications. Data is available through the OData Web API, enabling consistent access and automation within internal business processes. |
| 7 | Qlik Sense | A business intelligence and data visualization platform used for building dashboards and analytical reports. It allows users to connect to various data sources, perform transformations, and create interactive visualizations for business analysis. |

The table below identifies the data sources, their placement, and the destination data storage on Azure.

| DS_ID | Group of sources | Source type | Current placement | Authentication type | Destination | Note |
|---|---|---|---|---|---|---|
| DS-01 | ERP | Structured data via OData protocol | Internal server | OAuth 2.0 | Bronze (Lakehouse) | Primary PoV source |
| DS-02 | Accounting System (BAF) | Structured data via OData protocol | Internal server | OAuth 2.0 | Bronze (Lakehouse) | |
| DS-03 | Transport Management System | Structured data via OData protocol | Internal server | OAuth 2.0 | Bronze (Lakehouse) | |
| DS-04 | MS SQL (Sales, Visit Activity, Market Analytics) | Relational data (MS SQL) | Internal server | Internal network / API | Bronze (Lakehouse) | Highest volume |
| DS-05 | Excel (Project Activity) | Flat files (Excel / CSV) | Local computers | Manual upload | Bronze (Lakehouse) | Templated upload |
| DS-06 | Azure DB (Document Management) | Semi-structured (JSON via REST API) | External | OAuth 2.0 | Bronze (Lakehouse) | |
| DS-07 | Vehicle Tracking (GPS) | Semi-structured (JSON via REST API) | External | OAuth 2.0 | Bronze (Lakehouse) | |
| DS-08 | Other (SharePoint, Dataverse) | Semi-structured / reference data | Internal server | OAuth 2.0 | Bronze (Lakehouse) | |

## Data processing

The main need for data processing is a medallion architecture, a data design pattern used to organize data logically. Its goal is to incrementally and progressively improve the structure and quality of data as it flows through each layer of the architecture (from Bronze ⇒ Silver ⇒ Gold layer tables).

The terms bronze (raw), silver (validated), and gold (enriched) describe the quality of the data in each of these layers. By progressing data through these layers, the organization can incrementally improve data quality and reliability, making it more suitable for business intelligence applications.

There are three groups of stakeholders for the Data Warehouse:

- The first group consists of database developers and data engineers. They need access to the DWH to perform data cleaning and validation, build models, and develop pipelines.
- The second group consists of end report users, who do not need access to the DWH, as the vast majority of them view the reports through Power BI.
- The third group is data analysts. They require access to reports and to the Data Warehouse to work across multiple layers, such as the Silver and Gold layers, in order to extract valuable insights and generate reports.

At the data ingestion stage (bronze), no data processing takes place, as there is a need to store the data in the repository AS-IS, preserving the original format of each source system. Data cleanup, validation, and transformation are provided at the later stages (silver and gold), processed using Python notebooks and Spark jobs in Microsoft Fabric.

Data processing within Gladpharm is currently performed through an internally developed integration platform. This system manages ETL/ELT workflows — data extraction, transformation, and loading — and supports horizontal scalability to handle growing data volumes. Processed data is then loaded into analytical environments such as Qlik Sense, where it is used for reporting, performance monitoring, and management dashboards. In the recommendation section of this document, the Kyivstar team presents its vision on modern cloud integration technology and pipeline testing.

## Review and documentation of key metrics

This section documents the key metrics and analytical dimensions required to support Gladpharm's budgeting and financial analytics, beginning with the Proof of Value use case (budget planning and execution by CFR). The selected indicators are documented in terms of their definitions, calculation methods, and associated data sources to ensure consistency and traceability in subsequent analytical and reporting processes.

The information is structured as follows:

- Definition of Metrics: Names, common names, and formal definitions of the metrics.
- Metric Calculation: Formulas and units of measurement associated with each metric.
- Data Sources for Metrics: Source systems and databases from which the metrics are populated.

### Metrics

At this stage, the key budgeting and spend-related metrics were selected to support financial planning and cost management. *[TO CONFIRM — the full KPI catalogue beyond the PoV budget use case is to be finalized with Gladpharm business owners; the table below is drafted from the PoV `fct_spends` design.]*

Definition of metrics

| Metric Name | Common Name | Definition |
|---|---|---|
| AC | Actual Costs | The actual monetary amount spent against a budget item over a specific period, recorded from executed expense transactions. |
| PC | Planned Costs | The planned (budgeted) monetary amount allocated to a budget item for a specific period, defined in the annual budget. |
| PN | *[TO CONFIRM]* | A third spend measure carried in `fct_spends`. The exact meaning (e.g. previous-period plan or forecast/normative value) must be confirmed with Gladpharm finance. |
| Budget Variance | Budget Variance | The difference between planned and actual costs for a budget item over a period. |
| Achievement % | Budget Achievement Percentage | A metric showing how actual costs compare to planned costs over the selected period. |

Metric calculation

| Metric Name | Calculation Formula | Unit of Measurement |
|---|---|---|
| AC | ∑ Actual expense amount | UAH |
| PC | ∑ Planned budget amount | UAH |
| PN | *[TO CONFIRM]* | UAH |
| Budget Variance | Planned Costs − Actual Costs | UAH |
| Achievement % | Actual Costs / Planned Costs × 100% | % |

Data sources for metrics

| Metric Name | Data Sources |
|---|---|
| AC | ERP (actual expense transactions) |
| PC | ERP (planned budget documents) |
| PN | ERP *[TO CONFIRM]* |
| Budget Variance | Calculated using prior metrics |
| Achievement % | Calculated using prior metrics |

The listed metrics must be available across all the analytical dimensions specified below, except for specific cases where either the corresponding system does not store the required dimension, or the dimension is not relevant to the specific metric. In all other cases, the availability of metrics across the full set of dimensions is required to ensure consistency and comparability of analytical outputs.

### Dimensions

The table below describes the key analytical dimensions used in the reporting and data modeling processes. Each dimension is provided with a definition and a list of source systems from which the corresponding data is retrieved. *[TO CONFIRM — dimension catalogue derived from the PoV `fct_spends` star schema; to be extended for the full scope.]*

Dimensions and source systems

| Dimension Name | Common Name | Description | Data Sources | To historize |
|---|---|---|---|---|
| Budget Item | Budget Item | The cost-structure element of a budget (cost article / cost level hierarchy) against which spend is planned and recorded. | ERP (Статьи Бюджетов / Статьи Оперативных Бюджетов) | yes |
| Company Structure | Organization Hierarchy / CFR | The organizational unit and Center of Financial Responsibility (CFR) to which a spend is attributed. | ERP (Структура Предприятия) | yes |
| Employee | Responsible | The employee responsible for a given budget item or expense. | ERP (Пользователи) | yes |
| Organization | Legal Entity | The legal entity within the group to which the spend belongs. | ERP (Организация) | |
| Period | Period | The reporting period (monthly granularity) used for budget aggregation and comparison. | ERP / Calendar | Keep historical versions of budgets by period |
| Spends Type | Spends Type | Indicator of the originating source fact (e.g. Actual vs Planned) used to distinguish records consolidated into `fct_spends`. | ERP (derived from Recorder type) | |

The data necessary to support the described metrics and analytical dimensions must be fully loaded into the system, including complete datasets covering the entire available historical depth.

### Data sources

The table below summarizes the data loading strategies, synchronization frequency, and object types for each source system involved.

| Source | Object type | Loading Strategy | Data Collection Schedule (Kyiv time) |
|---|---|---|---|
| ERP | Dimensions: 6 objects, Facts: 2 objects (PoV) | Full Reload (PoV); incremental via hash comparison for scale phase | 1×/day Jan–Sep; 1×/hour Oct–Dec |
| MS SQL | Dimensions and facts across Sales, Visit Activity, Market Analytics | Update changed data using hash comparison; partition large tables by period | 4:00 everyday |
| Accounting System (BAF) | Structured financial objects | Update changed data using hash comparison | 4:00 everyday |
| Transport Management System | Operational/logistics objects | Update changed data using hash comparison | 4:00 everyday |
| Excel (Project Activity) | Flat files | Full Load via templated manual upload | On submission |
| Azure DB / REST API sources | Semi-structured objects | Incremental where feasible | TBD |

For the Proof of Value, the following ERP objects are in scope (six dimensions and two facts):

- Статьи Бюджетов (Dimension)
- Статьи Оперативных Бюджетов (Dimension)
- Статьи ОБ_СтатьиБюджета (Dimension)
- Пользователи (Dimension)
- Структура Предприятия (Dimension)
- Организация (Dimension)
- Каз_БюдАдминВитрат_ (Fact)
- ОБ_АдмінВитрат_RecordType (Fact)

# Data migration needs

The data will be loaded into the DWH from source systems to the full depth available in those sources. Migrating data from the existing solution, especially historical data, requires careful planning and several specific requirements to ensure a smooth, secure, and successful process.

The key requirements for this process are:

- **Database size and complexity:** Estimate the size of the database and the complexity of its schema, including tables, indexes, stored procedures, triggers, and functions.
- **Performance requirements:** Assess the current performance.
- **Initial data loading:** Perform an initial bulk transfer of historical data to the cloud environment.
- **Incremental data upload:** If required, use incremental data upload techniques to synchronize changes made during the initial upload phase.
- **Verify data:** Validate the migrated data to ensure that it matches the source data in terms of integrity and consistency.

The estimated total historical data volume is preliminarily 500 GB–1 TB (see the Budget section for capacity sizing).

# Performance requirements and data transfer requirements

The ETL should process data within the defined nightly window so that curated data is available by the start of business.

Data processing schedule

| Data Source | Processing Deadline | Average Processing Time | Maximum Processing Time |
|---|---|---|---|
| Raw Data (ERP, external) | 05:00 AM | 2 hours | 3 hours |
| Dimensions Data | 5:30 AM | 15 min | 1 hour |
| Fact Tables | 7:00 AM | 30 minutes | 1 hour |
| Data Marts | 8:00 AM | 20 minutes | 40 minutes |

Incoming data volumes per source

| Source | Daily data volume, MB | Data type | Location |
|---|---|---|---|
| ERP | 6 | Structured data exposed via OData protocol | Internal server |
| Accounting System | 2 | Structured data exposed via OData protocol | Internal server |
| Transport Management System | 3 | Structured data exposed via OData protocol | Internal server |
| MS SQL | 60 | Relational data (MS SQL) | Internal server |
| Excel (Project Activity) | 0.1 | Flat files (Excel / CSV) | Local computers |
| Azure DB (Document Management) | 0.5 | Semi-structured data (JSON from REST API) | External |
| Vehicle Tracking (GPS) | 0.5 | Semi-structured data (JSON from REST API) | External |
| Other Sources (SharePoint, Dataverse) | 0.3 | Semi-structured data | Internal server |

Performance and SLA considerations

| Performance Metric | Requirement |
|---|---|
| Data processing during peak times (EoM/EoQ/EoY) | Should not impact existing SLAs; prioritize new data |
| Response time for 80% of standard queries | Within 2 minutes |
| Impact of ad-hoc queries on solution performance | None (should not affect data processing, refreshes, etc.) |

The data presented above are approximate estimates based on currently available information. Actual volumes may vary depending on the reporting period, business activity, and integration frequency. These figures are intended for initial planning and assessment purposes and can be further refined.

# Data upload requirements

This section describes the functional requirements for the process of uploading data to the Bronze layer as part of the implementation of the Medallion architecture in the Data Lakehouse. The Bronze layer is designed to store raw data received unmodified from various sources in order to ensure its integrity, traceability to the original source, and further processing.

The requirements outlined in this section are intended to ensure reliable, controlled, and scalable data loading in a format that supports further cleansing, transformation, and analytics at the Silver and Gold levels. The section serves as a basis for developing ETL processes, defining technical and business expectations for processing incoming data, and forms the basis for further quality control and monitoring of the load.

## Requirements to control the emergence of new objects or changes in structures

| № | Requirement | Description |
|---|---|---|
| 1 | Loading all attributes of entities | The DWH must import all attributes of approved entities in accordance with the agreed requirements for each source system. Each table must be loaded in its entirety, including all relevant fields. Full data loading shall be performed daily with a guarantee of completion by 07:00 Kyiv time (on the Gold layer). |
| 2 | Notification of the appearance of a new entity | When a new entity (table or other data object) appears in the source system, responsible persons should automatically receive a notification containing information about the new entity and its affiliation with a particular system. It should also be possible to fix the list of objects that are present in the source but not yet integrated into the DWH. To do this, the source side must provide access to the full list of entities and their attributes (for example, through `information_schema.tables` and `information_schema.columns` in MS SQL). |
| 3 | Notification of adding a new attribute to an existing table | If a new attribute is added in the source system to a table integrated in the DWH, the system should automatically attempt to update the table structure in the DWH using the "schema merge" mechanism in Delta Tables, keep a log of such changes, and send notifications to responsible persons about the new attribute. |
| 4 | Notifications about deletion, renaming, or changing the data type of attributes or entities | In case of deletion of an entity or attribute, renaming of an attribute, or changing the data type of an attribute in the source system, the system should automatically generate notifications for responsible persons, indicating the entity, the changed attribute, and the nature of the change. This allows timely measures to prevent violations of data integrity and loading processes. |

## Requirements for the full data download process

| № | Requirement | Description |
|---|---|---|
| 5 | Full Load of entities | For reference tables and objects for which it is impossible to determine incremental changes, the full load strategy should be used — complete data updates with each import cycle. In cases where this does not critically affect system performance, it is recommended to switch to incremental data loading as much as possible in order to optimize resources and speed up the update process. |

## Requirements for the incremental data download process

| № | Requirement | Description |
|---|---|---|
| 6 | Incremental Load of entities | For all entities where technically feasible, a strategy should be defined to detect changes (delta) and load only new or updated records to the bronze level. To support efficient change detection and minimize data movement, a checksum-based delta detection strategy should be implemented where applicable. The source data is logically partitioned into segments (e.g. by business key ranges or other relevant criteria), and a hash or checksum is computed for each segment. These checksums are compared against their counterparts in the data warehouse. Segments with mismatched checksums indicate potential changes; only these segments are extracted and loaded into the staging area for further detailed comparison and processing. The incremental loading strategy should be adapted to the specifics of each type of data source, including MS SQL, ERP/OData, REST API, etc. |

## Requirements for the accumulation of history and the ability to return to a certain state of the object

| № | Requirement | Description |
|---|---|---|
| 7 | Accumulation of historical data | The system must provide continuous accumulation of change history for all entities at the bronze level. Historical data should be stored for the entire lifetime of the system without deleting or overwriting previous versions. Historization at the bronze layer enables the transfer of historical information and the extension of the historization process to upper layers when required. At the silver layer, full-depth historization of the dimensions defined in the dimensions table above is implemented using SCD Type 2 methodology. At the gold layer, current (actual) data is primarily retrieved, with the possibility to elevate specific historical dimensions from the lower layers if needed. |
| 8 | Access to data at a selected point in time | The ability to obtain data in the form in which it existed at a specific point in time may be required for analyzing retrospective changes and verification of analytical results. In Delta objects, the default retention period for historical data is 7 days; if necessary, this period can be extended, taking into account the growth of data volume. |

## Requirements for implementing data quality controls across data layers

As part of the DWH architecture built on Microsoft Fabric, particular attention is given to the implementation of data quality (DQ) controls across the bronze, silver, and gold layers. The key principles of the Data Quality module design are outlined below:

- **Layered approach to data quality checks.** The majority of DQ checks are implemented at the silver layer, ensuring that raw, unaltered data remains intact at the bronze layer. However, selected validations may also be performed directly at the bronze level, where early detection is required.
- **Use of staging tables.** At the bronze layer, staging tables are used primarily for initial data quality validations and for managing the data ingestion process. At the silver and gold layers, staging tables are used more selectively, typically for executing high-priority validations.
- **Use of alternative data quality validation methods.** Certain checks may be implemented as constraints at the database level. Alternatively, rules can be enforced via custom logic in the DQ module, or by using Microsoft Fabric capabilities such as dedicated views and reports.

Key data quality control scenarios include composite key uniqueness validation, format validation (e.g. for identifier fields using regular expressions), monitoring of anomalous drops or spikes in record volumes against historical baselines, and strict data-type validations to prevent incorrect values.

# Users and roles

| # | Role | Description | Data access / usage |
|---|---|---|---|
| 1 | Administrator | Manages infrastructure, user access, and security settings. | Full administrative access to the Fabric workspace and Azure resources; manages RBAC, does not consume analytical data directly. |
| 2 | Support | Monitors solutions, handles deployments, and ETL/ELT processes. Focuses on the PROD environment with read-only access to address user questions and issues. | Read-only access to PROD pipelines, logs, and DWH layers for monitoring and incident response. |
| 3 | Power BI Developer | Develops reports and dashboards with read-only access. | Read access to the Gold layer and semantic models to build and publish Power BI reports. |
| 4 | Developer | Manages development processes with full control over the DEV environment. Can modify the solution codebase for each component if necessary. Has read-only access to the PROD environment. | Read/write across Bronze/Silver/Gold in DEV; read-only in PROD. Accesses data through Fabric notebooks and the SQL endpoint. |
| 5 | DevOps | Automates deployment processes. Implements IaC principles using Terraform HCL. | Pipeline/infrastructure access; does not consume analytical data. |
| 6 | Data Owner | Manages data, including access permissions, usage policies, and monitoring data usage. | Approves access and data-quality rules; reviews data across layers; consumes governed reports. |
| 7 | Data Analyst | Handles data analysis processes, develops new data marts, and optimizes existing processes. | Read access to Silver and Gold layers via the SQL analytics endpoint and Power BI for ad-hoc analysis and data-mart development. |

| # | Role | Members |
|---|---|---|
| 1 | Administrator | TBD |
| 2 | Support | TBD |
| 3 | Power BI Developer | TBD |
| 4 | Developer | TBD |
| 5 | DevOps | TBD |
| 6 | Data Owner | khomenko.r@gladpharm.com |
| 7 | Data Analyst | khomenko.r@gladpharm.com |

*[TO CONFIRM — named members marked TBD to be provided by Gladpharm before implementation kickoff.]*

**Stakeholder engagement.** The solution serves three groups of data stakeholders, engaged across business, BI, and analytics functions:

- **Business users / executives** — consume governed Power BI reports and dashboards (e.g. budget-by-CFR analysis); do not access the DWH directly.
- **BI and analytics roles** — Power BI Developers and Data Analysts build reports and data marts on the Silver/Gold layers and engage with the Data Owner on metric definitions and data-quality rules.
- **Data engineering / platform roles** — Developers, Support, DevOps, and the Administrator build and operate the ingestion, transformation, and orchestration layers.

A dedicated **data-science persona** is **not in scope** for the current engagement (the workload is descriptive budget/financial analytics rather than predictive/ML modeling). The Fabric Lakehouse keeps this option open for the future without re-platforming. This scope should be confirmed with the Gladpharm sponsor.

# Data classification and related risks

| Data Source | Description | Classification | Risk |
|---|---|---|---|
| ERP | Stores core enterprise data related to financial planning, budgeting, treasury operations, and internal cost management. | Restricted | High risk — contains sensitive financial information; unauthorized access could result in financial loss or compliance violations. |
| Accounting System | Holds accounting records, general ledger entries, financial reporting information, and management accounting. | Restricted | High risk — includes confidential financial data; exposure could cause financial misstatements or regulatory non-compliance. |
| Transport Management System | Contains operational data on fleet management, vehicle usage, routes, and logistics performance. | Internal Use Only | Medium risk — may expose internal logistics operations and transport schedules. |
| MS SQL | Includes Operational Sales, Visit Activity (promotional interactions of medical representatives with healthcare professionals, conferences, and digital communication), and Market Analytics (market trends and competitive positioning). | Confidential | High risk — includes personally identifiable and commercial data; unauthorized access may cause privacy breaches, reputational harm, or competitive disadvantage. |
| Excel | Contains project management data, including task tracking, timelines, deliverables, and resource allocation. | Internal Use Only | Medium risk — exposure could reveal internal project structures, delivery timelines, or confidential development information. |
| Azure DB | Stores business documents, contracts, and approval workflows exchanged internally and with external partners. | Internal Use Only | Medium risk — unauthorized access could expose internal or partner documentation and agreements. |
| Vehicle Tracking (GPS) | Holds data on vehicle locations and movement history. | Internal Use Only | Medium risk — exposure may reveal logistical patterns, transport routes, or internal mobility details. |
| Other sources (SharePoint, Dataverse) | Contain semi-structured and reference data used for collaboration, document storage, and cross-departmental integrations. | Internal Use Only | Medium risk — exposure may reveal internal documents, shared resources, or integration data used in operational processes. |

# Applications infrastructure/networking components

## As-Is landscape

The customer's infrastructure is a hybrid IT system, hosted within:

- Local data centers secured by Fortinet network appliances, which provide perimeter protection, traffic filtering, and basic intrusion prevention capabilities.
- An Azure environment with an isolated cloud network protected by Azure services such as Network Security Groups.

There is currently no dedicated private channel to Azure such as ExpressRoute or VPN Gateway, meaning that all communication with external or cloud services occurs over the public internet using standard secure protocols (HTTPS, TLS). IP Allow lists and obligatory authentication provide an additional layer of defense. Network and endpoint monitoring are handled through the Fortinet ecosystem, which serves as the central network management system for the on-prem Data Center.

The organization gathers a comprehensive set of logs, including:

- Security agent logs and system events from endpoints.
- Sysmon data such as process launches, file creations, and DNS queries.
- Audit logs from Microsoft Defender.
- Fortinet network traffic logs, capturing ingress and egress flows.

At present, the environment does not utilize Azure Monitor or Log Analytics, and there is no centralized telemetry pipeline covering both on-premises and cloud resources. Monitoring is therefore siloed, focusing mainly on infrastructure-level and security events rather than application-level observability. Connectivity from cloud applications to on-prem data sources is established through authenticated public endpoints served by custom API Gateway instances. Identity management and access control are handled on a per-system basis, with limited integration into a unified identity provider such as Azure AD. Both on-prem Active Directory and Azure Entra ID are configured to perform synchronization.

## Future landscape

The Analytics Platform will be hosted and powered by Azure. The proposed solution is based on Microsoft Fabric and connects to Gladpharm's on-premises data sources using publicly exposed REST APIs managed by Azure API Management and protected by an OAuth 2.0 authentication layer. Data is ingested using the OData protocol. The architecture ensures scalability, performance, and end-to-end security while enabling seamless integration between data sources, data storage, and analytical tools. Building on the existing approach, access to customer data sources is provided using an API gateway with secure (TLS, HTTPS) and authenticated (OAuth 2.0) connections established over the public internet.

# Security and compliance needs

| Security Measure | Description |
|---|---|
| Data Encryption | Implement encryption at-rest to protect sensitive data, such as financial indicators. This ensures that even if unauthorized access occurs, the data remains unreadable and unusable, safeguarding its confidentiality and integrity. |
| Access Control | Utilize access control mechanisms to restrict access to the analytical solution and its underlying data. Implement role-based access control (RBAC) to ensure that only authorized personnel have access to specific data and functionalities based on their roles and responsibilities. |
| Secure Communication | Employ security protocols (e.g. HTTPS) to encrypt data transmission between different components of the analytical solution, including sources, integration components, data warehouse, analysis tools, and user interfaces. This prevents data tampering during data exchange, enhancing data confidentiality and integrity. |
| Geography Optimization | Optimize the solution for minimal latency for Ukrainian users, considering that all end users reside in Ukraine. Consider regional planning to address data availability and other region-specific risks. |
| Data Integrity Checks | Implement mechanisms to ensure data integrity throughout the data processing pipeline. Utilize hash functions to verify the integrity of data at different stages of processing, detecting any unauthorized alterations and maintaining data accuracy and reliability. |
| Regulatory & Industry Compliance | As a Ukrainian pharmaceutical manufacturer, Gladpharm is subject to Ukrainian personal-data protection legislation and, for any EU-related data, the EU GDPR. Pharmaceutical record-keeping practices (GxP / GDP) require traceability and auditability of data, supported by the Bronze-layer historization and audit trail. All end-user data resides in Ukraine, addressing data-residency requirements; no other industry- or geography-specific regulatory constraints were identified during the assessment. *[TO CONFIRM — applicable regimes to be validated with Gladpharm's compliance/legal function.]* |

Integrating these security measures into the solution allows the company to mitigate security risks, protect valuable data assets, and build trust with stakeholders, thereby enhancing the resilience and reliability of its operations and ensuring the confidentiality, integrity, and availability of sensitive data.

# Recommended changes and improvements

This document chapter covers the main opportunities and directions where the Kyivstar team sees the most valuable potential for future changes in Gladpharm.

| № | Module/Functional/Process | Description | Recommendations |
|---|---|---|---|
| 1 | Centralized Data Platform | Establish a unified data environment for all operational and analytical needs. | Implement a consolidated platform that integrates data from ERP, MS SQL, Accounting, Transport, and Project systems. This serves as a single source of truth, simplifying access, improving data reliability, and supporting analytics and reporting at the enterprise level. |
| 2 | Data Quality and Governance Framework | Define policies and automation for consistent, reliable data. | Introduce standardized data quality rules, validation checks, and governance policies across all data domains. Automating these controls minimizes manual intervention and ensures compliance with data management standards. |
| 3 | Templating the manual data sources | Set of policies and processes to control manual data sources. | Manual data sources are closely related to human data producers, who can make mistakes in data creation. To reduce errors, it is good practice to create templates for manual files (for example, templates of Excel files containing manual references). |
| 4 | Infrastructure as Code (IaC) | Automation and disaster recovery foundation. | Using Terraform to describe and deploy the entire DWH infrastructure ensures high availability and rapid recovery in case of incidents. Automation allows repeatability, quick rollback, and scaling, increasing platform resilience and minimizing downtime. |
| 5 | CI/CD Tool | Tool for continuous integration and deployment. | Provides centralized codebase versioning and automates deployments across environments, ensuring consistency and repeatability of releases. Facilitates collaboration by serving as a single source of truth for all developers. |
| 6 | Data Flow Management / Orchestration | Centralized control over data pipelines and their execution. | Manages and orchestrates complex data processing workflows with scheduling, triggering, and dependency tracking. Enables recalculation of business periods and ensures consistent, timely delivery of analytical results. |

The recommended changes and improvements above aim to streamline and optimize Gladpharm's existing workflows during the implementation of the new data consolidation platform. By implementing them, Gladpharm can use its data more effectively to drive business value, growth, and innovation.

# Resilience, availability, and disaster recovery requirements

The scalability of the solution stands as one of the key factors motivating the customer's choice to transition to the cloud.

**Projected Demand and Scalability:** Anticipated demand necessitates the solution's capacity to accommodate peak periods, during which data volume may surge up to 75% above the baseline. These peak intervals typically occur at month-end, quarter-end, and year-end. To address these demands, the solution should integrate a monitoring system that alerts when scaling up components becomes necessary. Elastic scaling up and down should be supported by the data warehouse database and ETL components, avoiding re-creations and minimizing downtime. Raw data sourced from the systems should be stored in cost-effective storage, permitting analysis and reprocessing without direct access to the source systems.

**Uptime and SLAs:** The customer requires the solution to maintain a minimum uptime of 96%, with the data warehouse upholding an SLA of at least 98% during weekdays. Scheduled maintenance should occur from Saturday 16:00 to Sunday 16:00 to mitigate disruptions during operational hours.

**Backup and Recovery:** Data housed in storage must be replicated across at least two distinct data centers, while the data warehouse database should enable automatic daily backups. Backup files should be replicated to at least two different data centers, restore from backup should support point-in-time recovery, and full recovery should not exceed 24 hours. All virtual machines containing data should have automatic backup configured, and all cloud component configurations should be centralized and stored separately (including change history).

**Conclusion:** The customer's expectations regarding scalability, monitoring, backup and recovery, and SLAs within Azure are well-defined. Fulfilling these expectations will be pivotal for the success of the migration initiative. Ensuring scalability, high availability, and resilience against disruptions is paramount, alongside rigorous testing of backup and recovery procedures.

# Data quality policy and framework establishment

A Data Quality Policy should be a set of guidelines that must be followed. This policy is integrated into the overall Data Governance framework of Gladpharm and aims to:

- Standardize corporate data within the platform based on Microsoft Fabric and medallion architecture.
- Define processes for data validation, cleansing, and quality improvement.
- Create a robust data quality monitoring framework to ensure data consistency, uniqueness, correctness, relevance, and completeness.
- Implement clear data quality metrics to continuously monitor, measure, and benchmark data quality performance.
- Define the structure and processes for timely elimination of data errors (Data Remediation).

Data Quality Management assesses how well data meets the organization's requirements and provides confidence in its accuracy. It helps to meet business needs and optimize the costs associated with maintaining data quality by measuring and monitoring quality levels and analyzing the cost and impact of issues.

Components of the Data Quality Framework implementation:

- **Data Quality Metrics** — clear indicators of data quality.
- **Data Quality Rules** — a set of rules for each metric.
- **Data Model** — defining models for storing rules, metrics, and errors in the Lakehouse (Bronze/Silver/Gold layers) within the medallion architecture.
- **Data Validation Pipelines** — building data validation pipelines based on Fabric Data Factory / Spark Notebooks / Fabric Pipelines.

The main metrics of data quality:

- **Correctness** — verification of the correctness of filling in the fields, using both simple rules (checking for null, negative values, valid range) and complex business logic (SQL or Spark queries against Bronze/Silver/Gold layer tables).
- **Consistency** — checks the integrity of foreign keys in fact tables — the presence of corresponding entries in directories.
- **Uniqueness** — checks business keys for uniqueness and searches for duplicates across Bronze/Silver/Gold layer data.

Implementation features in Microsoft Fabric: the Lakehouse is used to store data of different processing levels (Bronze → Silver → Gold), and Fabric Notebooks or Fabric Pipelines are used to create automated data validation and cleansing processes.

# Workflows orchestration

Data quality is closely related to workflow orchestration processes. Indicators such as timeliness (SLA), consistency, and completeness depend on how the source objects were processed. A DWH solution with complex data source entity dependencies, without proper workflow orchestration, will never become a single source of validated data because of possible data inconsistency. Failed data processing workflow executions also reduce data quality, which prevents the DWH from being used as a trusted data source. To solve these problems, a workflow orchestration engine can be used together with a data quality engine to increase data quality and avoid data inconsistency.

The existing client infrastructure has various data sources, which include different entities, and it is required to implement a workflow orchestration engine to keep DWH data in an actual, valid state in accordance with the existing business needs.

The workflow orchestration engine should meet the following requirements:

| # | Requirement |
|---|---|
| 1 | To support MS SQL Server as a data source to cover the project's scope |
| 2 | To support REST API as a data source to cover the project's scope |
| 3 | To support ERP/OData (e.g. 1C) as a data source to cover the project's scope |
| 4 | To support an Azure Storage Account as a data source to cover the project's scope |
| 5 | To be flexible in extending data source types |
| 6 | To support complex workflow scheduling (hourly/daily/monthly), including the ability to specify times and skip hours |
| 7 | To support different data ingestion patterns such as full loading and incremental loading with minimal configuration |
| 8 | To be flexible in extending data ingestion patterns |
| 9 | To support configuration and tracking of data source entity dependencies |
| 10 | To support workflow execution retries to cover the rerun executions strategy |
| 11 | To support storing of historical information about workflow executions (parameters, statuses, etc.) |
| 12 | To support workflow orchestration metrics monitoring |
| 13 | To support notifications about failed workflows |
| 14 | To provide a UI with the ability to restart failed workflows/activities |
| 15 | To support Microsoft Fabric as a primary service for data ingestion |
| 16 | To support calls to the Data Quality engine to validate data during ETL/ELT processes |
| 17 | To allow extending data ingestion orchestration with additional steps to refresh Power BI reports (useful in the future) |

# Single data repository

One of the greatest advantages of maintaining a centralized repository is the consolidation of all data sources in a single location. This central hub includes not only data from operational systems but also any supplementary data. With all data housed in one place, processes like conversion, analytics, and reporting can be executed without affecting existing production systems.

| Centralized Repository Advantages | Description |
|---|---|
| Unified Data Storage | Combines data from various sources, including operational systems and supplementary data. |
| Impact-Free Processing | Enables conversion, analytics, and reporting without disrupting production systems. |
| Historical Data Comparison | Facilitates direct comparison between legacy and post-conversion data at different time points. |
| Accelerated Validation | Speeds up the validation process by providing all relevant data as it existed at the time of conversion. |

To support Gladpharm's long-term data strategy and ensure scalability, flexibility, and governance, Kyivstar proposes to establish a centralized data platform on Microsoft Fabric. Microsoft Fabric provides a unified data foundation that brings together structured, semi-structured, and unstructured data from various internal and external systems (e.g. ERP, MS SQL, Accounting) into a single, governed environment. This platform leverages the Lakehouse architecture, which combines the scalability of a data lake with the performance and reliability of a traditional data warehouse.

Key benefits include:

- **Single source of truth:** all departments operate on the same consistent and verified data.
- **Tight integration with the Microsoft ecosystem:** native connectivity with Power BI, Microsoft Purview, and other Microsoft services.
- **Scalable and cloud-native:** automatically adjusts resources based on workload demands, removing the need for manual infrastructure scaling.
- **Supports real-time and batch data processing:** enables fast analytics and operational reporting with low-latency data access.
- **Improved time-to-insight:** through seamless access to curated data and pre-integrated analytical services.

## Microsoft Fabric Lakehouse concept

The Microsoft Fabric Lakehouse combines the flexibility and scalability of a traditional Data Lake with the data management features and performance of a Data Warehouse. Built on open standards like Delta Lake and integrated natively within Microsoft Fabric, it enables organizations to ingest, store, transform, and analyze vast volumes of data within a unified platform.

At its core, the Lakehouse in Fabric acts as a centralized data repository that stores raw data in its native format (Bronze layer) and gradually refines it through transformation stages (Silver and Gold layers). This layered Medallion Architecture allows for scalable and traceable data processing, supporting both exploratory data analysis and production-grade business intelligence. The Lakehouse creates a serving layer by automatically generating a SQL analytics endpoint and a default semantic model during creation.

| Advantages | Disadvantages |
|---|---|
| Unified Storage + Compute: native support for Spark and SQL workloads in one platform. | Requires initial transformation of raw enterprise data into lake-compatible formats (e.g. Parquet/Delta). |
| AI/ML Ready: centralizing raw and processed data enables easy access for machine learning and Copilot-powered features. | Lack of native support for primary and foreign keys in Delta tables — integrity must be enforced manually. |
| Lower Operational Overhead: fully managed environment — no manual setup of clusters or metadata stores. | Full potential is best unlocked by teams familiar with data engineering or scripting tools like SQL or PySpark. |
| Self-Service Friendly: deep Power BI integration allows business users to explore curated Gold-layer data. | Cloud Dependency: requires stable internet and reliance on Azure services. |
| Open Data Format: supports Delta Lake format, enabling ACID transactions and time-travel queries. | Maturity of the Platform: as a relatively new service, Microsoft Fabric may evolve and require architecture adjustments. |

The Bronze Layer in the Microsoft Fabric Lakehouse architecture represents an ideal foundation for building an Operational Data Store (ODS). It enables the storage of raw, unprocessed data in a centralized, scalable, and cost-efficient manner, while supporting both file-based and Delta table formats. Although often described as append-only, the Bronze Layer supports updates and deletions thanks to Delta Lake capabilities: rather than overwriting existing data, changes create new versions, preserving historical values and maintaining a complete audit trail.

# BI/ETL software modernization

The use of BI/ETL tools improves data governance and data processing efficiency within the organization. Such tools help end-users to be more flexible during development, data analysis, and business decision-making processes.

Gladpharm currently uses Qlik Sense as its BI tool. As part of the modernization, Microsoft Power BI is proposed as the primary visualization and reporting tool, providing the ability to build modern, complex analytical reporting solutions that connect to different data sources and data formats and deliver insights in different modes (static reports, scheduled refresh, near real-time data).

To modernize the integration part, Microsoft Fabric is used. Microsoft Fabric offers an all-in-one data platform that unifies ingestion, transformation, storage, and reporting in a single environment. Fabric natively supports the Lakehouse architecture and the Medallion (Bronze–Silver–Gold) data model, enabling more structured and scalable ETL pipelines. With built-in notebooks for advanced transformations, seamless integration with Power BI, and modern orchestration support, Fabric provides better performance, cost-efficiency, and development agility. As Microsoft's strategic platform for data, it ensures future-proofing through continuous innovation and deep ecosystem integration.

# Visual representation of As IS vs future landscape

## As IS landscape

Data is analyzed and aggregated for further processing. After aggregation, it is enriched with proprietary information (such as project and division mappings). Reports are then prepared manually, and the results are distributed to users via email. Although a dedicated data processing solution and Qlik Sense analytics exist within the client's landscape, the complexity of onboarding new processes through custom development prevents the process from being fully automated. The process starts with manual data collection from multiple operational systems.

## Future landscape

The proposed solution is based on Microsoft Fabric and deployed in Azure. It connects to the on-premises data sources from Gladpharm's environment using publicly exposed REST APIs managed by Azure API Management and protected by an OAuth 2.0 authentication layer. Data is ingested using the OData protocol. The architecture ensures scalability, performance, and end-to-end security while enabling seamless integration between data sources, data storage, and analytical tools.

**Azure DWH Environment**

- **Gladpharm DWH Workspace:** the main Microsoft Fabric Workspace, part of the Gladpharm Fabric Capacity. All Fabric Items needed for the ETL process and DWH storage are hosted here, such as data pipelines, notebooks, lakehouses, and warehouses.
- **Tenant-level App registrations:** Azure App registrations and their configuration needed to establish a secure and authorized connection between Fabric activities and the data sources' APIs.
- **Key Vault:** manages encryption keys, credentials, and connection strings used by pipelines or infrastructure provisioning tools.
- **Storage Account:** cloud-based storage for manual datasets, configuration files, or other static assets required for the ETL process.
- **Configuration Storage:** Azure Storage account required for environment configuration management performed by infrastructure provisioning tools.

Provisioning and configuration management are performed using Terraform HCL for infrastructure and configuration management of the DWH platform. The database schemas of the DWH storage layer are managed using Flyway migrations.

**Data Processing and Storage Layers**

- **ETL Workflow:** the Fabric Pipeline that orchestrates the ETL flow, containing data pipeline activities and Fabric notebook calls required for all stages of the ETL workflow.
- **Pipeline Activities:** predefined Fabric pipeline actions that handle automated data ingestion, transformation, and loading (ETL/ELT) from MS SQL, ERP, and manual sources.
- **Notebooks:** used for data actions not covered by Fabric pipeline activities or that require complex logic.
- **ERP OData API Connection:** a preconfigured API client for the external ERP data API service.
- **Managed Private Endpoints:** allow secure and private access to data sources or services managed by the Azure platform.
- **DWH:** serves as the central repository for raw and curated data, organized into Bronze (raw data ingested without transformation), Silver (cleaned and standardized data), and Gold (aggregated, business-ready datasets used by reporting tools) layers.
- **Landing Storage:** storage for temporary data ingested by the ETL workflow before promotion to the DWH, protecting the DWH from partial changes caused by failed ingestion processes.
- **ETL Metadata:** stores metrics produced by the ETL workflow and other required metadata.

**Reporting and Visualization**

- **Microsoft Power BI:** the primary visualization and reporting tool connected to the DWH, mainly to the Gold layer.

# Skilling plan

This skilling plan defines the key technical competencies required for the Gladpharm team to successfully adopt and operate the Microsoft Fabric-based data warehouse and analytics platform. It aligns required capabilities with the identified user roles and ensures readiness across data engineering and reporting functions. *[TO CONFIRM — current skill levels are estimated and should be validated with the Gladpharm team.]*

| Skill Area | Target Roles | Current Level | Training |
|---|---|---|---|
| Fabric Warehouse & Medallion Architecture | Data Analyst, Developer | None | Learning session + MS Learn guided modules |
| Data Ingestion & Pipeline Development | Developer, Support | None | Learning session + MS Learn guided modules |
| Notebook Development (Python, PySpark) | Developer | Basic | Project-based exercises |
| SQL-Based Data Transformation & Optimization | Data Analyst, Developer | Intermediate | Guided project exercises + reference documentation |
| Azure DevOps & Source Control (Git, CI/CD) | All technical roles | Basic | Practical Git/DevOps exercises + reference documentation |
| Data Quality Framework | Developer | None | Learning session + reference documentation |
| Workflow Orchestration & Monitoring | Developer, Support | None | Learning session + reference documentation |
| Fabric Workspace Management | Administrator, Developer | None | Learning session on Fabric workspace structure + how-to guides |
| Power BI Reporting | Power BI Developer, Data Analyst | Intermediate | Project-based exercises |
| Azure Resource Management & Security | Administrator, DevOps | Basic | Learning session + hands-on Azure Portal exercises |

Knowledge transfer will be integrated as a structured enablement phase toward the end of the implementation to ensure operational readiness of the Microsoft Fabric-based platform. The approach includes comprehensive how-to and architectural documentation, instructor-led learning sessions covering Fabric architecture and workspace structure, guided walkthroughs of the implemented solution, and practical exercises using real project components. Skilling success is measured by the Gladpharm team's ability to independently operate and extend the solution.

# Implementation roadmap

Based on the project business goals, we recommend implementing the solution in two phases: a Proof of Concept (PoC) phase, followed by a scaling implementation phase.

**Phase 1 — Proof of Concept (PoC)**

| Phase of PoC | Tasks | Start Date | End Date | Work Results |
|---|---|---|---|---|
| Stage 1 — Data Analysis & Infrastructure Setup | Data analysis; data collection; infra & network deployment | 03.11.25 | 14.11.25 | Full understanding of data sources; connected environments; ready infrastructure for next steps |
| Stage 2 — Model & Report Development | Model development; BI report development (non-automated); initial testing | 14.11.25 | 19.11.25 | First working version of the model; draft BI report; verified logic & data structure |
| Stage 3 — Pipeline & Automation Development | Data pipeline development; modelling automation; Power BI report automation; deployment to production | 19.11.25 | 02.12.25 | Automated pipelines; automated model refreshes; automated BI report refresh; deployed PoC solution |
| Stage 4 — UAT & Documentation | UAT testing; documentation | 02.12.25 | 09.12.25 | Validated PoC by business users; final PoC documentation & knowledge transfer |

**Phase 2 — Scaling Implementation**

| Phase of scaling | Tasks | Start Date | End Date | Work Results |
|---|---|---|---|---|
| Stage 1 — Architecture & Infrastructure Setup | Fabric Capacity (F16/F32) provisioning; Dev/Test/Prod workspaces & RBAC; network & gateway configuration; initial Lakehouse structure (Stage/Bronze/Silver/Gold); security setup (encryption, access control, audit) | 05.01.2026 | 19.01.2026 | Ready and secured Fabric platform; all environments prepared for development |
| Stage 2 — Data Ingestion & Integration Setup | Onboarding all data sources; building ingestion pipelines for each source; establishing data retention rules; manual file templating & validation (CSV/Excel) | 19.01.2026 | 09.02.2026 | Unified ingestion layer; standardized manual data upload process; stable daily data collection |
| Stage 3 — Modelling, Automation & CI/CD | Full Bronze → Silver → Gold transformations; business models for all entities; Data Quality Framework (schema checks, load completeness, alerts); pipeline orchestration & dependency management; CI/CD implementation (Dev → Test → Prod), Git versioning | 09.02.2026 | 05.03.2026 | Automated data pipelines; end-to-end model automation; CI/CD-ready development lifecycle; data quality monitoring in place |
| Stage 4 — Reporting, Performance, Migration | Migration of historical data (≈1 TB); migration of existing reports; development of new reports & semantic models; performance tuning (EoM/EoQ/EoY scenarios); SLA verification & load optimization | 05.03.2026 | 25.03.2026 | Full historical data in Fabric; optimized reporting environment; confirmed performance vs SLA |
| Stage 5 — UAT, Documentation & Go-Live | User acceptance testing; bug fixing & adjustments; operational documentation & handover; go-live & post-launch support | 25.03.2026 | 05.04.2026 | Production-ready solution; team fully onboarded; completed full implementation |

# Proof of Value (PoV) use case scope

**Description.** The Use Case reproduces the existing Excel report "Бюджет наступного року по ЦФВ" within Microsoft Fabric and Power BI. Data from ERP used for budgeting and financial reporting, along with reference catalogs (budget items, cost centers, and organizational units), is ingested, transformed, and aggregated automatically, replacing manual data preparation and consolidation. The resulting Power BI dashboard replicates the structure of the current Excel report, allowing filtering by organization, CFR, cost center, employee, and period, with export options for management review.

**Scope.**

- Data sources: ERP database
- Output: Power BI budget report with an agreed structure
- Processes tested: data ingestion, transformation, reporting
- Evaluated: data accuracy, report responsiveness, refresh speed, and user interactivity

**Expected outcomes.** Demonstrated automation of previously manual Excel-based budgeting and reporting workflows; reduced manual effort through automated data ingestion, transformation, and refresh in Fabric; improved data accuracy and consistency by consolidating data in a single environment; and a demonstration of how Microsoft Fabric simplifies reporting, ensures data integrity, and provides a scalable foundation for future analytics at Gladpharm.

**Success criteria.** The Proof of Value will be considered successful if Microsoft Fabric enables full automation of the report previously created manually in Excel, daily or on-demand refresh through Fabric pipelines, and delivery of an interactive Power BI report that replicates the existing structure while significantly reducing manual effort and demonstrating readiness for scalable, governed analytics within Gladpharm.

**Data processing for the PoV.** The source data is stored with monthly granularity. Data from the ERP instance is transmitted through a REST API using the OData protocol. The data collection schedule is once per day from January to September and once per hour from October to December, performing a Full Reload of the DWH.

**Structure of storage.** As an initial requirement, the business expects the following objects to be imported: Статьи Бюджетов, Статьи Оперативных Бюджетов, Статьи ОБ_СтатьиБюджета, Пользователи, Структура Предприятия, Организация (dimensions), and Каз_БюдАдминВитрат_, ОБ_АдмінВитрат_RecordType (facts). These objects are stored on the Lakehouse as-is following the naming convention `system_name_schema_name.src_tbl_name`. Each table contains the technical fields TechExecutorRunID, TechProcessorRunID, TechProcessingDateTime, and TechBusinessDateTime. The latest data snapshot is transferred into the Stage layer as-is using a pipeline with the DROP TABLE IF EXISTS option, then moved to the Bronze layer as-is through a stored procedure that accepts the table name and loading strategy (SCD1, SCD2, Full) as parameters. The Gold layer contains a single denormalized fact table, `FctSpends`, built from the above tables and a Calendar table, linked by `sk_date_id` and fed by a stored procedure using a Full Reload approach. The Gold table contains a surrogate key (`sk_fct_spends`) and the technical fields `created_at` and `created_by`. Since multiple source fact tables exist, `FctSpends` includes a `SpendsType` field indicating the originating source table.

Mapping of the columns describing how the fact table is built:

| Source Table.Column | Target Column | Comment |
|---|---|---|
| Surrogate key (ID) | sk_fct_spends | |
| ОБ_АдмінВитрат_RecordType.Recorder / Каз_БюдАдминВитрат_.Recorder | id | |
| ОБ_АдмінВитрат_RecordType.Period / Каз_БюдАдминВитрат_.Period | sk_date_id | e.g. 20260101 / 20250101 |
| SourceFlag (Actual2025, Planning2025) | spends_type | Built based on Recorder type |
| ОБ_АдмінВитрат_RecordType.Документ_Key / Каз_БюдАдминВитрат_.Документ_Key | document_id | |
| Каз_БюдАдминВитрат_.LineNumber | line_no | |
| Статьи ОБ | cost_level1 / cost_level2 / cost | |
| Структура Предприятия.Description | cost_center / cfr | |
| Пользователи.Description | responsible | |
| Организация | entity | |
| ОБ_АдмінВитрат_RecordType.Сума / Каз_БюдАдминВитрат_.Сума | PC, AC, PN (Total) | StandardODATA amount × −1 where applicable |

# Assumptions and limitations

This section summarizes the main assumptions and limitations based on which the solution vision and scope are designed and described in this document.

| ASSUMP-ID | Name | Description |
|---|---|---|
| ASSUMP-01 | Data quality | Data quality rules and their priorities should be defined and approved by data owners. |
| ASSUMP-02 | Workflows schedules | Data processing workflow schedules should be defined and approved by data owners. |
| ASSUMP-03 | Workflows dependencies | Data processing workflow dependencies should be defined and approved by data owners. |
| ASSUMP-04 | DWH implementation | The DWH implementation should be split into different phases in accordance with business prioritization. |
| ASSUMP-05 | Data sources ingestion priority | The first (PoV) phase of data source ingestion should include the ERP and Project Activity sources only. |
| ASSUMP-06 | Loading of heavy MS SQL objects | Some MS SQL objects contain large volumes of data and currently support only a full-load pattern. The client should revise and optimize the loading strategy for these objects before ingestion implementation. |
| ASSUMP-07 | Notification templates | Workflow orchestration notification templates should be defined and approved by data owners for every separate case before implementation. |
| ASSUMP-08 | Workflows compute engine | The workflows compute engine should be built using Microsoft Fabric, where possible. |
| ASSUMP-09 | Network connectivity | Network connectivity setup between the on-premises network and Azure is out of scope; connectivity is established over authenticated public endpoints. |
| ASSUMP-10 | Object count for capacity estimation | The total number of objects could not be fully collected; capacity estimates are based on industry-typical assumptions and previous experience (see Budget). |

# Budget

Dedicated Team engagement model with a Fixed Price billing model. Payments under this project are made according to the progress of completed work and the rates defined in the contract.

| Role | Description | FTE |
|---|---|---|
| Project Manager | Responsible for overall project management, planning, monitoring, and client communication. | 1 |
| Solution/Data Architect | Designs the DWH architecture, ensures proper data integration, and selects optimal solutions. | 1 |
| Data Analyst | Analyzes data, defines business requirements, and creates data models for the data warehouse. | 1 |
| Data Engineer | Implements ETL processes; responsible for data migration, transformation, and integration. | 2 |
| DevOps | Ensures stable infrastructure operation, deployment automation, and system monitoring. | 1 |
| QA | Performs data warehouse testing; checks data quality and solution compliance with requirements. | 1 |

*[TO CONFIRM — team composition and FTE counts above are indicative and should be aligned with the final contract.]*

**Capacity sizing inputs.** Based on questionnaire sessions, the following metrics were collected for consumption estimation:

| System | Access Approach | Access Protocol | Projected records per year |
|---|---|---|---|
| ERP | API Server | OData | 2,000,000 |
| Planning and Budgeting | API Server | OData | 1,000,000 |
| Treasury | API Server | OData | 1,000,000 |
| Accounting System | API Server | OData | 1,000,000 |
| Transport Management System | API Server | OData | 1,000,000 |
| MS SQL | Internal Network or API Server | MS SQL | 38,000,000 |
| Sales Operations | Internal Network or API Server | MS SQL | 30,000,000 |
| Visit Activity | Internal Network or API Server | MS SQL | 5,000,000 |
| Market Analytics | Internal Network or API Server | MS SQL | 3,000,000 |
| Project Activity | Excel | Excel | 1,000,000 |
| Document Management | REST API | REST API | 500,000 |
| Vehicle Tracking (GPS) | REST API | REST API | 1,000,000 |
| Other (SharePoint, Dataverse, Azure DB) | Mixed | REST API / OData Web API | 2,500,000 |
| **Total** | | | **44,500,000** |

The total historical data volume (actual) is preliminarily 500 GB–1 TB. Using the Fabric Calculator guidance ("if you only have the logical/uncompressed value, divide it by 6"), the value of 160 GB is used for the calculator. The total number of objects could not be collected; based on the collected metrics and previous experience, the estimated number of source tables is 500–550, of which 60–70% (≈300–385 tables) are relevant for the DWH. For the PoV (ERP and Project Activity), 145–225 tables are estimated in total, of which ≈100–160 are relevant for the DWH. For the PoV scope, the storage footprint is assumed to be ≈20% of total consumption (≈200 GB, corrected value 35 GB).

**Planned Azure consumption** (Azure calculator; North Europe selected as a cheaper region than Poland):

| Scope | Capacity | Estimated monthly cost | With 1-year reservation |
|---|---|---|---|
| Main scope | MS Fabric F16 | $2,260.60 | $1,361.40 |
| Main scope | MS Fabric F64 (with free read-only Power BI licenses, freeing ~100 Power BI licenses ≈ $1,400) | $8,876.80 | $5,280.00 |
| PoV scope | F4 | $555.60 | $330.81 |
| PoV scope | F8 | $1,117.88 | $668.28 |

# Annexes

## Annex 1. Data models

This annex documents the source-to-target data models underpinning the analytical solution. For the Proof of Value, the primary model is the `FctSpends` star schema (see *Proof of Value (PoV) use case scope → Structure of storage* for the full column mapping).

### ERP — FctSpends (PoV)

- **Fact table:** `FctSpends` — line-item expense/budget grain (document + line number), with measures PC, AC, PN and a `SpendsType` discriminator distinguishing planned vs actual source records.
- **Dimensions:** Budget Item (cost hierarchy: cost_level1/cost_level2/cost), Company Structure (cost_center / CFR), Employee (responsible), Organization (entity), and Period (sk_date_id, monthly grain via Calendar).

*[TO CONFIRM — the detailed SQL extraction logic and dimension business keys for the ERP source (analogous to the Yuria-Pharm data-model annexes) to be added once the ERP analyst provides the source object definitions.]*

### Other source systems

*[TO CONFIRM — data models for MS SQL (Sales, Visit Activity, Market Analytics), the Accounting System, and the Transport Management System to be documented in the scaling phase, following the same structure: source query, dimension logic, and business-key mapping.]*
