# Mediroza General Hospital — Penetration Testing Project

**Author:** Kritika Rai

**Program:** Networkwalks Academy — Batch B083, Week 4

**Target:** https://medirozahospital.com

**Engagement type:** Black-box Penetration Test

**Duration:** 5 Days


> ⚠️ **Educational project only.** This test was carried out in a controlled training environment with written permission from the client. The techniques, tools and evidence in this repo must never be used against any real system without explicit written authorisation from its owner.

---

## What this project is

A full black-box penetration test against a training web application (Mediroza General Hospital). The goal was to find and prove real vulnerabilities, not just list theoretical ones — every finding below has a screenshot as evidence.

The project followed 4 milestones:

| Milestone | Goal |
|---|---|
| **M1 — Initial Access** | Break into the website and retrieve 3 confidential patient PDF lab reports |
| **M2 — Data Extraction** | Crack the password protecting all 3 PDF files |
| **M3 — Critical Data Exposure** | Dig deeper to find what else was exposed on the server |
| **M4 — Report** | Write up every finding, its risk, and how to fix it |

## What was found (summary)

| ID | Milestone | Finding | Risk |
|---|---|---|---|
| F8 | M1 | robots.txt reveals hidden folders | Low |
| F7 | M1 | Login form leaks valid usernames | Low |
| F1 | M1 | SQL injection on the login form | Critical |
| F2 | M1 | Login can be bypassed to view patient reports | Critical |
| F5 | M2 | Patient PDF passwords are weak and crackable | Medium |
| F6 | M3 | PDF file details leak the backup's location | Medium |
| F4 | M3 | Old backup folder is open for anyone to browse | High |
| F3 | M3 | Full database backup file is public — no login needed | Critical |

Full write-up, proof, risk ratings and fixes for every finding are in the report.

## Evidence Index (linked)

Click any link to open that screenshot directly.

### M1 — Initial Access

| Item | Evidence |
|---|---|
| Recon — WHOIS lookup | [m1-whois.PNG](./evidence/M1-initial-access/m1-whois.PNG) |
| Recon — DNS lookup (nslookup) | [m1-nslookup.PNG](./evidence/M1-initial-access/m1-nslookup.PNG) |
| Recon — WhatWeb fingerprint | [m1-whatweb.PNG](./evidence/M1-initial-access/m1-whatweb.PNG) |
| Recon — HTTP headers (curl) | [m1-curl-headers.PNG](./evidence/M1-initial-access/m1-curl-headers.PNG) |
| **F8** — robots.txt reveals hidden folders | [m1-robots-txt.PNG](./evidence/M1-initial-access/m1-robots-txt.PNG) |
| **F7** — Username enumeration | [m1-username-enumeration.PNG](./evidence/M1-initial-access/m1-username-enumeration.PNG) |
| **F1** — SQL injection error | [m1-sql-injection-error.PNG](./evidence/M1-initial-access/m1-sql-injection-error.PNG) |
| **F2** — Patient login page | [m1-Patient-login.PNG](./evidence/M1-initial-access/m1-Patient-login.PNG) |
| **F2** — Unauthorised portal access | [m1-patient-portal-access.PNG](./evidence/M1-initial-access/m1-patient-portal-access.PNG) |

### M2 — Data Extraction

| Item | Evidence |
|---|---|
| **F5** — Report 1 hash extracted | [m2-pdf1-hash-extraction.PNG](./evidence/M2-data-extraction/m2-pdf1-hash-extraction.PNG) |
| **F5** — Report 1 password cracked ('123456') | [m2-report1-password-cracked.PNG](./evidence/M2-data-extraction/m2-report1-password-cracked.PNG) |
| **F5** — Report 2 hash extracted | [m2-report2-hash-extract.PNG](./evidence/M2-data-extraction/m2-report2-hash-extract.PNG) |
| **F5** — Report 2 password cracked ('password') | [m2-report2-password-cracked.PNG](./evidence/M2-data-extraction/m2-report2-password-cracked.PNG) |
| **F5** — Report 3 hash extracted | [m2-report3-hash-extract.PNG](./evidence/M2-data-extraction/m2-report3-hash-extract.PNG) |
| **F5** — Report 3 failed with small wordlist | [m3-report3-worldlist-failed.PNG](./evidence/M3-critical-data-exposure/m3-report3-worldlist-failed.PNG) |
| **F5** — Report 3 password cracked ('!@#$%^&') | [m2-report3-password-cracked.PNG](./evidence/M2-data-extraction/m2-report3-password-cracked.PNG) |
| **F5** — Report 3 decrypted and opened | [m2-report3-decrypted.PNG](./evidence/M2-data-extraction/m2-report3-decrypted.PNG) |

### M3 — Critical Data Exposure

| Item | Evidence |
|---|---|
| **F6** — PDF metadata leak | [m3-pdf3-metadata.PNG](./evidence/M3-critical-data-exposure/m3-pdf3-metadata.PNG) |
| **F4** — Open directory listing (/old/) | [m3-old-db-backup.PNG](./evidence/M3-critical-data-exposure/m3-old-db-backup.PNG) |
| **F3** — Staff data from backup file | [m3-staff_data.PNG](./evidence/M3-critical-data-exposure/m3-staff_data.PNG) |
| **F3** — Shareholder data from backup file | [m3-shareholder_data.PNG](./evidence/M3-critical-data-exposure/m3-shareholder_data.PNG) |

---

## Repo structure

```
.
├── README.md
├── report/
│   └── Mediroza_Pentest_Report.docx    ← full report (start here)
└── evidence/
    ├── M1-initial-access/              ← recon, SQLi, login bypass screenshots
    ├── M2-data-extraction/             ← PDF password cracking screenshots
    └── M3-critical-data-exposure/      ← metadata leak, exposed DB backup screenshots
```

## Report

👉 **[report/Mediroza_Pentest_Report.docx](./report/Mediroza_Pentest_Report.docx)**

Contains:
1. Executive Summary
2. Scope and Methodology
3. Findings and Proof of Exploitation (grouped by milestone, with screenshots)
4. Risk Rating
5. Recommendations and Remediation
6. Full data tables recovered from the exposed backup (30 staff records, 10 shareholder records)

## Tools used

- `nslookup`, `whois`, `whatweb`, `curl` — reconnaissance
- Manual browser-based testing — login form behaviour, SQL injection, directory browsing
- Hash Calculator + Password Cracker (dictionary attack) — PDF password recovery
- `exiftool` — file metadata analysis

## Disclaimer

All data shown (patient names, staff records, salaries, national ID numbers, shareholder details) belongs to a **fictional training environment** built for this course. Nothing here reflects real people or a real organisation. This repo is for educational and portfolio purposes only.
