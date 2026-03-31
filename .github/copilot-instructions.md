# Polish Genealogy Research Instructions

## Repository Purpose

This repository provides tools, skills, and reference materials for Polish genealogy research. It is designed to work with the GitHub Copilot CLI for AI-assisted genealogical investigation.

## Vault Configuration

The user's Obsidian vault containing genealogical data is specified by the environment variable `GENEALOGY_VAULT`. 

Default: `~/Documents/Genealogia/`

To set a custom path:

**Linux/Mac:**
```bash
export GENEALOGY_VAULT=/path/to/your/vault
```

**Windows PowerShell:**
```powershell
# Current session only:
$env:GENEALOGY_VAULT = "C:\Path\To\Your\Vault"

# Persistent (survives restarts):
[Environment]::SetEnvironmentVariable("GENEALOGY_VAULT", "C:\Path\To\Your\Vault", "User")
```

Key vault files:
- `Family_Tree.md`: Main family tree structure
- `Research_Log.md`: Log of all searches and findings
- `templates/`: Templates for person, parish, region, transcription files

## Confidence Tiers

All findings must be assessed using three confidence tiers:

- **Strong Signal**: Add to vault immediately (confidence: high)
- **Moderate Signal**: Add with `(unverified)` tag (confidence: moderate)
- **Speculative**: Do NOT add to vault; log in Research_Log.md and execute feedback loop

## Available Skills

Use these skills for specialized tasks:

- `/autoresearch`: Orchestrator for long-run pipeline (prep -> manual batch -> intake -> verify)
- `/autoresearch-prep`: Build `Search_Queue.md` and `Runtime_State.md` from current tree baseline
- `/autoresearch-intake`: Ingest `manual_search_batch_YYYY-MM-DD.md`, route confidence, update tree and queues
- `/autoresearch-verify`: Process `Verification_Queue.md` with bounded verification loops
- `/geneteka-search`: Search Geneteka (65M+ Polish records)
- `/cyrillic-ocr`: Extract data from Russian Cyrillic documents
- `/partition-research`: Identify partition and apply partition-specific strategies
- `/kresy-search`: Research Eastern Borderlands (Ukraine/Belarus/Lithuania)
- `/confidence-assessment`: Assess findings and determine next steps

## Available Agent

- `/agent genealogy-researcher`: Full-featured Polish genealogy expert

## Polish Historical Context

### The Three Partitions (1795-1918)
- Russian Partition: mazowieckie, łódzkie, lubelskie (Russian language 1868-1918)
- Prussian Partition: wielkopolskie, pomorskie (German/Gothic script)
- Austrian Partition: małopolskie, podkarpackie (Latin/Polish)

### Calendar Conversion
- Russian partition 1868-1918 used Julian calendar
- Add 12 days (19th c.) or 13 days (20th c.) for Gregorian

### Naming Conventions
- Przydomki (hereditary nicknames): "Kowalski vulgo Prusak"
- Female suffixes: -ówna (maiden), -owa (married)
- Grammatical forms: Kowalski/Kowalskiego/Kowalskim

## Source Citation Format

- Geneteka: "Geneteka: [Parish], [Year], act [number], [event type]"
- Szukaj w Archiwach: "[Archive], zespół [X], sygn. [Y], s. [page]"
- Always note if verified against original image

## File Naming

Use underscores, not spaces: `Jan_Kowalski.md`, not `John Smith.md`

## Style Guidelines

- No hyphens as punctuation
- No emojis
- Source-first: every claim needs a citation
- Log negative results ("Searched X, found nothing")
- Polish terms with English translations: przydomek (hereditary nickname)

