# Polish Cemetery Search

Locate burial records and grave photos for every deceased ancestor using Polish cemetery databases.

## Autoresearch Configuration

**Goal**: For every deceased ancestor in `[VAULT_PATH]/Family_Tree.md`, search Polish cemetery databases to find their burial location and grave information.

**Metric**: Number of deceased ancestors without a burial/cemetery citation

**Direction**: Minimize (lower is better)

**Verify**: Count deceased ancestors in Family_Tree.md who lack a burial location or cemetery source. Report the percentage with burial information.

**Guard**:
- Not all cemeteries are indexed online. Local parish or cemetery office may have records not in databases.
- Some graves no longer exist (removed after lease expired, destroyed in wars).
- Photos may show wrong grave if names are common. Verify dates match.
- Historical cemeteries (pre-1900) often poorly documented.

**Iterations**: 8

**Protocol**:

1. **Identify targets**: From Family_Tree.md, list all deceased ancestors without burial information. Prioritize:
   - Deaths after 1900 (better documentation)
   - Deaths in Poland (not Kresy)
   - Ancestors with known death location

2. **Search BillionGraves Poland**:
   - URL: billiongraves.com/pl
   - Search by name and location
   - Photos of headstones with GPS coordinates
   - AI-readable results
   
3. **Search regional cemetery indexes**:
   
   **Pomorskie TG Cemetery Index** (ptg.gda.pl):
   - Pomeranian region cemeteries
   - Indexed headstone inscriptions
   
   **Grobonet** (grobonet.com):
   - Some Polish cities have searchable cemetery databases
   - Warsaw, Kraków, and others
   
   **Municipal cemetery websites**:
   - Many cities have their own cemetery search
   - Example: Cmentarz Powązkowski (Warsaw)
   - Search: "[City name] cmentarz wyszukiwarka"

4. **Search historical cemetery records**:
   
   **Geneteka death records**:
   - Death records often mention burial parish
   - Use to identify which cemetery to search
   
   **Parish death registers**:
   - May have burial location details
   - Especially for church-owned cemeteries

5. **Search for destroyed/moved cemeteries**:
   
   For ancestors who died in now-changed areas:
   - Jewish cemeteries (often destroyed in WWII): Virtual Shtetl, JRI-Poland
   - German cemeteries (removed after 1945): Genealogical Society of Pomerania
   - Historical cemeteries that no longer exist: local historical societies

6. **Extract data from found records**:
   - Full name on headstone
   - Birth and death dates
   - Cemetery name and section/row/plot
   - Photo of headstone (if available)
   - Other family members on same grave
   - GPS coordinates (if available)

7. **Cross-reference headstone data**:
   - Compare dates with vital records
   - Note discrepancies (headstone vs certificate)
   - Identify additional family members

8. **Update the vault**:
   - Add burial location to person file
   - Add cemetery citation with section/plot if known
   - Link headstone photo if available
   - Add any newly discovered relatives (often found on family graves)
   - Update Family_Tree.md with burial information

9. **For not-found ancestors**:
   - Record which databases were searched
   - Note likely cemetery based on death location
   - Consider: small village cemeteries rarely indexed
   - Action: may require physical visit or local inquiry

10. **Log searches**: In Research_Log.md, record:
    - Ancestor searched
    - Databases checked
    - Results (positive or negative)
    - Possible next steps for not-found

## Cemetery Database Coverage

| Region | Best Resources |
|--------|----------------|
| Pomorze | PTG cemetery index |
| Wielkopolska | BillionGraves, local municipal sites |
| Mazowsze | Grobonet (Warsaw), BillionGraves |
| Małopolska | BillionGraves, parish records |
| Śląsk | BillionGraves, local German-era records |

## Tips for Polish Cemeteries

- **Cemetery lease system**: In Poland, graves are leased for 20 years. Unpaid leases = grave removed. This is why some ancestors have no grave.

- **Family graves**: Polish tradition is multi-generational family graves. Finding one ancestor often reveals others.

- **Parish vs municipal**: Before 1950s, most cemeteries were parish-owned. Municipal cemeteries more common after.

- **War graves**: WWII victims often in mass graves or special memorial sections.

- **Regional naming**:
  - cmentarz parafialny (parish cemetery)
  - cmentarz komunalny (municipal cemetery)
  - cmentarz żydowski (Jewish cemetery)
  - cmentarz ewangelicki (Protestant cemetery)
