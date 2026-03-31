---
name: geneteka-search
description: Search Geneteka (geneteka.genealodzy.pl) for Polish vital records. Use when asked to find birth, marriage, or death records from Poland, or when researching Polish ancestors.
allowed-tools: web_fetch, read, edit
---

# Geneteka Search Skill

## What is Geneteka

Geneteka is a free online index of over 65 million Polish vital records (births, marriages, deaths) maintained by the Polish Genealogical Society. It aggregates parish register indexes from archives across Poland. Records are indexed, not digitized: Geneteka provides metadata (names, dates, parish, act numbers) that you use to request original documents from archives.

## Search Strategy

### URL Structure

Base URL: `https://geneteka.genealodzy.pl/index.php?`

Key parameters:
- `op=gt` (search operation)
- `lang=pol` (language: pol, eng, ger)
- `bdm=B` (event type: B=births, M=marriages, D=deaths, or combination like BMD)
- `w=` (voivodeship code, e.g., 15sk for śląskie, 06lu for lubelskie)
- `rid=` (parish ID, leave empty for all parishes in voivodeship)
- `search_lastname=` (primary surname)
- `search_name=` (first name, optional)
- `search_lastname2=` (spouse surname for marriages)
- `from_date=` and `to_date=` (year range)

Example: `https://geneteka.genealodzy.pl/index.php?op=gt&lang=pol&bdm=M&w=10lo&search_lastname=Wiśniewski&from_date=1850&to_date=1900`

### Voivodeship Selection

Each search targets one voivodeship (województwo). Coverage varies significantly:
- **Best coverage**: mazowieckie (12M+ records), łódzkie (9.7M), małopolskie (6.7M), wielkopolskie (5.3M), lubelskie (4.4M)
- **Good coverage**: podlaskie (3M), śląskie (2.5M), kujawsko-pomorskie (2.8M)
- **Limited coverage**: dolnośląskie (52K), lubuskie (10K), zachodniopomorskie (80K)

Western voivodeships have sparse coverage due to post-WWII border changes and German-language records.

### Surname Variants and Polish Orthography

Polish spelling was inconsistent in historical records. Search for variants:
- rz ↔ ż (Kowalczyk vs Kowalczik)
- ó ↔ u (Król vs Krul)
- w ↔ v (Kowalski vs Kovalski)
- cz ↔ c (Wojciech vs Wojcech)
- sz ↔ s (Kaszuba vs Kasuba)
- Latinized endings: -ski/-ska, -wicz/-owicz
- Dropped diacritics: ł→l, ą→a, ę→e, ś→s, ć→c, ń→n, ź/ż→z

Always try the base surname first, then variants if results are sparse.

## Reading Results

Results display in a table with columns:
1. **Parafia** (Parish): location where the event was recorded
2. **Rok** (Year): year of the event
3. **Nr** (Act Number): the act number in the parish register
4. **Imię i nazwisko** (Name and Surname): names of individuals involved
5. **Uwagi** (Remarks): contains archive references, microfilm numbers, additional details

The "Uwagi" column is critical: it often contains the archive call number (sygnatura) needed to order the original record.

## Handling Common Surnames

For very common surnames (Kowalski, Nowak, Wiśniewski, Wójcik, Kamiński), narrow your search:
1. Add the spouse surname using `search_lastname2=` for marriage searches
2. Restrict the date range to ±5 years of expected date
3. Limit to a specific parish if known
4. Use first names when available

Without narrowing, common surnames return thousands of results.

## Confidence Assessment

When evaluating whether a Geneteka result matches your ancestor:

**Strong Signal**:
- Exact surname and first name match
- Date within ±2 years of expected
- Matching parish or nearby parish in the same region
- Corroborating detail (spouse name, parent name, age)

**Moderate Signal**:
- Minor spelling variant of surname
- Date within ±5 years of expected
- Same region but different parish
- One corroborating detail present

**Speculative**:
- Common surname with no distinguishing details
- Date off by more than 5 years
- Only location matches
- No corroborating details

## Output Format

Cite Geneteka results as:

`Geneteka: [Parish], [Year], act [number], [event type]`

Examples:
- `Geneteka: Grodzisk Mazowiecki, 1876, act 42, marriage`
- `Geneteka: Łódź-św. Krzyż, 1889, act 118, birth`

Include the archive reference from the Uwagi column when present:
- `Geneteka: Radom, 1852, act 7, death (AP Radom, sygn. 75)`

## Logging Negative Results

Always document when searches yield no results:
- "Searched Geneteka for [SURNAME] in [voivodeship], [date range], [event types]: no results"
- "Parish [NAME] has no Geneteka coverage for [event type]"
- "Voivodeship [NAME] has limited coverage (N records indexed)"

Negative results eliminate possibilities and guide next steps.
