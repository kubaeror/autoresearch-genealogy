---
name: geneteka-search
description: Guide users through searching Geneteka (geneteka.genealodzy.pl) for Polish vital records. Provides step-by-step instructions, URL construction, surname variant strategies, and result interpretation. Use when asked to find birth, marriage, or death records from Poland.
allowed-tools: read, edit
---

# Geneteka Search Skill

## Purpose

This skill **guides the user** through manual searching of Geneteka, the largest Polish genealogy database. It does NOT perform automated searches (Geneteka uses JavaScript that cannot be scraped). Instead, it provides detailed step-by-step instructions.

## What is Geneteka

Geneteka (geneteka.genealodzy.pl) is a free online index of over 65 million Polish vital records (births, marriages, deaths) maintained by the Polish Genealogical Society. It indexes records from over 6,000 parishes across Poland, Ukraine, Belarus, and Lithuania.

**Important**: Geneteka is an INDEX, not original images. It provides metadata (names, dates, parish, act numbers) that you use to find original documents in other archives.

## How to Guide Users

When a user asks to search Geneteka, provide these instructions:

### Step 1: Construct the Search URL

Build a URL with these parameters:

**Base**: `https://geneteka.genealodzy.pl/index.php?`

**Required parameters**:
- `op=gt` (search operation - always use this)
- `lang=pol` (interface language: pol/eng/ger)
- `bdm=[B/M/D/BMD]` (event type: B=births, M=marriages, D=deaths, or BMD=all)
- `w=[CODE]` (voivodeship code - see below)

**Optional parameters**:
- `search_lastname=[SURNAME]` (primary surname - accepts UTF-8 Polish characters)
- `search_name=[GIVEN_NAME]` (first name)
- `search_lastname2=[SURNAME2]` (spouse surname for marriages)
- `from_date=[YEAR]` (start year)
- `to_date=[YEAR]` (end year)
- `rid=[PARISH_ID]` (specific parish - leave empty for all parishes)

**Example URL**:
```
https://geneteka.genealodzy.pl/index.php?op=gt&lang=pol&bdm=B&w=07mz&search_lastname=Kowalski&from_date=1850&to_date=1900
```
This searches for births (B) of people surnamed Kowalski in mazowieckie (07mz) between 1850-1900.

### Step 2: Select Voivodeship

Each search targets ONE voivodeship (województwo). Coverage varies:

| Code | Voivodeship | Records | Coverage |
|------|-------------|---------|----------|
| 07mz | mazowieckie | 12.0M | Excellent |
| 71wa | Warszawa | 2.6M | Excellent |
| 05ld | łódzkie | 9.7M | Excellent |
| 06mp | małopolskie | 6.7M | Good |
| 15wp | wielkopolskie | 2.7M | Good |
| 03lb | lubelskie | 1.2M | Moderate |
| 12sl | śląskie | 6.3M | Good |
| 02kp | kujawsko-pomorskie | 3.6M | Good |
| 10pl | podlaskie | 3.6M | Good |
| 13sk | świętokrzyskie | 4.9M | Good |
| 09pk | podkarpackie | 4.2M | Moderate |
| 14wm | warmińsko-mazurskie | 0.7M | Limited |
| 11pm | pomorskie | 1.2M | Limited |
| 01ds | dolnośląskie | 52K | Very limited |
| 04ls | lubuskie | 10K | Very limited |
| 16zp | zachodniopomorskie | 5K | Very limited |
| 21uk | Ukraina (Kresy) | 2.9M | Good |
| 22br | Białoruś (Kresy) | 1.4M | Moderate |
| 23lt | Litwa (Kresy) | 1.3M | Moderate |

**Note**: Western voivodeships have poor coverage due to WWII destruction and German-language records.

### Step 3: Generate Surname Variants

**CRITICAL**: Polish surnames were spelled inconsistently. You MUST search multiple variants.

For any surname with Polish characters, generate these variants:

#### A. Remove diacritics
| Polish | ASCII | Example Original | Example ASCII |
|--------|-------|------------------|---------------|
| ą | a | Świątek | Swiatek |
| ć | c | Adamowić | Adamowic |
| ę | e | Wężyk | Wezyk |
| ł | l | Ławecki | Lawecki |
| ń | n | Woźniak | Wozniak |
| ó | u | Góral | Gural |
| ś | s | Kosiński | Kosinski |
| ź, ż | z | Żukowski | Zukowski |

#### B. Phonetic equivalents
- rz ↔ ż: Kowalczyk / Kowalżyk
- sz ↔ s: Szymański / Symański
- cz ↔ c: Wojciech / Wojcech
- ó ↔ u: Wójcik / Wujcik
- ch ↔ h: Machowski / Mahowski

#### C. Suffix variants
- -ski → -sky, -scki (Kowalski / Kowalsky / Kowalscki)
- -wicz → -owicz, -ewicz (Jankowicz / Jankowic)
- -czyk → -czuk (Pawelczyk / Pawelczuk)

**Gender-specific suffixes**:
- Male: -ski (Kowalski), Female: -ska (Kowalska)
- Male: -cki (Nowicki), Female: -cka (Nowicka)
- **Tip**: Search male form (-ski) for broader results (includes both genders in older records)

#### D. Przydomki (hereditary nicknames)
If records show "vulgo" or "zwany": search BOTH the official surname AND the przydomek separately.

Example: "Jan Kowalski vulgo Prusak" → search "Kowalski" AND "Prusak"

**Search order**:
1. Original spelling with diacritics
2. ASCII version (most common)
3. Phonetic variants
4. Short forms (e.g., Kowal for Kowalski)

### Step 4: Execute Search

**Tell the user**:
1. Open the constructed URL in a browser
2. The page will load a search form pre-filled with parameters
3. Click "Szukaj" (Search) button or press Enter
4. Results will appear in a table below (loaded dynamically via JavaScript)

**If no results appear**:
- Try variant spellings (see Step 3)
- Expand date range (±10 years)
- Try neighboring voivodeships (family may have moved)
- Check if parish is indexed (click voivodeship name on main page to see parish list)

### Step 5: Interpret Results

Results display in a table with these columns:

| Column | Polish | Meaning |
|--------|--------|---------|
| Parish | Parafia | Parish where event was recorded |
| Year | Rok | Year of the event |
| Act # | Nr | Act number in register |
| Name | Imię i nazwisko | Individual(s) involved |
| Remarks | Uwagi | Critical info: parents, spouse, archive reference |

**The "Uwagi" (Remarks) column is MOST IMPORTANT**:
- For births: shows parents' names ("s. Jana i Marianny z Nowaków" = son of Jan and Marianna née Nowak)
- For marriages: shows both spouses' parents
- For deaths: shows age, spouse name, parents
- Often contains archive reference: "AP Radom, sygn. 75" = State Archive in Radom, signature 75

### Step 6: Evaluate Confidence

For each result, assess whether it matches the ancestor:

**Strong Signal** (HIGH CONFIDENCE - add to vault):
- Exact surname AND first name match
- Date within ±2 years of expected
- Parish matches known location
- Corroborating detail in Uwagi (parent name, spouse name, etc.)

**Moderate Signal** (MODERATE CONFIDENCE - add with (unverified) tag):
- Minor surname variant (Kowalski vs Kowalsky)
- Date within ±5 years of expected
- Same region but different parish
- One corroborating detail present

**Speculative** (LOW CONFIDENCE - do NOT add to vault):
- Common surname with no distinguishing details
- Date off by >5 years
- Only location matches
- No corroborating details
- Execute feedback loop (search for more evidence)

### Step 7: Find Original Images

Geneteka shows only index data. To see actual document:

1. Note the parish name, year, and act number from Geneteka
2. Check "Uwagi" column for archive reference
3. Go to **Szukaj w Archiwach** (szukajwarchiwach.gov.pl)
4. Search for parish name
5. Navigate: Archive → Zespół → Year → Scans
6. Find the act number
7. Verify the Geneteka transcription against original image

**Always verify against original** - transcription errors occur.

## Special Cases

### Very Common Surnames

For Kowalski, Nowak, Wiśniewski, Wójcik, Kamiński (top 10 surnames):

**MUST narrow search**:
- Add `search_name=` (first name)
- Add `search_lastname2=` (spouse maiden name for marriages)
- Reduce date range to ±5 years
- Specify parish with `rid=` if known

Without narrowing, you'll get thousands of results.

### Przydomki (Hereditary Nicknames)

If you find "vulgo", "zwany", "dictus", or "alias" in records:

Example: "Jan Kowalski vulgo Prusak"

**Action**:
1. Search "Kowalski" (official surname)
2. ALSO search "Prusak" (przydomek) separately
3. Note both in vault: `przydomek: Prusak`
4. The family may have emigrated using either name

### Marriage Searches

For marriages, use BOTH surnames:

```
https://geneteka.genealodzy.pl/index.php?op=gt&lang=pol&bdm=M&w=07mz&search_lastname=Kowalski&search_lastname2=Nowak&from_date=1880&to_date=1900
```

This finds marriages between Kowalski and Nowak families.

**Tip**: Marriage records are BEST for finding parents' names. Always prioritize finding a marriage over a birth.

### Russian Partition (1868-1918)

For mazowieckie, łódzkie, lubelskie, świętokrzyskie during 1868-1918:
- Records are in Russian (Cyrillic script)
- Dates use Julian calendar (add 12-13 days for Gregorian)
- Surnames may be russified (Kowalski → Kovalski)

**Search strategy**: Try both Polish and Russian-influenced spellings.

### Kresy (Eastern Borderlands)

For regions now in Ukraine (21uk), Belarus (22br), Lithuania (23lt):
- Use modern voivodeship codes above
- Parish names may be in Polish, Russian, or local language
- Many records were destroyed or lost

## Output Format

When reporting results to the user, use this citation format:

```
Geneteka: [Parish], [Year], act [number], [event type]
```

**Examples**:
- `Geneteka: Grodzisk Mazowiecki, 1876, act 42, marriage`
- `Geneteka: Łódź-św. Krzyż, 1889, act 118, birth (AP Łódź, sygn. 45)`

Include archive reference from Uwagi when present.

## Logging Negative Results

**ALWAYS document when no results found**:

```
Searched Geneteka for [SURNAME] (and variants: [LIST]) in [voivodeship] 
[date range] for [event types]: no results found.

Possible reasons:
- Parish not indexed in Geneteka
- Family used przydomek as primary surname
- Records don't survive (WWII destruction)
- Wrong voivodeship (family moved before 1918)
```

Negative results are valuable - they eliminate dead ends and guide next steps.

## Troubleshooting

### Problem: No results for surname with Polish characters

**Solution**: 
1. Try ASCII version (ą→a, ę→e, ł→l, ó→u, ś→s, ć→c, ń→n, ź/ż→z)
2. Try phonetic variants (rz→ż, sz→s, cz→c)
3. Try suffix variants (-ski→-sky→-scki)

### Problem: Too many results (thousands)

**Solution**:
1. Add first name with `search_name=`
2. Narrow date range to ±5 years
3. Add spouse surname for marriages (`search_lastname2=`)
4. Specify parish if known

### Problem: Expected result not found

**Checklist**:
- ✅ Tried all surname variants?
- ✅ Searched neighboring voivodeships?
- ✅ Expanded date range by ±10 years?
- ✅ Checked if parish is indexed? (click voivodeship on main page)
- ✅ Considered przydomek usage?
- ✅ Checked if family emigrated before expected date?

### Problem: Found result but can't verify

**Next step**: Guide user to Szukaj w Archiwach to view original image.

## Example: Complete Search Workflow

**User request**: "Find birth record for Jan Kowalski born ~1875 in mazowieckie"

**Your response**:

```
I'll guide you through searching Geneteka for Jan Kowalski's birth record.

**Step 1: Construct URL**

Try this URL first:
https://geneteka.genealodzy.pl/index.php?op=gt&lang=pol&bdm=B&w=07mz&search_lastname=Kowalski&search_name=Jan&from_date=1870&to_date=1880

This searches births (B) in mazowieckie (07mz) for Jan Kowalski between 1870-1880.

**Step 2: Execute search**

1. Open the URL in your browser
2. The form will be pre-filled
3. Click "Szukaj" (Search)
4. Results will appear below (may take a few seconds)

**Step 3: If too many results**

Kowalski is a very common surname. If you get hundreds of results:
- Add father's name if known
- Narrow date range to 1873-1877
- Specify parish if you know the village

**Step 4: Evaluate results**

Look for entries where:
- Name: Jan Kowalski (or Joannes Kowalski in Latin)
- Year: 1875 ±2 years
- Uwagi (Remarks): Check for parents' names to confirm it's the right person

**Step 5: Try variants if no match**

If no results, try these variants:
- Kowalsky (German spelling)
- Kowal (short form)
- Check if family used a przydomek (hereditary nickname)

**Step 6: Record findings**

If found: Note parish, year, act number, parents' names from Uwagi
If not found: Document the search (helps avoid re-searching later)
```

---

## Summary

This skill guides users through:
1. ✅ Constructing Geneteka search URLs with proper parameters
2. ✅ Generating Polish surname variants (diacritics, phonetics, suffixes)
3. ✅ Interpreting results and assessing confidence
4. ✅ Finding original images in Szukaj w Archiwach
5. ✅ Troubleshooting when no results appear
6. ✅ Documenting both positive and negative results

**Remember**: Guide, don't execute. Users perform the actual search because Geneteka requires JavaScript that cannot be automated.
