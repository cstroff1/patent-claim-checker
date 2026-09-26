# Patent Claim Completeness Checker

**Live app:** https://cstroff1.github.io/patent-claim-checker/

Patent teams use this tool to check that every chemical compound disclosed by scientists appears in the claims section of a patent application. It compares the scientific brief against the draft claims, lists any compounds that were disclosed but never claimed, and keeps a history of reviews. The goal is to catch those gaps before the application goes to the USPTO.

> **Demo tool.** All sample patents and compounds (e.g. `DX-2031`, `Compound-A114`) are fictional. The tool works only with the names and documents you provide and has no connection to real patent filings or proprietary data.

---

## Contents

- [Quick start: 2-minute demo](#quick-start-2-minute-demo)
- [Screens](#screens)
  - [Dashboard](#1-dashboard)
  - [New Review](#2-new-review)
  - [Result](#3-result)
  - [Review Library](#4-review-library)
- [How compound detection works](#how-compound-detection-works)
- [How matching and scoring work](#how-matching-and-scoring-work)
- [Limitations](#limitations)
- [Data and privacy](#data-and-privacy)
- [Running it locally](#running-it-locally)
- [Project structure](#project-structure)

---

## Quick start: 2-minute demo

1. Open the [live app](https://cstroff1.github.io/patent-claim-checker/). The **Dashboard** shows three sample reviews and their summary statistics.
2. Click **New Review**.
3. Click **Load sample documents**. This fills in a fictional patent (`DX-2044 — Chelating Agents`), a scientific brief and a claims section.
4. Look at the lists under each document. The brief lists 6 disclosed compounds and the claims list 5.
5. Click **Compare**. The Result screen shows a completeness score of **83.3%** and flags **Compound-M6** as missing from the claims. Below the flag is the sentence from the brief that mentions it.
6. Click **Save to Dashboard**. The dashboard statistics update to include the new review.
7. Open **Review Library**, click the `DX-2044` row, then click **Edit review**.
8. At the end of the claims text, add `4. The composition of claim 1, further comprising Compound-M6.` Click **Compare**, then **Save Changes**. The review now shows 100% complete.

---

## Screens

### 1. Dashboard

This is the default view and gives an overview of all saved reviews.

| Card | What it shows |
|---|---|
| **Patents Reviewed** | Number of saved reviews, and how many still have gaps |
| **Total Compounds Checked** | Total disclosed compounds across all reviews |
| **Compounds Flagged Missing** | Disclosed compounds not found in the claims |
| **Completeness Rate** | Claimed compounds ÷ disclosed compounds, across all reviews |

Below the cards, the **Recent reviews** table lists each patent with its ID, title, compound count, flagged count, completeness and review date. Click a row to open that review in the Review Library.

### 2. New Review

Start a comparison here.

1. **Patent name or ID.** Use the form `ID — Title` (for example `DX-2044 — Chelating Agents`) so the ID and title show in separate columns. The ID is never mistaken for a compound.
2. **Scientific brief** (left panel): the invention disclosure from the research team.
3. **Patent claims** (right panel): the claims section of the draft application.

For each document you can:

- click **Upload** and choose a **PDF**, **Word (.docx)** or **text** file,
- drag a file onto the panel, or
- paste the text into the box. A plain list with one compound per line also works.

After you add a document, the list under it updates automatically:

- **Disclosed compounds**: what the app found in the brief.
- **Compounds found in claims**: what the app found in the claims.

**Check these lists before you compare.** Click **×** on a chip to remove a wrong match. Type a name into **Add a compound the scan missed** and press **Enter** to add one. Chips you add are outlined in blue. Click **Restore** to bring back removed chips.

Then click **Compare**.

### 3. Result

- **Warning banner.** If anything is missing, it reads *"N compound(s) disclosed but not found in claims — review before submission."*
- **Completeness score.** Matched compounds ÷ disclosed compounds, with counts for disclosed, properly claimed and flagged.
- **Properly Claimed.** Disclosed compounds that were found in the claims.
- **Flagged — Missing from Claims.** Disclosed compounds that were not found. Each one shows the passage from the brief where it is mentioned, so you can judge whether it should be claimed.
- **Claimed but not in the brief.** A note listing compounds that appear in the claims but not in the brief. These are shown for reference and don't affect the score.

Actions:

| Button | What it does |
|---|---|
| **Edit inputs** | Go back to the form without losing anything, for example to fix a detected list |
| **Check Another Patent** | Discard this result and start a blank review |
| **Save to Dashboard** | Save the review and return to the Dashboard |

When you're editing a saved review, the buttons read **Discard changes** and **Save Changes** instead.

### 4. Review Library

Every saved review, newest first.

- **Filter** by typing part of a patent name or ID into the search box.
- **Click a row** to expand it. You'll see the full disclosed list (missing compounds marked *not claimed*), the claimed list and the flagged list. You'll also see when the review was saved and last edited, and which files were used.
- **Edit review** reopens the review in the form with its documents and compound lists. Change anything, click **Compare**, then **Save Changes**. The existing review is updated in place.
- **Delete** removes the review after you confirm.

---

## How compound detection works

The app reads each document and looks for:

| Type | Examples |
|---|---|
| Compound labels | `Compound-A114`, `Compound 12`, `Cpd. B7` |
| Development codes | `ABT-199`, `XYZ-4410` |
| CAS registry numbers | `5465-99-5` |
| Hyphenated systematic names | `2-(4-chlorophenyl)-N-methylacetamide` |

If a document is a short list with one item per line, each line is taken as a compound.

In the claims, the app also searches the text for every compound found in the brief. A disclosed compound therefore counts as claimed wherever it appears, including inside a *"selected from the group consisting of …"* list.

Detection is a starting point. Always check the detected lists and correct them before comparing.

## How matching and scoring work

- Matching **ignores letter case, spaces and hyphens**. `Compound-M5`, `compound m5` and `COMPOUND‑M5` all count as the same compound.
- A name must match as a whole. `Compound-A11` does **not** match `Compound-A114`.
- Duplicate entries count once.
- **Completeness score** = properly claimed ÷ disclosed × 100.

## Limitations

- **Common or trade names** (e.g. "ibuprofen") and single-word chemical names aren't detected automatically. Add them by hand.
- **Markush structures and ranges** (e.g. "Compound-A114 through Compound-A118", or a generic formula) aren't expanded. Only compounds named individually in the claims count as claimed.
- **Scanned PDFs** with no selectable text can't be read. The app shows a message; paste the text instead.
- **Older `.doc` files** aren't supported. Save them as `.docx` or PDF.
- This tool helps with review and doesn't replace attorney judgment about claim scope.

## Data and privacy

- Everything runs **in your browser**. There's no server, account or login.
- Uploaded files are read in the browser and **never uploaded anywhere**.
- Reviews are saved in your browser's local storage. They stay on that browser and device and aren't shared with anyone else who opens the site.
- Clearing your browser's site data deletes saved reviews and brings back the sample reviews.
- If a very large document won't fit in storage, the review is still saved with its compound lists but without the document text.

## Running it locally

No build step or install is needed.

- **Simplest:** download `index.html` and open it in a browser.
- **With a local server:** run the command below in the project folder, then open http://localhost:8000.

```bash
python3 -m http.server 8000
```

PDF and Word reading loads two libraries from cdnjs on first use ([pdf.js](https://mozilla.github.io/pdf.js/) and [mammoth.js](https://github.com/mwilliamson/mammoth.js)), so uploads need an internet connection. Pasting text works offline.

## Project structure

```
index.html   The whole app: markup, styles and JavaScript in one file
README.md    This guide
```

The site is hosted on GitHub Pages from the `main` branch. Any push to `main` updates the live app within a minute or two.
