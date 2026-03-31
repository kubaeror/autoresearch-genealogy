# Tree Expansion (Polish Sources)

Push every branch of your family tree as far back as possible using Polish genealogy databases and archives.

## Autoresearch Configuration

**Goal**: For every ancestor currently in `[VAULT_PATH]/Family_Tree.md`, search Polish vital records databases (Geneteka, Szukaj w Archiwach, BaSIA) for their parents, siblings, spouses' families, and any additional generations. Update the vault after each discovery. Keep iterating until no more ancestors can be found through available Polish sources.

**Metric**: Number of new ancestors/individuals added to Family_Tree.md

**Direction**: Maximize

**Verify**: 
1. Count new individuals added by confidence tier
2. Count Moderate Signal items in verification queue
3. Count Speculative leads logged but not added
4. Report: "Added X ancestors (Y strong, Z moderate). W speculative leads pending. V items in verification queue."

**Guard**:
- Do not fabricate ancestors. Every addition must cite a source with archive reference (zespół, sygnatura, page number).
- Do not trust user-contributed trees (Geni, Ancestry hints) without corroboration from at least one indexed record or original image.
- Do not modify existing dates or names during expansion; that is the cross-reference audit's job.
- Mark any unverified additions with `(unverified)` in the tree.
- Coverage varies significantly by voivodeship: Wielkopolska and Małopolska have excellent coverage; eastern regions (Podlasie, Lubelszczyzna) have gaps.
- Different partitions produced records in different languages: Russian partition (Russian/Polish), Prussian partition (German/Latin), Austrian partition (Latin/German/Polish). Verify you are reading the correct language.
- Szlachta (nobility) claims require armorial verification through Boniecki, Uruski, or Złota Księga Szlachty Polskiej. Do not assume nobility without documented proof.
- Do not add Speculative ancestors to the tree. Log them for future research.
- Do not expand from Moderate Signal ancestors until verification attempted.
- Prioritize depth on Strong Signal lines over breadth on uncertain lines.

**Iterations**: 8

**Protocol**:

1. **Baseline**: Read `[VAULT_PATH]/Family_Tree.md` completely. Count every named individual. Record this as the baseline in `[VAULT_PATH]/Research_Log.md`.

2. **Identify expansion targets**: For each leaf node (an ancestor with no listed parents), note:
   - Name, dates, and parish (parafia)
   - Which partition the location was in (Russian, Prussian, Austrian)
   - Which databases cover that parish (Geneteka, BaSIA, Gesher Galicia, regional archives)

3. **Search strategy per ancestor**: For each target, search databases in this order:

   a. **Geneteka** (geneteka.genealodzy.pl): Search by surname and parish for births (urodzenia), marriages (małżeństwa), deaths (zgony). Check the "Inne" column for indexed parent names.
   
   b. **Szukaj w Archiwach** (szukajwarchiwach.gov.pl): Search for original scans by parish name. Navigate to Akta stanu cywilnego or Księgi metrykalne. Locate the specific year and record number from Geneteka.
   
   c. **BaSIA** (basia.famula.pl): For Wielkopolska (Poznań, Gniezno, Kalisz regions), search the Archiwum Państwowe w Poznaniu indexes. Provides direct links to images.
   
   d. **Gesher Galicia** (search.geshergalicia.org): For families from Austrian Galicia (Kraków, Lwów, Tarnów, Rzeszów). Search cadastral and vital record indexes.
   
   e. **Metryki.genealodzy.pl**: For older digitized parish records not yet in Geneteka.
   
   f. **Mapa Nazwisk** (mapa.nazwiska-polskie.pl): Search surname distribution to identify potential origin parishes if location is unknown.

4. **Evaluate results**: For each search hit:
   - Does the person match on name, dates, AND parish? All three must align.
   - Is the source an original register image or a transcription index? Verify transcriptions against originals when possible.
   - Note the archive reference: Archiwum (e.g., AP Poznań), zespół number, sygnatura, and page/act number.
   - Assess confidence tier for each potential new ancestor
   - If Speculative: execute Verification Loop before proceeding
   - Only add Strong or Moderate Signal ancestors to tree

5. **Update the vault**: For each confirmed new ancestor:
   - Add to Family_Tree.md in the correct position
   - If sufficient data exists, create a person file using the template at `[VAULT_PATH]/templates/person.md`
   - Note the source in the person file's Document Sources section with full archive reference

6. **Log the search**: In `[VAULT_PATH]/Research_Log.md`, record:
   - Date and search target
   - Databases and parishes searched
   - Results (positive or negative, including "parish not indexed in Geneteka")
   - New individuals added (if any)
   - What remains unresolved

7. **Update the count**: After each iteration, recount named individuals in Family_Tree.md. Report the delta.

8. **Repeat**: Move to the next set of expansion targets. Prioritize:
   - Lines with the fewest known generations (shallowest branches)
   - Ancestors from well-indexed parishes (check Geneteka coverage maps)
   - Lines with no person files yet (lowest current documentation)

## Tips

- **Przydomki**: Some Polish families (especially szlachta) used przydomki, distinguishing names added to differentiate branches of the same family. Kowalski might be "Kowalski z Dębna" or "Kowalski Wąż." These matter for accurate identification.

- **Partition-era spelling variations**: The same surname was often recorded differently across partitions:
  - Prussian records: Germanized spellings (Kowalski → Kowalsky, Szczepański → Schtschepanski)
  - Russian records: Cyrillic transliteration (Kowalski → Ковальский, then re-Romanized inconsistently)
  - Austrian records: Generally preserved Polish spelling but with Latin case endings

- **Grammatical cases for surnames**: Polish surnames decline by grammatical case. In records, you will see:
  - Nominative: Jan Kowalski (subject)
  - Genitive: syna Jana Kowalskiego ("son of Jan Kowalski")
  - Instrumental: z Anną Kowalską ("with Anna Kowalska")
  - The root surname is what matters; strip the case endings when recording.

- **Female surname forms**: Polish surnames have masculine and feminine forms. Kowalski (m) → Kowalska (f). Married women often used the masculine genitive: "Kowalskiego" (wife of Kowalski) or "Kowalszczyna" (older form).

- **Negative results matter**: If you search for an ancestor and find nothing, log it. This prevents duplicate searches later and helps identify coverage gaps.

- **Sibling research**: Finding siblings is often easier than finding parents directly. Search for marriages of potential siblings; marriage records list parents of both spouses.

- **Witnesses and godparents**: Polish vital records include witnesses (świadkowie) and godparents (rodzice chrzestni). These are often relatives. Note them for cross-reference.

## Confidence Assessment

### New Ancestor Confidence

**Strong Signal** (add to tree immediately):
- Primary source confirms relationship (birth record names parents)
- Multiple independent sources agree
- Name, date, AND location all consistent with known data
- No contradictions with existing tree

**Moderate Signal** (add with verification flag):
- Single primary source without corroboration
- Secondary source (index, database) without original image
- Two of three identifiers match
- Minor discrepancies explainable

**Speculative** (do not add yet):
- Only tertiary source (user tree, oral history)
- Common surname without distinguishing details
- Dates or locations inconsistent
- Single uncorroborated mention

### Verification Requirements by Tier

| Addition Type | Strong Signal | Moderate Signal | Speculative |
|--------------|---------------|-----------------|-------------|
| Parents | Add immediately | Add + queue birth record search | Loop: find birth/marriage record first |
| Siblings | Add immediately | Add + cross-check parent names | Loop: verify same parents |
| Spouse | Add immediately | Add + find marriage record | Loop: find marriage record first |
| Children | Add immediately | Add + queue birth records | Loop: verify parentage |

## Feedback Loop

### Before Adding Any Ancestor:

1. **Assess confidence** using criteria above

2. **If Strong Signal**:
   - Add to Family_Tree.md
   - Create person file with confidence: high
   - Continue expansion from this ancestor

3. **If Moderate Signal**:
   - Add to Family_Tree.md with `(unverified)` 
   - Create person file with confidence: moderate
   - Add to verification queue in Research_Log.md
   - Continue expansion BUT flag descendants as dependent on verification

4. **If Speculative**:
   - DO NOT add to tree yet
   - Log in Research_Log.md under "Potential Ancestors (Unconfirmed)"
   - **Execute verification loop**:

### Verification Loop for Speculative Ancestors:

**Attempt 1**: Search for primary source
- Search Geneteka for birth record
- Search for marriage record naming parents
- Search Szukaj w Archiwach for original images

**Attempt 2**: Search for corroborating evidence
- Search for sibling births (do they name same parents?)
- Search for parent's death record (does it name children?)
- Search for parent's marriage record

**Attempt 3**: Indirect verification
- Search witness lists (family often witnessed each other's events)
- Check if location and timeframe are plausible
- Compare with DNA matches' trees

**After 3 attempts**:
- If elevated to Moderate: add with flag
- If still Speculative: do NOT add, log reasoning
- Move to next expansion target

### Post-Addition Verification Queue

After each iteration, process verification queue:

1. List all Moderate Signal ancestors added this session
2. For each, attempt ONE verification search
3. If verified → update to Strong Signal
4. If contradicted → investigate discrepancy
5. If no new evidence → keep as Moderate, move to next

Spend maximum 20% of iteration time on verification queue.
