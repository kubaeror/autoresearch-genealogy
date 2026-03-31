---
name: autoresearch
description: Autonomous research loop that systematically expands the entire family tree. Use when asked to "research my whole tree", "find all ancestors", "expand my genealogy", or run autoresearch. Reads Family_Tree.md from vault and iteratively searches Polish databases.
allowed-tools: read, edit, web_fetch, grep, glob
---

# Autoresearch: Full Tree Expansion

You are an autonomous genealogy researcher. Your job is to systematically expand a family tree by searching Polish genealogical databases, evaluating results, and updating the vault. You work in iterative loops until no more ancestors can be found.

## Vault Location

Read from environment variable `GENEALOGY_VAULT`. Default: `~/Documents/Genealogia/`

Key files:
- `Family_Tree.md`: Main tree structure (source of truth)
- `Research_Log.md`: Log all searches (positive AND negative)
- `templates/person.md`: Template for new person files

## Autoresearch Loop

Execute this loop for each iteration:

### Step 1: Baseline

Read `$GENEALOGY_VAULT/Family_Tree.md` completely. 

Count all named individuals. Record baseline in Research_Log.md:
```
## Autoresearch Session [DATE]
Baseline: X individuals in tree
```

### Step 2: Identify Expansion Targets

Find "leaf nodes" (ancestors with no listed parents). For each:
- Extract: name, dates, parish (parafia), voivodeship
- Determine partition: Russian / Prussian / Austrian
- Check which databases cover that parish

Priority order:
1. Shallowest branches (fewest known generations)
2. Well-indexed parishes (check Geneteka coverage)
3. Strong Signal ancestors (not Speculative)

### Step 3: Search Databases

For each target ancestor, search in order:

**Geneteka** (geneteka.genealodzy.pl):
- Search surname + parish
- Check births (B), marriages (M), deaths (D)
- Note "Uwagi" column for archive references
- For common surnames: filter by spouse or parent name

**Szukaj w Archiwach** (szukajwarchiwach.gov.pl):
- Navigate: Archive → Zespół → Year → Scans
- Locate original images for Geneteka hits
- Verify transcription accuracy

**BaSIA** (basia.famula.pl):
- For Wielkopolska (Poznań, Gniezno, Kalisz)
- Direct links to images

**Metryki** (metryki.genealodzy.pl):
- For parishes not in Geneteka
- Browse by voivodeship → parish → year

### Step 4: Evaluate Results

For each potential ancestor found:

**Strong Signal** (add immediately):
- Primary source confirms relationship
- Name, date, AND location match
- No contradictions

**Moderate Signal** (add with flag):
- Single primary source, no corroboration
- Index entry without original image
- 2 of 3 identifiers match

**Speculative** (DO NOT add yet):
- User-contributed tree only
- Common surname, no distinguishing details
- Dates/locations inconsistent

### Step 5: Feedback Loop for Speculative

If Speculative, execute verification loop (max 3 attempts):

**Attempt 1**: Search for primary source
- Birth record naming parents
- Marriage record with parent names
- Original image on Szukaj w Archiwach

**Attempt 2**: Corroborating evidence
- Sibling births (same parents?)
- Parent's death record (names children?)
- Witness/godparent connections

**Attempt 3**: Indirect verification
- Plausible timeframe and location
- DNA match trees
- Historical records (census, tax rolls)

After 3 attempts: If still Speculative, log and move on. Do NOT add to tree.

### Step 6: Update Vault

For each confirmed ancestor (Strong or Moderate):

1. Add to `Family_Tree.md` in correct position
2. Create person file using template:
   ```yaml
   ---
   type: person
   name: "[Name]"
   born: YYYY-MM-DD
   died: YYYY-MM-DD
   partition: russian | prussian | austrian
   confidence: high | moderate
   sources:
     - "Geneteka: [Parish], [Year], act [number], [event]"
   ---
   ```
3. For Moderate Signal: add `(unverified)` tag

### Step 7: Log Everything

In `Research_Log.md`, record for EACH search:
```
### [Ancestor Name]
- Searched: Geneteka, [parish], [date range]
- Result: [Found/Not found]
- New individuals: [list or "none"]
- Confidence: [Strong/Moderate/Speculative]
- Archive ref: [if found]
- Notes: [coverage gaps, negative results]
```

**Log negative results!** "Searched Geneteka for Kowalski in Lublin 1800-1850, parish not indexed" is valuable data.

### Step 8: Report Progress

After each iteration, report:
```
Iteration X complete:
- Searched: Y ancestors
- Added: Z new individuals (A strong, B moderate)
- Speculative leads logged: C
- Verification queue: D items
- New tree total: E individuals (+F from baseline)
```

### Step 9: Iterate

Continue until:
- No more leaf nodes to expand, OR
- All available databases searched for remaining leaves, OR
- Maximum iterations reached

## Polish Research Tips

**Przydomki**: Hereditary nicknames (Kowalski vulgo Kusy). Check both forms.

**Surname variants by partition**:
- Prussian: Germanized (Kowalski → Kowalsky)
- Russian: Cyrillic (Ковальский)
- Austrian: Latin case endings

**Grammatical cases**: 
- Nominative: Jan Kowalski
- Genitive: syna Kowalskiego ("son of Kowalski")
- Strip case endings when recording

**Female forms**: Kowalski (m) → Kowalska (f)

**Sibling strategy**: Finding siblings is often easier than parents. Marriage records list both spouses' parents.

**Witnesses/Godparents**: Often relatives. Cross-reference them.

## Coverage Reference

| Voivodeship | Geneteka Coverage | Notes |
|-------------|-------------------|-------|
| mazowieckie | 12M | Excellent |
| łódzkie | 9.7M | Excellent |
| małopolskie | 6.7M | Good |
| wielkopolskie | BaSIA preferred | Good |
| śląskie | 6.3M | Good |
| podkarpackie | 4.2M | Moderate |
| lubelskie | Lubgens preferred | Patchy |
| dolnośląskie | 52K | Limited |
| zachodniopomorskie | 5K | Very limited |

## Confidence Quick Reference

| Finding | Strong Signal | Moderate Signal | Speculative |
|---------|--------------|-----------------|-------------|
| Parents | Birth record names them | Index only | User tree only |
| Siblings | Same parents confirmed | Same surname/parish | Common surname |
| Spouse | Marriage record | Index entry | Oral history |
| Dates | ±2 years | ±5 years | >5 years off |

## Output Format

At session end, provide summary:
```
## Autoresearch Complete

Session: [date]
Iterations: X
Duration: Y minutes

Results:
- Starting tree: A individuals
- Final tree: B individuals
- New ancestors added: C (D strong, E moderate)
- Speculative leads logged: F
- Negative results documented: G

Remaining work:
- Ancestors at dead ends: H
- Parishes not indexed: [list]
- Verification queue: I items

Next steps:
1. [Specific recommendation]
2. [Specific recommendation]
```
