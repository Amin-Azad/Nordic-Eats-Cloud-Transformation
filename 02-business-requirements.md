# Business Requirements

| Item | Value |
|------|-------|
| Project | Nordic shopping Cloud Transformation |
| Company | Nordic Shopping |
| Document | Business Requirements |
| Author | Amin Azad |
| Version | 1.0 |
| Status | Draft |
| Related Document | 01-business-case.md |

---

# 1. Purpose

This document defines the business and technical requirements for migrating Nordic Shopping's on-premises environment to Microsoft Azure. These requirements are used as the baseline for the target architecture, migration strategy, cost analysis and security assessment.

---

# 2. Business Goals

The cloud platform shall:

- Support business growth for the next 3–5 years.
- Improve platform availability and resilience.
- Reduce manual infrastructure management.
- Improve security using Azure native services.
- Automate infrastructure and application deployments.
- Improve monitoring and operational visibility.
- Provide disaster recovery capability.
- Keep Azure operational costs below the approved budget.

---

# 3. Functional Requirements

| ID | Requirement |
|----|-------------|
| FR-001 | Customers shall browse products through the website and mobile application. |
| FR-002 | Customers shall place and track orders. |
| FR-003 | Vendors shall manage products, inventory and pricing. |
| FR-004 | Employees shall manage orders through the Admin Portal. |
| FR-005 | Applications shall communicate through REST APIs. |
| FR-006 | Files and product images shall be stored centrally. |
| FR-007 | Customer and business data shall be stored in Azure SQL Database. |

Business Applications:

- Nordic Shopping Web
- Nordic Shopping Mobile App
- Nordic Vendor Portal
- Nordic Vendor Mobile App
- Nordic Admin Portal
- Nordic API Platform

---

# 4. Non-Functional Requirements

| ID | Requirement |
|----|-------------|
| NFR-001 | The solution shall use managed Azure services where practical. |
| NFR-002 | Infrastructure shall be repeatable using Infrastructure as Code. |
| NFR-003 | The platform shall be monitored continuously. |
| NFR-004 | The design shall support future business growth. |
| NFR-005 | Operational effort shall be minimized through automation. |

---

# 5. Availability Requirements

| ID | Requirement | Target |
|----|-------------|--------|
| AV-001 | Platform Availability | ≥99.9% |
| AV-002 | Planned Maintenance | Near zero customer impact |
| AV-003 | Regional Failover | Supported |
| AV-004 | Health Monitoring | Continuous |

Production deployments shall use deployment slots to reduce downtime.

---

# 6. Performance Requirements

| ID | Requirement | Target |
|----|-------------|--------|
| PF-001 | Homepage Load Time | ≤3 seconds |
| PF-002 | Product Search | ≤2 seconds |
| PF-003 | Checkout API | ≤1 second (95%) |
| PF-004 | Average API Response | ≤500 ms |

Application performance shall be monitored using Azure Monitor and Application Insights.

---

# 7. Scalability Requirements

The solution shall support growth without redesign.

| Metric | Current | Target |
|--------|--------:|-------:|
| Employees | 35 | 80 |
| Customers | 40,000 | 250,000 |
| Vendors | 150 | 800 |
| Daily Orders | 600 | 5,000 |

The platform shall support:

- Horizontal scaling
- Database growth
- Storage growth
- Regional expansion
- Increased API traffic

---

# 8. Security Requirements

## 8.1 Identity and Access Management

| ID | Requirement |
|----|-------------|
| SEC-001 | Microsoft Entra ID shall be the central identity provider. |
| SEC-002 | MFA shall be enabled for all privileged accounts. |
| SEC-003 | RBAC shall follow least privilege. |
| SEC-004 | Managed Identities shall be used where supported. |
| SEC-005 | Shared administrator accounts shall not be used. |

## 8.2 Secret Management

| ID | Requirement |
|----|-------------|
| SEC-006 | Secrets shall be stored in Azure Key Vault. |
| SEC-007 | No passwords or connection strings shall be stored in source code. |
| SEC-008 | Applications shall retrieve secrets using Managed Identity. |

## 8.3 Network Security

| ID | Requirement |
|----|-------------|
| SEC-009 | Azure Virtual Network shall isolate application resources. |
| SEC-010 | Storage and Key Vault shall use Private Endpoints. |
| SEC-011 | Private DNS Zones shall resolve private resources. |
| SEC-012 | HTTPS only shall be enforced. |
| SEC-013 | TLS 1.2 or higher shall be required. |

## 8.4 Data Protection

| ID | Requirement |
|----|-------------|
| SEC-014 | Data shall be encrypted at rest. |
| SEC-015 | Data shall be encrypted in transit. |
| SEC-016 | Azure SQL shall support Point-in-Time Restore. |
| SEC-017 | Backup data shall be protected. |

## 8.5 Logging and Auditing

| ID | Requirement |
|----|-------------|
| SEC-018 | Application logs shall be collected. |
| SEC-019 | Azure Activity Logs shall be enabled. |
| SEC-020 | Logs shall be stored in Log Analytics Workspace. |
| SEC-021 | Microsoft Defender for Cloud shall monitor security posture. |

## 8.6 Governance

| ID | Requirement |
|----|-------------|
| SEC-022 | Mandatory resource tags shall be enforced. |
| SEC-023 | Azure Policy shall enforce organizational standards. |
| SEC-024 | Resource deployment shall be limited to approved regions. |

## 8.7 Secure Delivery

| ID | Requirement |
|----|-------------|
| SEC-025 | Infrastructure shall be deployed using Bicep. |
| SEC-026 | CI/CD shall use GitHub Actions. |
| SEC-027 | Production changes shall be traceable through source control. |

---

# 9. Compliance Requirements

The solution should support:

- GDPR
- Azure Security Benchmark
- Microsoft Cloud Adoption Framework recommendations

Customer data shall remain within approved Azure regions.

---

# 10. Disaster Recovery Requirements

| Requirement | Target |
|------------|--------|
| Primary Region | West Europe |
| DR Region | Sweden Central |
| Recovery Time Objective (RTO) | ≤60 minutes |
| Recovery Point Objective (RPO) | ≤15 minutes |

The platform shall support automated backups, documented recovery procedures and regular disaster recovery testing.

---

# 11. Networking Requirements

The solution shall include:

- Azure Front Door
- Azure Virtual Network
- Dedicated subnets
- Private Endpoints
- Private DNS
- Network Security Groups

Public access shall be minimized wherever possible.

---

# 12. Monitoring Requirements

The solution shall use:

- Azure Monitor
- Application Insights
- Log Analytics Workspace
- Azure Alerts

Alerts shall be configured for:

- High CPU
- HTTP 5xx
- Failed deployments
- Availability failures
- Database performance
- Security recommendations

---

# 13. Deployment Requirements

Deployments shall:

- Use Bicep for Infrastructure as Code.
- Use GitHub Actions for CI/CD.
- Use deployment slots before production.
- Be fully version controlled.
- Avoid manual production changes.

---

# 14. Cost Requirements

The approved Azure operational budget is **DKK 10,000 per month**.

Normal monthly operating costs should remain between **DKK 6,000 and DKK 7,000**, leaving capacity for business growth and seasonal demand.

The solution shall implement:

- Azure Budgets
- Budget Alerts
- Resource Tagging
- Cost Reviews
- Storage Lifecycle Policies
- Controlled Autoscaling

---

# 15. AI and Automation Requirements

The platform shall include an AI Operations Assistant capable of:

- Summarizing Azure Monitor alerts
- Explaining deployment failures
- Analysing Application Insights exceptions
- Suggesting remediation steps
- Producing daily operational summaries
- Identifying recurring operational issues

---

# 16. Assumptions

- Applications are compatible with Azure App Service.
- Azure SQL Database satisfies current business needs.
- Managed services are preferred over virtual machines.
- Short maintenance windows are acceptable during migration.

---

# 17. Acceptance Criteria

The project will be accepted when:

- All applications run successfully in Azure.
- Infrastructure is deployed using Bicep.
- CI/CD automates deployments.
- Security requirements are implemented.
- Monitoring is operational.
- Disaster recovery is tested.
- Monthly Azure cost remains below DKK 10,000.
- The platform supports projected business growth.

---

# 18. Requirement Traceability

| Document | Purpose |
|----------|---------|
| 03-current-environment.md | Existing environment assessment |
| 04-target-architecture.md | Azure solution implementing these requirements |
| 05-migration-strategy.md | Migration approach |
| 06-cost-analysis.md | Budget validation |
| 07-security-assessment.md | Verification of security implementation |
