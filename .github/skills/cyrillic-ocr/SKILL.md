---
name: cyrillic-ocr
description: Extract genealogical data from Russian Cyrillic documents (akta stanu cywilnego) from the Russian Partition era (1868-1918). Use when reading Russian-language vital records or civil registration documents.
allowed-tools: read, edit
---

# Russian Partition Cyrillic OCR Instructions

## Context

Records from the Russian Partition of Poland (1868-1918) were written in Russian Cyrillic script. These documents follow standardized Russian Imperial civil registration formats (akta stanu cywilnego). The transition from Latin to Cyrillic script occurred after the January Uprising (1863), and records remained in Russian until Polish independence in 1918.

## Document Types and Key Fields

### Акт о рождении (Birth Record)
Extract the following fields:
- Child's name (имя) and sex (пол: мужской/женской)
- Date and place of birth (место рождения)
- Father's full name, age, occupation, and residence
- Mother's full name (including maiden name: урождённая)
- Godparents (крёстные родители): names and relationship to family
- Registration number (номер акта) and parish

### Акт о браке (Marriage Record)
Extract the following fields:
- Groom's full name, age, occupation, marital status, and parents
- Bride's full name, age, marital status, and parents
- Date and place of marriage ceremony
- Witnesses (свидетели): names, ages, occupations
- Banns information if present

### Акт о смерти (Death Record)
Extract the following fields:
- Deceased's full name, age, occupation, and residence
- Date, time, and place of death
- Cause of death (причина смерти) if stated
- Burial date and cemetery location
- Informant details (who reported the death)
- Surviving spouse or family members mentioned

## Name Mapping (Russian to Polish)

### Male Names
- Иван = Jan
- Пётр = Piotr
- Станислав = Stanisław
- Михаил = Michał
- Иосиф / Осип = Józef
- Антон = Antoni
- Франц / Францишек = Franciszek
- Павел = Paweł
- Андрей = Andrzej
- Томаш = Tomasz
- Якуб / Яков = Jakub
- Войцех = Wojciech
- Владислав = Władysław
- Казимир = Kazimierz

### Female Names
- Мария / Марианна = Maria / Marianna
- Катерина / Екатерина = Katarzyna
- Анна = Anna
- Агнешка = Agnieszka
- Ева = Ewa
- Розалия = Rozalia
- Франциска = Franciszka
- Юзефа = Józefa
- Теофила = Teofila
- Марцианна = Marcjanna

### Surname Conventions
- Common surname endings are preserved across languages
- Feminine forms often end in -ова or -евна in Russian (e.g., Ковальска = Kowalska)
- Patronymics (отчество) may appear: Иванович = son of Ivan

## Julian Calendar Conversion

Russian Partition records use the Julian calendar. Convert to Gregorian:
- **19th century (1800-1899)**: Add 12 days
- **20th century (1900-1918)**: Add 13 days

**ALWAYS record both dates in transcriptions:**
```
date_julian: 1895-03-15
date_gregorian: 1895-03-27
```

## Key Vocabulary Reference

### Document Terms
- рождение = birth
- брак = marriage
- смерть = death
- крещение = baptism
- запись / акт = record / act

### Family Terms
- сын = son
- дочь = daughter
- отец = father
- мать = mother
- муж = husband
- жена = wife
- вдова = widow
- вдовец = widower

### Occupations
- крестьянин = peasant farmer
- мещанин = townsman / burgher
- ремесленник = craftsman
- кузнец = blacksmith
- портной = tailor
- сапожник = shoemaker

### Places and Status
- деревня = village
- город = city
- уезд = district
- губерния = province (governorate)
- законный = legitimate
- незаконный = illegitimate

## Confidence Tiers for Transcription

### Strong Signal
- All text clearly legible with standard letterforms
- Document follows expected format for the record type
- Names and dates can be read without ambiguity
- Cross-references with other records confirm accuracy

### Moderate Signal
- Most text legible, some characters uncertain
- Mark uncertain readings with [?]: "Стани[с?]лав"
- Minor ink damage or fading that does not obscure meaning
- Format is recognizable but may have variations

### Speculative
- Significant portions illegible or damaged
- Multiple possible readings for names or dates
- Document heavily faded, torn, or water-damaged
- Requires external verification before use in research

## Feedback Loop for Speculative Transcriptions

When confidence is Speculative:
1. Adjust image contrast, brightness, or apply filters
2. Focus OCR on unclear sections with higher resolution
3. Cross-reference names with Geneteka (geneteka.genealodzy.pl) indexes
4. Check Metryki.genbaza.pl for digitized parish records
5. Compare handwriting style with other records from same parish/scribe
6. Note all alternative readings in transcription notes

## Output Format

Generate a YAML transcription note following vault conventions:

```yaml
---
type: transcription
source: "[[Archive_Name]], Fond X, Opis Y, Delo Z, page N"
document_type: birth | marriage | death
person: "[[Person_Name]]"
date_julian: YYYY-MM-DD
date_gregorian: YYYY-MM-DD
language: russian
calendar: julian
ocr_method: manual | assisted
ocr_quality: strong | moderate | speculative
confidence: strong | moderate | speculative
created: YYYY-MM-DD
tags:
  - transcription
  - russian-partition
  - cyrillic
---
```

Include the full transcription text below the frontmatter, preserving original Russian with Polish name equivalents noted in parentheses.
