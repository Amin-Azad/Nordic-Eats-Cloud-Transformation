# Business Case

| **Document** | Business Case |
|--------------|---------------|
| **Project** | Nordic Shopping Cloud Transformation |
| **Company** | Nordic Shopping |
| **Author** | Amin Azad |
| **Version** | 1.0 |
| **Status** | Draft |
| **Date** | August 2026 |

---

# 1. Executive Summary

Nordic Shopping is a growing Danish e-commerce startup that has reached a stage where its current on-premises infrastructure is becoming increasingly difficult to scale and maintain. Over the last few years, the company has experienced consistent growth in customers, vendors, and online transactions, making the existing infrastructure a potential business risk.

The company has decided to modernize its platform by migrating its core applications and infrastructure to Microsoft Azure. Rather than simply moving servers into the cloud, the objective is to build a secure, scalable, highly available, and cost-efficient cloud platform that can support future business growth.

The target architecture will use Azure managed services wherever practical to reduce operational overhead while improving security, deployment automation, monitoring, and disaster recovery.

The project has an approved Azure operational budget with a maximum limit of **DKK 10,000 per month**. The proposed architecture is expected to operate at approximately **DKK 6,000–7,000 per month** during normal business operations, leaving sufficient headroom for seasonal traffic and future growth.

---

# 2. Company Overview

## About Nordic Shopping

Nordic Shopping is a Copenhagen-based e-commerce marketplace founded in 2022. The company connects customers with local and international vendors through a modern online shopping platform.

Customers can browse products, compare prices, place orders, complete payments, and track deliveries using either the company website or mobile application.

Vendors manage products, inventory, pricing, promotions, and customer orders through dedicated vendor applications, while internal employees use an administration portal for customer support, finance, reporting, and operational management.

Although the company has grown steadily, its infrastructure has remained largely unchanged since the business was launched.

### Company Profile

| Item | Details |
|------|---------|
| Company | Nordic Shopping |
| Industry | E-commerce Marketplace |
| Headquarters | Copenhagen, Denmark |
| Founded | 2022 |
| Employees | 35 |
| Registered Customers | ~40,000 |
| Active Vendors | ~150 |
| Countries | Denmark |

---

# 3. Business Applications

The current platform consists of several business-critical applications.

| Application | Primary Users | Purpose |
|-------------|---------------|---------|
| Nordic Shopping Web | Customers | Browse products and place orders |
| Nordic Shopping Mobile App | Customers | Shopping, payments and order tracking |
| Nordic Vendor Portal | Vendors | Product, inventory and order management |
| Nordic Vendor Mobile App | Vendors | Order notifications and inventory updates |
| Nordic Admin Portal | Employees | Customer support, finance and operations |
| Nordic API Platform | Internal Services | Shared business logic and APIs |

All applications currently depend on the same backend infrastructure and database environment.

---

# 4. Business Growth

Nordic Shopping expects significant growth over the next three years.

The company plans to expand into Sweden and Norway while increasing the number of customers, vendors, and daily transactions.

| Business Metric | Current | Target (3 Years) |
|-----------------|--------:|-----------------:|
| Employees | 35 | 80 |
| Registered Customers | 40,000 | 250,000 |
| Active Vendors | 150 | 800 |
| Daily Orders | 600 | 5,000 |
| Countries | Denmark | Denmark, Sweden & Norway |
| Application Releases | Monthly | Weekly / On Demand |

The current infrastructure is not designed to support this level of growth efficiently.

---

# 5. Current Situation

Nordic Shopping currently operates from a small on-premises server environment.

The environment consists of:

- Windows Server hosting the web applications
- Microsoft SQL Server
- Shared file storage
- Backup server
- Active Directory
- Firewall and Internet gateway

While this infrastructure has supported the company during its early years, it now introduces several operational and business risks.

### Current Challenges

### Scalability

Scaling the application requires purchasing and configuring additional physical hardware. This process is expensive, time-consuming, and limits the company's ability to respond quickly to increasing customer demand.

### Availability

All production workloads are hosted in a single location.

A major hardware failure, power outage, or network disruption could result in extended downtime for customers and vendors.

### Manual Deployments

Application deployments are largely manual, increasing the likelihood of configuration errors, inconsistent environments, and production outages.

### Limited Monitoring

Application health, infrastructure metrics, and performance data are not centrally monitored, making troubleshooting slower and more reactive.

### Disaster Recovery

Although backups exist, there is no fully tested disaster recovery process or secondary production environment.

### Security

The current environment relies heavily on manually managed credentials and traditional network controls. The company requires stronger identity management, secure secret storage, improved access control, and centralized governance.

### Operational Overhead

The internal IT team spends considerable time maintaining infrastructure rather than delivering new business features.

---

# 6. Business Objectives

The cloud transformation project has the following objectives:

- Improve platform availability.
- Support future business growth.
- Reduce infrastructure management effort.
- Improve deployment reliability.
- Strengthen security.
- Introduce centralized monitoring.
- Improve backup and disaster recovery.
- Control long-term operational costs.
- Build a cloud platform that can evolve without major redesign.

---

# 7. Proposed Cloud Solution

Nordic Shopping will migrate its production platform to Microsoft Azure using managed Platform as a Service (PaaS) offerings wherever practical.

The proposed Azure platform includes:

| Area | Azure Service |
|------|---------------|
| Application Hosting | Azure App Service |
| Database | Azure SQL Database |
| Storage | Azure Storage Account |
| Global Routing | Azure Front Door |
| Networking | Azure Virtual Network |
| Secure Connectivity | Private Endpoints & Private DNS |
| Secrets | Azure Key Vault |
| Identity | Microsoft Entra ID & Managed Identity |
| Monitoring | Azure Monitor & Application Insights |
| Centralized Logging | Log Analytics Workspace |
| Infrastructure as Code | Bicep |
| CI/CD | GitHub Actions |
| Governance | Azure Policy |
| Cost Management | Azure Budgets & Alerts |

The primary production environment will be hosted in **West Europe**, while a secondary application environment will be deployed in **Sweden Central** to support disaster recovery.

---

# 8. Business Continuity Requirements

Because the company depends entirely on online sales, service continuity is a key business requirement.

| Requirement | Target |
|------------|--------|
| Availability | 99.9% or higher |
| Recovery Time Objective (RTO) | ≤ 60 minutes |
| Recovery Point Objective (RPO) | ≤ 15 minutes |
| Planned Maintenance | Near-zero customer impact using deployment slots |
| Disaster Recovery Region | Sweden Central |

These targets provide a practical balance between resilience and operational cost for a company of this size.

---

# 9. Security Objectives

The new platform will adopt a security-first approach using Azure native capabilities.

Key objectives include:

- Microsoft Entra ID authentication
- Role-Based Access Control (RBAC)
- Managed Identities
- Azure Key Vault
- Private Endpoints
- Encryption at rest and in transit
- Azure Policy
- Centralized logging
- Backup protection
- Secure CI/CD pipeline

These controls reduce operational risk while protecting customer and business data.

---

# 10. AI Operations Assistant

To improve operational efficiency, the project will include an AI-powered Operations Assistant.

The assistant will use data from Azure Monitor, Application Insights, Log Analytics, and GitHub Actions to support the IT team by:

- Summarizing incidents
- Explaining deployment failures
- Analysing application exceptions
- Recommending troubleshooting steps
- Producing daily operational summaries
- Highlighting unusual infrastructure behaviour

The AI assistant is intended to improve productivity rather than replace existing monitoring or operational processes.

---

# 11. Budget Considerations

The company has approved a maximum Azure operational budget of:

> **DKK 10,000 per month**

The proposed architecture is expected to operate between **DKK 6,000 and 7,000 per month** under normal business conditions.

Maintaining operational costs below the approved limit will be achieved by:

- Using managed Azure services
- Right-sizing compute resources
- Controlled autoscaling
- Storage lifecycle policies
- Budget alerts
- Cost monitoring
- Regular architecture reviews

The remaining budget provides capacity for seasonal demand, customer growth, and future platform expansion without immediate redesign.

---

# 12. Project Scope

## In Scope

- Azure cloud migration
- Application hosting
- Azure SQL Database
- Azure Storage
- Azure Front Door
- Virtual Network
- Private Endpoints
- Azure Key Vault
- Monitoring and logging
- CI/CD using GitHub Actions
- Infrastructure as Code using Bicep
- Backup and disaster recovery
- Cost management
- Security implementation

## Out of Scope

- Complete application redesign
- Enterprise landing zone
- Active-active database architecture
- Migration of unrelated internal systems
- End-user device replacement

---

# 13. Success Criteria

The project will be considered successful when:

- The platform is fully operational in Azure.
- Infrastructure is deployed using Bicep.
- CI/CD pipelines automate deployments.
- Production releases use deployment slots.
- Customer-facing applications achieve at least 99.9% availability.
- Disaster recovery objectives (RTO and RPO) are met.
- Security controls are implemented according to design.
- Centralized monitoring and alerting are operational.
- Monthly Azure costs remain below **DKK 10,000**.
- The platform can scale to support projected business growth without major architectural changes.

---

# 14. Conclusion

Nordic Shopping has reached a stage where continued business growth requires a more modern and resilient technology platform.

Migrating to Microsoft Azure will improve availability, scalability, security, operational efficiency, and deployment reliability while remaining within the approved budget.

The proposed architecture balances current business needs with future growth, allowing the company to expand into new markets without requiring a complete infrastructure redesign.

This business case forms the foundation for the remaining project documents, which will define the business requirements, current environment assessment, target architecture, migration strategy, cost analysis, and security assessment.
