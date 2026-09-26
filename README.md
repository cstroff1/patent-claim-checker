# Patent Claim Completeness Checker

A single-page tool that checks whether every compound disclosed by scientists appears in a patent application's claims section, and flags any that are missing before submission.

## How it works

1. Upload or paste the **scientific brief** (invention disclosure) and the **patent claims**. PDF, Word (.docx) and plain-text files are supported.
2. The app scans both documents for compound names: compound codes (e.g. `Compound-A114`), development codes (e.g. `ABT-199`), CAS numbers and hyphenated systematic names. A plain one-per-line list also works.
3. Review the detected compounds, remove any false matches and add anything the scan missed.
4. Compare. Every disclosed compound is checked against the claims, ignoring case, spaces and hyphens. Flagged compounds show the sentence from the brief where they appear.
5. Save the review. Saved reviews can be reopened and edited from the Review Library.

## Notes

- Runs entirely in the browser. Reviews are saved to `localStorage`; there is no backend or login, and documents never leave the browser.
- Scanned PDFs without selectable text can't be read; paste the text instead.
- Compounds referred to only by common names (e.g. "ibuprofen") or by Markush structures aren't detected automatically. Add them by hand.
- Ships with fictional sample data. It has no connection to real patent filings or proprietary data.
