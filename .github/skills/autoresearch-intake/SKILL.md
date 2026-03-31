---
name: autoresearch-intake
description: Ingest manual search batches into the vault, route findings by confidence, and update verification/runtime state for long-running sessions.
allowed-tools: read, edit, glob
---

# Autoresearch Intake Skill

## Purpose

Process manual search batches from interactive sources, apply confidence routing, update vault records safely, and enqueue unresolved leads for verification.

This skill is phase 2 in the background pipeline:
`autoresearch-prep -> manual_search_batch -> autoresearch-intake -> autoresearch-verify`.

## Required Input

The vault root must contain at least one file matching:
- `manual_search_batch_YYYY-MM-DD.md`

If no batch file exists:
- Do not fail hard
- Set `Runtime_State.md` to `phase: waiting_for_manual_batch`
- Set `next_action` to expected file pattern
- Append checkpoint note in `Research_Log.md`

## Runtime Files (vault root)

Read and update:
- `Runtime_State.md`
- `Search_Queue.md`
- `Verification_Queue.md`
- `Research_Log.md`

Update target records:
- `Family_Tree.md`
- Person files under `People/<Surname>/<Given>_<Surname>.md`

## Manual Batch Contract

A `manual_search_batch_YYYY-MM-DD.md` file must be organized in sections per target and include:

- `target_id`
- one or more records with:
  - parish
  - year
  - act
  - event
  - name
  - uwagi (remarks)
- optional user notes

Example section:

```md
## target_id: T-001 | person: Jan Kowalski
URL: https://geneteka.genealodzy.pl/index.php?... 
- parish: Płock | year: 1880 | act: 42 | event: birth | name: Jan Kowalski | uwagi: s. Piotra i Marianny
- notes: Candidate likely same line as [[Wojciech_Kowalski]]
```

Parser requirements:
- parse section-by-section by `target_id`
- if one section is malformed, log warning and continue with remaining sections

## Confidence Routing

For each parsed record:

### Strong
- Write/update person facts in vault
- Set `confidence: high`
- Add source citation
- Mark corresponding queue item as `ingested` when complete

### Moderate
- Write with `(unverified)` marker
- Set `confidence: moderate`
- Enqueue lead in `Verification_Queue.md` with `signal: moderate`

### Speculative
- Do not insert as confirmed person fact
- Log lead in `Research_Log.md`
- Enqueue lead in `Verification_Queue.md` with `signal: speculative`

Never overwrite existing Strong facts with lower confidence input.

## Deduplication and Idempotency

Compute:
- `source_hash = sha1(parish|year|act|event|person_normalized)`

Behavior:
- if source hash already exists in target record/log context, skip insert
- maintain stable output on repeated intake runs for identical input batches
- avoid duplicate queue entries for identical lead identifiers

## Queue and Runtime Updates

### Search_Queue.md
- update item status: `pending -> searched -> ingested`
- preserve rows that were not in current batch

### Verification_Queue.md
Columns:
- `lead_id`
- `person`
- `signal (moderate|speculative)`
- `evidence`
- `attempts`
- `next_step`
- `status (open|escalated|cold|resolved)`

Add new leads as:
- `attempts: 0`
- `status: open`

### Runtime_State.md
Set/update:
- `phase: intake_done` on successful processing
- `last_checkpoint`
- counters (tree_total, added_strong, added_moderate, speculative_open, queue_size)
- `next_action: run /autoresearch-verify`

## Checkpoint Logging

Append a checkpoint block to `Research_Log.md` at run start and run end.

Minimum fields:
- timestamp
- skill name (`autoresearch-intake`)
- processed section count
- added/updated by confidence tier
- parse warnings count
- queue/runtimes summary
- next action

## Non-Goals

- No scraping of JS-protected portals
- No browser automation
- No destructive overwrite of higher-confidence facts

## Completion Criteria

The run is complete when:
- all valid sections in target manual batch are processed
- runtime and queue files are updated
- checkpoint is appended to `Research_Log.md`
- unresolved leads are queued for `autoresearch-verify`
