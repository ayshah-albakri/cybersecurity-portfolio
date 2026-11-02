# Project 1: Cybersecurity Risk Assessment

- **Company:** FalconPay (fictional fintech, see [company profile](../../company-profile.md))
- **Frameworks used:** NIST SP 800-30 (risk assessment process), quantitative and qualitative analysis
- **Deliverables:** risk register ([CSV](risk-register.csv)), heat map, treatment plan, cost-benefit analysis

## 1. Objective

FalconPay has no formal view of its cybersecurity risks. The goal of this assessment is to identify the most significant risks to its critical business functions, measure them in both business terms (money) and simple ratings, and recommend which controls to fund first.

## 2. Scope

- **In scope:** the ten key assets in the company profile (payment platform, customer database, cloud hosting, identity, endpoints, backups, merchant portal, logging, office network).
- **Out of scope:** physical safety risks and non-cyber financial risks.

## 3. Method

1. Identified the critical business functions and the assets that support them.
2. For each asset, listed realistic threats and existing weaknesses.
3. Rated each risk two ways:
    - **Qualitative:** Likelihood (1 to 5) × Impact (1 to 5) = score from 1 to 25.
    - **Quantitative:** `SLE = Asset value × Exposure factor (EF)` and `ALE = SLE × ARO`.
4. Chose a treatment for each risk (mitigate, transfer, avoid, or accept) and estimated the residual risk.
5. Compared the yearly cost of each control with the loss it prevents using **ROSI**:
    `ROSI = ((ALE before − ALE after) − control cost) ÷ control cost`

### Rating scales

| Score | Likelihood | Impact |
|---|---|---|
| 1 | Rare (less than once in 10 years) | Minimal, no customer impact |
| 2 | Unlikely | Minor, internal only |
| 3 | Possible (about once in 3 to 5 years) | Moderate, some customers affected |
| 4 | Likely (about once a year) | Major, service outage or data exposure |
| 5 | Almost certain | Severe, regulatory action or business failure |

| Score range | Level |
|---|---|
| 15 to 25 | Critical |
| 10 to 14 | High |
| 5 to 9 | Medium |
| 1 to 4 | Low |

## 4. Heat map (inherent risk, before new controls)

| Likelihood ↓ / Impact → | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| **5** | · | · | · | · | · |
| **4** | · | R07 | · | R03 | · |
| **3** | · | · | R05, R10 | R04, R09 | R01, R02 |
| **2** | · | R11 | · | R08 | R06 |
| **1** | · | · | · | · | R12 |
## 5. Risk register (inherent risk)

| ID | Risk | Asset | SLE (SAR) | ARO | ALE (SAR) | L × I | Level |
|---|---|---|---|---|---|---|---|
| R01 | Ransomware encrypts payment platform servers | Payment processing platform | 1,600,000 | 0.2 | 320,000 | 3 × 5 = 15 | Critical |
| R02 | Customer database exposed through a misconfigured cloud storage policy | Customer database (PII) | 1,800,000 | 0.15 | 270,000 | 3 × 5 = 15 | Critical |
| R03 | Employee account taken over through phishing | Corporate identity (SSO) | 300,000 | 1.0 | 300,000 | 4 × 4 = 16 | Critical |
| R04 | DDoS attack takes the payment API offline | Mobile app & API gateway | 375,000 | 0.5 | 187,500 | 3 × 4 = 12 | High |
| R05 | Third-party SDK in the mobile app contains a vulnerability | Mobile app & API gateway | 300,000 | 0.3 | 90,000 | 3 × 3 = 9 | Medium |
| R06 | Insider with excessive privileges alters merchant settlement data | Payment processing platform | 400,000 | 0.1 | 40,000 | 2 × 5 = 10 | High |
| R07 | Laptop with unencrypted data is lost or stolen | Employee endpoints | 45,000 | 2.0 | 90,000 | 4 × 2 = 8 | Medium |
| R08 | Backups fail silently and cannot be restored | Backup storage | 400,000 | 0.1 | 40,000 | 2 × 4 = 8 | Medium |
| R09 | Unpatched internet-facing merchant portal is exploited | Merchant portal | 240,000 | 0.3 | 72,000 | 3 × 4 = 12 | High |
| R10 | Security logs are not retained long enough to investigate an incident | Logging / SIEM | 150,000 | 0.2 | 30,000 | 3 × 3 = 9 | Medium |
| R11 | Rogue access point in the office captures staff credentials | Office network & Wi-Fi | 50,000 | 0.2 | 10,000 | 2 × 2 = 4 | Low |
| R12 | Primary cloud region outage stops all services | Cloud hosting | 750,000 | 0.05 | 37,500 | 1 × 5 = 5 | Medium |
## 6. Treatment plan and residual risk

| ID | Treatment | Key controls | Residual | Cost / year (SAR) | ALE after (SAR) | ROSI |
|---|---|---|---|---|---|---|
| R01 | Mitigate | EDR on all servers; immutable offline backups; network segmentation; tested restore runbook | 6 (Medium) | 120,000 | 160,000 | 0.33 |
| R02 | Mitigate | Least-privilege resource policies; CSPM scanning; encryption with customer-managed keys; DLP | 4 (Low) | 120,000 | 90,000 | 0.5 |
| R03 | Mitigate | Phishing-resistant MFA; quarterly phishing simulations; conditional access | 6 (Medium) | 90,000 | 75,000 | 1.5 |
| R04 | Transfer + Mitigate | Cloud DDoS protection service; rate limiting; autoscaling; cyber insurance | 4 (Low) | 150,000 | 37,500 | 0.0 |
| R05 | Mitigate | Software composition analysis in CI; vendor security assessment; SBOM | 4 (Low) | 40,000 | 30,000 | 0.5 |
| R06 | Mitigate | Separation of duties; PAM; quarterly access recertification; integrity monitoring | 4 (Low) | 70,000 | 12,000 | -0.6 |
| R07 | Mitigate | Full disk encryption; MDM remote wipe; clean desk policy | 2 (Low) | 25,000 | 900 | 2.56 |
| R08 | Mitigate | Automated backup verification; monthly restore tests; 3-2-1 rule | 3 (Low) | 30,000 | 8,000 | 0.07 |
| R09 | Mitigate | Patch SLA (critical within 7 days); WAF; monthly vulnerability scans; annual penetration test | 6 (Medium) | 45,000 | 19,200 | 0.17 |
| R10 | Mitigate | 12-month log retention; SIEM correlation rules; log integrity protection | 2 (Low) | 35,000 | 3,000 | -0.23 |
| R11 | Accept | Monitor with wireless survey twice a year; WPA3-Enterprise already in place | 4 (Low) | 0 | 10,000 | n/a |
| R12 | Mitigate | Warm standby in a second availability zone; geo-redundant backups; DR runbook | 3 (Low) | 240,000 | 15,000 | -0.91 |
## 7. Key findings

1. **Three critical risks** need action first: phishing-based account takeover (R03), ransomware (R01), and exposure of customer data through a cloud misconfiguration (R02).
2. **Total expected yearly loss drops from SAR 1,487,000 to SAR 460,600** (a 69% reduction) for a combined control budget of SAR 965,000 per year.
3. **The best value controls** are full disk encryption with remote wipe (R07, ROSI 2.56) and phishing-resistant MFA with awareness training (R03, ROSI 1.5).
4. **Some controls have a negative ROSI but are still recommended:**
    - **R12 (cloud region outage):** rare, but a full outage stops every business function, and regulators expect a tested recovery capability.
    - **R06 (insider fraud):** separation of duties and access reviews are expected controls for a payment company, regardless of cost.
    - **R10 (log retention):** without logs, FalconPay cannot investigate incidents or prove compliance.

    ROSI supports the decision but does not replace regulatory and business judgment.
5. **One risk is accepted:** the rogue access point (R11). The impact is low, WPA3-Enterprise is already in place, and twice-yearly wireless surveys are enough to monitor it.

## 8. Recommended roadmap

| Phase | Timeline | Actions |
|---|---|---|
| 1 | First 30 days | Enforce MFA for all staff (R03); fix cloud storage policies and enable configuration scanning (R02); start monthly restore tests (R08) |
| 2 | 30 to 90 days | Deploy EDR and immutable backups (R01); enable DDoS protection and rate limiting (R04); set patch SLAs and a WAF (R09) |
| 3 | 90 to 180 days | Privileged access management and access recertification (R06); 12-month log retention (R10); warm standby site (R12) |
| Ongoing | Quarterly | Review the register, update ratings, and report residual risk to management |

## 9. Limitations

- Asset values, exposure factors, and occurrence rates are estimates for a fictional company. In a real assessment they would come from finance data, incident history, and industry reports.
- Ratings should be reviewed with each asset owner before approval.

## 10. What I learned

- Quantitative numbers make risks easier to explain to management, but they depend heavily on the quality of the estimates.
- A heat map shows priorities at a glance, while the register keeps the detail needed to track each risk over time.
- Risk treatment is a business decision: some controls are justified by regulation or catastrophic impact, not only by cost.
