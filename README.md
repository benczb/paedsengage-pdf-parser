# PaedsENGAGE PDF Parser Skill

An OpenClaw AgentSkill for converting PaedsENGAGE participating-clinic PDFs into structured JSON and CSV files.

This is useful for building clinic finders, review checklists, Excel workbooks, dashboards, or static website datasets.

## What this tool does

The parser reads a PaedsENGAGE participating-clinics PDF and generates:

- `clinics.json`
- `clinics.csv`
- `clinic_hours.csv`
- `clinic_hours_blocks.csv`
- A text review dump for manual spot-checking

It can also update a website data folder, for example:

- `site/data/clinics.json`

## Repository contents

```text
.
├── README.md
├── LICENSE
├── SKILL.md
├── scripts/
│   └── parse_paedsengage_pdf.py
└── references/
    └── output-schema.md
```

## Requirements

- Python 3.10+
- `pdfplumber`
- `pandas`

Install dependencies in a virtual environment:

```bash
python3 -m venv .venv
. .venv/bin/activate
pip install pdfplumber pandas
```

## Usage

From a project folder containing the source PDF:

```bash
python /path/to/paedsengage-pdf-parser/scripts/parse_paedsengage_pdf.py \
  --pdf data/paedsengage-clinics-YYYY-MM-DD.pdf \
  --out-dir data \
  --site-data-dir site/data
```

If using a local virtual environment:

```bash
.venv/bin/python /path/to/paedsengage-pdf-parser/scripts/parse_paedsengage_pdf.py \
  --pdf data/paedsengage-clinics-YYYY-MM-DD.pdf \
  --out-dir data \
  --site-data-dir site/data
```

## Output files

### `clinics.json`

Main structured clinic dataset.

### `clinics.csv`

Flat clinic list suitable for Excel review.

### `clinic_hours.csv`

Clinic opening hours in table format.

### `clinic_hours_blocks.csv`

Opening hours split into extracted text blocks for easier checking.

### Review dump

A plain-text extraction dump for comparing parser output against the original PDF.

## Validation

Validate the generated JSON:

```bash
python -m json.tool data/clinics.json >/dev/null
```

Run a quick count check:

```bash
python - <<'PY'
import json
from collections import Counter

clinics = json.load(open('data/clinics.json'))

print('clinics', len(clinics))
print('locations', len(set(c['location'] for c in clinics)))
print(Counter(c['location'] for c in clinics).most_common(10))
PY
```

## Important notes

PDF extraction is layout-sensitive. Always spot-check generated outputs against the official source PDF before publishing or using the data.

Generated Google Maps links are search URLs only. They do not confirm whether a clinic is open, permanently closed, or matched to a verified Google Place ID.

This repository does not include official PaedsENGAGE PDFs by default. Only add source PDFs if you have the right to redistribute them.

## License

MIT License.
