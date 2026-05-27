---
name: System Onboarding Security Gate
about: Definitive Definition of Done (DoD) checklist for replicating APAC Auto core systems.
title: '[SECURITY-GATE] - '
labels: security-audit, infrastructure
assignees: ''
---

## System Architecture Compliance Check
Before this system component is granted an automated deploy permit into the target staging environments, the assigning engineering lead must verify compliance against the APAC-Core Security Framework.

### 🔐 1. Identity & Access Governance
- [ ] **Internal Identity:** Centralized Azure Active Directory (AAD) integration verified.
- [ ] **External Identity:** Azure AD B2C (ADB2C) + ThreatMetrix risk-based MFA activated for agents/brokers.
- [ ] **Privileged Access:** Service account credentials stored natively in CyberArk with automated 90-day rotation.

### 💾 2. Cryptographic Data Protection
- [ ] **Data-in-Transit:** TLS 1.2+ forced; fallback ciphers permanently disabled.
- [ ] **RED Data (SPI/SBI):** Database-level transparent data encryption + explicit column-level tokenization active.
- [ ] **Unstructured PII:** Generated schedules/invoices encrypted using PGP on disk write.

### 🛡️ 3. Pipeline Security & Code Quality Gating
- [ ] **SAST/SCA:** SonarQube quality gate configured to block pull requests failing a `B` security rating.
- [ ] **DAST:** IBM Security AppScan pipeline hooks verified.
- [ ] **WAF:** Akamai WAF perimeter shielding bound to target subnets.
