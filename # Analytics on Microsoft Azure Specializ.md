# Analytics on Microsoft Azure Specialization (V2.8.1)

## Audit Preparation Guide

---

# Purpose

This document provides a practical overview of the **Analytics on Microsoft Azure Specialization (V2.8.1)** audit requirements and serves as a preparation guide for audit readiness.

The goal is to understand:

* What auditors are validating
* What evidence must be prepared
* How to organize customer artifacts
* Typical auditor questions
* Common audit pitfalls

---

# Understanding the Audit

The audit is not primarily a technology assessment.

The auditor evaluates:

1. Whether a repeatable process exists
2. Whether the process is consistently applied
3. Whether evidence proves successful execution

The audit follows the principle:

```text
Process
  ↓
Template
  ↓
Customer Example
  ↓
Evidence
```

---

# Audit Structure

The specialization consists of two modules:

## Module A – Azure Essentials Cloud Foundation

1. Readiness and Foundation
2. Design and Govern
3. Manage and Optimize

## Module B – Analytics on Microsoft Azure

1. Assess
2. Design and Proof of Concept
3. Deployment
4. Review and Release for Operations

---

# MODULE A

---

# 1.1 Cloud & AI Adoption Business Strategy

## Objective

Demonstrate the ability to align Azure and Analytics initiatives with customer business goals.

## Required Evidence

For 2 unique customers within the last 12 months:

### Mandatory

* FinOps Review

### Plus one of:

* Cloud Adoption Strategy Evaluator (CASE)
* Advisor Assessment

## Auditor Expectations

### Current State

* Existing environment
* Pain points
* Technical limitations
* Operational challenges

### Future State

* Expected business outcomes
* Cost optimization
* Scalability
* Modernization benefits

### Financial Justification

* Current costs
* Future Azure costs
* Savings opportunities
* ROI discussion

---

# 1.2 Cloud & AI Adoption Plan

## Objective

Demonstrate project planning and tracking capability.

## Required Evidence

For 2 unique customers:

### Mandatory

* Cost Management Report
* Azure Pricing Calculator Output
* DevOps Capability Assessment

## Auditor Expectations

Project lifecycle visibility:

```text
Assessment
    ↓
Design
    ↓
PoC
    ↓
Deployment
    ↓
Hypercare
```

### Recommended Artifacts

* Azure DevOps Boards
* Jira Plans
* Project Roadmaps
* Delivery Plans

---

# 2.1 Security & Governance Tooling

## Objective

Demonstrate governance and security implementation.

## Required Evidence

For 2 unique customers:

* Microsoft Defender for Cloud
  OR
* Equivalent third-party solution

Plus:

* Cloud Adoption Security Review

## Typical Areas Reviewed

### Security

* MFA
* Conditional Access
* RBAC
* Privileged Identity Management

### Data Protection

* Sensitivity Labels
* Data Classification
* Encryption

### Governance

* Resource ownership
* Cost governance
* Workspace governance

---

# 2.2 Well-Architected Workloads

## Objective

Validate architecture quality before production deployment.

## Required Evidence

For 2 unique customers:

* Well-Architected Review results

## Recommended Pillars

### Security

Focus on:

* Identity
* Access Control
* Data Protection

### Reliability

Focus on:

* Recovery
* Resilience
* Availability

---

# 3.1 Repeatable Deployment

## Objective

Demonstrate deployment standardization.

## Required Evidence

For 2 unique customers:

* Azure Landing Zone implementation
* Automated deployment approach

### Accepted Technologies

* Bicep
* Terraform
* ARM Templates

## Preferred Evidence

```text
Azure DevOps Repository
        ↓
Bicep/Terraform
        ↓
Pipeline
        ↓
Landing Zone
```

### Analytics/Fabric Exception

If no Identity or Networking components exist, Resource Organization evidence is sufficient:

* Naming Convention
* Resource Groups
* Tags
* Subscription Structure

---

# 3.2 Skilling Plan

## Objective

Demonstrate customer enablement.

## Required Evidence

For 2 unique customers:

* Customer-facing skilling plans

## Example

### Power BI Developer

* PL-300
* Fabric Learning Path

### Data Engineer

* DP-700
* Fabric Lakehouse Training

### Administrator

* Governance
* Capacity Management
* Monitoring

---

# 3.3 Operations Management Tooling

## Objective

Demonstrate operational readiness.

## Required Evidence

At least one:

* Azure Monitor
* Azure Automation
* Azure Backup / Site Recovery

Plus one artifact:

* Security Scan Report
* Monitoring Dashboard Export
* YAML Pipeline
* SBOM
* Azure Policy Report

---

# MODULE B

---

# 1.1 Analytics Portfolio Assessment

## Objective

Demonstrate a structured discovery process.

## Required Evidence

For 3 unique customers completed within the last 24 months.

## Assessment Areas

### Business

* Business objectives
* Pain points
* Budget

### Data

* Sources
* Volume
* Format
* Classification

### Users

* Executives
* Analysts
* Engineers
* Data Scientists

### Security

* Access Requirements
* Compliance

### Availability

* SLA
* Disaster Recovery
* Scalability

### Skilling

* Required customer capabilities

---

# 2.1 Solution Design

## Objective

Demonstrate complete solution architecture.

## Required Evidence

For 3 unique customers.

---

## Typical Fabric Architecture

```text
Source Systems
    ↓
Fabric Data Factory
    ↓
Lakehouse
    ↓
Warehouse
    ↓
Semantic Model
    ↓
Power BI
```

---

## Design Areas

### Data Sources

Examples:

* SQL Server
* SAP
* REST APIs
* Dynamics 365

### Ingestion

Examples:

* Fabric Data Factory
* Azure Data Factory
* Databricks

### Storage

Examples:

* OneLake
* Lakehouse
* Warehouse
* ADLS Gen2

### Security

* RBAC
* RLS
* CLS
* OLS

### Analytics

* Microsoft Fabric
* Azure Synapse
* Azure Databricks

### Reporting

* Power BI
* Tableau

### DevOps

* Git
* Azure DevOps
* Deployment Pipelines

---

# Fabric-Specific Governance Areas

## Cost Optimization

* Capacity sizing
* Autoscale
* Budget Alerts

## Monitoring

* Capacity Metrics App
* Monitoring Hub
* Azure Monitor

## Backup and Recovery

* Git Integration
* Deployment Pipelines
* Workspace Recovery Strategy

## Governance

* Workspace Strategy
* Naming Standards
* Ownership Model

---

# 2.2 Well-Architected Review

## Objective

Validate workload architecture.

## Required Evidence

For 3 customers:

Results for at least 2 pillars.

Recommended:

* Security
* Reliability

---

# 2.3 Proof of Concept / Pilot

## Objective

Validate design assumptions before production.

## Required Evidence

For 3 customers.

## Recommended Structure

### Problem

Example:

```text
ETL processing takes 6 hours
```

### Goal

```text
Reduce processing time below 1 hour
```

### Result

```text
Processing reduced to 52 minutes
```

### Acceptance

Customer sign-off

---

# 3.1 Deployment

## Objective

Demonstrate production implementation capability.

## Required Evidence

For 3 customers.

Minimum two documents:

* Signed SOW
* Architecture Diagram
* Project Plan
* HLD
* LLD
* As-Built Documentation

## Auditor Favorite

As-Built Documentation

This is often the strongest proof that the solution was deployed successfully.

---

# 4.1 Service Validation & Testing

## Objective

Validate deployed solution quality.

## Required Evidence

For 3 customers.

### Testing Types

#### Functional Testing

* Pipeline execution
* Data movement validation

#### Performance Testing

* Load testing
* Refresh performance

#### User Acceptance Testing

* Customer approval

---

# 4.2 Post-Deployment Documentation

## Objective

Ensure customer operational readiness.

## Required Evidence

For 3 customers.

### Typical Documents

* Operations Guide
* Runbooks
* Support Documentation
* Disaster Recovery Guide
* Escalation Matrix

---

# Recommended Customer Folder Structure

```text
Customer A
│
├── Assessment
├── Business Case
├── FinOps
├── Security Review
├── Well Architected Review
├── Solution Design
├── Architecture
├── PoC
├── Deployment
├── As-Built
├── Testing
├── SOP
└── Customer Sign-Off

Customer B
...

Customer C
...
```

---

# Top 10 Auditor Questions

1. Show the original source document.
2. Who created this document?
3. Where is it stored?
4. When was it created?
5. How is it used in the delivery process?
6. Show customer sign-off.
7. Show the DevOps repository.
8. Show the deployment process.
9. Show monitoring evidence.
10. Show production deployment evidence.

---

# Audit Readiness Checklist

## Module A

* [ ] 2 customer examples (last 12 months)
* [ ] FinOps Review
* [ ] Adoption Plan
* [ ] Security Review
* [ ] Well-Architected Review
* [ ] Landing Zone Evidence
* [ ] Skilling Plan
* [ ] Operations Tooling Evidence

## Module B

* [ ] 3 customer examples (last 24 months)
* [ ] Assessment
* [ ] Solution Design
* [ ] PoC / Pilot
* [ ] Deployment
* [ ] Testing
* [ ] SOP
* [ ] Customer Sign-Off

---

# Recommended Fabric Audit Package

For each of 3 customers prepare:

1. Assessment
2. FinOps Review
3. Security Review
4. Well-Architected Review
5. Solution Design
6. Architecture Diagram
7. PoC / Pilot
8. Deployment Plan
9. As-Built Documentation
10. Test Results
11. SOP / Runbooks
12. Customer Sign-Off

This package typically covers the vast majority of audit controls and significantly reduces audit risk.
