# Autoresearch Background Workflow

Operational runbook for long-cycle, resume-safe genealogy sessions.

## Runtime Files (vault root)

- `Search_Queue.md`
- `Verification_Queue.md`
- `Runtime_State.md`
- `Research_Log.md`

## End-to-End Cycle

1. Run `/autoresearch-prep`
2. Create `manual_search_batch_YYYY-MM-DD.md` from manual source checks
3. Run `/autoresearch-intake`
4. Run `/autoresearch-verify`
5. Repeat cycle or resume from `Runtime_State.md`

## Resume Rules

1. Read `Runtime_State.md`
2. Continue from `phase`
3. Execute `next_action`
4. Append checkpoint block to `Research_Log.md`

## Runtime State Template

```yaml
---
session_id: "2026-03-31-run-01"
phase: prep_done
last_checkpoint: "2026-03-31T17:00:00Z"
tree_total: 40
added_strong: 0
added_moderate: 0
speculative_open: 0
queue_size: 25
next_action: "Create manual_search_batch_YYYY-MM-DD.md and run /autoresearch-intake"
---
```

## Search Queue Schema

Columns:
- `target_id`
- `person`
- `surname_variants`
- `region_hint`
- `search_urls`
- `priority`
- `status` (`pending`, `searched`, `ingested`)

## Failure and Waiting States

If no batch file is present for intake:
- set `phase: waiting_for_manual_batch`
- update `next_action` with expected filename pattern
- append waiting checkpoint in `Research_Log.md`

## Idempotency Rules

- Keep deterministic queue row keys (`target_id`, `lead_id`)
- Avoid duplicate source insertions through hash-based checks
- Never downgrade Strong evidence with weaker findings

## Logging Requirements

Each pipeline run appends checkpoint blocks to `Research_Log.md` including:
- timestamp
- phase and skill
- processed count
- added/updated counts by confidence
- queue and blocker summary
- explicit next step
