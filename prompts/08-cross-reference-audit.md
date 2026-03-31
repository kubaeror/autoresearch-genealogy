# Cross-Reference Audit (Polish Records)

Find and fix every date, name, and place discrepancy between your family tree and your Polish source documents.

## Autoresearch Configuration

**Goal**: For every named person in `[VAULT_PATH]/Family_Tree.md`, compare their dates, names, and places against the corresponding person files and transcription notes. For each mismatch, determine which source is correct (accounting for partition-era complications) and fix the wrong file.

**Metric**: Number of discrepancies remaining (mismatches between Family_Tree.md and person/transcription files)

**Direction**: Minimize (lower is better)

**Verify**: 
1. Count discrepancies found
2. Count resolutions by confidence (strong/moderate/speculative-unresolved)
3. Count critical discrepancies pending
4. Report: "Found X discrepancies. Resolved Y (Z strong, W moderate). V critical discrepancies pending investigation."

**Guard**:
- When sources conflict, use this hierarchy for Polish records:
  1. Original parish register images (Szukaj w Archiwach, FamilySearch, Metryki) > Geneteka/PRADZIAD indexes > secondary compilations
  2. Birth/baptism records > marriage records > death records (ages in death records are often inaccurate)
  3. Alegata (supporting documents attached to marriage records) can be more reliable than the marriage record itself for birth data
- Do not silently choose one version. Document every discrepancy in the audit file.
- Do not change primary source transcriptions to match the family tree. If they disagree, the family tree is more likely wrong.
- Do not "correct" historical spelling variants. A name spelled differently across partitions is not an error but a historical artifact.
- Do not resolve critical discrepancies (parents, major dates) without Strong Signal confidence
- If resolution confidence is Speculative, document both values rather than guessing
- Prefer "unresolved with documentation" over "resolved incorrectly"

**Iterations**: 12

**Protocol**:

1. **Build the master list**: Read `[VAULT_PATH]/Family_Tree.md` completely. For every named person, extract:
   - Full name (all variants, including partition-era spellings)
   - Przydomek (family byname) if present
   - Birth date and place (noting Julian vs Gregorian calendar)
   - Death date and place
   - Marriage date, place, and spouse
   - Parents' names
   - Parish (parafia) associations

2. **Compare against source files**: For each person, read their person file (if one exists) and any transcription notes that mention them. Compare every fact, accounting for:
   - Geneteka indexes vs original images in Szukaj w Archiwach
   - Birth records vs marriage alegata (attached birth certificates)
   - Death records vs cemetery records (cmentarze)
   - Multiple language versions of the same record

3. **When a mismatch is found**:
   a. Record it in `[VAULT_PATH]/cross_reference_audit.md` with: person name, field, value in Family_Tree.md, value in person file, authoritative source, partition context
   b. Determine which source is correct using the hierarchy above
   c. Before applying any resolution:
      - Assess resolution confidence
      - If critical discrepancy + Speculative: execute Resolution Loop
      - Document confidence level in the resolution notes
   d. Fix the incorrect file using Edit
   e. Add a `## Data Discrepancies` section to the person file if one does not exist, documenting the conflict and resolution

4. **Polish-specific discrepancy types to check**:

   **Name variations across partitions**:
   - Russian partition: Names Russified (Wojciech → Адальберт/Adalbert, Katarzyna → Екатерина)
   - Prussian partition: Names Germanized (Wojciech → Adalbert, Kowalski → Kowalsky)
   - Austrian partition: Generally retained Polish spelling, sometimes Latinized
   - Record the canonical Polish form and all variants

   **Calendar discrepancies (Russian partition)**:
   - Before 1918: Russian partition used Julian calendar (12-13 days behind Gregorian)
   - Some records show both dates, others show only Julian
   - When cross-referencing, convert all dates to Gregorian and note original

   **Age discrepancies**:
   - Death records frequently have inaccurate ages (informants often guessed)
   - Cross-reference against birth records; birth record is authoritative
   - Marriage records state ages at marriage; these are more reliable than death records but less reliable than birth records

   **Przydomek (family byname) inconsistencies**:
   - May appear in some records but not others for the same person
   - More common in szlachta (nobility) records and certain regions
   - Record when present, do not treat absence as a discrepancy

   **Place name variations**:
   - Same village may appear as: Polish name, Russian transliteration, German name
   - Parish boundaries and administrative divisions changed across partitions
   - Use the modern Polish name as canonical, record historical variants

5. **Source-specific cross-checks**:

   | Source A | Source B | Common Discrepancies |
   |----------|----------|----------------------|
   | Geneteka index | Original image (Szukaj w Archiwach) | Transcription errors, OCR mistakes, missing data |
   | Birth record | Marriage alegata | Birth alegata may include corrections not in original |
   | Death record | Cemetery record | Different dates (death vs burial), age discrepancies |
   | Polish-language record | Russian/German-language record | Name spellings, place names |
   | Church record | Civil registration | Dates may differ by days (event vs registration) |

6. **After each family line is audited**, update the count of remaining discrepancies.

7. **Final pass**: Re-read Family_Tree.md and compare against the audit file. Every discrepancy should be marked as RESOLVED in the audit file.

## Confidence Assessment

### Resolution Confidence

**Strong Signal** (resolution definitive):
- Primary source clearly correct (original document vs. index transcription error)
- Multiple independent sources agree on correct value
- Error cause identified (e.g., Julian calendar not converted)
- Resolution consistent with all other known data

**Moderate Signal** (resolution likely but not certain):
- Higher-tier source preferred per hierarchy, but single source
- Logical resolution (e.g., death age rounded vs. calculated from birth)
- No contradicting evidence, but limited corroboration

**Speculative** (resolution uncertain):
- Both sources equally reliable
- Multiple possible explanations
- Resolution would change significant conclusions
- Insufficient evidence to determine correct value

### Discrepancy Types and Confidence Requirements

| Discrepancy Type | Minimum Confidence to Resolve | If Below Threshold |
|------------------|-------------------------------|-------------------|
| Spelling variation | Moderate | Accept both as variants |
| Date ±1-2 years | Moderate | Use primary source, note discrepancy |
| Date >5 years | Strong | Loop: find additional source |
| Different location | Strong | Loop: investigate both locations |
| Different parents | Strong | Loop: critical genealogical question |
| Name completely different | Strong | Loop: may be different person |

## Feedback Loop

### For Each Discrepancy:

1. **Identify discrepancy** and categorize type

2. **Assess initial resolution confidence** using source hierarchy

3. **If Strong Signal**:
   - Apply resolution
   - Update vault with correct value
   - Document in Data Discrepancies section
   - Move to next discrepancy

4. **If Moderate Signal**:
   - Apply resolution tentatively
   - Add note: "Resolved based on [source], pending verification"
   - Add to verification queue
   - Move to next discrepancy

5. **If Speculative**:
   - DO NOT resolve yet
   - **Execute Resolution Loop**:

### Resolution Loop for Speculative Discrepancies:

**Attempt 1**: Find additional sources
- Search Geneteka for related records (siblings, marriages)
- Search Szukaj w Archiwach for original images of cited sources
- Check alegata for copies of birth certificates

**Attempt 2**: Apply contextual analysis
- Check historical context (calendar systems, naming conventions)
- Compare with known reliable data points
- Consider which source was created closer to event

**Attempt 3**: Seek corroborating evidence
- Search for census records showing age progression
- Check death records for age/birthdate
- Find records of siblings that might clarify parents

**After 3 attempts**:
- If elevated to at least Moderate: apply resolution
- If still Speculative: 
  - Log as "Unresolved Discrepancy" in Research_Log
  - Note both values in person file with explanation
  - Flag in Open_Questions.md for future research
  - Move to next discrepancy

### Critical Discrepancies (Always Loop)

These discrepancies ALWAYS require Strong Signal before resolution:
- Different parents listed
- Birth year off by >10 years  
- Different birthplace (different parish/region)
- Different spouse
- Person may be two different individuals

For critical discrepancies, do not accept Moderate Signal. Either achieve Strong Signal or leave unresolved with documentation.

## Output

The audit file (`cross_reference_audit.md`) should contain:

```
| Person | Field | Family_Tree Value | Person File Value | Correct Value | Source | Partition | Status |
|---|---|---|---|---|---|---|---|
| [ANCESTOR] | birth_date | 1866 | May 10, 1866 (Julian) | May 22, 1866 (Gregorian) | Baptism record, Szukaj w Archiwach | Russian | RESOLVED |
| [ANCESTOR] | name | Wojciech | Адальберт | Wojciech (canonical) | Birth record | Russian | RESOLVED |
| [ANCESTOR] | przydomek | (none) | Czerny | Czerny | Marriage record | Austrian | RESOLVED |
```

## Resolution Notes

When resolving discrepancies in Polish records:

1. **Original images always override indexes**: Geneteka is invaluable for finding records, but always verify against the original image in Szukaj w Archiwach or FamilySearch.

2. **Alegata are often the best source for birth data**: When a person married, they often had to provide birth documentation. These alegata may contain more complete or corrected information.

3. **Death record ages are estimates**: Unless the informant was the spouse or a close relative with direct knowledge, treat ages in death records as approximate.

4. **Name spelling is not a discrepancy**: "Kowalski" in Polish records and "Ковальский" in Russian records are the same person, not a conflict to resolve.

5. **Calendar conversion is required**: Always note whether dates are Julian or Gregorian. In the Russian partition before 1918, add 12-13 days to convert Julian to Gregorian.
