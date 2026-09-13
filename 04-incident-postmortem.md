# Incident Postmortem: Elevated Authorization Decline Rate Post Go-Live

**Incident ID:** INC-2026-0142
**Severity:** P2 (degraded service, no full outage)
**Date/Time Detected:** Sunday 06:47, ~1h47m after cutover completion
**Time Resolved:** Sunday 08:15
**Duration of Impact:** ~1h28m

## Summary
During early hypercare monitoring, the authorization decline rate for the migrated debit BINs rose from a baseline of ~2.1% to 6.8%. No full outage occurred — approved transactions continued to process normally — but a meaningfully higher share of legitimate transactions were being declined.

## Timeline

| Time | Event |
|---|---|
| 06:47 | Monitoring dashboard alert: decline rate exceeds 5% threshold for 15 consecutive minutes |
| 06:50 | On-call engineer acknowledges alert, begins triage |
| 06:55 | TPM notified via on-call escalation; war room reconvened |
| 07:05 | Pattern identified: declines concentrated on a specific merchant category code (MCC) — online/e-commerce transactions |
| 07:20 | Root cause hypothesis: new processor's fraud-scoring ruleset was applying a stricter default threshold for card-not-present (CNP) transactions than the legacy system |
| 07:35 | Confirmed with Processor Engineer: default CNP fraud threshold was more conservative than agreed configuration |
| 07:45 | Fraud threshold adjusted to match agreed configuration; change deployed |
| 08:00 | Decline rate observed returning to baseline (~2.3%) |
| 08:15 | Incident closed; confirmed stable for 15 minutes post-fix |

## Root Cause
A configuration mismatch: the new processor's default fraud-scoring threshold for card-not-present transactions was not overridden with the client's agreed risk settings during the environment setup phase. This was not caught during pre-cutover testing because the test suite used card-present (in-store) transaction scenarios, not CNP scenarios.

## Impact
- Estimated 4.7% of legitimate e-commerce transactions declined in error during the ~1h28m window
- No data loss, no security exposure, no funds at risk
- Customer support received a small spike in related inquiries (handled within normal SLA)

## Corrective Actions

| Action | Owner | Status |
|---|---|---|
| Add CNP-specific transaction scenarios to the standard pre-cutover test suite | QA Lead | Completed |
| Add fraud-threshold configuration values to the pre-cutover sign-off checklist | TPM | Completed |
| Add a dedicated "decline rate by transaction type" panel to hypercare monitoring dashboard (not just aggregate rate) | Infra/Ops Lead | Completed |
| Post-incident review shared with client steering committee | TPM | Completed |

## Lessons Learned
Aggregate-level monitoring (overall decline rate) can mask a problem that's concentrated in one transaction type. Segmenting monitoring by transaction category from day one of hypercare would have surfaced this pattern faster. This is now standard practice for future migrations.
