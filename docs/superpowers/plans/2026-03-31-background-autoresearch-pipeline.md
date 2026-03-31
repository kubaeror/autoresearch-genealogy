# Background Autoresearch Pipeline Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Deliver a resumable three-skill workflow (`autoresearch-prep`, `autoresearch-intake`, `autoresearch-verify`) that runs in long cycles with manual batch ingestion and confidence-driven verification loops.

**Architecture:** Implement a lightweight state model in vault root using `Search_Queue.md`, `Verification_Queue.md`, and `Runtime_State.md`. Split responsibilities across three dedicated skills, keep `/autoresearch` as orchestrator wrapper, and align agent/docs with explicit `prep -> manual batch -> intake -> verify -> resume` flow.

**Tech Stack:** Markdown skills (`SKILL.md`), repository docs (`README.md`, `workflows/*.md`), Copilot custom agent markdown.

---

## File Structure and Responsibilities

- Create: `.github/skills/autoresearch-prep/SKILL.md`
  - Generates queue and runtime state from vault baseline.
- Create: `.github/skills/autoresearch-intake/SKILL.md`
  - Parses `manual_search_batch_YYYY-MM-DD.md`, applies confidence routing, updates vault, dedups by source hash.
- Create: `.github/skills/autoresearch-verify/SKILL.md`
  - Processes verification queue with attempt limits and cold queue transitions.
- Modify: `.github/skills/autoresearch/SKILL.md`
  - Wrapper/orchestrator pointing to prep/intake/verify lifecycle.
- Modify: `.github/skills/confidence-assessment/SKILL.md`
  - Queue contract alignment (`Verification_Queue.md`, `Runtime_State.md`).
- Modify: `.github/agents/genealogy-researcher.agent.md`
  - Runtime pipeline section + resume rules.
- Create: `workflows/autoresearch-background.md`
  - Operational runbook.
- Create: `workflows/verification-loop.md`
  - Verification decision process and status transitions.
- Modify: `README.md`
  - User-facing background workflow usage.
- Test artifacts: none committed; use command verification and dry-run markdown fixtures.

---

### Task 1: Define runtime contracts in docs first

**Files:**
- Create: `workflows/autoresearch-background.md`
- Create: `workflows/verification-loop.md`
- Modify: `README.md` (new background section)

- [ ] **Step 1: Write failing verification checks (docs absent)**

Run:
```bash
rg -n "autoresearch-background|verification-loop|prep -> manual batch -> intake -> verify" workflows README.md
```
Expected: no matches for new operational flow.

- [ ] **Step 2: Add `workflows/autoresearch-background.md`**

```md
# Autoresearch Background Workflow

## Runtime Files (vault root)
- `Search_Queue.md`
- `Verification_Queue.md`
- `Runtime_State.md`

## End-to-End Cycle
1. Run `/autoresearch-prep`
2. User creates `manual_search_batch_YYYY-MM-DD.md`
3. Run `/autoresearch-intake`
4. Run `/autoresearch-verify`
5. Repeat from prep or resume from runtime state

## Resume Rules
- Read `Runtime_State.md`
- Continue from `phase`
- Append checkpoint block to `Research_Log.md`
```

- [ ] **Step 3: Add `workflows/verification-loop.md`**

```md
# Verification Loop

## Signals
- Strong: update facts now
- Moderate: add `(unverified)` and queue
- Speculative: queue only, no factual insert

## Attempt Limits
- Moderate: max 2 attempts
- Speculative: max 3 attempts then `status: cold`

## Queue Statuses
`open -> escalated -> resolved`
`open -> cold` (speculative exhausted)
```

- [ ] **Step 4: Update README with background usage**

```md
### Background Pipeline (Long Runs)

1. `Use /autoresearch-prep to build Search_Queue.md`
2. Create `manual_search_batch_YYYY-MM-DD.md` from manual source checks
3. `Use /autoresearch-intake to ingest and update the vault`
4. `Use /autoresearch-verify to process verification queue`
5. Resume anytime via `Runtime_State.md`
```

- [ ] **Step 5: Run verification checks**

Run:
```bash
rg -n "Runtime_State.md|Search_Queue.md|Verification_Queue.md" workflows README.md
```
Expected: matches in both new workflow docs and README.

- [ ] **Step 6: Commit docs contract**

```bash
git add workflows/autoresearch-background.md workflows/verification-loop.md README.md
git commit -m "docs: add background autoresearch runtime contracts"
```

---

### Task 2: Create `autoresearch-prep` skill

**Files:**
- Create: `.github/skills/autoresearch-prep/SKILL.md`

- [ ] **Step 1: Write failing check for missing skill**

Run:
```bash
rg -n "name: autoresearch-prep" .github/skills
```
Expected: no matches.

- [ ] **Step 2: Create skill frontmatter and purpose**

```md
---
name: autoresearch-prep
description: Build search queue and runtime checkpoint for long-running genealogy sessions. Reads Family_Tree.md and writes Search_Queue.md + Runtime_State.md.
allowed-tools: read, edit, glob
---

# Autoresearch Prep
```

- [ ] **Step 3: Add deterministic output contract**

```md
## Output Files (vault root)
- `Search_Queue.md`
- `Runtime_State.md`

## Search Queue Columns
`target_id | person | surname_variants | region_hint | search_urls | priority | status`

## Runtime Fields
`session_id, phase, last_checkpoint, tree_total, queue_size, next_action`
```

- [ ] **Step 4: Add algorithm steps**

```md
1. Read `Family_Tree.md` and identify leaf targets.
2. Generate surname variants (diacritics, phonetics, suffixes, przydomki).
3. Build source-specific manual search URLs.
4. Write queue with `status: pending`.
5. Write runtime state with `phase: prep_done`.
6. Append checkpoint to `Research_Log.md`.
```

- [ ] **Step 5: Validate skill exists and has required sections**

Run:
```bash
rg -n "name: autoresearch-prep|Output Files|phase: prep_done" .github/skills/autoresearch-prep/SKILL.md
```
Expected: 3+ matches.

- [ ] **Step 6: Commit prep skill**

```bash
git add .github/skills/autoresearch-prep/SKILL.md
git commit -m "feat: add autoresearch-prep skill"
```

---

### Task 3: Create `autoresearch-intake` skill

**Files:**
- Create: `.github/skills/autoresearch-intake/SKILL.md`

- [ ] **Step 1: Write failing check for missing skill**

Run:
```bash
rg -n "name: autoresearch-intake" .github/skills
```
Expected: no matches.

- [ ] **Step 2: Create input contract for manual batch markdown**

```md
---
name: autoresearch-intake
description: Ingest manual_search_batch_YYYY-MM-DD.md, route by confidence, update tree/person files, and queue unresolved leads.
allowed-tools: read, edit, glob
---

## Required Input File
`manual_search_batch_YYYY-MM-DD.md`
```

- [ ] **Step 3: Add parser rules and fault tolerance**

```md
## Parser Rules
- Process section-by-section by `target_id`.
- Parse rows: parish, year, act, event, name, uwagi.
- If one section fails parsing, log warning and continue.
```

- [ ] **Step 4: Add confidence routing and dedup rules**

```md
## Routing
- Strong -> write fact + `confidence: high`
- Moderate -> write with `(unverified)` + enqueue verify
- Speculative -> no factual insert, enqueue verify

## Dedup
`source_hash = sha1(parish|year|act|event|person_normalized)`
Skip insert if hash already exists.
```

- [ ] **Step 5: Add runtime transitions**

```md
## Runtime Updates
- Missing batch file -> `phase: waiting_for_manual_batch`
- Successful run -> `phase: intake_done`
- Always update counters and `last_checkpoint`
```

- [ ] **Step 6: Validate intake skill content**

Run:
```bash
rg -n "name: autoresearch-intake|source_hash|waiting_for_manual_batch|phase: intake_done" .github/skills/autoresearch-intake/SKILL.md
```
Expected: matches for all required terms.

- [ ] **Step 7: Commit intake skill**

```bash
git add .github/skills/autoresearch-intake/SKILL.md
git commit -m "feat: add autoresearch-intake skill"
```

---

### Task 4: Create `autoresearch-verify` skill

**Files:**
- Create: `.github/skills/autoresearch-verify/SKILL.md`

- [ ] **Step 1: Write failing check for missing skill**

Run:
```bash
rg -n "name: autoresearch-verify" .github/skills
```
Expected: no matches.

- [ ] **Step 2: Add queue contract and attempt logic**

```md
---
name: autoresearch-verify
description: Process Verification_Queue.md with bounded loops for moderate and speculative findings.
allowed-tools: read, edit, glob
---

## Queue Input
`Verification_Queue.md`
```

- [ ] **Step 3: Define transition rules**

```md
## Moderate
- Max 2 attempts
- If corroborated -> `resolved`
- Else remain `open` or set `escalated`

## Speculative
- Max 3 attempts
- If unresolved after attempt 3 -> `cold`
```

- [ ] **Step 4: Add runtime/checkpoint updates**

```md
## Runtime
- On progress: `phase: verify_done`
- On missing dependency info: `phase: waiting_for_manual_batch`
- Always append checkpoint to `Research_Log.md`
```

- [ ] **Step 5: Validate verify skill content**

Run:
```bash
rg -n "name: autoresearch-verify|Max 2 attempts|Max 3 attempts|cold|phase: verify_done" .github/skills/autoresearch-verify/SKILL.md
```
Expected: required matches present.

- [ ] **Step 6: Commit verify skill**

```bash
git add .github/skills/autoresearch-verify/SKILL.md
git commit -m "feat: add autoresearch-verify skill"
```

---

### Task 5: Convert `/autoresearch` into wrapper orchestrator

**Files:**
- Modify: `.github/skills/autoresearch/SKILL.md`

- [ ] **Step 1: Write failing check for old monolithic behavior**

Run:
```bash
rg -n "Step 3: Search Databases|Execute this loop for each iteration" .github/skills/autoresearch/SKILL.md
```
Expected: existing monolithic loop text found.

- [ ] **Step 2: Replace core protocol with wrapper flow**

```md
# Autoresearch Orchestrator

Use this sequence:
1. Run `/autoresearch-prep`
2. Collect manual results in `manual_search_batch_YYYY-MM-DD.md`
3. Run `/autoresearch-intake`
4. Run `/autoresearch-verify`
5. Resume based on `Runtime_State.md`
```

- [ ] **Step 3: Add explicit non-goals**

```md
## Non-goals
- Do not claim automated scraping of JS-protected portals.
- Do not bypass manual batch ingestion.
```

- [ ] **Step 4: Validate wrapper content**

Run:
```bash
rg -n "autoresearch-prep|autoresearch-intake|autoresearch-verify|Non-goals" .github/skills/autoresearch/SKILL.md
```
Expected: references to all three child skills and non-goals.

- [ ] **Step 5: Commit wrapper refactor**

```bash
git add .github/skills/autoresearch/SKILL.md
git commit -m "refactor: make autoresearch a pipeline orchestrator"
```

---

### Task 6: Align confidence and agent contracts

**Files:**
- Modify: `.github/skills/confidence-assessment/SKILL.md`
- Modify: `.github/agents/genealogy-researcher.agent.md`

- [ ] **Step 1: Add queue contract to confidence skill**

```md
## Queue Integration
- Moderate findings must be written to `Verification_Queue.md` with `signal: moderate`.
- Speculative findings must be written to `Verification_Queue.md` with `signal: speculative`.
- Update `Runtime_State.md` counters after each assessment batch.
```

- [ ] **Step 2: Add runtime lifecycle to main agent**

```md
## Background Runtime Lifecycle
- Preferred flow: prep -> manual batch -> intake -> verify
- Resume by reading `Runtime_State.md`
- Never overwrite Strong with lower-confidence findings
```

- [ ] **Step 3: Validate both files for new contracts**

Run:
```bash
rg -n "Verification_Queue.md|Runtime_State.md|prep -> manual batch -> intake -> verify" .github/skills/confidence-assessment/SKILL.md .github/agents/genealogy-researcher.agent.md
```
Expected: matches in both files.

- [ ] **Step 4: Commit alignment changes**

```bash
git add .github/skills/confidence-assessment/SKILL.md .github/agents/genealogy-researcher.agent.md
git commit -m "docs: align confidence and agent with background runtime contracts"
```

---

### Task 7: Dry-run validation with fixture batch

**Files:**
- Create (temp during validation, then remove): `manual_search_batch_2099-01-01.md` in local test vault
- Verify docs/skills only in repo

- [ ] **Step 1: Create minimal fixture example content (outside repo or temp)**

```md
## target_id: T-001 | person: Jan Kowalski
URL: https://geneteka.genealodzy.pl/index.php?... 
- parish: Płock | year: 1880 | act: 42 | event: birth | name: Jan Kowalski | uwagi: s. Piotra i Marianny
```

- [ ] **Step 2: Validate parser contract references exist**

Run:
```bash
rg -n "manual_search_batch_YYYY-MM-DD.md|target_id|parish|year|act|event|uwagi" .github/skills/autoresearch-intake/SKILL.md
```
Expected: complete input contract present.

- [ ] **Step 3: Validate phase/resume references exist globally**

Run:
```bash
rg -n "phase: prep_done|phase: intake_done|phase: verify_done|waiting_for_manual_batch|Runtime_State.md" .github/skills workflows README.md
```
Expected: all lifecycle states covered.

- [ ] **Step 4: Validate queue status model exists**

Run:
```bash
rg -n "pending|searched|ingested|open|escalated|cold|resolved" .github/skills workflows
```
Expected: status vocabulary defined.

- [ ] **Step 5: Commit final integration updates**

```bash
git add .github/skills .github/agents README.md workflows
git commit -m "feat: implement background autoresearch prep/intake/verify pipeline docs"
```

---

### Task 8: Final verification and push

**Files:**
- Modify: none (verification only)

- [ ] **Step 1: Run repository sanity checks**

Run:
```bash
git --no-pager status
```
Expected: clean working tree (or only intentionally untracked local artifacts).

- [ ] **Step 2: Verify new skill registry coverage**

Run:
```bash
rg -n "autoresearch-prep|autoresearch-intake|autoresearch-verify" README.md .github/agents .github/skills
```
Expected: all three skills documented and referenced.

- [ ] **Step 3: Push commits**

```bash
git push
```
Expected: branch updated on remote without conflicts.

- [ ] **Step 4: Capture release summary in Research_Log-compatible format**

```md
## Background Pipeline Release
- Added: 3 skills (prep/intake/verify)
- Added: runtime docs and verification loop docs
- Updated: orchestrator, confidence contract, agent, README
- Ready for: long-cycle resumable operation
```

---

## Self-Review Checklist (Completed)

### Spec coverage
- Three-skill pipeline: covered by Tasks 2-5.
- Runtime files and checkpointing: covered by Tasks 1-4 and 7.
- Idempotency and source hash: covered by Task 3.
- Verification loop attempt caps/cold queue: covered by Task 4.
- Docs and operational flow: covered by Tasks 1 and 6.
- Dry-run + resume validation: covered by Task 7.

### Placeholder scan
- No TBD/TODO placeholders in steps.
- Every code-edit step includes concrete markdown content.
- Every verification step includes exact command and expected result.

### Type consistency
- Runtime file names consistent: `Search_Queue.md`, `Verification_Queue.md`, `Runtime_State.md`.
- Phases consistent: `prep_done`, `intake_done`, `verify_done`, `waiting_for_manual_batch`.
- Queue statuses consistent with spec and tasks.
