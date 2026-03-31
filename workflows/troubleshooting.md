# Troubleshooting Polish Genealogy Searches

A comprehensive guide for when searches yield no results or unexpected outcomes.

## Problem: No Results in Geneteka

### Checklist (try in order)

#### 1. Surname Variants
**Most common reason for no results**: incorrect spelling

✅ **Try ASCII version** (remove Polish diacritics):
- Świątek → Swiatek
- Wężyk → Wezyk  
- Góral → Gural
- Woźniak → Wozniak

✅ **Try phonetic equivalents**:
- rz ↔ ż: Kowalczyk / Kowalżyk
- sz ↔ s: Szymański / Symański
- cz ↔ c: Wojciech / Wojcech
- ó ↔ u: Wójcik / Wujcik

✅ **Try suffix variants**:
- -ski → -sky, -scki: Kowalski / Kowalsky / Kowalscki
- -wicz → -owicz: Jankowicz / Jankowic
- -czyk → -czuk: Pawelczyk / Pawelczuk

✅ **Try short forms**:
- Kowalski → Kowal
- Nowicki → Nowik
- Szymański → Szyman

#### 2. Date Range
**Births/deaths may be mis-dated by years**

✅ **Expand range**: If searching 1875-1880, try 1870-1885 (±5 years)

✅ **Calendar systems**: Russian partition 1868-1918 used Julian calendar
- Add 12 days (19th century) or 13 days (20th century)
- Birth on "March 15, 1890" (Julian) = March 27, 1890 (Gregorian)

✅ **Estimate errors**: Family tradition says "born 1875" but may be 1872 or 1878

#### 3. Wrong Voivodeship
**Families moved; modern borders differ from historical**

✅ **Try neighboring voivodeships**:
- If no results in mazowieckie (07mz), try Warszawa (71wa), łódzkie (05ld)
- If no results in małopolskie (06mp), try podkarpackie (09pk), świętokrzyskie (13sk)

✅ **Check historical partitions** (1795-1918):
- Russian: mazowieckie, łódzkie, lubelskie, świętokrzyskie, podlaskie
- Prussian: wielkopolskie, pomorskie, warmińsko-mazurskie, zachodniopomorskie
- Austrian: małopolskie, podkarpackie, śląskie (eastern)

Family in "Galicia" before 1918 → search małopolskie or podkarpackie
Family in "Congress Poland" → search mazowieckie, łódzkie, or lubelskie

#### 4. Parish Not Indexed
**Geneteka doesn't have every parish**

✅ **Check coverage**: On Geneteka main page, click voivodeship name to see parish list

✅ **Check indexing status**:
- Green checkmarks = well indexed
- Few or no years listed = poor coverage
- Parish not listed = NOT in Geneteka

✅ **Alternative databases**:
- **BaSIA** (basia.famula.pl) for Wielkopolska
- **Lubgens** (regestry.lubgens.eu) for Lubelskie
- **Metryki** (metryki.genealodzy.pl) for non-indexed parishes

#### 5. Przydomek (Hereditary Nickname)
**Family may have used przydomek as primary surname**

✅ **Check for "vulgo"**: In records, look for:
- "Jan Kowalski vulgo Młot"
- "Jan Kowalski zwany Prusak"
- "Joannes Kowalski dictus Młot"

✅ **Search przydomek separately**:
- If family is "Kowalski vulgo Młot" → search both "Kowalski" AND "Młot"

✅ **Common przydomki**:
- Prusak (the Prussian - indicates migration)
- Mazur (the Mazovian)
- Rusin (the Ruthenian - from eastern borders)
- Młot (the Hammer)
- Niemiec (the German)

#### 6. Records Don't Survive
**WWII destroyed many archives**

✅ **Check archive status**:
- Warsaw: ~70% of archives destroyed in Warsaw Uprising (1944)
- Western Poland: Many German-language records lost
- Eastern Poland (Kresy): Records now in Ukraine/Belarus/Lithuania archives

✅ **No coverage areas**:
- dolnośląskie (01ds): 52K records (vs 12M in mazowieckie) - heavily destroyed
- zachodniopomorskie (16zp): 5K records - German territory until 1945

#### 7. Wrong Event Type
**Searching births when marriage would be better**

✅ **Try marriages first**: Marriage records contain:
- Both spouses' names
- Both sets of parents
- Ages (calculate birth year)
- Parish of origin (if couple from different places)

✅ **Birth records**: Often only show:
- Child's name
- Parents' names
- Birthdate

✅ **Death records**: Often show:
- Age at death (calculate birth year)
- Spouse name
- Sometimes parents' names

**Best strategy**: Find marriage → use parents' names to find births → find deaths

---

## Problem: Too Many Results (Thousands)

### For Common Surnames

Kowalski, Nowak, Wiśniewski, Wójcik, Kamiński, Lewandowski, Zieliński, Szymański, Woźniak, Dąbrowski

✅ **Add first name**: `search_name=Jan`

✅ **Add spouse surname** (for marriages): `search_lastname2=Nowak`

✅ **Narrow date range**: Instead of 1850-1900, try 1873-1877

✅ **Add parish**: If you know village, find parish ID and use `rid=[ID]`

✅ **Use parents' names**: Search remarks (Uwagi) column for specific parent names

---

## Problem: Found Record But Unsure If It's the Right Person

### Confidence Assessment

**Strong Signal (HIGH confidence)** - Add to vault:
- ✅ Surname AND first name match
- ✅ Date within ±2 years
- ✅ Parish matches known location
- ✅ Parents' names match known family (from Uwagi column)
- ✅ Spouse name matches (for marriages)

**Moderate Signal (MODERATE confidence)** - Add with (unverified) tag:
- ⚠️ Minor surname variant (Kowalski vs Kowalsky)
- ⚠️ Date within ±5 years
- ⚠️ Same region but different parish
- ⚠️ One corroborating detail (parent OR spouse name, not both)

**Speculative (LOW confidence)** - Do NOT add:
- ❌ Common surname, no distinguishing details
- ❌ Date off by >5 years
- ❌ Wrong region
- ❌ No corroborating details

**Action for Speculative**: Execute feedback loop - search for more evidence:
1. Find marriage record (has parents' names for both spouses)
2. Find siblings' births (same parents confirm family)
3. Find death record (may name children/spouse)
4. Find original image on Szukaj w Archiwach

---

## Problem: Can't Find Original Image

### After Finding Geneteka Index Entry

Geneteka shows: "Geneteka: Łódź-św. Krzyż, 1889, act 118, birth (AP Łódź, sygn. 45)"

✅ **Go to Szukaj w Archiwach**: szukajwarchiwach.gov.pl

✅ **Search for parish**: Enter "Łódź" or "św. Krzyż"

✅ **Navigate hierarchy**:
```
Archiwum Państwowe w Łodzi (Archive)
  → Akta stanu cywilnego Parafii Rzymskokatolickiej św. Krzyż (Fond)
    → Urodzenia (Births)
      → 1889 (Year)
        → Scan images
```

✅ **Find act number**: Browse images to find "Akt 118"

✅ **If not digitized**:
- Contact archive: email or visit in person
- Request scan: many archives offer paid scanning services
- Check FamilySearch: some Polish records on familysearch.org (requires free account)

---

## Problem: Record in Cyrillic (Russian)

### Russian Partition 1868-1918

Records in mazowieckie, łódzkie, lubelskie, świętokrzyskie between 1868-1918 are in Russian.

✅ **Use /cyrillic-ocr skill**: This repo has a skill for extracting data from Cyrillic documents

✅ **Key Russian genealogy terms**:
| Russian | Polish | English |
|---------|--------|---------|
| Родился | Urodzony | Born |
| Крещён | Chrzczony | Baptized |
| Умер | Zmarł | Died |
| Отец | Ojciec | Father |
| Мать | Matka | Mother |
| Жених | Pan młody | Groom |
| Невеста | Panna młoda | Bride |

✅ **Surname transliteration**:
| Polish | Cyrillic | Back to Latin |
|--------|----------|---------------|
| Kowalski | Ковальски | Kovalski |
| Wiśniewski | Вишневски | Vishnevski |
| Wójcik | Войцик | Voitsik |

**Search strategy**: Try both Polish and Russian-influenced spellings in Geneteka.

---

## Problem: Parish Name Has Changed

### Historical vs Modern Names

Many places have different names now:

| Historical (in records) | Modern | Location |
|-------------------------|--------|----------|
| Wilno | Vilnius | Lithuania |
| Lwów | Lviv | Ukraine |
| Grodno | Hrodna | Belarus |
| Królewiec | Kaliningrad | Russia |
| Breslau | Wrocław | Poland |
| Danzig | Gdańsk | Poland |
| Stettin | Szczecin | Poland |

✅ **Check both names**: Search "Wilno" AND "Vilnius"

✅ **Use modern voivodeship**: Even if place is now in Ukraine, use historical Polish voivodeship code (21uk for Ukraine)

---

## Problem: Multiple People with Same Name

### Distinguishing Between Namesakes

In small villages, multiple unrelated families share common names.

✅ **Use przydomki**: "Jan Kowalski vulgo Młot" vs "Jan Kowalski vulgo Prusak" are different families

✅ **Use parents' names**: Check Uwagi column in Geneteka or original records

✅ **Use ages/dates**: Calculate birth year from age at death

✅ **Use witnesses/godparents**: Same witnesses often indicate same family network

✅ **Cross-reference**: Find marriage → use parents' names to find correct birth

---

## Alternative Strategies

### When Geneteka Has Nothing

#### 1. Try BaSIA (Wielkopolska only)
- URL: basia.famula.pl
- Coverage: 6.6M records from Wielkopolska (Poznań, Gniezno, Kalisz, Konin, Piła regions)
- Format: Direct links to original images

#### 2. Try Lubgens (Lubelskie only)
- URL: regestry.lubgens.eu
- Coverage: Lubelskie voivodeship
- Format: Parish-by-parish transcriptions

#### 3. Browse Metryki
- URL: metryki.genealodzy.pl
- Coverage: 12.7M scanned pages
- Format: Browse by voivodeship → parish → year
- Use: When parish not indexed in Geneteka, browse images directly

#### 4. Search Szukaj w Archiwach Directly
- URL: szukajwarchiwach.gov.pl
- Method: Navigate to parish → year → browse all acts
- Slow but comprehensive

#### 5. FamilySearch
- URL: familysearch.org (free account required)
- Coverage: Millions of Polish records, including some not in Geneteka
- Search: Use "Poland" + parish name + surname

#### 6. JRI-Poland (Jewish records)
- URL: jri-poland.org
- Coverage: Jewish vital records, primarily from Congress Poland
- Use: If ancestor was Jewish

---

## Quick Troubleshooting Decision Tree

```
No results in Geneteka?
│
├─ Tried all surname variants (ą→a, rz→ż, -ski→-sky)?
│  NO → Try variants first
│  YES ↓
│
├─ Expanded date range by ±10 years?
│  NO → Try wider range
│  YES ↓
│
├─ Searched neighboring voivodeships?
│  NO → Try adjacent regions
│  YES ↓
│
├─ Checked if parish is indexed?
│  NO → Check voivodeship parish list
│  YES (not indexed) ↓
│
├─ Try alternative databases:
│  - BaSIA (if Wielkopolska)
│  - Lubgens (if Lubelskie)
│  - Metryki (browse images)
│  - Szukaj w Archiwach (direct browsing)
│  - FamilySearch
│
└─ Records may not survive (WWII destruction)
   Document negative result and try other evidence
```

---

## Logging Negative Results

**Always document searches that yield nothing**:

```
Searched Geneteka for [SURNAME] in [VOIVODESHIP] [DATE_RANGE] for [EVENT_TYPE]:
- Variants tried: [LIST]
- Results: None found

Possible reasons:
- Parish [NAME] not indexed in Geneteka (checked parish list)
- Records may not survive (western Poland WWII destruction)
- Family may have used przydomek as primary surname
- Wrong voivodeship (family moved before 1918)

Next steps:
- Try [ALTERNATIVE_DATABASE]
- Browse Szukaj w Archiwach directly
- Search neighboring parishes
```

This documentation prevents re-searching the same dead ends and guides future research.

---

## Summary

When searches fail:
1. ✅ Try all surname variants (diacritics, phonetics, suffixes, przydomki)
2. ✅ Expand date range and try neighboring voivodeships
3. ✅ Verify parish is indexed (check coverage)
4. ✅ Try alternative databases (BaSIA, Lubgens, Metryki)
5. ✅ Browse Szukaj w Archiwach images directly
6. ✅ Check FamilySearch for records not in Polish databases
7. ✅ Document negative results to avoid re-searching

Remember: Absence of a record in Geneteka ≠ record doesn't exist. Many parishes aren't indexed yet, and WWII destroyed many archives. Always try multiple sources.