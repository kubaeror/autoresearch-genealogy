# Prompts

Autoresearch prompts for AI-assisted Polish genealogy research. Designed for Claude Code's `/autoresearch` command but adaptable to any AI tool that supports autonomous iteration.

## How to Use

1. Open Claude Code in your genealogy vault directory
2. Type `/autoresearch` and paste the contents of a prompt file
3. Replace all `[PLACEHOLDER]` values with your actual data
4. The AI will run autonomously for the specified number of iterations

## Prompt Anatomy

Every prompt contains these fields:

| Field | Purpose |
|---|---|
| **Goal** | What the prompt is trying to accomplish |
| **Metric** | A measurable quantity that tracks progress |
| **Direction** | Whether to maximize or minimize the metric |
| **Verify** | A command or check that measures current state |
| **Guard** | What the prompt should NOT do (safety rails) |
| **Iterations** | How many autonomous loops to run |
| **Protocol** | Step-by-step instructions for each iteration |

## Polish Genealogy Prompts

### Core Research Sequence

| Prompt | Purpose | Use When |
|---|---|---|
| 01-geneteka-search | Search Geneteka indexes for vital records | Starting research, finding new ancestors |
| 02-partition-records | Identify partition and apply partition-specific strategies | Researching 1795-1918 ancestors |
| 03-cyrillic-extraction | Extract data from Russian partition documents | You have Cyrillic (Russian) language scans |
| 04-kresy-search | Research Eastern Borderlands ancestors | Family came from modern Ukraine/Belarus/Lithuania |
| 05-deportation-tracking | Track WWII deportations and displacement | Ancestors were deported, displaced, or imprisoned |
| 06-cmentarze-sweep | Find burial records in Polish cemeteries | Looking for cemetery/burial information |
| 07-tree-expansion | Expand tree using Polish sources | After initial Geneteka search, to find more ancestors |
| 08-cross-reference-audit | Find and fix discrepancies | After gathering records, to verify accuracy |

### Universal Prompts

| Prompt | Purpose |
|---|---|
| 09-gedcom-completeness | Verify GEDCOM matches vault data |
| 10-source-citation-audit | Ensure all claims are sourced |
| 11-unresolved-persons | Identify unnamed people in documents |
| 12-timeline-gap-analysis | Find gaps where records should exist |
| 13-open-question-resolution | Attack research questions systematically |
| 14-immigration-search | Find emigration/immigration records |
| 15-dna-chromosome-analysis | Analyze DNA ancestry data |

## Recommended Workflow

1. **Start with Geneteka**: Run `01-geneteka-search` to find indexed records
2. **Identify partitions**: Run `02-partition-records` for 1795-1918 ancestors  
3. **Handle languages**: Run `03-cyrillic-extraction` for Russian partition documents
4. **Check Kresy**: Run `04-kresy-search` if family came from Eastern Borderlands
5. **Find burials**: Run `06-cmentarze-sweep` for cemetery records
6. **Expand tree**: Run `07-tree-expansion` to push branches further
7. **Verify data**: Run `08-cross-reference-audit` to fix discrepancies

## Placeholders

All prompts use these placeholders. Replace them with your actual data:

- `[SURNAME]` — A family surname (e.g., "Kowalski")
- `[ANCESTOR]` — A specific ancestor's name (e.g., "Jan Kowalski")
- `[PARISH]` — A parish name (e.g., "Łódź, św. Krzyża")
- `[VOIVODESHIP]` — A voivodeship (e.g., "łódzkie", "mazowieckie")
- `[DATE]` — A date or date range (e.g., "1866" or "1880-1920")
- `[VAULT_PATH]` — The path to your vault (e.g., `~/Vaults/MyVault/Genealogy/`)
