# CLAUDE.md

Project instructions for autoresearch-genealogy-poland.

## Project Focus

This repository is specifically designed for Polish genealogy research, covering:
- Modern Poland territory
- Former Polish territories (Kresy: now Ukraine, Belarus, Lithuania)
- Three partition-era record systems (Russian, Prussian, Austrian)
- Polish Jewish communities

## Project Structure

- `prompts/` — Autoresearch prompts for Claude Code. Polish-specific prompts for Geneteka, partition records, Cyrillic extraction, Kresy research, deportation tracking.
- `vault-template/` — Obsidian vault starter kit with Polish-specific fields (partition, przydomek, herb).
- `archives/` — Guides to Polish archives: Geneteka, Szukaj w Archiwach, partition-specific resources, Kresy archives.
- `reference/` — Methodology guides including Polish naming conventions and multilingual glossary.
- `workflows/` — Step-by-step procedures for Geneteka, Szukaj w Archiwach, OCR of Cyrillic/Gothic scripts.

## Prompt Format

Every prompt in `prompts/` follows this structure:

- **Goal**: What the prompt is trying to accomplish
- **Metric**: A measurable quantity that indicates progress
- **Direction**: Whether to maximize or minimize the metric
- **Verify**: A command or check that measures current state
- **Guard**: Safety rails (what the prompt should NOT do)
- **Iterations**: How many autonomous loops to run
- **Protocol**: Step-by-step instructions for each iteration

Prompts use placeholder names: `[SURNAME]`, `[ANCESTOR]`, `[PARISH]`, `[VOIVODESHIP]`, `[DATE]`, `[VAULT_PATH]`.

## Vault Template Conventions

- All vault files use YAML frontmatter with at minimum: `type`, `created`, `tags`
- Person files add: `name`, `born`, `died`, `family`, `przydomek`, `partition`, `herb`, `confidence`, `sources`
- Parish files add: `denomination`, `voivodeship`, `partition`, `name_german`, `name_russian`
- Transcription files add: `source`, `document_type`, `person`, `date`, `ocr_method`, `ocr_quality`, `language`, `calendar`
- Region files add: `type_region`, `partition`, `modern_voivodeship`
- Wikilinks (`[[File_Name]]`) connect files within the vault
- File names use underscores, not spaces: `Jan_Kowalski.md`, not `Jan Kowalski.md`

## Polish-Specific Conventions

### Naming
- Record przydomki (hereditary nicknames) when present: "Kowalski vulgo Prusak"
- Note partition-era name variations: Polish, Russified, Germanized, Latinized
- For women, note maiden name suffix changes (-ówna, -owa)

### Dates
- Russian partition records (1868-1918) use Julian calendar
- Always note calendar system and provide Gregorian conversion
- Add 12 days (19th century) or 13 days (20th century) for conversion

### Partitions
- Always identify which partition a location was in (1795-1918)
- Russian partition: mazowieckie, łódzkie, lubelskie, świętokrzyskie, podlaskie
- Prussian partition: wielkopolskie, pomorskie, warmińsko-mazurskie, śląskie (west)
- Austrian partition: małopolskie, podkarpackie, śląskie (east)

### Languages in Records
- Polish: throughout
- Latin: church records (all partitions)
- Russian (Cyrillic): civil records in Russian partition 1868-1918
- German (Gothic/Kurrent): Prussian partition records

### Sources
- Geneteka citations: "Geneteka: [Parish], [Year], act [number], [event type]"
- Szukaj w Archiwach: "[Archive], zespół [X], sygn. [Y], s. [page]"
- Always note if verified against original image

## Style

- No hyphens as punctuation. Use commas, periods, colons, semicolons, or parentheses.
- No emojis.
- Source-first: every claim should cite its source. Unsourced claims should be flagged.
- Log negative results. "Searched Geneteka for [parish], found nothing" is valuable data.
- Use confidence tiers (Strong Signal / Moderate Signal / Speculative) for all claims.
- Include Polish terms with English translations: przydomek (hereditary nickname)

## When Contributing

- All examples must use placeholder names. Zero real family names.
- Every prompt must include all 7 fields (Goal, Metric, Direction, Verify, Guard, Iterations, Protocol).
- Vault templates must have valid YAML frontmatter.
- Test that prompts work end-to-end before submitting.
- Include Polish terminology with English translations for international accessibility.
