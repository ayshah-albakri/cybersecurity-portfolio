# Project 2: Information Security Policies

- **Company:** FalconPay (fictional fintech, see [company profile](../../company-profile.md))
- **Frameworks referenced:** NIST SP 800-63B (passwords), NCA Essential Cybersecurity Controls (ECC-2:2024), CIS Controls
- **Deliverables:** three policies ready for management approval

| Policy | Addresses risks | Related ECC subdomains |
|---|---|---|
| [Acceptable Use Policy](acceptable-use-policy.md) | R03 phishing, R07 lost laptops, R11 rogue devices | 1-3, 1-9, 1-10, 2-6 |
| [Password and Authentication Policy](password-policy.md) | R03 account takeover, R06 insider misuse | 2-2 |
| [Backup and Recovery Policy](backup-policy.md) | R01 ransomware, R08 failed backups, R12 region outage | 2-9, 3-1 |

## Why these three

The [risk assessment](../01-risk-assessment/README.md) showed that FalconPay's critical risks come from three places: **people** (phishing and misuse of devices), **identity** (weak authentication), and **recovery** (untested backups). Each policy closes one of these gaps.

## How the policies are structured

Every policy uses the same structure so staff can find information quickly:

1. **Purpose:** why the policy exists.
2. **Scope:** who and what it covers.
3. **Roles and responsibilities:** who owns, enforces, and follows it.
4. **Policy statements:** numbered, testable rules using "must" and "must not".
5. **Compliance and exceptions:** how compliance is checked and how exceptions are approved.
6. **Review:** how often the policy is updated.
7. **Version history.**

## Design choices

- **Testable statements.** Each rule can be checked by an auditor, for example "MFA must be enabled for all accounts", not "accounts should be secure".
- **Modern password guidance.** Following NIST SP 800-63B, the password policy favors length and blocklists over forced complexity and periodic changes.
- **Plain language.** Policies are written for all employees, not only technical staff.
- **Traceability.** Each policy links back to the risks it reduces and the ECC subdomains it supports.

## What I learned

- A policy is only useful if it can be followed and measured.
- Policies, standards, and procedures are different: the policy says *what* must happen, while procedures explain *how*.
- Good policies need an owner, an exception process, and a review date, or they quickly become outdated.
