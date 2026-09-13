# Go-Live / Cutover Plan: Debit Card BIN Migration

**Cutover Window:** Saturday 23:00 – Sunday 05:00 (low-traffic window)
**Rollback Decision Deadline:** 03:00 (must decide go/rollback with 2 hours buffer before peak Sunday morning traffic)

## War Room Roles

| Role | Person | Responsibility |
|---|---|---|
| Cutover Lead (TPM) | Akhim | Overall coordination, go/no-go calls, stakeholder comms |
| Processor Engineer | Processor team | Executes BIN cutover on processing platform |
| Client Bank Rep | Client IT | Confirms core banking system readiness at each checkpoint |
| QA Lead | QA team | Runs post-cutover smoke tests |
| Infra/Ops Lead | Infra team | Monitors system health, DR standby |
| Customer Support Lead | Support team | On standby for live customer issues |

## Timeline

| Time | Action | Go/No-Go Checkpoint? |
|---|---|---|
| 22:00 | Final pre-cutover health check on legacy system; freeze all non-critical changes | No |
| 23:00 | Legacy processor placed into read-only mode; final transaction reconciliation begins | Yes — confirm reconciliation matches before proceeding |
| 23:30 | BIN routing switched to new processor | No |
| 00:00 | Smoke tests: sample authorization, decline, and settlement transactions | Yes — pass/fail gate |
| 00:30 | Monitor live authorization approval rate vs. baseline (target: within 0.5%) | Yes — continuous monitoring |
| 01:30 | Chargeback/dispute workflow validation test | No |
| 02:30 | Full system health review with all leads | Yes — final go/no-go |
| 03:00 | **Decision point:** proceed to full production or trigger rollback | Yes — hard deadline |
| 04:00 | If GO: legacy processor fully decommissioned from routing | No |
| 05:00 | Cutover closed; hand off to hypercare monitoring (next 2 weeks) | No |

## Rollback Trigger Criteria
Rollback to legacy processor is triggered if, at any checkpoint:
- Authorization approval rate drops more than 0.5% below baseline, OR
- Any P1 (critical) system failure is unresolved after 30 minutes, OR
- Core banking reconciliation does not match within acceptable tolerance

## Communication Cadence
- Internal war room: status update every 30 minutes via dedicated channel
- Client steering committee: update at 23:00, 01:00, 03:00 (decision point), and 05:00 (close)
- Customer-facing: no proactive comms unless rollback or incident occurs (avoid alarming customers over a routine low-traffic window)

## Hypercare (Weeks 12–13 post go-live)
- Daily monitoring of authorization approval rate, decline reasons, and dispute volume
- Dedicated on-call rotation for P1/P2 issues
- Daily 15-minute check-in, reducing to twice-weekly after week 1 if stable
