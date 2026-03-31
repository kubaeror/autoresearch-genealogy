# Szukaj w Archiwach Navigation Workflow

A step-by-step guide to navigating Szukaj w Archiwach (szukajwarchiwach.gov.pl) to find and view original record images.

## What is Szukaj w Archiwach?

Szukaj w Archiwach (Search in Archives) is the Polish state archives' portal for digitized records. Unlike Geneteka (an index), this contains ORIGINAL SCANNED IMAGES of vital records, church registers, and other archival materials.

**URL**: https://www.szukajwarchiwach.gov.pl/

## When to Use This

- After finding a record in Geneteka, to view the original image
- To browse records for a parish not indexed in Geneteka
- To find alegata (marriage supplements)
- To search for records beyond vital records (land, court, military)

## Step 1: Access the Portal

1. Go to: https://www.szukajwarchiwach.gov.pl/
2. Interface is in Polish (English version limited)

## Step 2: Understand the Structure

Archives are organized hierarchically:

```
Archiwum (Archive)
└── Zespół (Fond/Collection)
    └── Seria (Series)
        └── Jednostka (Unit/Item)
            └── Skan (Scan/Image)
```

### Key Archives for Vital Records

| Archive | Abbreviation | Coverage |
|---------|--------------|----------|
| AP Łódź | APŁ | łódzkie voivodeship |
| AP Lublin | APL | lubelskie voivodeship |
| AP Warszawa | APW | mazowieckie, Warszawa |
| AP Kraków | APK | małopolskie |
| AP Poznań | APP | wielkopolskie |
| AP Gdańsk | APG | pomorskie |
| AP Wrocław | APWr | dolnośląskie |
| AP Przemyśl | APPrz | podkarpackie |

## Step 3: Search Methods

### Method A: Direct Search

1. Use the search bar (Szukaj)
2. Enter parish name (e.g., "Łódź parafia")
3. Filter by archive if known

### Method B: Browse by Archive

1. Click "Archiwa" (Archives)
2. Select the relevant state archive
3. Browse zespoły (fonds)

### Method C: Use Geneteka Reference

When Geneteka gives you a citation like:
```
AP Lublin, zespół 35/1234/0, sygn. 5, s. 67
```

Parse it:
- AP Lublin = Archive
- zespół 35/1234/0 = Fond number
- sygn. 5 = Signature (unit)
- s. 67 = Page (strona) 67

## Step 4: Navigate to Parish Records

### Finding Vital Records (Akta stanu cywilnego)

1. In the archive, look for zespoły named:
   - "Akta stanu cywilnego" (civil registration)
   - "USC [Parish name]" (Urząd Stanu Cywilnego)
   - "Akta metrykalne" (metric records)

2. Within the zespół, units are usually organized by:
   - Year
   - Record type (urodzenia, małżeństwa, zgony)

### Finding Parish Registers (Księgi metrykalne)

1. Look for zespoły named:
   - "Księgi metrykalne parafii [Name]"
   - "Akta parafii [Name]"
   - Under the relevant diocese collection

## Step 5: View Scans

1. Navigate to the specific unit (jednostka)
2. Click on "Skany" or the scan icon
3. Images open in a viewer

### Viewer Controls

- Zoom in/out
- Download individual pages (some archives allow)
- Navigate between pages

## Step 6: Find Specific Records

### By Act Number

If Geneteka says "act 45, year 1875":

1. Navigate to the unit for 1875
2. Records are usually in chronological order
3. Look for act number 45 (numer aktu 45)

### By Browsing

If you don't have an act number:

1. Go to the year you need
2. Birth records (urodzenia) are usually in one unit
3. Browse page by page
4. Records are chronological by date

## Step 7: Reading Record References

### Zespół (Fond) Numbering

Example: `35/1234/0`
- 35 = Archive internal number
- 1234 = Collection number
- 0 = Sub-collection

### Sygnatura (Signature)

The specific unit within the fond. Usually corresponds to a year or date range.

### Citation Format

When you find a record, cite it as:
```
[Archive name], zespół [number], sygnatura [number], strona [page]
```

Example:
```
AP Lublin, z. 35/1234/0, sygn. 5, s. 67
```

## Step 8: Find Alegata (Marriage Supplements)

Alegata are attached documents (birth certificates, etc.) included with marriage records.

1. In the marriage year's unit, look for a separate alegata section
2. OR look for a separate "Alegata" unit for that year
3. Alegata are usually numbered to match the marriage act number

**Why alegata matter**: They often contain birth certificate copies that may be the ONLY surviving record of a birth.

## Tips for Effective Searching

### Coverage Gaps

Not all records are digitized. If you can't find something:
- Records may exist but not be scanned
- Try contacting the archive directly
- Check Metryki.genealodzy.pl (different digitization project)

### Language by Era

| Era | Expect |
|-----|--------|
| Pre-1795 | Latin/Polish |
| 1795-1867 (Russian) | Polish |
| 1868-1918 (Russian) | Russian (Cyrillic) |
| 1795-1918 (Prussian) | German |
| 1795-1918 (Austrian) | Latin/German/Polish |
| Post-1918 | Polish |

### Image Quality

- Some scans are low quality (old microfilm)
- Try adjusting brightness/contrast
- For difficult records, see `workflows/ocr-pipeline.md`

## Common Issues

### "Brak skanów" (No Scans)

The record exists but isn't digitized. Options:
- Visit the archive in person
- Request a remote copy (paid service)
- Check if available on Metryki.genealodzy.pl

### Wrong Archive

Not sure which archive holds records? 
- Check PRADZIAD database for archive locations
- Records were transferred between archives

### Damaged/Missing Records

Some records were destroyed in WWII or earlier. If a year is missing:
- Check if alegata survive for that period
- Look for census records (rewizje) as alternatives
- Check if another parish covered the area

## Companion Resources

- `workflows/geneteka-search.md`: How to find index entries first
- `workflows/ocr-pipeline.md`: How to read difficult documents
- `reference/glossary.md`: Polish/Latin/Russian/German term translations
