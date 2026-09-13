# Project Charter: Debit Card BIN Migration & Go-Live

## 1. Project Overview
A retail bank ("the Client") is migrating its debit card portfolio (~450,000 active cards) from a legacy card processor to a new processing platform, to reduce processing costs and enable new features (tokenized digital wallet support, real-time authorization analytics). This document defines scope, stakeholders, timeline, and success criteria for the migration and go-live.

## 2. Objectives
- Migrate all active debit BINs to the new processor with zero customer-facing service interruption.
- Achieve full certification with the card scheme (Visa) before go-live.
- Establish production support and disaster recovery (DR) readiness before cutover.
- Complete migration within a 12-week delivery window.

## 3. Scope

**In scope:**
- BIN range migration for debit card products (consumer + business debit)
- Card scheme (Visa) re-certification testing
- Authorization and settlement system cutover
- Chargeback/dispute workflow continuity
- Go-live cutover execution and hypercare (first 2 weeks post go-live)

**Out of scope:**
- Credit card portfolio (separate future phase)
- New physical card issuance/redesign
- Core banking system changes

## 4. Key Stakeholders

| Stakeholder | Role |
|---|---|
| Client Bank (Issuer) | Business owner, final go/no-go authority |
| New Processor | Technical delivery, platform readiness |
| Visa (Card Scheme) | Certification approval, compliance rules |
| Internal Engineering | Integration build, API/connectivity |
| QA Team | Test planning, scheme certification test execution |
| Infrastructure/Ops | Environment readiness, monitoring, DR |
| Customer Support | Front-line readiness for post-go-live issues |

## 5. High-Level Timeline

| Phase | Duration | Milestone |
|---|---|---|
| Planning & Design | Weeks 1–2 | Charter, RAID log, architecture sign-off |
| Build & Integration | Weeks 3–6 | Processor connectivity, test environment ready |
| Scheme Certification | Weeks 7–9 | Visa test cases passed |
| Go-Live Readiness | Weeks 10–11 | Cutover plan rehearsed, DR tested |
| Cutover & Hypercare | Week 12 | Go-live executed, 2-week hypercare monitoring |

## 6. Success Criteria
- 100% of BINs successfully migrated with no unplanned downtime
- Visa certification passed on first submission
- Authorization approval rate within 0.5% of pre-migration baseline
- No P1 incidents unresolved beyond SLA during hypercare

## 7. Governance & Reporting Cadence
- Weekly steering committee update (status, risks, decisions needed)
- Daily stand-up during build and cutover phases
- RAID log reviewed weekly
