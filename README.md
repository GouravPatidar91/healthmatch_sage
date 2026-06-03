# HealthMatch Sage

HealthMatch Sage is a healthcare-focused web platform built with React + Vite and Supabase for authentication, scheduling, symptom analysis, emergency support, and medical-report interpretation workflows.

## Comprehensive Project Report Artifacts

This repository includes a full documentation pack for academic and stakeholder use:

- `generate_healthmatch_report.py` — Python script (using `python-docx`) that generates a **50+ page** polished report
- `HealthMatch_Sage_Comprehensive_Project_Report_50Pages.docx` — generated main report
- `DIAGRAMS.md` — ASCII diagram catalog and visual mapping notes
- `API_SPECIFICATION.md` — endpoint-level API documentation
- `DATABASE_SCHEMA.md` — schema, relationships, and SQL examples
- `DEPLOYMENT_GUIDE.md` — environment setup and deployment workflow

## Generate the DOCX Report

```bash
pip install python-docx
python generate_healthmatch_report.py
```

## Frontend Development

```bash
npm i
npm run dev
```

## Build and Lint

```bash
npm run lint
npm run build
```

> Note: this repository currently has pre-existing lint issues unrelated to report-generation artifacts.
