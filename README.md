# Bojonegoro Regency (Indonesia): law history in git

Part of [lexifina/global-law](https://github.com/lexifina/global-law), one git history for every country's law: this is the law of Bojonegoro Regency, East Java, Indonesia, which global-law reads at `indonesia/east-java/bojonegoro-regency/acts/`.

The Peraturan Daerah (Perda) of Kabupaten Bojonegoro, Indonesia, as a git history: one folder per Perda, one file per Pasal (article), one paragraph per line, so `git blame`, `git log` and `git diff` work line by line. The text is the Indonesian text of each Perda as enacted, from the copy (salinan) published by JDIH Kabupaten Bojonegoro (Bagian Hukum Sekretariat Daerah Kabupaten Bojonegoro).

It follows the shared design of [lexifina/global-law](https://github.com/lexifina/global-law).

## What this repository holds

**Each Perda as enacted, not yet a history of amendments.** JDIH publishes each Perda as its signed copy; there is no consolidated text. So each Perda is one commit holding its text as enacted ("oldest version available"), credited to the publisher, not to an amending law. An amending Perda is its own folder; its amendments are not applied to the Perda it amends, and a repeal is not applied.

| File | What |
| --- | --- |
| `a-pembukaan.md` | heading, title, preamble (Menimbang, Mengingat) and enacting words |
| `pasal-NNN.md` | one Pasal; chapter, part and paragraph headings printed before the next Pasal stay at its end |
| `z1-penutup.md` | promulgation order, signatures, Lembaran Daerah number, certification of the copy |
| `z2-penjelasan.md` | the elucidation (Penjelasan), where printed |
| `z3-lampiran.md` | the annex (Lampiran), where printed |

The record is built in parts, oldest Perda first, and holds only the Perda JDIH publishes as a PDF that passes the checks below (a text layer, or a scan read by OCR); documents the reader cannot split into Pasal are left out for now. Scans are read by OCR (see "OCR texts"). Budgets (APBD and their accountability reports), development plans (RPJMD, RPJPD) and spatial plans (RTRW, zoning), which are mostly tables and maps, are not included. It is not (yet) every Perda of Kabupaten Bojonegoro.

## Source

[JDIH Kabupaten Bojonegoro (Bagian Hukum Sekretariat Daerah Kabupaten Bojonegoro)](https://jdih.bojonegorokab.go.id): each Perda as a PDF (a text layer, or a scan read by OCR). Each PDF's sha256 is recorded with its version in `data/versions.json`.

## Dates

Each Perda is dated by the day it takes effect under its own last Pasal, at noon local time (WIB, UTC+7): the day it was promulgated (diundangkan, printed in its closing) when it says "mulai berlaku pada tanggal diundangkan", or the calendar day it names. Perda whose commencement is a period after promulgation or another event are left out for now.

## How it is built

Lexifina reads the sources listed here and records each act's dated versions, and the laws that made each change, in one corpus file. `tools/build.py` writes this repository from that file, and the same corpus always gives the same commit hashes; `REPRODUCE.md` gives the details and the checks. A model (Claude) wrote Lexifina's code; it wrote no legal text, and no model runs when the history is built.

The text layer of each PDF becomes the record (scans: see "OCR texts" below), row by row in reading order, rows joined into paragraphs. Left out: page numbers and the "SALINAN" stamp line. Nothing is reworded.

## OCR texts

3 Perda in this repository are read by OCR from the official scans JDIH publishes (Alan's decision D8, 2026-11-02: OCR is allowed for official scans whose terms allow reuse, marked as OCR and spot-checked). Each such file starts with a front-matter line

    Text-source: OCR (Tesseract <version>, ind) of the official scan <url>

and its commit message says the same. Reader: Tesseract (tessdata_best model "ind", --psm 3, pages at 300 dpi); pages with a real text layer keep it; lines with no letter or digit are left out. The strict letters check needs a text layer, so these acts are spot-checked instead: 3 paragraphs of every act, drawn at random, are cut out of the scan and read again with a different setting (tessdata_fast, --psm 6); the two readings must agree at 98% or more, character for character, or the act is left out. The structural checks still apply (Pasal in order, the closing formula, the promulgation day, the number and year against JDIH). OCR can misread single characters, so for anything that matters, read the scan.

| Act | In force | Spot-check agreement | Scan | Part |
| --- | --- | --- | --- | --- |
| Perda Bojonegoro Regency 4/2019 | 2019-09-06 | 99.35% | <https://jdih.bojonegorokab.go.id/storage/produk-hukum/108_Perda_No_4_ttg_perubahan_Perda_no_1_2017_ttg_Peran.pdf> | 30-ocr-01 |
| Perda Bojonegoro Regency 3/2020 | 2020-04-03 | 99.53% | <https://jdih.bojonegorokab.go.id/storage/produk-hukum/4_kabbojonegoro_jdih_jatimprov_go_default.pdf> | 30-ocr-01 |
| Perda Bojonegoro Regency 12/2020 | 2020-11-20 | 99.55% | <https://jdih.bojonegorokab.go.id/storage/produk-hukum/54_perda_12_th_2020_ttg_perub_perda_15_th_2011_ttg_pa.pdf> | 30-ocr-01 |

## How it is checked

Every version is read back from git on the day it took effect and must match the corpus. A second, independent reading of every PDF (a different PDF engine, pdftotext) must hold every paragraph of the record as one unbroken stretch, letter for letter and digit for digit, and the paragraphs together must cover the whole PDF with nothing left over but page numbers and the stamp. Results are in `REPRODUCE.md`.

## What "author" means

The author of each commit is the publisher, with an e-mail address that cannot exist; the committer is always Lexifina.

## Limits

Only each Perda as enacted: no later amendments, no consolidation, no repeal applied, Indonesian text only, and only the Perda that pass the checks; OCR'd texts may misread single characters. The official text is the one promulgated in the Lembaran Daerah.

## Licence

See [LICENSE](LICENSE): Undang-Undang Nomor 28 Tahun 2014 tentang Hak Cipta, Pasal 42, gives no copyright in peraturan perundang-undangan. Source: JDIH Kabupaten Bojonegoro (Bagian Hukum Sekretariat Daerah Kabupaten Bojonegoro), https://jdih.bojonegorokab.go.id.
