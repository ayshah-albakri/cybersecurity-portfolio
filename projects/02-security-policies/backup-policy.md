# Backup and Recovery Policy

| | |
|---|---|
| **Policy ID** | FP-SEC-POL-03 |
| **Owner** | Head of IT Operations |
| **Approved by** | Chief Technology Officer |
| **Effective date** | Draft, pending approval |
| **Review cycle** | Every 12 months, or after a major change to systems |
| **Related** | NCA ECC subdomains 2-9 (Backup and Recovery Management) and 3-1 (Cybersecurity Resilience Aspects of BCM) |

> FalconPay is a fictional company. This document is a portfolio sample.

## 1. Purpose

To make sure FalconPay can restore its systems and data after ransomware, accidental deletion, hardware failure, or a disaster, within the recovery targets set in the business impact analysis.

## 2. Scope

All production systems, databases, cloud workloads, configuration files, and critical business documents.

## 3. Roles and responsibilities

| Role | Responsibility |
|---|---|
| Head of IT Operations | Owns the policy and the backup systems |
| System owners | Define what must be backed up and confirm recovery targets |
| Security Lead | Reviews backup security and encryption |
| Internal audit | Checks that restore tests are performed and documented |

## 4. Policy statements

### 4.1 Backup frequency and type

| Data tier | Examples | Backup method | RPO |
|---|---|---|---|
| Tier 1 | Payment platform, customer database | Continuous replication + daily full backup | 15 minutes |
| Tier 2 | Merchant portal, fraud monitoring, SIEM | Daily incremental + weekly full | 24 hours |
| Tier 3 | Internal finance and HR files | Weekly full | 7 days |

### 4.2 The 3-2-1 rule

1. Every Tier 1 and Tier 2 system must have at least **3 copies** of its data, on **2 different storage types**, with **1 copy offline or immutable** and stored in a separate location.
2. The offline or immutable copy must not be reachable using normal administrator accounts, so ransomware cannot encrypt or delete it.

### 4.3 Security of backups

3. Backups must be **encrypted** at rest and in transit.
4. Encryption keys must be stored separately from the backups, in the key management system.
5. Access to backup systems must be limited to named backup administrators and protected with phishing-resistant MFA.

### 4.4 Retention

6. Daily backups must be kept for **35 days**, monthly backups for **12 months**, and yearly backups for **5 years**, or longer where the law requires.
7. Personal data must not be kept in backups longer than the retention period allows.

### 4.5 Testing

8. Backup jobs must be monitored daily, and failures must be fixed within 1 business day.
9. A **restore test** must be performed **every month** for at least one Tier 1 system, and every quarter for Tier 2 systems.
10. A **full recovery exercise** of the payment platform must be performed at least **once a year**.
11. Every test must be documented: what was restored, how long it took, whether it met the RTO and RPO, and any issues found.

## 5. Compliance and exceptions

- Monthly reports show backup success rates and restore test results.
- Any system that misses its RPO or RTO in a test must have a corrective action plan within 30 days.
- Exceptions require written approval from the CTO.

## 6. Related documents

- Business Impact Analysis and Disaster Recovery Plan (Project 4)
- Risk register: R01, R08, R12

## 7. Version history

| Version | Date | Change | Author |
|---|---|---|---|
| 0.1 | 2026 | First draft | Ayshah Albakri |
