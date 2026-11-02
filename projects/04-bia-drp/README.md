# Project 4: Business Impact Analysis and Disaster Recovery Plan

- **Company:** FalconPay (fictional fintech, see [company profile](../../company-profile.md))
- **Frameworks referenced:** NIST SP 800-34 (contingency planning), ISO 22301 concepts, NCA ECC subdomain 3-1
- **Deliverables:** business impact analysis (BIA), recovery objectives, disaster recovery plan (DRP), testing plan

---

## Part A: Business Impact Analysis

### A1. Objective

Find out how long each business function can be down before the damage becomes unacceptable, and set recovery targets that the disaster recovery plan must meet.

### A2. Method

1. Listed FalconPay's business functions with their owners (simulated interviews).
2. Estimated the impact of downtime over time: financial, customer, regulatory, and reputational.
3. Set four recovery metrics for each function:
    - **MTD (Maximum Tolerable Downtime):** the longest outage before the damage cannot be recovered.
    - **RTO (Recovery Time Objective):** the time allowed to restore the supporting systems.
    - **WRT (Work Recovery Time):** the time to verify data, reconnect systems, and resume normal work after systems are back.
    - **RPO (Recovery Point Objective):** the maximum amount of data that can be lost, measured in time.
4. Checked that **RTO + WRT ≤ MTD** for every function.

### A3. Impact of downtime over time

Average daily transaction revenue is SAR 450,000, which is about **SAR 18,750 per hour** of payment downtime, before counting penalties, merchant compensation, and lost customers.

| Function | 1 hour | 4 hours | 24 hours | 3 days |
|---|---|---|---|---|
| F1 Payment authorization | High | Critical | Critical | Critical |
| F2 Merchant settlement | Low | Medium | High | Critical |
| F3 Customer wallet and login | Medium | High | Critical | Critical |
| F4 Fraud monitoring | Medium | High | Critical | Critical |
| F5 Customer support | Low | Medium | High | High |
| F6 Internal finance and HR | Low | Low | Medium | High |

### A4. Recovery objectives

| ID | Function | Supporting assets | MTD | RTO | WRT | RTO + WRT | RPO | Tier |
|---|---|---|---|---|---|---|---|---|
| F1 | Payment authorization | A01, A03, A04, A05 | 4 hours | 2 hours | 1 hour | 3 hours ✓ | 15 minutes | 1 |
| F3 | Customer wallet and login | A02, A03, A05 | 8 hours | 4 hours | 2 hours | 6 hours ✓ | 15 minutes | 1 |
| F4 | Fraud monitoring | A01, A09 | 8 hours | 4 hours | 2 hours | 6 hours ✓ | 1 hour | 1 |
| F2 | Merchant settlement | A01, A02, A08 | 24 hours | 12 hours | 4 hours | 16 hours ✓ | 15 minutes | 2 |
| F5 | Customer support | A05, A06, support system (SaaS) | 48 hours | 24 hours | 8 hours | 32 hours ✓ | 24 hours | 2 |
| F6 | Internal finance and HR | A05, A06, finance system (SaaS) | 7 days | 3 days | 1 day | 4 days ✓ | 7 days | 3 |

**Notes**

- F2 has a long MTD but a short RPO: settlement can wait a few hours, but no transaction record can be lost, because merchants must be paid exactly.
- The **cloud hosting environment (A04)** and **identity (A05)** support almost every function. They are single points of failure and must be recovered first.

### A5. Dependencies and single points of failure

| Dependency | Functions affected | Mitigation |
|---|---|---|
| Single cloud region | F1 to F5 | Warm standby in a second availability zone (risk R12) |
| SSO / identity service | All | Break-glass admin accounts stored offline; identity replicated to standby |
| DNS provider | F1, F3 | Secondary DNS provider; low TTL records for fast failover |
| Payment network connection | F1, F2 | Two separate connections to the payment network |
| 3-person security team | Incident response | Retainer with an external incident response provider |

---

## Part B: Disaster Recovery Plan

### B1. Scope and scenarios

This plan covers the recovery of FalconPay's production technology after:

1. **Ransomware** encrypting production systems (risk R01).
2. **Outage of the primary cloud region or availability zone** (risk R12).
3. **Loss or corruption of the customer database** (risks R02, R08).
4. **Loss of the office** (fire or utility failure). Staff work remotely; production is not affected.

### B2. Recovery strategy

| Tier | Strategy | Site type | Meets |
|---|---|---|---|
| Tier 1 (F1, F3, F4) | Continuous database replication to a second availability zone, with application servers pre-configured and scaled down | **Warm site** | RTO 2 to 4 hours, RPO 15 minutes |
| Tier 2 (F2, F5) | Daily backups restored to the standby environment | Warm site | RTO 12 to 24 hours |
| Tier 3 (F6) | SaaS provider recovery and weekly backups | Provider | RTO 3 days |

A **hot site** (fully active in two zones) was considered for F1. It would cut RTO to minutes but roughly double hosting costs. Since the 4-hour MTD can be met with a warm site, the warm site was chosen. This should be reviewed as transaction volume grows.

**Ransomware scenario:** backups follow the 3-2-1 rule with one **immutable copy**, so attackers who gain admin access cannot delete or encrypt it. Systems are rebuilt from clean images (infrastructure as code), not restored from possibly infected servers.

### B3. Roles

| Role | Primary | Backup | Responsibility |
|---|---|---|---|
| DR Coordinator | Head of IT Operations | Senior Cloud Engineer | Declares the disaster, leads recovery |
| Technical Recovery Team | Cloud and database engineers | On-call engineer | Restores systems in the agreed order |
| Security Lead | Security Lead | External IR provider | Confirms the environment is clean before go-live |
| Communications Lead | Head of Customer Support | Marketing Manager | Updates customers, merchants, and staff |
| Executive Sponsor | CTO | CEO | Approves major decisions and regulatory notifications |

### B4. Activation

1. **Detect:** monitoring alert, cloud provider notice, or staff report.
2. **Assess (within 30 minutes):** the DR Coordinator confirms the scope and expected duration.
3. **Declare:** if the expected outage of any Tier 1 function exceeds **1 hour**, the DR Coordinator declares a disaster and activates this plan.
4. **Communicate:** the team meets on the out-of-band channel (an encrypted messaging group that does not depend on company systems).

### B5. Order of restoration

1. Cloud account access and break-glass accounts
2. Network and security controls (virtual networks, firewalls, security groups)
3. Identity service (SSO)
4. DNS, key management, and secrets
5. Databases (customer database, transaction database), with integrity checks
6. Payment platform and API gateway (F1)
7. Wallet app back end (F3) and fraud monitoring (F4)
8. Merchant portal and settlement (F2)
9. Support and internal systems (F5, F6)
10. Monitoring and logging fully restored before closing the incident

Restoring in the wrong order risks failures caused by missing dependencies, for example applications starting before the identity service or database are available.

### B6. Communication plan

| Audience | When | Channel | Owner |
|---|---|---|---|
| Recovery team | Immediately | Out-of-band encrypted group | DR Coordinator |
| Executives | Within 30 minutes | Phone call | DR Coordinator |
| Merchants | Within 1 hour, then every 2 hours | Status page and email | Communications Lead |
| Customers | Within 1 hour | In-app message and social media | Communications Lead |
| Regulators | As required by applicable regulations | Official channels | Executive Sponsor |

### B7. Return to normal

1. Confirm data integrity: transaction totals match between systems.
2. Security Lead confirms no attacker access remains (for cyber incidents).
3. Fail back to the primary site in a planned maintenance window.
4. Hold a **lessons learned** meeting within 5 business days and update this plan.

### B8. Testing and maintenance

| Test | Frequency | Purpose |
|---|---|---|
| Tabletop exercise | Every 6 months | Walk through a scenario and check that everyone knows their role |
| Restore test (one Tier 1 system) | Monthly | Prove that backups work and measure the real RTO |
| Functional failover test | Yearly | Fail over Tier 1 to the standby zone in a planned window |
| Plan review | Yearly, or after major changes | Keep contacts, systems, and procedures current |

---

## What I learned

- The BIA must come before the DRP: recovery targets come from the business, not from technology.
- RPO and RTO measure different things: RPO is about **data** (how much we can lose), RTO is about **time** (how long we can be down).
- The cheapest site type that still meets the MTD is usually the right choice, and the decision should be revisited as the business grows.
- A plan that has never been tested should not be trusted.
