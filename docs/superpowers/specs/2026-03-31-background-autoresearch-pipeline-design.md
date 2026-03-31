# Design Spec: Background Autoresearch Pipeline (prep, intake, verify)

Date: 2026-03-31
Repository: `autoresearch-genealogy`
Status: Approved for implementation

## 1. Problem Statement

Current skills are strong as guides but insufficient for long-running, resumable workflows. We need a practical background-capable process that can run for hours, survive interruptions, and systematically process the whole tree with confidence-driven verification loops.

Because major sources like Geneteka and Szukaj w Archiwach are interaction-heavy, the design uses a hybrid pipeline: AI-prep and AI-analysis phases run autonomously, with manual search batches as explicit inputs.

## 2. Scope

### In scope
- New three-skill pipeline:
  - `/autoresearch-prep`
  - `/autoresearch-intake`
  - `/autoresearch-verify`
- Runtime state files in vault root:
  - `Search_Queue.md`
  - `Verification_Queue.md`
  - `Runtime_State.md`
- Checkpoint markers in `Research_Log.md`
- Idempotent ingestion with source-level deduplication
- Documentation updates (README + workflows + agent/skills alignment)

### Out of scope
- Fully automated web scraping of JavaScript-protected sources
- Browser automation frameworks or external RPA tooling
- Replacing manual research judgment for ambiguous source interpretation

## 3. Architecture

### 3.1 Pipeline overview

1. `autoresearch-prep`
- Reads `Family_Tree.md` and `Research_Log.md`
- Selects targets (leaf nodes, sparse branches, high-value unresolved lines)
- Generates surname variants and search instructions
- Writes `Search_Queue.md`
- Updates `Runtime_State.md` to `phase: prep_done`

2. `autoresearch-intake`
- Reads `manual_search_batch_YYYY-MM-DD.md`
- Parses findings per target
- Runs confidence evaluation (Strong, Moderate, Speculative)
- Updates vault entities (`Family_Tree.md`, person files, `Research_Log.md`)
- Enqueues unresolved findings to `Verification_Queue.md`
- Updates `Runtime_State.md` to `phase: intake_done` (or waiting state)

3. `autoresearch-verify`
- Processes rows from `Verification_Queue.md`
- Moderate path: up to 2 verification attempts
- Speculative path: up to 3 attempts, then move to cold queue
- Logs outcomes and updates queue statuses
- Updates `Runtime_State.md` to `phase: verify_done` or `waiting_for_manual_batch`

### 3.2 Runtime files (vault root)

#### `Runtime_State.md`
Frontmatter fields:
- `session_id`
- `phase`
- `last_checkpoint`
- `tree_total`
- `added_strong`
- `added_moderate`
- `speculative_open`
- `queue_size`
- `next_action`

#### `Search_Queue.md`
Table columns:
- `target_id`
- `person`
- `surname_variants`
- `region_hint`
- `search_urls`
- `priority`
- `status` (`pending`, `searched`, `ingested`)

#### `Verification_Queue.md`
Table columns:
- `lead_id`
- `person`
- `signal` (`moderate`, `speculative`)
- `evidence`
- `attempts`
- `next_step`
- `status` (`open`, `escalated`, `cold`, `resolved`)

### 3.3 Input contract for intake

`manual_search_batch_YYYY-MM-DD.md`:
- section per target
- contains `target_id`
- one or more result lines with structured fields:
  - parish
  - year
  - act
  - event type
  - name
  - remarks/uwagi
- optional user notes

The intake skill must continue if one section is malformed and process remaining sections.

## 4. Data Integrity and Idempotency

### 4.1 Deduplication key
`source_hash = sha1(parish|year|act|event|person_normalized)`

Behavior:
- If hash exists in target person/source section, skip insert
- If new data conflicts with existing Strong evidence, do not overwrite Strong with Moderate/Speculative
- Log conflicts to `Research_Log.md` under discrepancy section

### 4.2 Update rules
- Strong: update vault immediately
- Moderate: add with `(unverified)` marker and queue verification
- Speculative: do not write to person profile as fact; enqueue and log lead

## 5. Error Handling

- Missing batch file:
  - set `phase: waiting_for_manual_batch`
  - set `next_action` with expected file name pattern
  - append checkpoint in `Research_Log.md`

- Parse errors in one target section:
  - log parse warning with `target_id`
  - continue with next section

- Source contradiction (existing Strong vs incoming lower confidence):
  - no destructive overwrite
  - log discrepancy and required follow-up

## 6. Observability and Checkpoints

Each skill appends checkpoint block to `Research_Log.md`:
- timestamp
- skill name
- processed item counts
- added/updated counts by confidence
- queue stats
- blockers and `next_action`

Checkpoint cadence:
- at start of skill run
- after each batch chunk
- at run end

## 7. Testing Strategy (Dry Run)

1. Prep test
- Input: current `Family_Tree.md`
- Output: valid `Search_Queue.md` + `Runtime_State.md`

2. Intake test
- Input: synthetic `manual_search_batch_*.md`
- Validate parsing, confidence branching, and hash dedup

3. Verify test
- Input: seeded `Verification_Queue.md`
- Validate attempt increments and speculative cold-queue transition

4. Resume test
- Interrupt after intake checkpoint
- Re-run verify and ensure continuation from `Runtime_State.md`

## 8. Documentation Changes

- README: add full operational flow
  - prep -> manual batch -> intake -> verify -> resume
- Workflows:
  - `workflows/autoresearch-background.md`
  - `workflows/verification-loop.md`
- Agent and skill docs aligned with queue/state contracts

## 9. Trade-offs and Rationale

### Chosen approach: Lightweight 3-file state model (A)
Why:
- human-readable and easy to edit manually
- robust restart semantics
- low complexity overhead
- clear separation between queue, verification, and runtime status

Alternatives rejected:
- single monolithic runtime file: less readable and harder for manual correction
- per-iteration file tree: better audit depth but unnecessary complexity for current scale

## 10. Definition of Done

- Three skills exist and follow contracts above
- Runtime files are generated and maintained in vault root
- Verification loops execute with attempt limits and cold queue behavior
- README and workflow docs explain full operational lifecycle
- Dry run passes end-to-end with checkpoint logs

## 11. Open Risks and Mitigations

1. Manual batch quality variability
- Mitigation: strict but tolerant parser + section-level error logging

2. Duplicate/near-duplicate records
- Mitigation: source_hash + normalized-person matching

3. Overgrowth of verification queue
- Mitigation: priority ordering, attempt caps, cold queue statuses

4. Long-run drift in goals
- Mitigation: explicit `next_action` and `phase` transitions in Runtime_State
