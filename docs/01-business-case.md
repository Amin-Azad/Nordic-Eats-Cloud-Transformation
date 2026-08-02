# Business Case: Nordic Eats Cloud Transformation

| Document field | Value |
| --- | --- |
| Project | Nordic Eats Cloud Transformation |
| Client | Nordic Eats (fictional company) |
| Location | Copenhagen, Denmark |
| Document | Business Case |
| Status | Draft for stakeholder approval |
| Version | 1.0 |
| Date | 2 August 2026 |

## 1. Executive Summary

Nordic Eats is a Copenhagen-based digital-commerce startup with 25 employees and approximately 40,000 monthly users. Its customer website, mobile application, internal administration portal, SQL Server database, and shared files currently depend on a small on-premises server environment managed by one IT administrator.

The current environment limits the company's ability to grow. Application deployments are manual, monitoring is limited, recovery depends on local infrastructure, and there is no tested disaster-recovery capability. A hardware failure, cyber incident, or office outage could interrupt customer services and cause data loss.

This project proposes a phased migration to Microsoft Azure using managed cloud services wherever practical. The transformation will improve reliability, security, scalability, deployment speed, monitoring, backup, and disaster recovery while keeping the target Azure operating cost at approximately **5,000 DKK per month**. It will also introduce a controlled AI-powered customer-support capability to reduce repetitive support work and improve response times.

## 2. Company Background

Nordic Eats provides food-ordering and related digital services through:

- A customer-facing website
- A mobile application
- An internal administration portal
- A SQL Server database containing application and operational data
- Shared file storage used by employees and business processes

The company operates from one Copenhagen office. Its technology environment is maintained by one IT administrator, with development and operational support shared across a small team.

## 3. Current Business Problem

The on-premises platform was sufficient during the company's early stage, but it now creates material business risks.

| Problem | Business impact |
| --- | --- |
| Single on-premises environment | Hardware or office failure can interrupt all digital services. |
| Limited capacity and scalability | Traffic growth or demand peaks may reduce performance and customer satisfaction. |
| Manual deployments | Releases are slow, inconsistent, and more likely to introduce errors. |
| Limited monitoring and alerting | Problems may be discovered by customers before the IT team. |
| Inadequate backup and no tested DR | A major failure could cause extended downtime or permanent data loss. |
| One IT administrator | Routine maintenance creates an operational bottleneck and key-person dependency. |
| Weak security visibility | Threats, misconfigurations, and suspicious activity are difficult to detect centrally. |
| Hardware-led cost model | Capacity must be purchased in advance, even when it is not continuously required. |

## 4. Case for Change

Maintaining the current environment would avoid an immediate migration effort, but it would leave the main risks unresolved and require further hardware investment as the company grows. Expanding the on-premises platform would also increase maintenance responsibilities for an already limited IT team.

A cloud transformation offers a better strategic fit because Nordic Eats needs flexible capacity, dependable customer services, faster releases, stronger recovery, and lower infrastructure-management effort. Azure also supports infrastructure as code, automated deployment, centralized security, monitoring, managed data services, and AI capabilities within one platform.

## 5. Options Considered

| Option | Advantages | Disadvantages | Decision |
| --- | --- | --- | --- |
| Continue on-premises | No immediate migration; minimal short-term change | Existing reliability, recovery, scalability, and staffing risks remain | Rejected |
| Expand on-premises | Retains current operating model | Requires capital investment and more maintenance; does not solve agility concerns | Rejected |
| Lift and shift all servers to Azure VMs | Faster initial migration; fewer application changes | Preserves server-management overhead and may exceed the cost target | Not preferred |
| Phased Azure migration using managed services | Reduces administration, supports scaling and automation, improves resilience | Requires planning, skills, and controlled migration | Recommended |

## 6. Proposed Transformation

The recommended approach is a phased migration from the on-premises environment to Azure. The programme will:

- Establish a governed Azure foundation with identity, access control, networking, tagging, policy, and budget controls.
- Move the customer application and administration portal to an appropriate managed application platform.
- Migrate SQL Server data to a managed Azure database service after compatibility and sizing assessment.
- Move shared and application files to secure Azure storage.
- Implement automated infrastructure deployment with Bicep.
- Implement application CI/CD through GitHub Actions.
- Introduce centralized logs, metrics, dashboards, alerts, and operational runbooks.
- Provide backup, restore, and tested disaster-recovery procedures.
- Add an AI-powered customer-support assistant with human escalation and controlled data access.
- Apply continuous cost monitoring and optimisation to remain close to the monthly target.

Detailed Azure services and architecture choices will be made in later design phases. This business case approves the direction and outcomes, not a final technical design.

## 7. Business Objectives

1. Improve the reliability and availability of customer-facing services.
2. Support growth beyond 40,000 monthly users without large upfront hardware purchases.
3. Reduce deployment lead time and release risk through automation.
4. Improve security, auditability, and protection of customer and business data.
5. Establish recoverable backups and a tested disaster-recovery capability.
6. Give the small IT team centralized operational visibility and actionable alerts.
7. Keep normal Azure operating expenditure at approximately 5,000 DKK per month.
8. Improve customer-support response time through a safe, limited AI capability.

## 8. Expected Benefits

### 8.1 Quantifiable Benefits

- At least 99.9% monthly availability for the customer-facing production service, excluding approved maintenance.
- Standard application releases completed through an automated pipeline in 15 minutes or less.
- Critical service alerts generated within 5 minutes of a detected threshold breach.
- Recovery point objective (RPO) of 15 minutes or better for critical transactional data.
- Recovery time objective (RTO) of 4 hours or better for the critical customer service.
- Monthly Azure cost maintained within 5,000 DKK under the agreed baseline workload, with alerts before overspend.
- At least 30% of eligible repetitive support enquiries handled by the AI assistant after controlled rollout.

### 8.2 Qualitative Benefits

- Reduced dependence on office hardware and a single administrator.
- Faster and more consistent software delivery.
- Better customer trust through improved uptime and recovery readiness.
- Stronger visibility into application health, security events, and spending.
- A repeatable platform that can support future products and geographic expansion.

## 9. Financial Considerations

The target steady-state Azure operating budget is **approximately 5,000 DKK per month**, equivalent to approximately **60,000 DKK per year**. This target covers the production cloud platform at the agreed baseline usage and is subject to validation during detailed architecture and cost-estimation work.

The following principles will control spending:

- Prefer appropriately sized managed and platform services over continuously running virtual machines.
- Scale services according to demand where technically and financially suitable.
- Apply budgets, tags, cost allocation, and alert thresholds.
- Use retention and storage lifecycle policies.
- Separate essential production controls from optional enhancements.
- Review forecast and actual cost monthly.
- Set explicit consumption limits for the AI capability.

One-time migration effort, staff time, training, domain registration, end-user devices, and third-party licence costs are not included in the 5,000 DKK monthly Azure target unless later cost analysis explicitly includes them.

## 10. Scope

### 10.1 In Scope

- Discovery and assessment of the current environment
- Azure cloud strategy and target architecture
- Azure governance, identity, network, and security foundation
- Migration of the website, mobile application backend, and administration portal
- SQL Server assessment and database migration
- Shared and application file migration
- Backup, restore, high availability, and disaster recovery
- Infrastructure as code using Bicep
- CI/CD using GitHub Actions
- Monitoring, logging, alerting, dashboards, and runbooks
- Cost estimation, budgeting, tagging, and optimisation
- AI-powered customer-support capability with human escalation
- Documentation, testing, knowledge transfer, and a portfolio demonstration

### 10.2 Out of Scope

- Replacing the entire customer-facing application with a new product
- Redesigning the mobile application's user interface
- Replacing employee laptops, office Wi-Fi, or unrelated end-user systems
- A 24/7 staffed security operations centre
- Large-scale data science or model training
- Migration of unspecified third-party SaaS platforms
- Production payment-provider replacement

Any out-of-scope item requires separate approval, cost analysis, and planning.

## 11. Key Assumptions and Constraints

### Assumptions

- Nordic Eats owns or can modify the applications and deployment process.
- Required application source code, database access, and system documentation will be available.
- The current application can be migrated or minimally modernised without a complete rewrite.
- Workload and data volumes are compatible with the target budget after right-sizing.
- Stakeholders will participate in discovery, testing, migration approval, and recovery exercises.
- Personal and business data will be processed in accordance with applicable GDPR obligations.

### Constraints

- Target Azure operating cost is approximately 5,000 DKK per month.
- The company has one IT administrator and limited operational capacity.
- Customer disruption during migration must be minimised.
- Security, backup, monitoring, and recovery controls cannot be deferred from the production release.
- Technical choices should avoid unnecessary operational complexity.

## 12. Risks and Mitigations

| Risk | Likelihood | Impact | Planned mitigation |
| --- | --- | --- | --- |
| Cost exceeds the monthly target | Medium | High | Validate pricing, right-size services, use budgets and alerts, and phase optional capabilities. |
| Application is incompatible with managed services | Medium | High | Perform dependency and compatibility assessment; use a staged migration path. |
| Migration causes customer downtime | Medium | High | Use rehearsals, rollback plans, staged cutover, and approved maintenance windows. |
| Data is lost or corrupted during migration | Low | Critical | Take validated backups, reconcile data, test restore, and retain rollback copies. |
| Team lacks required Azure skills | Medium | Medium | Use documented automation, training, runbooks, and knowledge transfer. |
| Security is misconfigured | Medium | High | Apply least privilege, policy, code review, security testing, and centralized logging. |
| AI produces inaccurate responses or exposes data | Medium | High | Restrict knowledge sources, avoid unnecessary personal data, log interactions, provide human escalation, and test before release. |
| Vendor dependency increases | Medium | Medium | Use documented interfaces, portable data formats, source-controlled infrastructure, and an exit plan. |

## 13. Success Criteria

The transformation will be considered successful when:

- The agreed workloads operate in Azure and pass functional and business acceptance testing.
- Production availability meets the 99.9% monthly target during the agreed measurement period.
- Backup restoration and disaster-recovery exercises meet the stated RPO and RTO.
- Infrastructure and normal application releases are deployed through reviewed automation.
- Monitoring, security logging, alerting, ownership, and response procedures are operational.
- The forecast steady-state Azure cost is at or near 5,000 DKK per month for baseline usage.
- Critical data is protected in transit and at rest, and access follows least privilege.
- The AI support capability passes accuracy, privacy, escalation, and cost-control acceptance tests.
- The IT administrator receives usable documentation, dashboards, and operational runbooks.

## 14. Recommendation

Approve the phased Azure cloud transformation and proceed to current-state assessment, requirements validation, architecture design, migration planning, and detailed cost estimation. Approval is conditional on maintaining the cost-control principles and validating technical feasibility before production migration.

## 15. Approval

| Role | Name | Decision | Date |
| --- | --- | --- | --- |
| Executive Sponsor | To be assigned | Pending | — |
| Product Owner | To be assigned | Pending | — |
| IT Administrator | To be assigned | Pending | — |
| Project Lead | Amin Azad | Pending | — |

