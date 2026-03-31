# Kresy (Eastern Borderlands) Search

Research ancestors from territories that were Polish before 1939 but are now in Ukraine, Belarus, or Lithuania.

## Autoresearch Configuration

**Goal**: For every ancestor identified as originating from Kresy (former Polish Eastern Borderlands), locate records in Polish, Ukrainian, Belarusian, or Lithuanian archives.

**Metric**: Number of Kresy-origin ancestors with records found in foreign archives or repatriation documents

**Direction**: Maximize

**Verify**: 
1. Count Kresy ancestors by location confidence (strong/moderate/speculative)
2. Count Kresy ancestors with foreign archive records found
3. Report: "X Kresy ancestors researched (Y locations confirmed, Z pending, W records found)"

**Guard**:
- Place names have changed multiple times. A single village may have Polish, Ukrainian, Russian, and Soviet names.
- Records may be in Polish, Russian, Ukrainian, Yiddish, or German depending on era and community.
- Many records were destroyed in WWII or scattered across multiple countries.
- If family was repatriated 1944-1946, Polish records may exist for post-repatriation life.

**Iterations**: 8

**Protocol**:

1. **Identify Kresy ancestors**: From Family_Tree.md, list ancestors who:
   - Were born in territories east of the Bug River
   - Have locations in modern Ukraine, Belarus, or Lithuania
   - Were "repatriated" to Poland after 1944
   - Have family stories of coming from "the East"

2. **Identify exact location**: This is CRITICAL. You must find the specific village/town, not just a region.
   
   Sources for location identification:
   - Family documents (birth certificates, passports)
   - Oral history ("grandfather came from near Lwów")
   - DNA matches with specific locations
   - Immigration/repatriation documents
   
   For location name mapping, use:
   - Słownik geograficzny Królestwa Polskiego (on polona.pl)
   - JewishGen gazetteer
   - Kresy-Siberia village database

   After gathering location information:
   - Assess location confidence (Strong/Moderate/Speculative)
   - If Speculative: execute Location Feedback Loop before proceeding to step 3
   - Do not waste archive searches on unconfirmed locations

3. **Map location to modern country**:
   | Polish Region | Modern Country | Major City |
   |---------------|----------------|------------|
   | Wołyń | Ukraine | Łuck/Lutsk |
   | Podole | Ukraine | Tarnopol/Ternopil |
   | Galicja Wschodnia | Ukraine | Lwów/Lviv |
   | Polesie | Belarus | Brześć/Brest |
   | Nowogródczyzna | Belarus | Nowogródek/Navahrudak |
   | Wileńszczyzna | Lithuania | Wilno/Vilnius |

4. **Search Polish indexes first**:
   - Geneteka: check "Ukraina", "Białoruś", "Litwa" tabs
   - Coverage is limited but may have indexed records
   - Note which parishes have any coverage

5. **Search foreign archives**:
   
   **Ukraine (CDIAU Lviv)**:
   - Central State Historical Archive: http://archives.gov.ua
   - Holds Galician records
   - Some digitized on FamilySearch
   
   **Belarus (NIAB)**:
   - National Historical Archive: http://archives.gov.by
   - Request records by mail/email
   - Limited online access
   
   **Lithuania (LVIA)**:
   - Lithuanian State Historical Archives
   - Some records on epaveldas.lt
   
6. **Search for repatriation records**:
   If ancestor moved to Poland 1944-1946:
   - State Archives (Archiwa Państwowe): "Państwowy Urząd Repatriacyjny"
   - Lists of repatriates often include birthplace, family members
   
   Keywords to search:
   - "repatriacja" + location name
   - "przesiedlenie" (resettlement)
   - "PUR" (Państwowy Urząd Repatriacyjny)

7. **Check for deportation records** (if applicable):
   If family was deported to Siberia/Kazakhstan (1940-1941):
   - Indeks Represjonowanych (represjonowani.pl)
   - Ośrodek KARTA database
   - IPN (Instytut Pamięci Narodowej)
   
   See prompt `05-deportation-tracking.md` for detailed protocol.

8. **Create region note**: Use template at `[VAULT_PATH]/templates/region.md`:
   - Document the specific Kresy location
   - Map Polish/Ukrainian/Russian place names
   - Note which archives hold records
   - Track what has been searched

9. **Update person files**:
   - Add `origin: kresy` tag
   - Add exact birthplace (with all name variants)
   - Add foreign archive citations
   - Link to repatriation documents if found

10. **Log searches**: In Research_Log.md, record:
    - Locations searched
    - Archives checked
    - Negative results (important for future reference)
    - Language of records found

## Confidence Assessment

### Location Identification Confidence

**Strong Signal** (location confirmed):
- Exact village name from primary document (birth certificate, passport)
- Village exists in historical gazetteers (Słownik geograficzny)
- Unambiguous: only one village with that name in the region
- Parish records confirm the location

**Moderate Signal** (likely location):
- Location from secondary source (oral history matches one specific place)
- Village name common but context narrows to 2-3 possibilities
- Repatriation document mentions region but not exact village
- DNA matches cluster in one area

**Speculative** (location unclear):
- Only region known, not specific village
- Multiple villages with same name across Kresy
- Contradictory information from different sources
- Location name may have changed or village no longer exists

### Archive Matching Confidence

**Strong Signal**:
- Found actual record in foreign archive (CDIAU, NIAB, LVIA)
- Record matches ancestor on name, date, AND location
- Record language/format consistent with region

**Moderate Signal**:
- Found indexed reference but no image access
- Record matches on 2 of 3 identifiers
- Geneteka index entry for Kresy parish

**Speculative**:
- Only possible match (common name, approximate dates)
- Archive holdings unclear for that parish/period
- Record destroyed or inaccessible

## Feedback Loop

### For Speculative Locations:

DO NOT proceed to archive search until location is at least Moderate confidence.

**Loop iterations**:

1. **First attempt** - Gather more location clues:
   - Re-interview family members with specific questions
   - Search for siblings who may have clearer records
   - Check US naturalization records (post-1906 have exact birthplace)
   - Search passenger manifests for village name

2. **Second attempt** - Use geographic analysis:
   - Plot all known family locations on historical map
   - Check Słownik geograficzny for village descriptions
   - Use Mapa Nazwisk to find surname concentrations
   - Search for przydomek which may indicate specific village

3. **Third attempt** - DNA triangulation:
   - Identify DNA matches with known Kresy ancestry
   - Contact matches to compare locations
   - Look for surname clusters in match list

4. **After 3 attempts**: If still Speculative:
   - Log all gathered clues in Research_Log
   - Create hypothesis file with possible locations
   - Mark as "location pending - requires additional evidence"
   - Move to next ancestor

### For Speculative Archive Matches:

1. **Loop back with alternative searches**:
   - Try all spelling variants (Polish/Ukrainian/Russian/German)
   - Search broader date range (±15 years)
   - Search for parents or siblings instead
   - Check repatriation records for family group

2. **Attempt archive contact**:
   - Prepare formal request letter
   - Log request details and expected response time
   - Continue with other ancestors while waiting

3. **After 3 search attempts**: 
   - Log as "requires archive visit or professional researcher"
   - Note specific archive and fond where records should be
   - Calculate cost/effort for future planning

## Place Name Resources

- Słownik geograficzny Królestwa Polskiego: https://polona.pl/
- JewishGen Gazetteer: https://www.jewishgen.org/Communities/
- Mapa Kresy: http://www.mapywig.org/
- Kresy-Siberia Foundation: http://www.kresy-siberia.org/

## Common Challenges

1. **Village no longer exists**: Many small villages were destroyed in WWII or depopulated. Use historical maps.

2. **Multiple villages with same name**: Be very specific. "Michałówka" exists in many locations.

3. **Family scattered across countries**: After 1945, siblings may have ended up in Poland, USSR, and Western countries.

4. **Greek Catholic vs Roman Catholic**: In Kresy, many ethnic Poles were Greek Catholic (Uniate). Records are in different archives.
