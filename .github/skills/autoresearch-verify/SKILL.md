---
name: autoresearch-verify
description: Process verification queue with bounded retry loops for moderate and speculative findings, then update runtime/checkpoints.
allowed-tools: read, edit, glob
---

# Autoresearch Verify Skill

## Purpose

Run bounded verification loops for unresolved leads after intake.

This skill is phase 3 in the background pipeline:
`autoresearch-prep -> manual_search_batch -> autoresearch-intake -> autoresearch-verify`.

## Inputs and Runtime Files (vault root)

Read and update:
- `Verification_Queue.md`
- `Runtime_State.md`
- `Research_Log.md`
- `Search_Queue.md` (optional status sync)

Use person files and `Family_Tree.md` only when a lead is upgraded and confirmed.

## Queue Contract

`Verification_Queue.md` rows must include:
- `lead_id`
- `person`
- `signal (moderate|speculative)`
- `evidence`
- `attempts`
- `next_step`
- `status (open|escalated|cold|resolved)`

Process rows with status `open` first, then `escalated`.

## Verification Logic

### Moderate Signal Path

- maximum 2 attempts
- each attempt seeks corroboration through independent evidence
- if corroborated:
  - upgrade finding to Strong
  - mark lead `resolved`
  - remove `(unverified)` marker from affected claim
- if attempts exhausted without corroboration:
  - keep `status: escalated` or retain moderate state for future manual batch

### Speculative Signal Path

- maximum 3 attempts
- attempt sequence:
  1. alternative variants / neighboring context
  2. related-family cross-reference
  3. source-image or stronger indirect corroboration
- if unresolved after attempt 3:
  - move to `status: cold`
  - do not treat as confirmed fact

## Runtime Updates

Update `Runtime_State.md` with:
- `phase: verify_done` when verification pass completes
- `phase: waiting_for_manual_batch` if queue requires new external evidence to proceed
- `last_checkpoint`
- counters:
  - resolved leads
  - escalated leads
  - cold leads
  - remaining open leads
- `next_action`

## Checkpoint Logging

Append checkpoint blocks to `Research_Log.md` with:
- timestamp
- skill name (`autoresearch-verify`)
- processed lead counts by signal
- outcomes: resolved/escalated/cold/open
- blockers and next action

## Safety Rules

- Never overwrite Strong evidence with weaker data
- Never convert speculative lead into confirmed fact without corroboration
- Keep queue edits deterministic and idempotent for repeated runs

## Non-Goals

- No JS portal scraping
- No hidden browser automation
- No unbounded verification loops

## Completion Criteria

Run is complete when:
- all currently eligible queue rows are processed according to attempt limits
- queue statuses and attempts are updated deterministically
- runtime and research checkpoints are written
- next action is explicit for resume
