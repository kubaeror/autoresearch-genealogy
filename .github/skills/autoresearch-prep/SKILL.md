---
name: autoresearch-prep
description: build search queue and runtime checkpoint for long-running sessions
allowed-tools: read, edit, glob
---

# Autoresearch Prep Skill

## Purpose

Prepare targets from the vault for manual batch search and a resume-safe runtime checkpoint. This skill builds a queue from existing tree context, writes deterministic prep artifacts, and records a checkpoint in the research log before any search execution begins.

## Output Files

Write these files in the vault root:
- `Search_Queue.md`
- `Runtime_State.md`

## Search Queue Schema

`Search_Queue.md` must include these columns exactly:
- `target_id`
- `person`
- `surname_variants`
- `region_hint`
- `search_urls`
- `priority`
- `status (pending|searched|ingested)`

## Runtime State Schema

`Runtime_State.md` must include these fields exactly:
- `session_id`
- `phase`
- `last_checkpoint`
- `tree_total`
- `queue_size`
- `next_action`

Required value after prep completes:
- `phase: prep_done`

## Algorithm

1. read `Family_Tree.md` + `Research_Log.md`
2. detect expansion targets
3. generate surname variants
4. generate source-specific search URLs (manual use)
5. write `Search_Queue.md` with status pending
6. write `Runtime_State.md` with phase prep_done
7. append checkpoint block to `Research_Log.md`

## Non-Goals

- No scraping of JS-protected portals.
- No direct writes to person facts.

## Notes

- Queue links are for manual researcher execution.
- Prep is idempotent when source inputs are unchanged.
- Checkpoint blocks in `Research_Log.md` should include timestamp and queue counts.
