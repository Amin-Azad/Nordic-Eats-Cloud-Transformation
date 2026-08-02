# Business Requirements: Nordic Eats Cloud Transformation

| Document field | Value |
| --- | --- |
| Project | Nordic Eats Cloud Transformation |
| Client | Nordic Eats (fictional company) |
| Document | Business Requirements |
| Status | Draft for stakeholder validation |
| Version | 1.0 |
| Date | 2 August 2026 |

## 1. Purpose

This document defines what the Nordic Eats cloud transformation must deliver from a business perspective. It translates the approved business case into measurable requirements without prescribing the final Azure architecture.

## 2. Business Context

Nordic Eats is a Copenhagen startup with 25 employees and approximately 40,000 monthly users. Its customer website, mobile application, administration portal, SQL Server database, and shared file storage currently depend on one on-premises environment. Deployments are manual, monitoring is limited, and there is no tested disaster-recovery solution. One IT administrator supports the environment.

The target solution must enable reliable growth, faster delivery, stronger security, effective recovery, operational visibility, and controlled AI-assisted support while maintaining an Azure operating target of approximately 5,000 DKK per month.

## 3. Requirement Conventions

### 3.1 Priority

| Priority | Meaning |
| --- | --- |
| Must | Required for production approval or business-case success |
| Should | Important; may be phased with an approved workaround |
| Could | Desirable enhancement delivered when budget and schedule allow |

### 3.2 Status

All requirements are initially **Proposed** and must be validated with the relevant stakeholder. Later project phases may mark them Approved, Deferred, Rejected, or Implemented.

## 4. Stakeholders

| Stakeholder | Interest and responsibility |
| --- | --- |
| Executive Sponsor | Approves funding, scope, risk, and business outcomes |
| Product Owner | Defines customer and application priorities; accepts functionality |
| IT Administrator | Operates the platform and validates supportability |
| Development Team | Builds, tests, releases, and supports applications |
| Customer Support Team | Owns support content, escalation, and AI response quality |
| Finance/Management | Reviews budget, forecasts, and benefits |
| Customers | Require secure, reliable, and responsive digital services |

## 5. Business Requirements

### 5.1 Availability and Reliability

| ID | Requirement | Priority | Acceptance measure |
| --- | --- | --- | --- |
| BR-AVL-001 | Customer-facing production services shall achieve at least 99.9% monthly availability, excluding approved maintenance. | Must | Availability report demonstrates compliance during the agreed measurement period. |
| BR-AVL-002 | Failure of a single application instance shall not cause a complete customer-service outage. | Must | Resilience test confirms service remains available during an instance failure. |
| BR-AVL-003 | The platform shall support planned maintenance with minimal customer disruption. | Must | Approved maintenance test meets the communicated downtime target. |
| BR-AVL-004 | Internal administration services shall be available during agreed business operating hours. | Should | Monitoring report shows availability against the agreed schedule. |

### 5.2 Performance and Scalability

| ID | Requirement | Priority | Acceptance measure |
| --- | --- | --- | --- |
| BR-PER-001 | The platform shall support the current baseline of approximately 40,000 monthly users. | Must | Load test meets the agreed response-time and error-rate thresholds at baseline traffic. |
| BR-PER-002 | Capacity shall be adjustable without purchasing and installing new physical servers. | Must | Demonstration shows capacity can be changed through configuration or automation. |
| BR-PER-003 | The solution shall support at least twice the current peak demand without architectural replacement. | Should | Load or scaling test supports 2x recorded peak demand within approved thresholds. |
| BR-PER-004 | Customer-facing transactions shall meet documented response-time targets for critical journeys. | Must | Performance test results meet targets agreed during application assessment. |

### 5.3 Security, Privacy, and Access

| ID | Requirement | Priority | Acceptance measure |
| --- | --- | --- | --- |
| BR-SEC-001 | Customer and business data shall be protected in transit and at rest. | Must | Security review confirms approved encryption controls are enabled. |
| BR-SEC-002 | Access shall follow least privilege and be assigned through managed roles rather than shared administrator accounts. | Must | Access review finds no unapproved shared or excessive privileged access. |
| BR-SEC-003 | Privileged users shall use multi-factor authentication. | Must | Identity report confirms MFA enforcement for all privileged accounts. |
| BR-SEC-004 | Secrets and credentials shall not be stored in application source code or deployment files. | Must | Repository and configuration scan finds no unmanaged production secrets. |
| BR-SEC-005 | Security-relevant activity shall be centrally logged and retained for an agreed period. | Must | Required event sources are searchable and retention settings are documented. |
| BR-SEC-006 | The solution shall support Nordic Eats' applicable GDPR responsibilities, including controlled access and data lifecycle procedures. | Must | Privacy review and data-handling documentation receive stakeholder approval. |
| BR-SEC-007 | Public exposure shall be limited to services that have an approved business need. | Must | Architecture and exposure review find no unapproved public endpoints. |
| BR-SEC-008 | Privileged access shall be reviewed at least quarterly. | Should | Completed quarterly review record is available. |

### 5.4 Backup and Disaster Recovery

| ID | Requirement | Priority | Acceptance measure |
| --- | --- | --- | --- |
| BR-DR-001 | Critical transactional data shall have an RPO of 15 minutes or better. | Must | Recovery test demonstrates data loss does not exceed 15 minutes. |
| BR-DR-002 | Critical customer services shall have an RTO of 4 hours or better after a declared disaster. | Must | Timed recovery exercise restores the service within 4 hours. |
| BR-DR-003 | Backups shall be automated, monitored, protected from accidental deletion, and retained according to an approved policy. | Must | Backup reports and configuration review show successful jobs and approved protection settings. |
| BR-DR-004 | Restore procedures shall be tested at least quarterly for critical data. | Must | A quarterly restore record shows result, duration, issues, and owner. |
| BR-DR-005 | A documented disaster-recovery plan shall define declaration, communication, recovery, validation, and return-to-normal activities. | Must | Stakeholders approve the plan and a tabletop or technical exercise is completed. |

### 5.5 Deployment and Change Delivery

| ID | Requirement | Priority | Acceptance measure |
| --- | --- | --- | --- |
| BR-DEV-001 | Standard application deployments shall use an automated, repeatable CI/CD process. | Must | A release is completed through the approved pipeline without manual server changes. |
| BR-DEV-002 | Cloud infrastructure shall be defined and deployed through version-controlled infrastructure as code. | Must | The approved environment can be deployed or updated from reviewed Bicep code. |
| BR-DEV-003 | Production changes shall require review, testing, and approval appropriate to their risk. | Must | Pipeline evidence shows the required controls before production deployment. |
| BR-DEV-004 | A standard application release shall complete in 15 minutes or less, excluding approval waiting time. | Should | Pipeline history demonstrates the target for an agreed standard release. |
| BR-DEV-005 | Failed releases shall have a documented and tested rollback or forward-fix procedure. | Must | Release exercise demonstrates recovery using the documented procedure. |
| BR-DEV-006 | Production and non-production configuration shall be separated. | Must | Configuration review confirms environment-specific values and access boundaries. |

### 5.6 Monitoring and Operations

| ID | Requirement | Priority | Acceptance measure |
| --- | --- | --- | --- |
| BR-OPS-001 | The IT administrator shall have a centralized view of service health, performance, failures, security signals, and cost. | Must | Operational dashboard displays the agreed indicators. |
| BR-OPS-002 | Critical incidents shall generate an actionable alert within 5 minutes of detecting the agreed condition. | Must | Alert test delivers the notification with service, severity, and response information. |
| BR-OPS-003 | Alerts shall identify an owner, severity, and response procedure. | Must | Alert catalogue contains the required fields and links to runbooks. |
| BR-OPS-004 | Operational logs shall support investigation of customer-impacting incidents. | Must | An incident simulation can be traced across the agreed application components. |
| BR-OPS-005 | Repetitive operational tasks shall be automated where this reduces risk and administrative workload. | Should | At least three approved repetitive tasks are automated and documented. |
| BR-OPS-006 | Runbooks shall cover the most likely critical service incidents. | Must | IT administrator validates and uses the runbooks in an exercise. |

### 5.7 Cost Management

| ID | Requirement | Priority | Acceptance measure |
| --- | --- | --- | --- |
| BR-CST-001 | Forecast steady-state Azure operating cost shall remain at approximately 5,000 DKK per month for the agreed baseline workload. | Must | Approved cost estimate shows the baseline design at or near the target, with assumptions documented. |
| BR-CST-002 | Management shall receive alerts before forecast or actual spending exceeds the approved monthly target. | Must | Budget-alert test confirms notifications at approved thresholds. |
| BR-CST-003 | Every deployed resource shall contain the required ownership, environment, project, and cost-allocation metadata. | Must | Compliance report shows required tags on all in-scope resources or approved exemptions. |
| BR-CST-004 | Actual and forecast cloud spending shall be reviewed monthly. | Must | Monthly review record documents variance, forecast, actions, and owner. |
| BR-CST-005 | Non-production services shall avoid unnecessary out-of-hours consumption where technically practical. | Should | Schedule or scaling evidence demonstrates reduced unused consumption. |
| BR-CST-006 | Optional capabilities shall not be enabled in production without identified ownership and budget impact. | Must | Change record includes owner and approved cost estimate. |

### 5.8 Data and File Services

| ID | Requirement | Priority | Acceptance measure |
| --- | --- | --- | --- |
| BR-DAT-001 | Existing application and operational data shall be migrated without unacceptable loss, duplication, or corruption. | Must | Reconciliation confirms agreed record counts, totals, and integrity checks. |
| BR-DAT-002 | Database access shall be restricted to authorised users, applications, and administrative paths. | Must | Access and network review confirms only approved access paths. |
| BR-DAT-003 | Shared and application files shall retain agreed permissions, ownership, and folder structure after migration. | Must | Business-owner sampling and permission comparison pass agreed criteria. |
| BR-DAT-004 | Data retention and deletion rules shall be documented and enforceable. | Must | Stakeholders approve the retention schedule and implementation evidence. |
| BR-DAT-005 | The migration shall include a validated rollback or recovery point before final cutover. | Must | Cutover checklist confirms recoverable source and target states. |

### 5.9 AI-Powered Customer Support

| ID | Requirement | Priority | Acceptance measure |
| --- | --- | --- | --- |
| BR-AI-001 | Customers shall be able to obtain answers to approved, repetitive support questions through an AI assistant. | Should | User acceptance testing confirms the approved question set can be answered. |
| BR-AI-002 | The assistant shall use only approved knowledge sources and shall not invent transactional or policy information. | Must | Evaluation against the approved test set meets the defined groundedness threshold. |
| BR-AI-003 | The assistant shall clearly identify itself as automated and provide escalation to a human support channel. | Must | Conversation testing confirms disclosure and escalation are always available. |
| BR-AI-004 | Personal or sensitive data shall not be sent to the AI service unless explicitly required, approved, and protected. | Must | Privacy and data-flow review confirms compliance with the approved design. |
| BR-AI-005 | AI interactions shall be logged sufficiently for quality, safety, and cost review while respecting privacy requirements. | Must | Authorized reviewers can inspect the agreed audit and usage measures. |
| BR-AI-006 | AI usage shall have measurable limits, monitoring, and budget controls. | Must | Usage dashboard and configured thresholds demonstrate cost control. |
| BR-AI-007 | The initial assistant should handle at least 30% of eligible repetitive enquiries after the controlled rollout. | Could | Support reporting demonstrates the target without an unacceptable escalation or complaint rate. |

### 5.10 Migration and Business Continuity

| ID | Requirement | Priority | Acceptance measure |
| --- | --- | --- | --- |
| BR-MIG-001 | Migration shall be phased to reduce customer and operational risk. | Must | Approved migration plan defines stages, dependencies, gates, and rollback. |
| BR-MIG-002 | Customer-impacting cutovers shall occur within an approved maintenance window and communication plan. | Must | Cutover record confirms approvals and stakeholder communications. |
| BR-MIG-003 | Business and technical owners shall validate each migrated workload before source decommissioning. | Must | Signed acceptance exists for each workload. |
| BR-MIG-004 | Existing systems shall not be decommissioned until rollback criteria expire and backup validation is complete. | Must | Decommission checklist confirms all gates were met. |
| BR-MIG-005 | The IT administrator shall receive documentation and knowledge transfer before operational handover. | Must | Handover checklist and administrator sign-off are complete. |

## 6. Reporting Requirements

| ID | Required report or dashboard | Frequency | Audience |
| --- | --- | --- | --- |
| RR-001 | Service availability and performance | Monthly and on demand | Product Owner, IT Administrator |
| RR-002 | Cloud cost, forecast, and budget variance | Monthly | Management, IT Administrator |
| RR-003 | Backup and restore status | Weekly summary; quarterly test | IT Administrator, Project Sponsor |
| RR-004 | Security posture and privileged access review | Monthly; quarterly access certification | IT Administrator, Management |
| RR-005 | Deployment frequency, duration, and failures | Monthly | Product and Development Teams |
| RR-006 | AI usage, cost, escalation, and quality | Monthly during rollout | Support Lead, Product Owner, IT Administrator |

## 7. Assumptions and Dependencies

- Application owners, source code, database access, and current-system information will be available.
- Baseline traffic, peak demand, storage use, database size, and support volumes will be measured during assessment.
- Final performance thresholds will be agreed after current-state measurement.
- The target budget depends on right-sizing and may require phased or scheduled non-production services.
- Business owners will approve data classification, retention, recovery priority, and acceptable maintenance windows.
- External providers, including payment and notification services, will support the required target integrations.
- AI scope will begin with approved informational support content rather than unrestricted access to customer transactions.

## 8. Exclusions

The requirements do not include a complete application rewrite, mobile UI redesign, employee-device replacement, office-network refresh, 24/7 staffed operations centre, custom foundation-model training, third-party SaaS migration, or payment-provider replacement.

## 9. Requirement Traceability

Each approved business requirement will be traced through later project documents:

| Project artifact | Traceability purpose |
| --- | --- |
| Current-state assessment | Establishes baseline, gaps, dependencies, and feasibility |
| Target architecture | Identifies solution components that satisfy requirements |
| Security strategy | Maps security, privacy, identity, and logging controls |
| Migration strategy | Maps workloads, phases, validation, rollback, and cutover |
| Cost estimation | Validates the monthly target and documents cost assumptions |
| Test and acceptance plan | Provides evidence that each acceptance measure is met |
| Operational runbooks | Defines ongoing ownership and response procedures |

## 10. Open Items for Stakeholder Validation

The following values must be confirmed during discovery before architecture approval:

1. Peak concurrent users and seasonal demand pattern
2. Critical customer journeys and response-time targets
3. Database size, growth rate, dependencies, and downtime tolerance
4. File volumes, permissions, retention, and access patterns
5. Final data classifications and regulatory obligations
6. Notification recipients and incident escalation paths
7. Approved maintenance windows
8. AI knowledge sources, supported languages, quality threshold, and human escalation process
9. Budget alert thresholds and ownership
10. Final workload recovery tiers beyond the critical RPO and RTO

## 11. Approval

| Role | Name | Decision | Date |
| --- | --- | --- | --- |
| Executive Sponsor | To be assigned | Pending | — |
| Product Owner | To be assigned | Pending | — |
| IT Administrator | To be assigned | Pending | — |
| Project Lead | Amin Azad | Pending | — |

