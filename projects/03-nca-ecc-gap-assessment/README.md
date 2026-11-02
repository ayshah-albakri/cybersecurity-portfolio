# Project 3: NCA ECC Compliance Gap Assessment

- **Company:** FalconPay (fictional fintech, see [company profile](../../company-profile.md))
- **Framework:** National Cybersecurity Authority (NCA), Essential Cybersecurity Controls, **ECC-2:2024**
- **Deliverables:** gap assessment for all 28 subdomains ([CSV](gap-assessment.csv)), compliance scores, prioritized remediation plan

## 1. Objective

Measure how far FalconPay is from meeting the NCA Essential Cybersecurity Controls, and produce a prioritized plan to close the gaps.

## 2. Scope and approach

- **Framework structure:** ECC-2:2024 has **4 main domains, 28 subdomains, and 110 controls**.
- **Level of assessment:** this portfolio assesses each of the **28 subdomains**. A full audit would test every individual control and collect evidence for each one.
- **Evidence (simulated):** interviews with system owners, review of existing documents, and configuration screenshots.
- **Scoring:**

| Status | Score | Meaning |
|---|---|---|
| Implemented | 2 | Requirement is met and evidence exists |
| Partially implemented | 1 | Some parts exist, or it is done but not documented or approved |
| Not implemented | 0 | No meaningful control in place |

`Compliance % = total score ÷ maximum possible score`

> **Note on regulation:** a real payment company in Saudi Arabia would also need to meet the Saudi Central Bank (SAMA) Cyber Security Framework. This project focuses on ECC as the national baseline.

## 3. Results summary

| Domain | Subdomains | Score | Compliance |
|---|---|---|---|
| 1. Cybersecurity Governance | 10 | 7 / 20 | 35% |
| 2. Cybersecurity Defense | 15 | 16 / 30 | 53% |
| 3. Cybersecurity Resilience | 1 | 0 / 2 | 0% |
| 4. Third-Party and Cloud Computing Cybersecurity | 2 | 2 / 4 | 50% |
| **Overall** | **28** | **25 / 56** | **45%** |

- **3** subdomains implemented, **19** partially implemented, **6** not implemented.
- **14** gaps are high priority.

### Main observations

1. **Governance is the weakest area (35%).** FalconPay has technical tools, but no approved strategy, risk management process, audit program, or clear security roles. Without governance, technical controls are not managed consistently.
2. **Resilience is at 0%.** There is no business impact analysis or disaster recovery plan, which is a serious gap for a payment company. Project 4 addresses this.
3. **Identity, backups, and monitoring are partial.** These match the critical risks found in Project 1 (R01, R03, R10).
4. **Email protection, cryptography, and physical security are strong** and only need maintenance.

## 4. Detailed findings

| Subdomain | Name | Status | Finding | Recommendation | Priority |
|---|---|---|---|---|---|
| 1-1 | Cybersecurity Strategy | Partially implemented | A security roadmap exists in slides but is not approved by management or linked to business goals. | Formalize a 2-year strategy and get board approval. | Medium |
| 1-2 | Cybersecurity Management | Partially implemented | A Security Lead exists but reports to the Head of IT Ops, not independently. | Create a cybersecurity function reporting to senior management and a steering committee. | High |
| 1-3 | Cybersecurity Policies and Procedures | Partially implemented | Policies are outdated and unapproved. | Approve the new policy set (Project 2) and review it yearly. | High |
| 1-4 | Cybersecurity Roles and Responsibilities | Not implemented | No documented RACI for security tasks. | Document roles and responsibilities and include them in job descriptions. | Medium |
| 1-5 | Cybersecurity Risk Management | Not implemented | No risk register or risk methodology before this project. | Adopt the risk methodology and register from Project 1; review quarterly. | High |
| 1-6 | Cybersecurity in IT Project Management | Partially implemented | Security reviews happen for some releases but are not mandatory. | Add security requirements and review gates to the project lifecycle (secure SDLC). | Medium |
| 1-7 | Compliance with Cybersecurity Standards, Laws and Regulations | Partially implemented | Regulatory requirements are known informally but not tracked. | Maintain a compliance obligations register. | Medium |
| 1-8 | Periodical Cybersecurity Review and Audit | Not implemented | No internal or independent security audit has been performed. | Schedule a yearly independent cybersecurity review. | Medium |
| 1-9 | Cybersecurity in Human Resources | Partially implemented | Background checks are done; offboarding does not always disable access the same day. | Link HR offboarding to automatic account disabling; signed AUP and NDA for all staff. | High |
| 1-10 | Cybersecurity Awareness and Training Program | Partially implemented | Onboarding training only; no phishing simulations. | Yearly training plus quarterly phishing simulations. | High |
| 2-1 | Asset Management | Partially implemented | Cloud assets are listed; laptops and SaaS tools are not fully inventoried. | Maintain a complete asset inventory with owners and classification. | Medium |
| 2-2 | Identity and Access Management | Partially implemented | SSO in place; MFA only for engineers; no access reviews. | MFA for all users, PAM for admins, quarterly access recertification. | High |
| 2-3 | Information System and Information Processing Facilities Protection | Partially implemented | Antivirus on laptops; no EDR on servers. | Deploy EDR on servers and laptops; harden baseline configurations. | High |
| 2-4 | Email Protection | Implemented | Email filtering, SPF, DKIM, and DMARC are configured. | Keep monitoring; add a phishing report button. | Low |
| 2-5 | Network Security Management | Partially implemented | Cloud networks are segmented; office network is flat. | Segment the office network and restrict management access. | Medium |
| 2-6 | Mobile Devices Security | Partially implemented | MDM covers company phones, not laptops. | Enroll all laptops in MDM with full disk encryption and remote wipe. | Medium |
| 2-7 | Data and Information Protection | Partially implemented | Customer data is encrypted in the database; no data classification or DLP. | Introduce data classification and DLP for customer data. | High |
| 2-8 | Cryptography | Implemented | TLS 1.2+ for all traffic; keys managed in the cloud KMS. | Document a cryptography standard and key rotation schedule. | Low |
| 2-9 | Backup and Recovery Management | Partially implemented | Daily backups run; restores are never tested; no immutable copy. | Apply the Backup and Recovery Policy (Project 2), including monthly restore tests. | High |
| 2-10 | Vulnerability Management | Partially implemented | Scans run occasionally; no patching deadlines. | Monthly scans and patch SLAs based on severity (CVSS). | High |
| 2-11 | Penetration Testing | Not implemented | No penetration test has been performed. | Yearly external penetration test of internet-facing systems. | Medium |
| 2-12 | Cybersecurity Event Logs and Monitoring Management | Partially implemented | Logs collected in a SIEM; only 30 days retention; no 24/7 monitoring. | 12-month retention, correlation rules, and a managed monitoring service. | High |
| 2-13 | Cybersecurity Incident and Threat Management | Not implemented | No written incident response plan. | Write an incident response plan and playbooks; run a tabletop exercise. | High |
| 2-14 | Physical Security | Implemented | Badge access, CCTV, and visitor logs at the office; production is in the cloud. | Review badge access lists quarterly. | Low |
| 2-15 | Web Application Security | Partially implemented | Code reviews done; no WAF; no automated security testing. | Add a WAF and security testing in the CI pipeline. | Medium |
| 3-1 | Cybersecurity Resilience Aspects of Business Continuity Management | Not implemented | No disaster recovery plan or BIA. | Complete the BIA and DRP (Project 4) and test them yearly. | High |
| 4-1 | Third-Party Cybersecurity | Partially implemented | Contracts include confidentiality clauses; no security assessment of vendors. | Security assessment before onboarding critical vendors; security clauses in contracts. | Medium |
| 4-2 | Cloud Computing and Hosting Cybersecurity | Partially implemented | Hosted in a Saudi cloud region; no cloud security posture monitoring. | Enable configuration monitoring and document shared responsibilities with the provider. | High |
## 5. Remediation roadmap

| Phase | Timeline | Focus | Subdomains |
|---|---|---|---|
| 1. Foundations | 0 to 3 months | Approve policies, start risk management, MFA for all, backup testing, incident response plan | 1-3, 1-5, 2-2, 2-9, 2-13 |
| 2. Detection and protection | 3 to 6 months | EDR, log retention and monitoring, vulnerability management, cloud configuration monitoring, DLP | 2-3, 2-7, 2-10, 2-12, 4-2 |
| 3. Resilience and assurance | 6 to 12 months | BIA and DRP testing, penetration test, yearly audit, security in projects, third-party assessments | 3-1, 2-11, 1-8, 1-6, 4-1 |
| 4. Maturity | 12 months + | Strategy, roles, awareness program, remaining medium and low items | All remaining |

**Target:** reach at least **80% overall compliance** within 12 months, with no "Not implemented" subdomains.

## 6. Link to the other projects

| Gap | Addressed by |
|---|---|
| 1-3 Policies and procedures | Project 2: Security Policies |
| 1-5 Risk management | Project 1: Risk Assessment |
| 2-2 Identity and access, 2-9 Backup | Project 2: Password Policy and Backup Policy |
| 3-1 Resilience and BCM | Project 4: BIA and DRP |

## 7. What I learned

- A gap assessment turns a long list of requirements into a clear picture of where a company stands and what to fix first.
- Governance gaps often matter more than missing tools, because they decide whether controls are maintained.
- "Partially implemented" is the most common result in real assessments: something exists, but it is not documented, approved, or measured.
