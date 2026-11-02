# FalconPay: Case Study Company Profile

> **FalconPay is a fictional company** created for this portfolio. Any resemblance to a real company is unintentional. All figures are illustrative estimates.

All four projects in this portfolio use the same company, so the work connects: the risks found in Project 1 drive the policies in Project 2, the compliance gaps in Project 3, and the recovery priorities in Project 4.

## Overview

| Item | Detail |
|---|---|
| Industry | Financial technology (payments) |
| Location | Riyadh, Saudi Arabia |
| Employees | 220 (45 engineering, 6 IT operations, 3 security) |
| Products | Payment gateway for e-commerce merchants, consumer wallet app, merchant portal |
| Customers | About 1.2 million wallet users and 3,500 merchants |
| Average daily transaction revenue | SAR 450,000 |
| Hosting | Public cloud (IaaS and PaaS) in a Saudi region, plus a small office network |

## Critical business functions

| ID | Function | Why it matters |
|---|---|---|
| F1 | Payment authorization | Every minute offline means failed purchases for merchants |
| F2 | Merchant settlement | Merchants must be paid on time every day |
| F3 | Customer wallet and login | Customers expect 24/7 access to their money |
| F4 | Fraud monitoring | Required to stop fraudulent transactions in real time |
| F5 | Customer support | Handles disputes and account issues |
| F6 | Internal finance and HR | Important, but can pause for a few days |

## Key assets

| ID | Asset | Owner | Data | Estimated value (SAR)* |
|---|---|---|---|---|
| A01 | Payment processing platform | CTO | Transactions | 4,000,000 |
| A02 | Customer database | Head of Data | PII, card tokens | 3,000,000 |
| A03 | Mobile app and API gateway | Head of Engineering | Session data | 1,500,000 |
| A04 | Cloud hosting environment | Head of IT Ops | All production workloads | 5,000,000 |
| A05 | Corporate identity (SSO / directory) | Head of IT Ops | Staff accounts | 600,000 |
| A06 | Employee laptops (220) | Head of IT Ops | Internal documents | 900,000 |
| A07 | Backup storage | Head of IT Ops | Copies of A01 and A02 | 400,000 |
| A08 | Merchant portal | Head of Product | Merchant data | 800,000 |
| A09 | Logging and SIEM | Security Lead | Security logs | 300,000 |
| A10 | Office network and Wi-Fi | Head of IT Ops | Internal traffic | 250,000 |

\* Value includes replacement cost, downtime cost, and reputational impact, not only the purchase price.

## Current security posture (starting point)

- A small security team of 3 with no formal risk register.
- Policies exist but are outdated and not approved by management.
- MFA is enabled for engineers only.
- Backups run daily, but restores have never been tested.
- No documented disaster recovery plan.
- Logs are kept for 30 days.
