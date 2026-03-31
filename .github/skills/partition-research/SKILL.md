---
name: partition-research
description: Identify partition (Russian, Prussian, Austrian) for Polish ancestors 1795-1918 and apply partition-specific research strategies. Use when researching partition-era ancestors or determining which archives to search.
allowed-tools: read, edit, web_fetch
---

# Partition Research Skill

This skill helps identify which of the three partitions of Poland (1795-1918) applies to an ancestor and provides partition-specific research strategies, archive sources, and document characteristics.

## 1. The Three Partitions (1795-1918)

### Russian Partition (Congress Poland / Królestwo Kongresowe)

**Territory:**
- Modern voivodeships: mazowieckie, łódzkie, lubelskie, świętokrzyskie, podlaskie, parts of podkarpackie
- Major cities: Warszawa, Łódź, Lublin, Kielce, Radom, Siedlce, Płock

**Record Characteristics:**
- Civil registration began in 1808 (Napoleonic Code influence)
- Languages: Polish (1808-1867), Russian (1868-1918)
- Records often in narrative format with detailed descriptions
- After 1868, records use Cyrillic script; invoke `/cyrillic-ocr` skill for transcription

**Primary Archives and Databases:**
- Szukaj w Archiwach (szukajwarchiwach.gov.pl): centralized portal
- AP Lublin, AP Łódź, AP Warszawa: regional state archives
- Geneteka (geneteka.genealodzy.pl): index database
- Metryki.genealodzy.pl: scanned records

**Research Tips:**
- Check both Catholic and civil registration (duplicate systems existed)
- Jewish records often in separate books but same archive collections
- Look for "alegata" (supplementary documents) attached to marriage records

---

### Prussian Partition (Greater Poland, Pomerania, Silesia)

**Territory:**
- Modern voivodeships: wielkopolskie, pomorskie, warmińsko-mazurskie, kujawsko-pomorskie, dolnośląskie, lubuskie
- Major cities: Poznań, Gdańsk, Wrocław, Toruń, Bydgoszcz, Szczecin

**Record Characteristics:**
- Civil registration began in 1874 (earlier church records are primary source)
- Language: German, written in Gothic Kurrent script (requires paleography skills)
- Standesamt (civil registry office) records are highly standardized
- Pre-1874: rely on Catholic/Protestant church books in Latin or German

**Primary Archives and Databases:**
- BaSIA (basia.famula.pl): Wielkopolska vital records index
- Poznan Project (poznan-project.psnc.pl): marriage index 1800-1899
- FamilySearch: extensive Prussian collections
- Ancestry: some digitized Standesamt records
- AP Poznań, AP Gdańsk: regional state archives

**Research Tips:**
- For pre-1874 research, identify the parish (Kirchspiel) not just the town
- Protestant records often better preserved than Catholic in some areas
- Meyers Gazetteer (meyersgaz.org) helps locate historical place names
- German naming patterns: patronymics less common, surnames stable earlier

---

### Austrian Partition (Galicia / Galizien)

**Territory:**
- Modern voivodeships: małopolskie, podkarpackie, parts of śląskie
- Major cities: Kraków, Lwów (now Lviv, Ukraine), Rzeszów, Tarnów, Przemyśl, Nowy Sącz

**Record Characteristics:**
- Civil registration began in 1784 for non-Catholics, 1787 for Catholics (earliest in partitions)
- Languages: Latin (church records), German (civil administration), Polish
- Distinctive tabular format: columns for date, names, parents, godparents, etc.
- Generally easier to read than Russian or Prussian records due to tabular structure

**Primary Archives and Databases:**
- AP Kraków, AP Rzeszów: regional state archives
- Szukaj w Archiwach: includes Galician collections
- Gesher Galicia (geshergalicia.org): Jewish genealogy focus
- AGAD (for some Galician administrative records)
- FamilySearch: extensive microfilm collections

**Research Tips:**
- Eastern Galicia (Lwów region) records now in Ukraine; check CDIAL Lviv
- Look for cadastral maps (Kataster) for property and boundary information
- Josephine and Franciscan cadastres provide early land ownership data
- Jewish records: check both kehilla records and civil registration

---

## 2. How to Determine Partition

Follow this process to identify the correct partition:

1. **Map location to modern voivodeship**: Use the ancestor's birthplace or residence and identify which modern Polish voivodeship it falls within. Use online gazetteers or maps.

2. **Cross-reference with partition boundaries**: The lists above cover most cases, but border areas require additional verification.

3. **Check historical maps for border regions**: Towns near partition borders may have changed hands. Use Mapire.eu or David Rumsey Map Collection for period maps.

4. **Confirm via record language**: The language of surviving records confirms the partition:
   - Polish/Russian with Cyrillic after 1868 → Russian Partition
   - German in Gothic Kurrent → Prussian Partition
   - Latin in tabular format → Austrian Partition

5. **Note boundary changes**: Some areas changed partitions during the period (e.g., after 1815 Congress of Vienna adjustments).

---

## 3. Confidence Tiers for Partition Identification

Apply these confidence levels when documenting partition assignments:

**Strong Signal:**
- Location is clearly within one partition's core territory
- Record language matches expected partition
- Multiple sources confirm the same partition

**Moderate Signal:**
- Location is near a partition border
- Only one confirming source available
- Recommend searching archives from both adjacent partitions

**Speculative:**
- Location name is ambiguous or common across regions
- No records yet found to confirm language/format
- Historical maps show disputed or changing boundaries

---

## 4. Updating Person Files

When partition is determined, update the person's markdown file with the partition field in the YAML frontmatter:

```yaml
---
type: person
name: Jan Kowalski
born: 1845
died: 1910
partition: Russian
partition_confidence: Strong
family: Kowalski
sources:
  - "Birth record, AP Lublin, 1845"
---
```

Include `partition_confidence` using the tiers above.

---

## 5. Related Skills

- `/cyrillic-ocr`: Use for transcribing Russian Partition records written in Cyrillic (post-1868)
- `/latin-transcription`: Use for Austrian Partition church records in Latin
- `/kurrent-reading`: Use for Prussian Partition records in Gothic German script

---

## 6. Quick Reference Table

| Partition | Civil Reg. Start | Primary Language | Script | Key Database |
|-----------|------------------|------------------|--------|--------------|
| Russian | 1808 | Polish/Russian | Latin/Cyrillic | Geneteka |
| Prussian | 1874 | German | Gothic Kurrent | BaSIA, Poznan Project |
| Austrian | 1784-1787 | Latin/Polish | Latin | Gesher Galicia |

---

## 7. Common Pitfalls

- **Assuming modern borders match historical**: Many towns changed countries multiple times
- **Ignoring language shifts**: Russian Partition switched from Polish to Russian in 1868
- **Missing duplicate registrations**: Both church and civil records may exist for the same event
- **Overlooking Ukrainian archives**: Eastern Galicia records are now in Lviv, Ukraine
