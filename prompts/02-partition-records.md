# Partition Records Research

Identify which partition (Russian, Prussian, or Austrian) each ancestor lived under and apply partition-specific research strategies.

## Autoresearch Configuration

**Goal**: For every ancestor in `[VAULT_PATH]/Family_Tree.md` living between 1795 and 1918, determine their partition and search partition-appropriate archives and record types.

**Metric**: Number of ancestors with partition identified and partition-specific records found

**Direction**: Maximize

**Verify**: 
1. Count ancestors with partition identified (strong/moderate confidence)
2. Count ancestors with partition-specific records found
3. Report: "X of Y partition-era ancestors identified (Z pending location clarification)"

**Guard**:
- Border areas changed hands. Verify partition using historical maps, not just modern location.
- Records may be in Russian (Cyrillic), German (Gothic script), Latin, or Polish depending on partition and time period.
- Do not assume one archive has all records. Parish records, civil records, and military records may be in different archives.

**Iterations**: 8

**Protocol**:

1. **Identify partition-era ancestors**: From Family_Tree.md, list ancestors who lived between 1795-1918. For each, note:
   - Location (as specific as possible)
   - Date range of life
   - Current partition assignment (if any)

2. **Determine partition**: For each ancestor's location:
   
   **Russian Partition** (Congress Poland):
   - Modern voivodeships: mazowieckie, łódzkie, lubelskie, świętokrzyskie, podlaskie (west), kieleckie
   - Major cities: Warszawa, Łódź, Lublin, Kielce
   
   **Prussian Partition**:
   - Modern voivodeships: wielkopolskie, pomorskie, warmińsko-mazurskie, kujawsko-pomorskie, śląskie (west), dolnośląskie
   - Major cities: Poznań, Gdańsk, Wrocław, Toruń
   
   **Austrian Partition** (Galicia):
   - Modern voivodeships: małopolskie, podkarpackie, śląskie (east)
   - Major cities: Kraków, Rzeszów, Tarnów, Przemyśl
   
   Use historical maps if uncertain (e.g., Mapster, David Rumsey Map Collection).

3. **Update person files**: Add partition field to each ancestor's file:
   ```yaml
   partition: russian | prussian | austrian
   ```

4. **Apply partition-specific search strategy**:

   **Russian Partition**:
   - Szukaj w Archiwach: search by archive (AP Lublin, AP Łódź, AP Warszawa)
   - Civil registration begins 1808 (akta stanu cywilnego)
   - After 1868: records in Russian (Cyrillic script)
   - Look for: births (urodzenia), marriages (małżeństwa), deaths (zgony)
   - Check alegata (marriage supplements) for birth certificate copies

   **Prussian Partition**:
   - Szukaj w Archiwach: AP Poznań, AP Gdańsk, AP Wrocław
   - Civil registration begins 1874 (Standesamt)
   - Records in German (Gothic Kurrent script)
   - Also search: BaSIA, Poznan Project (marriages 1800-1899)
   - FamilySearch has extensive Prussian microfilms

   **Austrian Partition**:
   - Szukaj w Archiwach: AP Kraków, AP Rzeszów, AP Przemyśl
   - Church records dominant (no mandatory civil registration until late)
   - Records primarily in Latin, some Polish
   - Gesher Galicia for Jewish records
   - Tabular format (tables, not narrative text)

5. **Handle language barriers**:
   - Russian records: use Russian genealogical vocabulary guide
   - German records: learn basic Gothic script (Kurrent)
   - Latin records: use Latin genealogical terms reference

6. **Extract data**: From found records, capture:
   - Full transcription or key details
   - Archive reference (zespół, sygnatura, page)
   - Language of record
   - Record type

7. **Log progress**: In Research_Log.md, note:
   - Partition identified for each ancestor
   - Archives searched
   - Records found (with citations)
   - Language challenges encountered

## Confidence Assessment

### Partition Identification Confidence

**Strong Signal** (proceed with partition-specific search):
- Location clearly within one partition's territory
- Historical maps confirm partition assignment
- Multiple records from same location confirm language/format

**Moderate Signal** (search both possible partitions):
- Location near partition border
- Location changed hands during partition era
- Only one record found, partition unclear

**Speculative** (requires research before proceeding):
- Location name ambiguous (multiple places with same name)
- No records found yet to confirm partition
- Family oral history contradicts geographic evidence

### Record Match Confidence

**Strong Signal**:
- Name, date, AND location all match
- Record language matches expected partition
- Parents/spouse names corroborate existing data

**Moderate Signal**:
- Two of three identifiers match (name+date, name+location, date+location)
- Record format consistent with partition but language unexpected
- Minor discrepancies explainable by historical context

**Speculative**:
- Only name matches (common surname)
- Unexpected record format or language
- Contradicts existing genealogical data

## Feedback Loop

### For Partition Identification:

1. **If Strong Signal**: Proceed with partition-specific archives
2. **If Moderate Signal**: 
   - Search BOTH possible partitions' archives
   - Compare results to determine which partition applies
   - Loop until one partition shows stronger evidence
3. **If Speculative**:
   - DO NOT assign partition yet
   - **Loop back**:
     a. Search for ANY record in Geneteka to establish location
     b. Use historical maps (Mapster, AGAD) to identify partition
     c. Search for siblings/parents who may have clearer records
     d. Check post-1918 records which list birthplace
   - Repeat until at least Moderate confidence achieved

### For Record Matching:

1. **If Strong Signal**: Add to vault with confidence: high
2. **If Moderate Signal**: 
   - Add with confidence: moderate and `(unverified)` tag
   - Queue for cross-reference with original image
3. **If Speculative**:
   - Log in Research_Log.md under "Unconfirmed Partition-Era Leads"
   - **Loop back**:
     a. Search alegata (marriage supplements) for birth certificate copies
     b. Try alternate name spellings for that partition's language
     c. Search neighboring parishes in same partition
   - Continue looping until elevated to Moderate or exhausted (max 3 attempts)

## Quick Reference: Record Languages by Partition and Era

| Partition | Era | Civil Records | Church Records |
|-----------|-----|---------------|----------------|
| Russian | 1808-1867 | Polish | Latin (headers), Polish |
| Russian | 1868-1918 | Russian | Latin (headers), Russian/Polish |
| Prussian | Pre-1874 | N/A (church only) | German/Latin |
| Prussian | 1874-1918 | German | German/Latin |
| Austrian | 1780s-1918 | German (admin) | Latin, Polish |

## Tips

- Use the prompt `03-cyrillic-extraction.md` for Russian partition records
- For Prussian records, learn to read Gothic script (many online tutorials)
- Austrian Galician records often easier because of Latin/tabular format
