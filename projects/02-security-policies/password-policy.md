# Password and Authentication Policy

| | |
|---|---|
| **Policy ID** | FP-SEC-POL-02 |
| **Owner** | Security Lead |
| **Approved by** | Chief Executive Officer |
| **Effective date** | Draft, pending approval |
| **Review cycle** | Every 12 months |
| **Based on** | NIST SP 800-63B, NCA ECC subdomain 2-2 (Identity and Access Management) |

> FalconPay is a fictional company. This document is a portfolio sample.

## 1. Purpose

Weak or stolen credentials are one of the most common ways attackers get in. This policy sets the minimum requirements for passwords and authentication to protect FalconPay accounts.

## 2. Scope

All user, administrator, and service accounts on FalconPay systems, including cloud consoles, SSO, VPN, and production systems.

## 3. Roles and responsibilities

| Role | Responsibility |
|---|---|
| Security Lead | Owns the policy and reviews compliance |
| IT Operations | Configures technical settings in the identity system |
| System owners | Make sure their systems follow the policy or use SSO |
| All users | Create strong passwords and protect their credentials |

## 4. Policy statements

### 4.1 Passwords

1. Passwords must be at least **12 characters** for user accounts and **16 characters** for administrator accounts.
2. Users are encouraged to use **passphrases** (several words). Up to 64 characters must be supported.
3. New passwords must be checked against a **blocklist** of common and breached passwords.
4. Passwords must **not** be changed on a fixed schedule. They must be changed immediately if a compromise is suspected.
5. Password hints and knowledge-based questions ("What is your pet's name?") must not be used.
6. The last **5 passwords** must not be reused.
7. Passwords must never be shared, written down in plain text, or sent by email or chat.
8. Staff should use the company-approved **password manager**.

### 4.2 Multifactor authentication (MFA)

9. **MFA must be enabled for all accounts**, with no exceptions for senior staff.
10. Administrator, cloud console, and remote access accounts must use **phishing-resistant MFA** (for example FIDO2 security keys).
11. SMS codes may only be used as a temporary fallback, approved by IT.

### 4.3 Account protection

12. Accounts must lock for 15 minutes after **10 failed login attempts**.
13. Logins from unusual locations or "impossible travel" must trigger additional verification (conditional access).
14. Default passwords on all systems and devices must be changed before they go into use.

### 4.4 Privileged and service accounts

15. Administrators must use a **separate admin account** for privileged tasks, not their everyday account.
16. Privileged credentials must be stored and rotated in the privileged access management (PAM) system.
17. Service accounts must not allow interactive login, and their secrets must not be stored in source code.
18. Privileged access must be reviewed every **quarter** (access recertification).

### 4.5 Storage of passwords by systems

19. Systems must store passwords only as **salted hashes** using a slow algorithm (for example bcrypt, scrypt, or Argon2). Passwords must never be stored in plain text or reversible encryption.

## 5. Why no forced complexity or 90-day changes?

NIST SP 800-63B found that forced complexity rules and regular password changes lead people to choose predictable passwords (such as `Summer2026!`) or write them down. Length, blocklists, and MFA provide better protection.

## 6. Compliance and exceptions

- The identity system enforces statements 1, 3, 6, 9, and 12 automatically.
- Quarterly reports cover MFA coverage, privileged account reviews, and accounts that have not been used in 90 days (to be disabled).
- Exceptions require Security Lead approval, a compensating control, and an expiry date.

## 7. Related documents

- Acceptable Use Policy (FP-SEC-POL-01)
- Risk register: R03, R06

## 8. Version history

| Version | Date | Change | Author |
|---|---|---|---|
| 0.1 | 2026 | First draft | Ayshah Albakri |
