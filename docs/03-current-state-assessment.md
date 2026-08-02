# Current-State Assessment: Nordic Eats

| Document details | |
| --- | --- |
| Company | Nordic Eats (fictional case study) |
| Prepared by | Amin Azad |
| Date | 2 August 2026 |
| Status | Draft for stakeholder validation |

## 1. Why this assessment matters

Before deciding what Nordic Eats should build in Azure, we need a clear picture of what the business depends on today. This assessment looks at the current applications, servers, data, security controls and operating practices. It also highlights the weaknesses that could affect the migration.

The findings are based on the agreed case-study scenario and reasonable assumptions for a small digital-commerce company. In a real project, they would be confirmed through interviews, system exports, monitoring data and hands-on discovery. Items that still need evidence are listed at the end of the document.

## 2. Business and technology context

Nordic Eats is a Copenhagen-based startup with 25 employees and approximately 40,000 monthly users. Customers use its website and mobile application to browse food providers, place orders and manage their accounts. Staff use an internal administration portal to manage products, orders, refunds and customer-support cases.

Most of the core technology runs from the company's only office. One IT administrator looks after infrastructure, user access, backups and operational support, while a small development team maintains the applications. The environment was adequate when the business was smaller, but it has grown without a corresponding improvement in resilience or automation.

There is no evidence of an immediate system failure. The concern is that several normal incidents—a server fault, office outage, failed deployment or ransomware event—could interrupt the whole customer service and take longer to recover from than the business can accept.

## 3. Current environment at a glance

| Area | Current position | Main concern |
| --- | --- | --- |
| Hosting | Core workloads run on two physical servers in the office | The office remains a single point of failure |
| Customer application | Website and API are hosted together | A release or resource problem can affect the full service |
| Admin portal | Hosted in the same environment as customer services | Internal and public workloads are not strongly separated |
| Database | SQL Server supports customers, products and orders | Recovery and capacity depend on one local environment |
| Files | Shared folders and application uploads use local storage | Permissions, backup coverage and growth are difficult to manage |
| Deployment | Developers deploy application packages manually | Releases are inconsistent and rollback is slow |
| Monitoring | Basic server checks and application logs | Problems may be discovered by users before IT receives an alert |
| Backup | Nightly local backups with occasional external copies | Restore time and backup integrity are not regularly tested |
| Disaster recovery | No secondary site or automated failover | A serious office incident could cause a prolonged outage |
| Security | Firewall, endpoint protection and individual accounts | Privileged access, secrets and logging need stronger control |

## 4. Assumed infrastructure inventory

The inventory below is a working baseline for architecture and migration planning. Specifications and utilization must be verified before services are sized or priced.

| Asset | Current role | Assumed specification | Typical use | Criticality |
| --- | --- | --- | --- | --- |
| SRV-01 | Application and web server | Windows Server, 8 vCPU, 32 GB RAM | Customer website, API and administration portal | Critical |
| SRV-02 | Database and file server | Windows Server, 8 vCPU, 64 GB RAM, 2 TB usable storage | SQL Server, shared folders and application files | Critical |
| FW-01 | Internet gateway and firewall | Small-business firewall appliance | Office internet access, NAT and basic filtering | High |
| NAS-01 | Local backup target | 4 TB network storage | Nightly server and database backups | High |
| UPS-01 | Short-duration power protection | Single UPS | Supports servers during brief power interruptions | Medium |

Both servers are assumed to be between four and six years old and no longer covered by comprehensive vendor support. They share the same office power, internet connection and physical location. This means adding redundancy inside the office would not protect the business from a building outage, theft, fire or extended connectivity failure.

## 5. Applications and dependencies

### Customer website and API

The public website and backend API are the most important workloads. They handle customer sign-in, product browsing, order submission and order history. The mobile application calls the same API, so an API outage affects both customer channels.

The application depends on:

- SQL Server for customer, product and order data;
- local file storage for images, exports and uploaded content;
- a third-party payment provider;
- an email or messaging provider for confirmations; and
- DNS and the office internet connection.

The application is assumed to be largely stateless, but this must be checked for local sessions, temporary files and scheduled jobs before it can run across multiple instances.

### Administration portal

Employees use the administration portal for operational tasks such as product updates, order review, refunds and support. It uses the same database and application environment as the customer service. This creates a dependency between internal administration and public traffic: high load or a failed change in one area may affect the other.

### SQL Server database

The SQL Server database is the system of record for customers, products, orders and operational status. The current database is assumed to be approximately 150 GB, growing by 5–8 GB per month. There is no separate high-availability replica.

Nightly full backups alone would not meet the agreed 15-minute recovery-point objective. Transaction-log configuration, integrity checks, retention and actual restore duration must be assessed before choosing the migration approach.

### File storage

Nordic Eats uses shared folders for business documents and local application storage for product images, exports and uploads. The total volume is assumed to be 600–800 GB. Folder permissions have developed over time, and some access may be granted directly to individuals rather than through groups.

Before migration, the company needs to identify file owners, remove obsolete data and separate business documents from application content. Moving everything without cleanup would carry old permission and retention problems into the new environment.

## 6. Network and connectivity

The office has one business internet connection and a small firewall. Public requests are forwarded through the firewall to the application server. There is no dedicated secondary connection, cloud network or private link to another site.

The network is assumed to have limited separation between servers, employee devices and administrative access. Firewall rules exist, but there is no recent documented rule review. Remote administration may depend on a VPN or restricted remote desktop access; the exact method must be confirmed.

During migration, the office will need reliable connectivity to Azure while data is copied and systems temporarily operate across both environments. The expected transfer volume and available upload speed should be measured early because they will affect the migration schedule.

## 7. Identity and access

Employees have individual work accounts, but access is managed separately across local servers and software services. Joiner, mover and leaver tasks are largely manual. There is no regular review of privileged roles, and multi-factor authentication is not consistently enforced for every administrative path.

Application passwords and connection strings are assumed to be stored in server configuration files or deployment settings. No exposed credentials are known, but the current approach makes rotation and auditing difficult.

The migration should establish one clear identity source, role-based access and MFA for administrators. Existing accounts and permissions must be reviewed before they are reproduced in Azure.

## 8. Deployment and change process

Application changes are prepared by developers and manually copied to the production server during an agreed release window. Some checks happen before release, but the process is not fully automated or consistently recorded. Infrastructure changes are also performed manually and are not represented as version-controlled code.

This creates three practical problems:

1. Production may differ from development and test environments.
2. A deployment can depend on one person's knowledge and sequence of steps.
3. Rollback may require restoring files or repeating earlier manual actions under pressure.

Source code is assumed to be stored in GitHub, which gives Nordic Eats a sensible starting point for automated testing, approval and deployment. Infrastructure as code can also make the Azure environment repeatable and easier to review.

## 9. Monitoring and incident response

Current monitoring is limited to basic server status, operating-system logs and application log files. There is no single dashboard covering user experience, API errors, database health, security events, backups and cost. Alerting is mainly reactive, and customers or employees may report a problem before the IT administrator sees it.

There is no formal on-call team. Serious incidents are handled by the IT administrator with help from developers when needed. Troubleshooting knowledge is held mostly by individuals, and there are no complete runbooks for the most likely failures.

The small team does not need a complex enterprise monitoring platform, but it does need central logs, useful alerts, named incident owners and short runbooks. Alerts should lead to an action rather than simply creating more noise.

## 10. Backup and disaster recovery

Servers and databases are assumed to be backed up nightly to the local NAS, with irregular copies placed on an external device or separate location. Backup jobs may report success, but full restoration is not tested on a fixed schedule.

The present process has several gaps:

- the backup target is normally in the same office as the production servers;
- a nightly schedule cannot meet the 15-minute RPO for transactional data;
- recovery time has not been measured against the four-hour RTO;
- there is no ready secondary application environment; and
- disaster roles, communication and return-to-service steps are not documented.

Backup and disaster recovery should be treated separately. Backups protect data, while disaster recovery restores the service. Nordic Eats needs both, followed by scheduled recovery exercises.

## 11. Security and compliance observations

Nordic Eats processes personal data such as customer names, contact details, addresses and order histories. Payment-card information is assumed to remain with the external payment provider; this must be confirmed because storing card data would significantly change the security and compliance scope.

Existing controls include a perimeter firewall, endpoint protection, operating-system accounts and some application logging. These provide a base, but the following gaps need attention:

- inconsistent MFA for privileged access;
- limited separation between public, administrative and data workloads;
- secrets stored in application or server configuration;
- no central security and administrative audit trail;
- informal access reviews and leaver processes;
- uncertain patching and vulnerability-management evidence; and
- no documented data classification or retention schedule.

There is no indication of a known breach. These are control weaknesses to resolve, not evidence that the environment has already been compromised.

## 12. Operational effort and cost

The single IT administrator is responsible for servers, backups, access, troubleshooting and vendor coordination. Routine maintenance competes with improvement work, and specialist knowledge is not always available when an incident occurs.

Current on-premises costs are not limited to hardware purchases. Electricity, support, licenses, backup devices, replacement parts and staff time also matter, although several are not tracked separately. A fair comparison with Azure must include these costs as well as the future replacement of aging servers.

Azure will not remove operational work. It should reduce physical maintenance and make automation easier, but the team will still need to manage identity, security, application health, backup, cost and recovery testing.

## 13. Key findings and migration implications

| Finding | Business impact | Migration implication |
| --- | --- | --- |
| The office is the only production location | A local outage can stop all digital services | Remove customer-facing production dependency on the office |
| Website, API and admin portal share one environment | One fault or release can affect several services | Separate responsibilities and allow independent scaling or release where useful |
| SQL Server has no high-availability copy | Database failure can stop ordering | Select a managed or resilient database design and test migration carefully |
| Backup and recovery are not proven | Data loss and outage duration are uncertain | Measure restore performance and run recovery tests before acceptance |
| Deployments are manual | Releases are slow and error-prone | Introduce CI/CD, approvals and rollback procedures |
| Monitoring is fragmented | Detection and diagnosis take too long | Centralize application, platform and security telemetry |
| Access and secrets are managed manually | Excess access or leaked credentials may go unnoticed | Use central identity, MFA, roles and managed secret storage |
| The team is small | A complex design would be difficult to operate | Prefer managed services, automation and short practical runbooks |
| Workload measurements are incomplete | Cost and sizing estimates may be inaccurate | Collect baseline metrics before final architecture approval |

## 14. Initial migration readiness

Nordic Eats is a reasonable candidate for a phased Azure migration. The application appears small enough to move without a full rewrite, GitHub can support automated delivery, and the business has clear reasons to improve availability and recovery.

Readiness is currently **medium**, not high. The main blockers are incomplete utilization data, unverified application dependencies, uncertain restore performance and undocumented access and file ownership. These issues are manageable, but they should be resolved through discovery and testing rather than left until cutover.

The likely migration sequence is:

1. Establish identity, governance, networking, monitoring and deployment foundations.
2. Prepare non-production application and data services in Azure.
3. Test the customer application, database migration, files and external integrations.
4. Migrate the production workload during an approved window with a rollback path.
5. Validate service, security, backup and recovery before retiring the old environment.
6. Pilot the AI support capability after the core platform is stable.

This is an initial direction only. Specific Azure services belong in the target architecture and technical design, not in this current-state assessment.

## 15. Information to validate during discovery

| Area | Evidence needed | Owner |
| --- | --- | --- |
| Traffic | Peak requests, concurrent users, seasonal events and response times | Product Owner / Development Lead |
| Servers | CPU, memory, disk, network utilization, age, warranty and patch status | IT Administrator |
| Application | Components, runtime versions, local state, background jobs and integrations | Development Lead |
| Database | Size, growth, edition, compatibility, transaction rate, backup chain and restore time | Development Lead / IT Administrator |
| Files | Volume, growth, ownership, permissions, file types and retention | Department Owners |
| Network | Internet bandwidth, public rules, remote administration and current diagrams | IT Administrator |
| Identity | Account sources, privileged users, MFA coverage and leaver history | IT Administrator / Management |
| Security | Vulnerability results, endpoint coverage, audit logs and recent incidents | IT Administrator |
| Recovery | Last successful restore, actual recovery duration and acceptable maintenance windows | IT Administrator / Sponsor |
| Third parties | Payment, email, messaging, DNS and contractual dependencies | Product Owner |
| Cost | Hardware, licenses, support, electricity and staff effort | Management / Finance |
| AI support | Support volume, common questions, approved content and escalation process | Support Lead |

## 16. Recommended next step

Nordic Eats should run a short discovery exercise to confirm the inventory and collect at least two to four weeks of workload data. The results should then feed into the target Azure architecture, migration method and detailed cost estimate.

The next project document will be the target architecture, where the validated requirements and current-state findings are translated into an Azure design.

## 17. Review and approval

| Role | Name | Decision | Date |
| --- | --- | --- | --- |
| Executive Sponsor | To be assigned | Pending | — |
| Product Owner | To be assigned | Pending | — |
| IT Administrator | To be assigned | Pending | — |
| Development Lead | To be assigned | Pending | — |
| Project Lead | Amin Azad | Pending | — |
