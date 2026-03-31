# OCR Pipeline for Polish Genealogical Documents

How to convert scanned Polish genealogical documents into structured, searchable vault notes. This guide covers the three major script types encountered in Polish records: Latin, Cyrillic (Russian), and Gothic/Kurrent (German).

## Introduction

### Document Types in Polish Genealogy

Polish genealogical research involves several document categories:

| Document Type | Period | Typical Language/Script |
|---|---|---|
| Roman Catholic parish records | 1600s–present | Latin (entries), Polish (annotations) |
| Civil registration (Russian partition) | 1808–1825 | Polish, then Latin |
| Civil registration (Russian partition) | 1868–1918 | Russian Cyrillic |
| Civil registration (Congress Poland) | 1826–1867 | Polish/Latin |
| Evangelical/Lutheran records | 1700s–1940s | German (Gothic/Kurrent) |
| Prussian civil records | 1874–1918 | German (Gothic/Kurrent) |
| Austrian/Galician records | 1784–1918 | Latin, German, Polish |
| Jewish records (various) | varies | Hebrew, Yiddish, Polish, Russian, German |

### Languages and Scripts Encountered

| Script | Where Used | Difficulty |
|---|---|---|
| **Latin script (Polish)** | Church records, Austrian partition, modern | Standard |
| **Latin script (Latin language)** | Church records (sacramental formulas) | Requires Latin vocabulary |
| **Cyrillic script (Russian)** | Russian partition civil records 1868–1918 | Moderate |
| **Gothic/Kurrent script** | Prussian and German records | Difficult |
| **Hebrew script** | Jewish religious records | Specialized |

---

## Script Types

### Latin Script (Polish and Latin)

**Where found**: Most Polish church records, Austrian partition civil records, and all modern Polish records.

**Characteristics**:
- Church records often use Latin for sacramental formulas with Polish for names and places
- Handwriting styles vary by era and priest
- Standard OCR tools work well for printed documents
- Watch for diacritics: ą, ć, ę, ł, ń, ó, ś, ź, ż

**Common patterns**:
- Birth records begin with "Anno Domini..." or "Roku Pańskiego..."
- Names appear in Latin declensions (Joannes, Josephus, Maria)
- Dates use Latin month names or Roman numerals

**OCR approach**: Standard tools (Tesseract with Polish language pack, Google Vision, Claude multimodal) all work well.

### Cyrillic Script (Russian)

**Where found**: Russian partition civil registration (akta stanu cywilnego) from 1868–1918. Covers Congress Poland, including Warsaw, Łódź, Lublin, and surrounding areas.

**Characteristics**:
- May be handwritten (most common) or printed (index books)
- Pre-1918 Russian uses the old orthography with ъ, і, ѣ, and ѳ
- Polish names are transliterated phonetically into Cyrillic
- Place names may be Russified (Варшава for Warszawa)

**Reading tips**:
- Learn the Cyrillic alphabet (33 letters)
- Polish names follow phonetic rules: "ł" becomes "л", "w" becomes "в"
- Dates use the Julian calendar (12–13 days behind Gregorian until 1918)
- Numbers may be written out in Russian words

**OCR approach**: Claude multimodal handles both printed and handwritten Cyrillic well. Google Vision works for printed text. Handwritten requires careful verification.

### Gothic/Kurrent Script (German)

**Where found**: Prussian partition records (Pomerania, Silesia, Greater Poland, Warmia, Masuria), German Lutheran church records, and any German administrative documents.

**Characteristics**:
- Kurrent is a cursive form of Gothic script used until ~1941
- Letters look very different from modern Latin script
- Easy to confuse similar letters (see reference table below)
- Mixed usage: proper nouns sometimes in Latin script, body text in Kurrent

**Major confusions**:
- "e" looks like "n" in Latin script
- "n" looks like a series of vertical strokes
- "s" has multiple forms (long s, round s, sz ligature)
- "f" and long "s" are nearly identical
- Capital letters are highly ornate

**OCR approach**: Automated OCR rarely works. Use Transkribus with trained models, or manual transcription with Kurrent reading guides.

---

## OCR Tools

### Tools by Script Type

| Script | Primary Tool | Secondary Tool | Notes |
|---|---|---|---|
| Latin (printed) | Tesseract, Google Vision | Claude multimodal | Use `-l pol` for Polish |
| Latin (handwritten) | Claude multimodal | Transkribus | Context helps Claude |
| Cyrillic (printed) | Google Vision, Tesseract | Claude multimodal | Use `-l rus` for Russian |
| Cyrillic (handwritten) | Claude multimodal | Manual | Old orthography may confuse Tesseract |
| Gothic/Kurrent | Transkribus | Manual | Requires trained HTR models |

### Tool Details

**Tesseract**

```bash
# Polish language pack
tesseract input.jpg output -l pol

# Russian language pack (for Cyrillic)
tesseract input.jpg output -l rus

# Multiple languages (Polish names in Russian text)
tesseract input.jpg output -l rus+pol
```

Install language packs:
```bash
# macOS
brew install tesseract-lang

# Linux (Debian/Ubuntu)
apt install tesseract-ocr-pol tesseract-ocr-rus
```

**Claude Multimodal**

Best for handwritten documents in any script. Provide context for better results:

```
Read the file at [VAULT_PATH]/sources/birth_record_1895.jpg

This is a Russian-language birth record from Congress Poland, circa 1895.
It will be written in Cyrillic script using pre-revolutionary orthography.
Transcribe all text, preserving the Cyrillic characters.
Mark illegible portions with [unclear].
Note any Polish names and provide their likely Polish spelling.
```

For Kurrent:
```
Read the file at [VAULT_PATH]/sources/prussian_death_1890.jpg

This is a German death record from Prussian Poland, written in Kurrent script.
Transcribe what you can read, but note that Kurrent is very difficult.
Mark uncertain readings with [?] and illegible portions with [unclear].
Provide the German text, then a translation if possible.
```

**Transkribus**

For Gothic/Kurrent, Transkribus offers trained Handwritten Text Recognition (HTR) models:

1. Create a free account at transkribus.eu
2. Upload document images
3. Select an appropriate model (search for "Kurrent", "German", or "19th century")
4. Run recognition and export results
5. Manually verify output (models are imperfect)

Useful models for Polish research:
- German Kurrent 19th/20th century models
- Austrian administrative hand models
- Generic 19th century German models

**Google Vision API**

Works well for printed text in Polish, Russian, and German. Less effective for handwriting.

```bash
# Using gcloud CLI
gcloud ml vision detect-text input.jpg --language-hints=pl,ru
```

---

## Workflow Steps

### Step 1: Identify the Script Type

Before OCR, determine what you are looking at:

| Clue | Likely Script |
|---|---|
| Rounded letters, familiar Latin alphabet | Latin (Polish or Latin language) |
| Angular letters with unfamiliar shapes (б, ж, ц, ш, щ) | Cyrillic (Russian) |
| Sharp, angular, interconnected strokes | Gothic/Kurrent (German) |
| Document from Prussian regions (Posen, Silesia, Pomerania) | Likely Gothic/Kurrent |
| Document from Congress Poland 1868–1918 | Likely Cyrillic |
| Church record with "Anno Domini" | Latin script, Latin language |

### Step 2: Choose Appropriate Tool

| Script + Quality | Tool Choice |
|---|---|
| Latin, printed, clear | Tesseract (`-l pol`) |
| Latin, handwritten | Claude multimodal |
| Cyrillic, printed | Google Vision or Tesseract (`-l rus`) |
| Cyrillic, handwritten | Claude multimodal |
| Gothic/Kurrent, any | Transkribus, then manual verification |
| Mixed or unclear | Claude multimodal with detailed context |

### Step 3: Perform Initial Transcription

**For Latin/Polish (Tesseract)**:
```bash
# Preprocess if needed
convert input.jpg -colorspace Gray -normalize -sharpen 0x1 preprocessed.jpg

# OCR with Polish
tesseract preprocessed.jpg output -l pol
```

**For Cyrillic (Claude)**:
```
Transcribe the Russian text in [image]. This is a civil birth record from 1892.
Preserve the original Cyrillic spelling including old orthography (ъ, і, ѣ).
After the transcription, provide:
1. Polish versions of any personal names
2. Modern Russian transliteration if helpful
3. English translation of key details
```

**For Gothic/Kurrent**:
1. Upload to Transkribus
2. Run HTR with appropriate model
3. Export and review every line manually

### Step 4: Verify Against Known Patterns

Cross-check OCR output against expected content:

**For birth records**, expect:
- Date and place of birth
- Child's name and sex
- Parents' names, ages, occupations, residence
- Witnesses' names
- Priest or registrar name

**For death records**, expect:
- Date and place of death
- Deceased's name, age, occupation
- Cause of death (sometimes)
- Surviving family mentioned
- Informant's name

**For marriage records**, expect:
- Date and place of marriage
- Bride and groom names, ages, residence
- Parents of both parties
- Witnesses (often four)
- Banns publication dates

### Step 5: Create Transcription Note in Vault

Use the transcription template with complete metadata:

```markdown
---
type: transcription
source: sources/birth_1892_kowalski.jpg
document_type: birth_record
person: "[[Jan_Kowalski]]"
date: 1892-03-15
ocr_method: claude_multimodal
ocr_quality: Partial
language: Russian
script: Cyrillic
created: [DATE]
tags:
  - transcription
  - russian-partition
  - birth
---

# Transcription: Jan Kowalski Birth Record (1892)

## Original Text (Cyrillic)

Года тысяча восемьсот девяносто второго, марта пятнадцатого дня...
[continue transcription]

## Transliteration

Goda tysyacha vosemʹsot devyanosto vtorogo, marta pyatnadtsatogo dnya...

## Translation

In the year one thousand eight hundred ninety-two, on the fifteenth day of March...

## Extracted Facts

| Fact | Value | Confidence |
|---|---|---|
| Birth date | 15 March 1892 (Julian) / 27 March 1892 (Gregorian) | Strong Signal |
| Birth place | [Village], [Parish] | Strong Signal |
| Child's name | Jan Kowalski | Strong Signal |
| Father | Wojciech Kowalski, age 32, farmer | Strong Signal |
| Mother | Anna née Nowak | Strong Signal |
| Witnesses | [Names] | Moderate Signal |

## Notes

- Document is in fair condition with some fading in margins
- Date is Julian calendar; Gregorian equivalent noted above
- Father's occupation given as "крестьянинъ" (peasant farmer)
```

---

## Quality Assessment

### OCR Quality Grades

| Grade | Definition | When to Use |
|---|---|---|
| **Good** | 95%+ accurate, all key data readable | Proceed with confidence |
| **Partial** | 70–95% accurate, some gaps or uncertain readings | Mark uncertain portions, extract available data |
| **Poor** | <70% accurate, significant gaps | Re-attempt with different tool; flag for expert review |
| **Failed** | OCR produced garbage or no usable text | Document may require manual transcription |

### When to Mark as Uncertain

Use `[unclear]` when:
- Text is physically illegible (faded, damaged, obscured)
- OCR produces nonsense characters
- You cannot determine the intended word

Use `[?]` after a word when:
- You have a guess but are not confident
- The reading is plausible but not certain
- Context suggests a word but script is ambiguous

Example:
```
Марта [unclear] дня въ селѣ Камень[?] родился младенецъ...
```

### Verification Techniques

1. **Cross-reference with indexes**: Many archives have typed or printed indexes; compare names and dates
2. **Check neighboring records**: Same registrar, same handwriting; patterns become recognizable
3. **Validate against known facts**: Does the information match what you already know about the family?
4. **Consult language resources**: If a word seems wrong, check dictionaries for the language and era

---

## Common Challenges

### Multi-Script Documents

Some documents contain multiple scripts:

| Pattern | Example | Approach |
|---|---|---|
| Latin headings, Cyrillic body | Russian-era printed forms | OCR headings separately; use Russian model for body |
| Kurrent body, Latin names | German records with Polish names | Note which portions are Latin script |
| Mixed Polish/Latin | Church records | Single OCR pass usually works; Latin phrases are formulaic |

For mixed documents, process in layers:
1. Identify which portions use which script
2. OCR each portion with the appropriate tool
3. Combine results in the transcription note
4. Note the script switches in your documentation

### Low Quality Scans

**Old microfilm**:
- Often low contrast, grainy
- Preprocess with ImageMagick: `convert input.jpg -normalize -sharpen 0x2 output.jpg`
- Claude multimodal often outperforms Tesseract on poor scans

**Damaged originals**:
- Water damage, tears, fading
- Document visible damage in your notes
- Transcribe what is readable; mark damaged portions

**Bound volumes with gutter shadow**:
- Text near binding may be curved or dark
- Request re-scan if critical information is lost
- Note in transcription which portions were affected

**Enhancement workflow**:
```bash
# Increase contrast
convert input.jpg -normalize -level 10%,90% enhanced.jpg

# Sharpen blurry text
convert input.jpg -sharpen 0x2 sharpened.jpg

# Remove background noise
convert input.jpg -morphology Open Square:1 cleaned.jpg

# Combined preprocessing
convert input.jpg -colorspace Gray -normalize -sharpen 0x1.5 -level 5%,95% final.jpg
```

### Abbreviations

**Latin abbreviations in church records**:

| Abbreviation | Expansion | Meaning |
|---|---|---|
| bapt. | baptizatus/baptizata | baptized |
| n. / nat. | natus/nata | born |
| ob. / obt. | obiit | died |
| sep. | sepultus/sepulta | buried |
| c. / conj. | conjuges | spouses |
| fil. / f. | filius/filia | son/daughter |
| leg. | legitimus/legitima | legitimate |
| ill. / illeg. | illegitimus | illegitimate |
| vid. | vidua/viduus | widow/widower |
| d. / dn. / dns. | dominus | lord, master, Mr. |
| p.d. | praenobilis dominus | noble lord |
| lab. | laborator | laborer |
| agr. | agricola | farmer |
| fab. | faber | smith |
| ss. / suprascr. | suprascriptus | above-written |
| ejusd. | ejusdem | of the same |
| test. | testes | witnesses |
| patr. | patrini | godparents |
| matr. | matrina | godmother |
| l.s. | locus sigilli | place of seal |

**Russian abbreviations**:

| Abbreviation | Expansion | Meaning |
|---|---|---|
| г. | год / года | year |
| м. | месяц | month |
| д. | день | day |
| с. | село | village |
| у. | уезд | district |
| губ. | губерния | province |
| кр. | крестьянин | peasant |
| мещ. | мещанин | townsman |

**Expanding abbreviations**:
- Familiarize yourself with common patterns for your document type
- Check reference guides for the language and era
- When uncertain, transcribe the abbreviation as-is and note the expansion in brackets

---

## Reference Tables

### Cyrillic Alphabet with Polish Equivalents

For reading Polish names in Russian documents:

| Cyrillic | Sound | Polish Equivalent | Example |
|---|---|---|---|
| А а | a | a | Анна = Anna |
| Б б | b | b | Богданъ = Bogdan |
| В в | v | w | Владиславъ = Władysław |
| Г г | g | g, h | Григорій = Grzegorz |
| Д д | d | d | Дмитрій = Dymitr |
| Е е | ye/e | e, ie | Еленa = Helena |
| Ж ж | zh | ż | Жигмундъ = Zygmunt |
| З з | z | z | Зофія = Zofia |
| И и | i | i, y | Иванъ = Jan |
| Й й | y | j | (combining) |
| К к | k | k | Катерина = Katarzyna |
| Л л | l | l, ł | Людвикъ = Ludwik |
| М м | m | m | Маріанна = Marianna |
| Н н | n | n | Николай = Mikołaj |
| О о | o | o | Осипъ = Józef |
| П п | p | p | Павелъ = Paweł |
| Р р | r | r | Розалія = Rozalia |
| С с | s | s | Станиславъ = Stanisław |
| Т т | t | t | Теодоръ = Teodor |
| У у | u | u | Урсула = Urszula |
| Ф ф | f | f | Францишекъ = Franciszek |
| Х х | kh | ch | Христина = Krystyna |
| Ц ц | ts | c | Цецилія = Cecylia |
| Ч ч | ch | cz | Чеславъ = Czesław |
| Ш ш | sh | sz | — |
| Щ щ | shch | szcz | — |
| Ъ ъ | (hard sign) | — | (silent, old orthography) |
| Ы ы | y | y | — |
| Ь ь | (soft sign) | ś, ć, ń, etc. | — |
| Ѣ ѣ | ye | ie | (old orthography) |
| Э э | e | e | — |
| Ю ю | yu | ju | Юзефъ = Józef |
| Я я | ya | ja | Янъ = Jan |
| І і | i | i | (old orthography) |
| Ѳ ѳ | f/th | f, t | Ѳома = Tomasz (old orth.) |

### Polish Name Equivalents in Russian Records

| Russian Form | Polish Equivalent |
|---|---|
| Антоній / Антонъ | Antoni |
| Войцехъ / Войтехъ | Wojciech |
| Иванъ / Янъ | Jan |
| Іосифъ / Осипъ | Józef |
| Казимиръ | Kazimierz |
| Михаилъ | Michał |
| Петръ | Piotr |
| Станиславъ | Stanisław |
| Владиславъ | Władysław |
| Агнесса / Агнешка | Agnieszka |
| Аполлонія | Apolonia |
| Бригида | Brygida |
| Екатерина / Катерина | Katarzyna |
| Маріанна | Marianna |
| Марія | Maria |
| Текля | Tekla |
| Ядвига | Jadwiga |

### Gothic/Kurrent Letter Reference

Common letter confusions in Kurrent script:

| Kurrent Letter | Often Confused With | Distinguishing Feature |
|---|---|---|
| e | n (Latin) | Sharp angle at top |
| n | series of vertical strokes | Count the strokes |
| m | looks like "nn" | Three humps minimum |
| u | n | Has a curved bottom, often with a breve mark |
| a | o | Small connecting stroke at top right |
| long s (ſ) | f | No crossbar |
| round s | modern s | Only at end of words |
| h | looks like "li" | Tall ascender with loop |
| k | looks like "lk" | Complex letter, practice needed |
| z | looks like "3" | Sits on baseline |
| C | looks like E | More rounded |
| S | looks like G | Practice distinguishing |

**Learning resources**:
- German Script Tutorial: [search for "German Kurrent alphabet"]
- Script comparison charts showing Latin vs. Kurrent side by side
- Practice reading with known transcriptions before attempting unknowns

---

## Integration with Vault

### Creating Transcription Notes

1. Create a new file in your `transcriptions/` folder
2. Name it descriptively: `Birth_Jan_Kowalski_1892.md`
3. Use the transcription template from `templates/transcription.md`
4. Fill in all YAML frontmatter fields, including script and language

### Linking to Person Files

In your transcription note, link to person files:

```markdown
## Extracted Facts

The parents of [[Jan_Kowalski]] were:
- Father: [[Wojciech_Kowalski]] (age 32, farmer)
- Mother: [[Anna_Nowak_Kowalska]]

Witnesses: [[Piotr_Mazur]], [[Tomasz_Wozniak]]
```

In the person file, link back to sources:

```markdown
## Sources

- [[Birth_Jan_Kowalski_1892]] (primary source)
- [[Marriage_Wojciech_Kowalski_Anna_Nowak_1888]] (parents' marriage)
```

### Documenting Script and Language

Always record in the frontmatter:

```yaml
language: Russian  # or Polish, Latin, German
script: Cyrillic   # or Latin, Gothic, Kurrent
```

This enables searching and filtering by script type when reviewing your transcription work.

### Quality Tracking

Create a transcription audit table to track progress:

```markdown
| File | Script | Language | OCR Tool | Quality | Transcription Note |
|---|---|---|---|---|---|
| birth_1892_001.jpg | Cyrillic | Russian | Claude | Good | [[Birth_Jan_Kowalski_1892]] |
| marriage_1885_002.jpg | Kurrent | German | Transkribus | Partial | [[Marriage_Kowalski_Nowak_1885]] |
| baptism_1850_003.jpg | Latin | Latin | Tesseract | Good | [[Baptism_Wojciech_Kowalski_1850]] |
```

---

## Tips

- **Start with printed documents**: Build your skills on clearer records before tackling difficult handwriting
- **Learn the formulaic phrases**: Church and civil records follow predictable patterns; once you recognize them, reading becomes faster
- **Use parallel processing**: When working through a batch, sort by script type first, then process each group with the appropriate tool
- **Save raw output**: Keep original OCR text files alongside your polished transcriptions
- **Build a personal glossary**: Track unusual names, occupations, and place names as you encounter them
- **When Kurrent defeats you**: Post images to genealogy forums; experienced readers often volunteer help
- **Julian vs. Gregorian**: Russian partition records use the Julian calendar; always note both dates
- **Verify, verify, verify**: OCR errors in names propagate through your research; double-check every name against indexes or other records
