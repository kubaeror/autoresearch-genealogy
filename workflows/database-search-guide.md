# Polish Genealogy Databases - Complete Search Guide

Practical step-by-step instructions for each major Polish genealogy database.

---

## 1. Geneteka (geneteka.genealodzy.pl)

### Coverage
65+ million indexed vital records from 6,000+ parishes across Poland, Ukraine, Belarus, Lithuania.

### Best For
- Finding quick references to births, marriages, deaths
- Identifying which parish to search
- Getting archive call numbers to order original documents

### Limitations
- Index only (no images)
- Not all parishes indexed
- Transcription errors possible
- Requires JavaScript (cannot be scraped)

### How to Search

#### Step 1: Build URL

Template:
```
https://geneteka.genealodzy.pl/index.php?op=gt&lang=pol&bdm=[B/M/D]&w=[CODE]&search_lastname=[SURNAME]&from_date=[YEAR]&to_date=[YEAR]
```

Parameters:
- `bdm=B` - Births only
- `bdm=M` - Marriages only
- `bdm=D` - Deaths only
- `bdm=BMD` - All events
- `w=07mz` - Voivodeship code (see table below)
- `search_lastname=Kowalski` - Surname (UTF-8 Polish characters OK)
- `search_name=Jan` - First name (optional)
- `search_lastname2=Nowak` - Spouse surname for marriages (optional)
- `from_date=1850` - Start year
- `to_date=1900` - End year

#### Step 2: Voivodeship Codes

| Code | Name | Records | Quality |
|------|------|---------|---------|
| 07mz | mazowieckie | 12.0M | Excellent |
| 71wa | Warszawa | 2.6M | Excellent |
| 05ld | łódzkie | 9.7M | Excellent |
| 06mp | małopolskie | 6.7M | Good |
| 12sl | śląskie | 6.3M | Good |
| 13sk | świętokrzyskie | 4.9M | Good |
| 09pk | podkarpackie | 4.2M | Moderate |
| 02kp | kujawsko-pomorskie | 3.6M | Good |
| 10pl | podlaskie | 3.6M | Good |
| 21uk | Ukraina (Kresy) | 2.9M | Good |
| 15wp | wielkopolskie | 2.7M | Good |
| 22br | Białoruś (Kresy) | 1.4M | Moderate |
| 23lt | Litwa (Kresy) | 1.3M | Moderate |
| 03lb | lubelskie | 1.2M | Moderate |
| 11pm | pomorskie | 1.2M | Limited |
| 14wm | warmińsko-mazurskie | 0.7M | Limited |
| 01ds | dolnośląskie | 52K | Very poor |
| 04ls | lubuskie | 10K | Very poor |
| 16zp | zachodniopomorskie | 5K | Very poor |

#### Step 3: Example Searches

**Birth search**:
```
https://geneteka.genealodzy.pl/index.php?op=gt&lang=pol&bdm=B&w=07mz&search_lastname=Kowalski&search_name=Jan&from_date=1870&to_date=1880
```
Searches for Jan Kowalski born 1870-1880 in mazowieckie.

**Marriage search**:
```
https://geneteka.genealodzy.pl/index.php?op=gt&lang=pol&bdm=M&w=07mz&search_lastname=Kowalski&search_lastname2=Nowak&from_date=1890&to_date=1910
```
Searches for marriages between Kowalski and Nowak families 1890-1910 in mazowieckie.

**All events, wide range**:
```
https://geneteka.genealodzy.pl/index.php?op=gt&lang=pol&bdm=BMD&w=05ld&search_lastname=Świątek&from_date=1800&to_date=1950
```
Searches for all Świątek events 1800-1950 in łódzkie.

#### Step 4: Interpret Results

Results table columns:
- **Parafia** (Parish) - Where event was recorded
- **Rok** (Year) - Year of event
- **Nr** (Act number) - Act number in register
- **Imię i nazwisko** (Name) - Person(s) involved
- **Uwagi** (Remarks) - **MOST IMPORTANT**: parents, spouse, archive reference

Example row:
```
Parafia: Łódź-św. Krzyż
Rok: 1889
Nr: 118
Imię i nazwisko: Jan Kowalski
Uwagi: s. Piotra i Marianny z Nowaków (AP Łódź, sygn. 45/123/0)
```

Translation:
- Parish: Łódź-Holy Cross
- Year: 1889
- Act: 118
- Name: Jan Kowalski
- Remarks: son of Piotr and Marianna née Nowak (State Archive in Łódź, signature 45/123/0)

#### Step 5: Get Original Image

1. Note parish, year, act number from Geneteka
2. Check Uwagi for archive reference
3. Go to Szukaj w Archiwach (see section 2 below)
4. Navigate to the specific act
5. Verify Geneteka transcription against original

### Common Mistakes

❌ **Only trying one spelling** → Try all variants (see Troubleshooting guide)  
❌ **Ignoring Uwagi column** → This has critical info (parents, spouse)  
❌ **Assuming complete coverage** → Many parishes NOT indexed  
❌ **Not verifying against original** → Transcription errors occur  

---

## 2. Szukaj w Archiwach (szukajwarchiwach.gov.pl)

### Coverage
Digitized holdings from all Polish state archives. Millions of scanned pages including original parish registers and civil registration.

### Best For
- Viewing original document images
- Verifying Geneteka transcriptions
- Browsing non-indexed parishes
- Finding alegata (marriage supplements)

### Limitations
- Protected by Cloudflare (cannot scrape)
- Navigation is manual (no name search within records)
- Not all records digitized
- Some archives restrict online access

### How to Search

#### Method 1: Following Geneteka Reference

Geneteka gave you: "AP Łódź, zespół 45/123/0, sygn. 67, s. 89"

Parse:
- **AP Łódź** = Archiwum Państwowe w Łodzi (State Archive in Łódź)
- **zespół 45/123/0** = Fond/collection number
- **sygn. 67** = Signature (unit within collection)
- **s. 89** = Page 89

Steps:
1. Go to szukajwarchiwach.gov.pl
2. Search for "Łódź" + parish name
3. Click on result → navigate to zespół 45/123/0
4. Find sygn. 67 in the list
5. Open scans, browse to page 89

#### Method 2: Parish Name Search

If you don't have Geneteka reference:

1. Go to szukajwarchiwach.gov.pl
2. Use search box: enter parish name (e.g., "Łódź parafia św. Krzyż")
3. Filter by: "Akta stanu cywilnego" (civil registration) or "Księgi metrykalne" (parish registers)
4. Click result → shows zespół (collection)
5. Browse series: Urodzenia (births), Małżeństwa (marriages), Zgony (deaths)
6. Select year → view scans

#### Method 3: Browse by Archive

If you know the archive but not the exact parish:

1. Go to szukajwarchiwach.gov.pl
2. Click "Archiwa" (Archives)
3. Select archive (e.g., "AP Łódź")
4. Browse zespoły (collections)
5. Look for:
   - "Akta stanu cywilnego Parafii Rzymskokatolickiej w [Parish]"
   - "Księgi metrykalne parafii [Parish]"

#### Navigation Hierarchy

```
Archiwum (Archive)
  └─ Zespół (Fond/Collection)
      └─ Seria (Series: births/marriages/deaths)
          └─ Jednostka (Unit: specific year or range)
              └─ Skany (Scanned images)
```

### Types of Records

| Polish | English | What It Contains |
|--------|---------|------------------|
| Akta stanu cywilnego | Civil registration | Post-1808 vital records |
| Księgi metrykalne | Parish registers | Pre-1808 church records |
| Akta urodzeń | Birth records | Names, parents, date, place |
| Akta małżeństw | Marriage records | Couple, parents, ages, origins |
| Akta zgonów | Death records | Name, age, spouse, cause |
| Alegata | Marriage supplements | Birth certs, parental consent |

### Common Mistakes

❌ **Searching for person names** → Search finds archival descriptions, not individuals  
❌ **Expecting English interface** → Mostly Polish only  
❌ **Assuming all records online** → Many archives not digitized yet  
❌ **Not checking multiple zespoły** → Same parish may have multiple collections  

---

## 3. BaSIA (basia.famula.pl)

### Coverage
6.6+ million records from Wielkopolska region (Poznań, Gniezno, Kalisz, Konin, Piła areas).

### Best For
- Wielkopolska research (western Poland)
- Direct links to original images
- Well-organized parish-by-parish structure

### Limitations
- Wielkopolska only
- Requires free account to view full results
- Some parishes incomplete

### How to Search

#### Step 1: Create Account (Free)
1. Go to basia.famula.pl
2. Click "Załóż konto" (Create account)
3. Fill in email, username, password
4. Confirm email

#### Step 2: Search

Interface has search box for surnames.

Try:
1. Enter surname (Polish characters OK)
2. Select event type: Urodzenia (births), Małżeństwa (marriages), Zgony (deaths)
3. Optionally filter by year range
4. Click "Szukaj" (Search)

#### Step 3: View Results

Results show:
- Parish
- Year
- Act number
- Names
- **Link to original image** (click to view scan)

### Advantages Over Geneteka

✅ Direct image links (no need to navigate Szukaj w Archiwach)  
✅ Often better transcriptions  
✅ User-friendly interface  
✅ Good coverage for Wielkopolska  

---

## 4. Lubgens (regestry.lubgens.eu)

### Coverage
Lubelskie voivodeship parish registers and civil registration.

### Best For
- Lubelskie region research
- Parishes not in Geneteka
- Greek Catholic and Orthodox records

### How to Search

#### Step 1: Select Parish

1. Go to regestry.lubgens.eu
2. Alphabetical parish list displayed
3. Click on parish name

#### Step 2: View Transcriptions

Each parish page shows:
- Record type (urodzenia/małżeństwa/zgony)
- Years covered
- Transcribed entries

#### Step 3: Search Within Parish

Use browser search (Ctrl+F) to find surnames within transcriptions.

### Advantages

✅ Simple static pages (works without JavaScript)  
✅ Covers many parishes NOT in Geneteka  
✅ Greek Catholic and Orthodox records included  
✅ Direct transcriptions (no navigation needed)  

---

## 5. Metryki (metryki.genealodzy.pl)

### Coverage
12.7+ million scanned pages from parish registers across Poland.

### Best For
- Browsing when parish not indexed
- Viewing original handwriting
- Finding records pre-1808 (church records)

### How to Search

#### Method: Browse Only (No Name Search)

1. Go to metryki.genealodzy.pl
2. Select voivodeship from map or list
3. Select parish from list
4. Select record type: U (urodzenia/births), M (małżeństwa/marriages), Z (zgony/deaths)
5. Select year
6. Browse page-by-page through images

### When to Use

Use Metryki when:
- ✅ Parish not indexed in Geneteka
- ✅ Need to see original handwriting for OCR
- ✅ Searching for siblings (browse all births in parish/year)
- ✅ Verifying transcriptions

### Limitations

⚠️ No name index - must browse all images  
⚠️ Time-consuming for large parishes  
⚠️ Image quality varies  

---

## 6. FamilySearch (familysearch.org)

### Coverage
Millions of Polish records, including some not in Polish databases.

### Best For
- Records not in Geneteka/BaSIA/Lubgens
- Mormon emigrants (extensive Mormon indexing)
- Cross-referencing Polish databases

### How to Search

#### Step 1: Create Free Account
1. Go to familysearch.org
2. Create free account (no payment required)
3. Log in

#### Step 2: Search Records

1. Click "Search" → "Records"
2. Enter: First name, Last name
3. Add: Birth year (approximate), Birth place (Poland or specific region)
4. Click "Search"

#### Step 3: Filter Results

Use filters:
- Collection (narrow to Polish records)
- Record type (birth/marriage/death)
- Year range

#### Step 4: View Images

Many Polish records have viewable images on FamilySearch.

### Coverage Notes

✅ Extensive Poznań region records  
✅ Some German partition records  
✅ Jewish records from various regions  
✅ Sometimes has records NOT in Geneteka  

---

## 7. JRI-Poland (jri-poland.org)

### Coverage
Jewish vital records from Poland, primarily Congress Poland (Russian partition).

### Best For
- Jewish ancestors
- Congress Poland region
- Surnames that don't appear in Catholic records

### How to Search

1. Go to jri-poland.org
2. Select database: Town Index or Name Index
3. Enter surname (try variants)
4. Results show: name, town, year, record type, archive reference

### Specialized Features

✅ Hebrew name variants  
✅ Jewish calendar dates  
✅ Rabbinical records  
✅ Kehilla (community) registers  

---

## Search Strategy Summary

### For Any Polish Ancestor:

**Step 1**: Start with **Geneteka** (fastest, largest index)
- Try all surname variants
- Check neighboring voivodeships

**Step 2**: If no Geneteka results, try region-specific database:
- Wielkopolska → **BaSIA**
- Lubelskie → **Lubgens**
- Any region → **Metryki** (browse images)

**Step 3**: Get original images:
- **Szukaj w Archiwach** (following Geneteka references)
- **BaSIA** (direct links)
- **FamilySearch** (may have scans)

**Step 4**: Cross-reference with **FamilySearch**
- Sometimes has records not in Polish databases

**Step 5**: If Jewish ancestor: **JRI-Poland**

### Priority Order:

1. 🥇 **Geneteka** - try first, fastest
2. 🥈 **BaSIA** (if Wielkopolska) or **Lubgens** (if Lubelskie)
3. 🥉 **Szukaj w Archiwach** - for original images
4. 🏅 **Metryki** - when parish not indexed
5. 🏅 **FamilySearch** - cross-reference
6. 🏅 **JRI-Poland** - if Jewish

---

## Quick Reference Table

| Database | URL | Coverage | Best For | Searchable | Images |
|----------|-----|----------|----------|------------|--------|
| Geneteka | geneteka.genealodzy.pl | 65M records, all Poland | Quick index lookup | Yes (surname, date, parish) | No |
| Szukaj w Archiwach | szukajwarchiwach.gov.pl | All state archives | Original images | No (description only) | Yes |
| BaSIA | basia.famula.pl | 6.6M, Wielkopolska | Wielkopolska + images | Yes (surname, parish) | Yes |
| Lubgens | regestry.lubgens.eu | Lubelskie | Lubelskie parishes | Browser search only | No (transcriptions) |
| Metryki | metryki.genealodzy.pl | 12.7M pages | Browse non-indexed | No (browse only) | Yes |
| FamilySearch | familysearch.org | Millions | Cross-reference | Yes (name, place, date) | Many |
| JRI-Poland | jri-poland.org | Jewish records | Jewish ancestors | Yes (surname, town) | No |

---

## Tips for Success

✅ **Always try surname variants** - diacritics, phonetics, suffixes  
✅ **Search multiple databases** - Geneteka doesn't have everything  
✅ **Verify against original images** - transcription errors happen  
✅ **Document negative results** - avoid re-searching dead ends  
✅ **Use marriage records first** - they contain the most genealogical information  
✅ **Check neighboring parishes** - families moved frequently  
✅ **Expect gaps** - WWII destroyed many archives  
✅ **Be patient** - Polish research takes time and persistence  

---

For troubleshooting when searches fail, see: `workflows/troubleshooting.md`