# autoresearch-genealogy-poland

Structured prompts, vault templates, and research workflows for AI-assisted Polish genealogy research. **Built for GitHub Copilot CLI**, also compatible with Claude Code and other AI tools.

This project provides tools and methodologies specifically designed for researching Polish family history, handling the unique challenges of partition-era records, multiple languages (Polish, Latin, Russian, German), and the complex archival landscape of Poland.

## Who This Is For

- **Genealogy researchers with Polish ancestry** who want to use AI to accelerate their family history work without sacrificing source rigor
- **Researchers of former Polish-Lithuanian Commonwealth territories** including modern Ukraine, Belarus, and Lithuania
- **AI/tech enthusiasts** who want a concrete example of autonomous research loops applied to Polish archives
- **Anyone with ancestors from Poland or Kresy** (Eastern Borderlands) who has documents in multiple scripts and languages

## Quick Start with Copilot CLI

### 1. Install and Configure

```bash
# Clone the repo
git clone https://github.com/kubaeror/autoresearch-genealogy.git
cd autoresearch-genealogy

# Set your vault path (where your Obsidian genealogy notes are)
# Linux/Mac:
export GENEALOGY_VAULT=~/Documents/Genealogia

# Windows PowerShell:
$env:GENEALOGY_VAULT = "$HOME\Documents\Genealogia"

# Windows PowerShell (persistent - add to profile):
[Environment]::SetEnvironmentVariable("GENEALOGY_VAULT", "$HOME\Documents\Genealogia", "User")

# Start Copilot CLI
copilot
```

### 2. Use the Genealogy Agent

```
> /agent genealogy-researcher
> Find all birth records for the Kowalski family in Lublin parish, 1850-1900
```

### 3. Run Autoresearch (Expand Whole Tree)

```
> Use /autoresearch to expand my entire family tree
```

This runs the orchestrator. For long sessions, use the background pipeline below: prep, manual batch, intake, verify, then resume from runtime state.

### 3a. Background Pipeline (Long Runs)

For long sessions with resumable checkpoints:

```
> Use /autoresearch-prep to build Search_Queue.md and Runtime_State.md
# run manual searches and save as manual_search_batch_YYYY-MM-DD.md in vault root
> Use /autoresearch-intake to ingest batch and update tree/queues
> Use /autoresearch-verify to process verification queue
```

Resume at any time by reading `Runtime_State.md` and executing `next_action`.

Runtime files are stored in the vault root:
- `Search_Queue.md`
- `Verification_Queue.md`
- `Runtime_State.md`
### 4. Or Use Individual Skills

```
> Use /geneteka-search to find Jan Kowalski born around 1850 in mazowieckie
> Use /cyrillic-ocr to extract data from this Russian partition birth record
> Use /partition-research to identify which partition my ancestor lived in
> Use /kresy-search to find records from Lwów area
> Use /confidence-assessment to evaluate this finding
```

### 5. Traditional Workflow (Claude Code)

You can also use the prompts directly:
1. Copy `vault-template/` into your Obsidian vault
2. Fill in `Family_Tree.md` with what you know
3. Run prompts from `prompts/` folder

See `workflows/getting-started.md` for the full walkthrough.

## What's Included

### Copilot CLI Integration (`.github/`)

**Agent** (`agents/`):
- `genealogy-researcher.agent.md`: Full-featured Polish genealogy expert agent

**Skills** (`skills/`):
| Skill | Purpose |
|-------|---------|
| autoresearch | Orchestrator: prep -> manual batch -> intake -> verify |
| autoresearch-prep | Build Search_Queue.md and Runtime_State.md |
| autoresearch-intake | Ingest manual search batches and route by confidence |
| autoresearch-verify | Process Verification_Queue.md with bounded retry loops |
| geneteka-search | Search Geneteka (65M+ Polish records) |
| cyrillic-ocr | Extract data from Russian Cyrillic documents |
| partition-research | Identify partition and apply partition-specific strategies |
| kresy-search | Research Eastern Borderlands archives |
| confidence-assessment | Assess findings with feedback loops |

**Instructions** (`copilot-instructions.md`): Repository-wide custom instructions

### Prompts (`prompts/`)

Autoresearch prompts designed for Claude Code. Each defines a Goal, Metric, Direction, Verify condition, Guard rails, Iterations, and Protocol. They run autonomously: searching Polish databases, updating your vault, and verifying their own work.

**Polish-Specific Prompts**:

| Prompt | Purpose |
|---|---|
| 01-geneteka-search | Search Geneteka indexes for vital records across Poland |
| 02-partition-records | Apply partition-specific research strategies (Russian, Prussian, Austrian) |
| 03-cyrillic-extraction | Extract data from Russian partition documents in Cyrillic script |
| 04-kresy-search | Research Eastern Borderlands ancestors in Ukrainian, Belarusian, Lithuanian archives |
| 05-deportation-tracking | Track WWII deportations, Siberian exile, and displacement records |
| 06-cmentarze-sweep | Search Polish cemetery databases and photograph collections |
| 07-tree-expansion | Expand family tree using Polish sources and naming patterns |
| 08-cross-reference-audit | Verify and fix discrepancies between Polish source documents |

**Universal Prompts** (also included):

| Prompt | Purpose |
|---|---|
| gedcom-completeness | Ensure your GEDCOM file matches your vault data |
| source-citation-audit | Verify every person file cites at least two independent sources |
| dna-chromosome-analysis | Analyze per-chromosome ancestry data to map genetic segments |
| immigration-search | Locate passenger manifests and naturalization records |

### Archive Guides (`archives/`)

Comprehensive guides to Polish genealogical sources and related archives.

| Guide | Coverage |
|---|---|
| poland.md | Comprehensive guide to Polish sources (Geneteka, Szukaj w Archiwach, Metryki, BaSIA, etc.) |
| polish-partitions.md | Russian, Prussian, and Austrian partition records: languages, formats, locations |
| kresy-borderlands.md | Ukrainian, Belarusian, Lithuanian archives for former Polish territories |
| jewish-genealogy.md | Polish Jewish records, kehilla registers, and Holocaust research |

### Vault Template (`vault-template/`)

A complete Obsidian vault starter kit with YAML frontmatter, designed for Polish genealogy.

- **Core files**: Family tree, research log, open questions, data inventory, timeline
- **Templates**: Person template (with partition, przydomek, herb fields), parish template (tracking record availability by year), region template (Polish administrative divisions: województwo, powiat, gmina)
- **Transcription templates**: For Latin, Cyrillic, and German Gothic scripts

### Reference Guides (`reference/`)

Methodology documents tailored to Polish research.

| Guide | Contents |
|---|---|
| naming-conventions.md | Polish naming: przydomki (hereditary nicknames), suffixes (-ówna, -owa), partition-era name changes, Latinization patterns |
| glossary.md | Polish, Latin, Russian, and German genealogical terms with translations |
| source-hierarchy.md | Polish document reliability ranking: parish registers > civil registration > tax rolls > censuses |

### Workflows (`workflows/`)

Step-by-step guides for Polish research tasks.

| Workflow | Purpose |
|---|---|
| geneteka-search.md | Step-by-step Geneteka usage: search strategies, interpreting results, finding original scans |
| szukaj-w-archiwach.md | Navigating the state archives portal (szukajwarchiwach.gov.pl) |
| ocr-pipeline.md | Handling Cyrillic, German Gothic (Kurrent), and Latin scripts with AI OCR |
| partition-identification.md | Determining which partition your ancestors lived in and what records to expect |

### Examples (`examples/`)

Anonymized worked examples showing autoresearch applied to Polish genealogy: Geneteka search sessions, Cyrillic transcription, partition-crossing families, Kresy research.

## Key Polish Sources

| Source | Records | URL |
|--------|---------|-----|
| Geneteka | 65M+ indexed vital records | geneteka.genealodzy.pl |
| Szukaj w Archiwach | Scanned original images from state archives | szukajwarchiwach.gov.pl |
| Metryki | 12.7M scanned parish register pages | metryki.genealodzy.pl |
| BaSIA | 6.6M Wielkopolska records (Prussian partition) | basia.famula.pl |
| Lubgens | Lublin region indexes and scans | lubgens.eu |
| Poznan Project | Wielkopolska marriage indexes 1800-1899 | poznan-project.psnc.pl |

## Polish Genealogy Challenges

This project addresses several challenges unique to Polish research:

**Three Partitions, Three Languages**: From 1795 to 1918, Poland was divided between Russia, Prussia, and Austria. Records from the Russian partition are in Russian (Cyrillic) or Polish. Prussian records are in German (often Gothic script) or Latin. Austrian records are in Latin, German, or Polish. A single family might have documents in all four languages.

**Przydomki (Hereditary Nicknames)**: Many Polish families used hereditary nicknames that functioned like secondary surnames. Jan Kowalski przydomkiem Kusy might be recorded as Jan Kusy, Jan Kowalski Kusy, or Jan Kowalski depending on the parish clerk.

**Border Changes and Kresy**: Poland's borders shifted dramatically in the 20th century. Ancestors from Lwów, Wilno, or Grodno lived in places that are now in Ukraine, Lithuania, or Belarus. Their records may be split between multiple national archives.

**WWII Destruction and Displacement**: Many parish registers were destroyed during WWII. Millions of Poles were deported to Siberia, resettled from Kresy to western Poland, or emigrated. Tracking these movements requires multiple archive systems.

## Philosophy

**Structured autonomous research with mechanical verification, not AI guessing.**

Polish genealogy is different from most AI tasks. There is no compiler. Sources disagree with each other. Confidence is probabilistic, not binary. A name that appears as "Wojciech" in one record and "Adalbert" in another might both be correct (Polish vs Latin forms). A village listed as "Kowalówka" in 1880 and "Ковалівка" in 1910 is the same place in different scripts.

The autoresearch approach adapts to this by:

- **Defining measurable metrics** (count of sourced claims, count of resolved questions, count of remaining discrepancies)
- **Requiring verification after every iteration** (cross-reference against Geneteka, original scans, and secondary sources)
- **Logging negative results** (what you searched for in Szukaj w Archiwach and did not find is as important as what you found)
- **Maintaining confidence tiers** (Strong Signal / Moderate Signal / Speculative) rather than treating all claims as equal

This is inspired by Andrej Karpathy's autoresearch concept: autonomous goal-directed loops where the AI modifies, verifies, keeps or discards, and repeats. Applied to Polish genealogy, the "compiler" is replaced by cross-referencing Geneteka indexes against original parish register scans.

## License

MIT. See `LICENSE`.

## Contributing

Contributions welcome. If you have prompts, workflows, or archive guides that worked for your Polish research, open a PR.

Requirements:
- All examples must use placeholder names: `[SURNAME]`, `[ANCESTOR]`, `[LOCATION]`. No real family data.
- Every prompt must include all 7 fields (Goal, Metric, Direction, Verify, Guard, Iterations, Protocol)
- Vault templates must have valid YAML frontmatter
- Test that prompts work end-to-end before submitting


