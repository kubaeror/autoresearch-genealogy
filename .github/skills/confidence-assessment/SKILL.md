---
name: confidence-assessment
description: Assess confidence level of genealogical findings (Strong/Moderate/Speculative) and determine appropriate next steps. Use after finding records to decide whether to add to vault, flag for verification, or execute feedback loop.
allowed-tools: read, edit
---

# Confidence Assessment Protocol

After finding any genealogical record, apply this systematic assessment to determine confidence level and appropriate action. Every finding must be categorized before any vault modification occurs.

## 1. Three Confidence Tiers

### STRONG SIGNAL (Add Immediately)

A finding qualifies as Strong Signal when ALL of the following criteria are met:

- **Name Match**: Name matches exactly, allowing for grammatical case endings common in Polish records (-ski/-skiego/-skiemu, -ska/-skiej, -wicz/-wicza/-wiczem)
- **Date Alignment**: Date falls within ±2 years of the expected date based on existing knowledge
- **Location Confirmation**: Location matches a known family location (parish, village, or gmina already documented)
- **Corroboration**: At least one corroborating detail exists (parent name, spouse name, witness who appears in other family records, occupation matching known family trade)

**Action for Strong Signal:**
- Add immediately to the relevant person file in the vault
- Set `confidence: high` in the frontmatter
- Link to source document with full citation
- No additional verification required before adding

### MODERATE SIGNAL (Add with Flag)

A finding qualifies as Moderate Signal when:

- **Name Match**: Name matches with minor spelling variation (Kowalski/Kowalsky, Wiśniewski/Wisniewski, sz/sch substitution)
- **Date Alignment**: Date falls within ±5 years of expected
- **Location**: Location is in the same powiat (district) or region, even if not the exact parish
- **No Contradictions**: While no corroborating details exist, nothing contradicts existing information

**Action for Moderate Signal:**
- Add to the person file with `(unverified)` tag appended to the claim
- Set `confidence: moderate` in the frontmatter
- Document the specific uncertainty in the file (e.g., "Birth year based on age at marriage, exact date unconfirmed")
- Queue for verification sub-loop (see Section 3)

### SPECULATIVE (Do Not Add Yet)

A finding is Speculative when ANY of the following apply:

- **Common Surname Problem**: A common surname (Kowalski, Nowak, Wiśniewski) with no distinguishing details
- **Date Discrepancy**: Date is off by more than 5 years from expected
- **Location Mismatch**: Different location with no known family connection to that area
- **Contradiction**: Information contradicts existing documented facts (wrong parent name, impossible date overlap)
- **Insufficient Context**: Record exists but provides no way to confirm identity

**Action for Speculative:**
- DO NOT add to any person file in the vault
- Log the finding in Research_Log.md under "Unconfirmed Leads" section
- Execute feedback loop (see Section 2)
- Maximum 3 feedback loop attempts before moving on

## 2. Feedback Loop for Speculative Findings

When a finding is assessed as Speculative, execute the following attempts before abandoning or escalating:

### Attempt 1: Alternative Search Strategies

Try each of these approaches to find corroborating evidence:

- Search using the przydomek (hereditary nickname) if known for the family
- Search the spouse's maiden surname in the same parish records
- Search neighboring parishes within approximately 20km radius
- Widen the date range by 10 years in each direction
- Try phonetic spelling variants (W/V substitution, omitted diacritics, German transliteration)
- Search for the surname in civil registration if searching parish records, or vice versa

### Attempt 2: Cross-Reference Related Records

- Locate a related record for a known family member (sibling birth, parent death)
- Check alegata (marriage supplements) which often contain birth certificates or parental consent documents
- Search for godparent/witness patterns across multiple records
- Look for land records (hipoteka) or census data (spisy ludności) that might confirm residence

### Attempt 3: Original Image Verification

- Access the original scan on Szukaj w Archiwach (szukajwarchiwach.gov.pl)
- Check Metryki.genealodzy.pl or Geneteka for indexed entries with links to images
- Verify transcription accuracy against original handwriting
- Check for marginal annotations (especially marriage annotations on birth records)
- Look for record numbers that might link to other documents

**After 3 Attempts:**
If the finding remains Speculative after exhausting all three attempt categories:
- Log as "requires further evidence" in Research_Log.md
- Note which verification strategies were attempted
- Move on to other research tasks
- Do not revisit unless new information becomes available

## 3. Verification Sub-Loop for Moderate Findings

Moderate findings should be actively verified, but with limited effort:

- Spend a maximum of 2 search attempts to elevate from Moderate to Strong
- Look for a corroborating record (e.g., if you have a marriage record, search for the birth record of the same person)
- Check if witnesses or godparents appear in other confirmed family records
- Verify location details against historical gazetters (Słownik geograficzny Królestwa Polskiego)

**If Successful (Elevated to Strong):**
- Update the person file to remove `(unverified)` tag
- Change `confidence: moderate` to `confidence: high`
- Document the corroborating evidence found

**If Unsuccessful After 2 Attempts:**
- Keep the finding at `confidence: moderate`
- Document verification attempts in the file
- Move on; do not continue indefinitely

## 4. Documentation Requirements

All assessments must be documented regardless of outcome:

### In Research_Log.md:
- Record the finding with date of discovery
- State the assessed confidence level
- Explain the reasoning (which criteria were met or not met)
- For Speculative findings, log under "Unconfirmed Leads" heading
- For feedback loop attempts, note what was tried and results

### In Person Files:
- Set the `confidence` field in frontmatter (high, moderate, or leave absent for speculative)
- Use inline `(unverified)` markers for moderate confidence claims
- Never add speculative claims to person files

### For Speculative Findings:
- Create entry only in Research_Log.md
- Include enough detail to revisit if new evidence emerges
- Tag with relevant surnames and locations for future searchability

## 5. Updating the Vault

Summary of vault modification rules:

| Confidence | Add to Person File? | Frontmatter | Inline Marker | Research_Log Entry |
|------------|---------------------|-------------|---------------|-------------------|
| Strong | Yes, immediately | `confidence: high` | None needed | Optional |
| Moderate | Yes, with flag | `confidence: moderate` | `(unverified)` | Recommended |
| Speculative | NO | N/A | N/A | Required |

Always preserve existing information when updating. Never overwrite higher-confidence data with lower-confidence data. If a new finding contradicts existing Strong Signal data, flag the discrepancy in Research_Log.md for manual review rather than modifying the person file.
