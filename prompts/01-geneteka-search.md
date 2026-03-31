# Geneteka Search

Systematically search Geneteka (geneteka.genealodzy.pl) for every ancestor in your family tree.

## Autoresearch Configuration

**Goal**: For every ancestor in `[VAULT_PATH]/Family_Tree.md`, search Geneteka for their vital records (birth, marriage, death) and any records mentioning them as parents, witnesses, or other roles.

**Metric**: Number of ancestors with at least one Geneteka citation

**Direction**: Maximize

**Verify**: 
1. Count ancestors in Family_Tree.md with Geneteka citations
2. Count citations by confidence tier (high/moderate/speculative logged)
3. Report: "X ancestors sourced (Y strong, Z moderate, W speculative leads pending)"

**Guard**:
- Geneteka is an index, not the original record. Always note that verification against original images (Szukaj w Archiwach, Metryki) is recommended.
- Common surnames (Kowalski, Nowak, Wiśniewski) may return thousands of results. Use spouse names and specific parishes to narrow.
- Do not assume all records for a parish are indexed. Coverage varies significantly.
- Record negative results: if a parish has no Geneteka coverage, note this to avoid repeated searches.

**Iterations**: 10

**Protocol**:

1. **Baseline**: Read `[VAULT_PATH]/Family_Tree.md`. List every ancestor with their:
   - Full name (including surname variants, przydomek if known)
   - Approximate birth year (or range)
   - Parish or location (if known)
   - Voivodeship (województwo) if identifiable

2. **Prioritize targets**:
   - Ancestors with no Geneteka citation yet
   - Ancestors with specific location information
   - Lines with the least documentation

3. **Search strategy per ancestor**:
   a. Go to geneteka.genealodzy.pl
   b. Select the voivodeship (or "All voivodeships" if unknown)
   c. Enter surname in primary search field
   d. If searching for a married woman, enter maiden name in "Surname 2" or search under husband's surname
   e. Set date range (±10 years from estimated dates)
   f. Search births (B), marriages (M), deaths (D) separately

4. **Handle common surnames**:
   - For very common names, ALWAYS filter by:
     - Specific parish
     - Spouse's surname (for marriages)
     - Parent's name (for births)
   - Use the "Remarks" field results to find additional family connections

5. **Extract data from results**:
   - Record: Year, Parish, Act Number, Names, Date
   - Note the archive reference (e.g., "AP Lublin, zespół 35, sygn. 456")
   - Copy any remarks (uwagi) which may mention parents, witnesses
   - Assign preliminary confidence tier (Strong/Moderate/Speculative)
   - If Speculative, DO NOT proceed to step 7 yet: execute Feedback Loop first

6. **Cross-reference spouses and parents**:
   - When you find a marriage, search for birth records of both spouses
   - Search for children's births using parents' names
   - Search for deaths of parents mentioned in marriage records

7. **Update the vault**:
   - Add Geneteka citation to person files
   - Format: "Geneteka: [Parish], [Year], act [number], [event type]"
   - Note if image is available on Szukaj w Archiwach or Metryki
   - Add newly discovered family members to Family_Tree.md
   - Set confidence field based on assessment
   - For Moderate Signal: add `(unverified)` to the entry
   - For Speculative: do not add; log in Research_Log.md instead

8. **Log searches**: In `[VAULT_PATH]/Research_Log.md` record:
   - Date
   - Ancestor searched
   - Voivodeships and parishes checked
   - Results (positive or negative)
   - Parishes with no coverage (to avoid re-searching)

9. **Iterate**: Move to next ancestor. Prioritize newly discovered relatives.

## Confidence Assessment

After finding a record in Geneteka, assess confidence before adding to vault:

### Strong Signal (add immediately)
- Name matches exactly (allowing for grammatical endings: -ski/-skiego/-skiemu)
- Date within ±2 years of expected
- Parish matches known family location
- At least one corroborating detail (parent name, spouse name, witness)

### Moderate Signal (add with flag)
- Name matches with minor spelling variation
- Date within ±5 years of expected  
- Parish in same powiat/region as known location
- No corroborating details but no contradictions

### Speculative (requires more research before adding)
- Common surname with no distinguishing details
- Date off by more than 5 years
- Different parish with no known connection
- Contradicts existing information

## Feedback Loop

For each search result:

1. **Assess confidence** using the tiers above

2. **If Strong Signal**: 
   - Add to vault immediately
   - Mark confidence: high in person file
   - Continue to next ancestor

3. **If Moderate Signal**:
   - Add to vault with `(unverified)` tag
   - Mark confidence: moderate in person file
   - Queue for verification: search for corroborating record (marriage → find birth, birth → find siblings)
   - Continue to next ancestor

4. **If Speculative**:
   - DO NOT add to vault yet
   - Log the potential match in Research_Log.md under "Unconfirmed Leads"
   - **Loop back**: Try alternative search strategies:
     a. Search with przydomek if known
     b. Search spouse's surname to find marriage
     c. Search neighboring parishes (±20km)
     d. Widen date range by 10 years
     e. Try phonetic variants of surname
   - After exhausting alternatives, if still Speculative, log as "requires original image verification"

5. **Verification sub-loop** (for Moderate Signal items):
   - After each iteration, check for Moderate Signal items needing verification
   - Spend up to 2 search attempts per item trying to elevate to Strong Signal
   - If successful, update confidence to high
   - If unsuccessful after 2 attempts, keep as moderate and move on

## Surname Variant Strategies

When searching, try:
- Base form and grammatical variants (Kowalski, Kowalskiego, Kowalskim)
- With and without przydomek
- Common spelling variants:
  - rz/ż interchange (Rzeszowski / Żeszowski)
  - ó/u interchange (Góra / Gura)
  - w/v interchange (Kowalski / Kovalski)
  - doubled letters (Krasiński / Krassinski)

## Coverage Notes

Geneteka coverage varies dramatically by voivodeship:
- Best: łódzkie (9.7M), mazowieckie (12M), małopolskie (6.7M)
- Good: śląskie (6.3M), świętokrzyskie (4.9M), podkarpackie (4.2M)
- Limited: dolnośląskie (52K), lubuskie (10K), zachodniopomorskie (5K)

Check coverage before concluding a search is complete.
