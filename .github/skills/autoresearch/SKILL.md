---
name: autoresearch
description: Orchestrate long-running family tree expansion through a resumable 3-phase pipeline (prep, intake, verify).
allowed-tools: read, edit, glob
---

# Autoresearch Orchestrator

## Purpose

Use this skill as the controller for long-cycle genealogy runs. It does not perform direct scraping of protected portals. It coordinates three dedicated skills with runtime checkpoints and resume semantics.

## Pipeline

Run this sequence:

1. `/autoresearch-prep`
   - builds `Search_Queue.md`
   - initializes or updates `Runtime_State.md`

2. manual search collection
   - user prepares `manual_search_batch_YYYY-MM-DD.md` in vault root

3. `/autoresearch-intake`
   - ingests batch
   - updates `Family_Tree.md`, person files, queue state, and checkpoints

4. `/autoresearch-verify`
   - processes Moderate and Speculative leads from `Verification_Queue.md`
   - applies bounded verification loops

5. resume
   - read `Runtime_State.md`
   - continue from recorded `phase` and `next_action`

## Runtime Files (vault root)

- `Search_Queue.md`
- `Verification_Queue.md`
- `Runtime_State.md`
- `Research_Log.md`

## Phase Semantics

Expected phase transitions:
- `prep_done`
- `intake_done`
- `verify_done`
- `waiting_for_manual_batch`

## Non-goals

- No scraping of JavaScript-protected portals
- No bypass of manual batch ingestion
- No destructive overwrite of stronger confidence evidence

## Quick Operator Playbook

- New run: start with `/autoresearch-prep`
- After manual search batch is saved: run `/autoresearch-intake`
- To process unresolved leads: run `/autoresearch-verify`
- On interruption: reopen state and resume from `Runtime_State.md`

## Success Criteria

A cycle is successful when:
- queue and runtime files are updated deterministically
- checkpoints are appended in `Research_Log.md`
- unresolved findings are tracked in `Verification_Queue.md`
- `next_action` clearly indicates the next pipeline step
