# paedsengage-pdf-parser
Parse PDF from Paedsengage

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
