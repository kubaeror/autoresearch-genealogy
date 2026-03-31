# Cyrillic Document Extraction

Extract genealogical data from Russian-language civil records (akta stanu cywilnego) from the Russian Partition (1868-1918).

## Autoresearch Configuration

**Goal**: For each scanned Russian-language document in your collection, extract all genealogical data (names, dates, places, relationships, witnesses) and create structured transcription notes.

**Metric**: Number of Russian-language documents fully transcribed and linked to person files

**Direction**: Maximize

**Verify**: 
1. Count documents transcribed by confidence tier
2. Count fields marked as uncertain [?]
3. Report: "X documents transcribed (Y strong, Z moderate, W speculative pending re-extraction)"

**Guard**:
- Russian records use Julian calendar (12-13 days behind Gregorian). Always note both dates or specify which calendar.
- Names were Russified in records but the person used Polish names in daily life. Map Russified names to Polish equivalents.
- Witnesses and parents' information is valuable. Do not skip these fields.
- If OCR/transcription is uncertain, mark with [?] rather than guessing.

**Iterations**: 6

**Protocol**:

1. **Inventory Russian documents**: From Data_Inventory.md, list all documents identified as Russian-language or from Russian Partition (1868-1918) that lack transcription notes.

2. **Document structure**: Russian partition civil records follow a standard format:
   
   **Birth Record (Акт о рождении)**:
   - Act number and date
   - Location (parish/registry office)
   - Father's full name, age, occupation, residence
   - Mother's full name and maiden name
   - Child's name and birth date
   - Godparents (восприемники)
   - Witnesses
   
   **Marriage Record (Акт о браке)**:
   - Act number and date
   - Groom: name, age, occupation, residence, parents' names
   - Bride: name, age, residence, parents' names
   - Witnesses (свидетели)
   - Sometimes: previous marriages, consent statements
   
   **Death Record (Акт о смерти)**:
   - Act number and date
   - Deceased: name, age, occupation, residence
   - Cause of death
   - Informants/witnesses
   - Burial information

3. **Transcription process**:
   a. Use Claude's multimodal capabilities to read the document image
   b. Transcribe the Cyrillic text as-is first
   c. Then translate/transliterate key genealogical fields
   d. Map Russified names to Polish equivalents
   e. Assess transcription confidence for each field
   f. If overall confidence is Speculative, execute Feedback Loop before proceeding
   g. If any critical field (name, date) is Speculative, attempt re-extraction

4. **Name mapping reference**:
   | Russian | Polish | Notes |
   |---------|--------|-------|
   | Иван | Jan | |
   | Пётр | Piotr | |
   | Антон | Antoni | |
   | Станислав | Stanisław | |
   | Мария | Maria | |
   | Катерина | Katarzyna | |
   | Ковальский | Kowalski | surname |
   | Новак | Nowak | surname |

5. **Create transcription note**: Use template at `[VAULT_PATH]/templates/transcription.md`:
   ```yaml
   ---
   type: transcription
   source: "[Archive], zespół [X], sygn. [Y], p. [Z]"
   document_type: birth | marriage | death
   person: "[[Person_Name]]"
   date: YYYY-MM-DD
   ocr_method: claude-multimodal
   ocr_quality: high | medium | low
   language: russian
   calendar: julian
   created: YYYY-MM-DD
   tags: [transcription, russian-partition]
   ---
   ```

6. **Handle calendar conversion**:
   - Julian to Gregorian (19th century): add 12 days
   - Julian to Gregorian (20th century): add 13 days
   - Always record original Julian date AND converted Gregorian date

7. **Link to person files**: Update the relevant person file with:
   - New source citation
   - Any new information (exact dates, parents' names, occupations)
   - Link to transcription note

8. **Common Cyrillic genealogical terms**:
   | Russian | Transliteration | Polish | English |
   |---------|-----------------|--------|---------|
   | рождение | rozhdenie | urodzenie | birth |
   | брак | brak | małżeństwo | marriage |
   | смерть | smert' | śmierć/zgon | death |
   | сын | syn | syn | son |
   | дочь | doch' | córka | daughter |
   | отец | otets | ojciec | father |
   | мать | mat' | matka | mother |
   | жена | zhena | żona | wife |
   | муж | muzh | mąż | husband |
   | вдова | vdova | wdowa | widow |
   | крестьянин | krest'yanin | chłop | peasant |
   | мещанин | meshchanin | mieszczanin | townsman |

9. **Log progress**: Record in Research_Log.md:
   - Document transcribed
   - Key data extracted
   - Uncertainties or illegible sections
   - Calendar conversion applied

## Confidence Assessment

### Transcription Quality Tiers

**Strong Signal** (transcription reliable):
- All text clearly legible
- Standard printed or neat handwriting
- No damaged/faded areas
- All names and dates unambiguous
- Familiar document format recognized

**Moderate Signal** (transcription needs verification):
- Most text legible but some words unclear
- Handwriting readable but some letters ambiguous
- Minor damage or fading in non-critical areas
- Names clear but some details uncertain
- Mark uncertain characters with [?]

**Speculative** (transcription unreliable):
- Significant portions illegible
- Heavy damage, fading, or bleed-through
- Unusual handwriting style
- Critical fields (names, dates) unclear
- Multiple possible readings for key data

### Per-Field Confidence

For each extracted field, note confidence:
- **Name**: [strong/moderate/speculative] - reason
- **Date**: [strong/moderate/speculative] - reason  
- **Place**: [strong/moderate/speculative] - reason
- **Parents**: [strong/moderate/speculative] - reason
- **Witnesses**: [strong/moderate/speculative] - reason

## Feedback Loop

### For Speculative Transcriptions:

1. **Attempt re-extraction**:
   - Adjust image (brightness, contrast, rotation)
   - Focus on specific unclear sections
   - Try different prompting: "This appears to be a [birth/marriage/death] record from [year]. The unclear word in the father's name field appears to be..."

2. **Cross-reference strategy**:
   - If name unclear: search Geneteka for possible spellings, compare
   - If date unclear: check surrounding records for date sequence
   - If place unclear: compare with other records from same parish

3. **Loop iterations**:
   - First attempt: standard extraction
   - If Speculative → Second attempt: enhanced image + focused prompts
   - If still Speculative → Third attempt: cross-reference with known data
   - If still Speculative after 3 attempts: mark as "requires expert review" and move on

### For Moderate Transcriptions:

1. **Flag uncertain fields** in the transcription note:
   ```
   Father: Antoni [?Kowalski/Kowaliski?] - handwriting unclear
   ```

2. **Queue for verification**: Add to Research_Log under "Transcriptions Needing Verification"

3. **Verification loop**: During future sessions, attempt to verify:
   - Find related record (sibling's birth, parent's death) to confirm spelling
   - If confirmed, update to Strong Signal
   - If contradicted, investigate discrepancy

## Quality Metrics

Track in Research_Log.md:
- Documents transcribed: X
- Strong Signal: Y (Z%)
- Moderate Signal: W (V%)  
- Speculative (pending): U (T%)
- Failed/illegible: S

## Tips

- Pre-1868 records are usually in Polish with Latin headings, not Russian
- Russian records are often in cursive script which is harder to read than printed text
- The document structure is consistent, so once you learn the format, subsequent documents are easier
- Witnesses often include family members. Always record their names.
