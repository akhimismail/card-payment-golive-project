# RAID Log: Debit Card BIN Migration & Go-Live

RAID = Risks, Assumptions, Issues, Dependencies. Reviewed weekly with the steering committee.

## Risks

| ID | Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|---|
| R1 | Visa certification test cases fail on first submission, delaying go-live | Medium | High | Run internal mock-certification testing 2 weeks before formal submission | QA Lead |
| R2 | Authorization approval rate drops post-cutover due to routing misconfiguration | Medium | High | Parallel-run old and new systems for 48 hours pre-cutover to compare live approval rates | Processor Lead |
| R3 | Legacy processor decommissioned before all edge-case BINs (e.g. inactive/dormant cards) are migrated | Low | Medium | Full BIN inventory reconciliation sign-off before decommission approval | TPM |
| R4 | Customer support team not trained on new dispute/chargeback workflow before go-live | Medium | Medium | Mandatory support team training + runbook completed by Week 10 | Customer Support Lead |
| R5 | DR failover not tested under real transaction load | Low | High | Schedule a full DR failover drill during Week 11 readiness window | Infrastructure Lead |

## Assumptions

| ID | Assumption | Validation Owner |
|---|---|---|
| A1 | New processor's API supports current authorization response time SLA (<1s) | Engineering |
| A2 | Visa certification lead time will not exceed 3 weeks | TPM (confirm with Visa account manager) |
| A3 | No core banking system changes required in parallel with this migration | Client Bank IT |

## Issues (active/resolved log)

| ID | Issue | Status | Resolution |
|---|---|---|---|
| I1 | Test environment for processor not available until Week 4 (1 week later than planned) | Resolved | Compressed integration test window; added 1 extra QA resource |
| I2 | Discrepancy found between client's BIN inventory and processor's onboarding list (12 BINs missing) | Resolved | Joint reconciliation session with client + processor; corrected list signed off |

## Dependencies

| ID | Dependency | Depends On | Needed By |
|---|---|---|---|
| D1 | Go-live cutover cannot start | Visa certification sign-off | Week 10 |
| D2 | Hypercare monitoring | Infrastructure/Ops dashboard setup | Week 12 |
| D3 | Customer support readiness | Completed training + runbook | Week 11 |
| D4 | Final go/no-go decision | Client Bank steering committee approval | Week 11, Day 5 |
