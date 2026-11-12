# Resume (LaTeX CV)

Build: `xelatex Roy_Kisluk_Resume.tex` (XeLaTeX only — fonts come from ./Fonts).
Style macros live in `cv.sty`.

One version only (2026-11-12, Roy): no phone number, so the same PDF goes on roykisluk.com
(`Tools/Website/site/cv.pdf`; recopy it whenever the CV changes). Check: `pdftotext Roy_Kisluk_Resume.pdf - | grep PHONE` prints nothing.

## Lesson log

### 2026-09-02 — long award lines looked broken
- **Symptom:** a long entry in Awards wrapped, leaving the year orphaned on line 2 and
  line 1 stretched by justification.
- **Cause:** `\cvPlain` items push the year with `\hfill`, which only works when the item
  fits one line.
- **Fix:** added `\awardentry{text}{year}` in `cv.sty` — tabularx with a ragged-right text
  column and a right-aligned year column (`\hyphenpenalty=10000` to stop mid-word breaks).
  Years now align across all entries and long text wraps cleanly.

### 2026-11-11 — web variant for the personal site
- **Need:** roykisluk.com links a CV, but the full CV has the phone number and the Ministry
  of Finance entry (Scholarship/Website rule: nothing may imply Roy works at the Ministry).
- **Fix:** one source, a `\webcv` switch (see build note above) instead of a second `.tex` that
  would drift.
- **Changed same day (Roy):** the Ministry rule is only for scholarship applications, so the
  web CV keeps the Ministry entry; only the phone is left out.

### 2026-11-12 — one CV, no phone (Roy)
- **Symptom:** the site's CV lost the Population Science scholarship after a rebuild.
- **Cause:** the web CV was rebuilt from a local checkout that was behind the remote (the scholarship was
  committed from another session), then copied to the site.
- **Fix:** rebased onto the remote and rebuilt. The `\webcv` switch and `Roy_Kisluk_CV_web.pdf` are gone
  because Roy chose a single version with no phone number. Before rebuilding the CV, run `git pull`.

### 2026-11-12 — academic pass on the CV (Roy's choices, so they are not re-argued)
- **Kept on purpose:** the Gmail address (a TAU address expires one day), C# in skills, one
  "Research & Professional Experience" heading, all three Stonehenge bullets. BDO bullets are Roy's wording.
- **Changed:** Work in Progress section added; Awards moved above Presentations and Teaching; cum laude
  lines removed from Awards (they are in Education); private tutoring removed; publication in AEA style with
  the title linked to the paper on the site; "Updated <month> <year>" at the end comes from the build date.
- **Work in Progress uses the "with ..." form** because the author order of that paper is not set.
- **Open:** roykisluk.com sits behind a Cloudflare Access login (checked with curl, 2026-11-12), so the CV's
  site and paper links do not open for outsiders until the site goes public. Roy keeps both links
  pointing at the site.
- **Economic Quarterly, no volume or pages yet:** ieca.org.il lists the paper under "accepted for publication"
  (מאמרים שהתקבלו לפרסום); the latest issue is vol. 69 (2025) and the paper is not in it. Roy keeps "2026"
  rather than "forthcoming". Add volume and pages when the 2026 issue appears. The journal hosts a public PDF:
  `https://ieca.org.il/wp-content/uploads/2026/07/Structual_transformation_IL-5.pdf`.
- **Symptom:** the BDO header sat at the foot of page 1 with its bullets on page 2.
  **Cause:** `\cventry` allowed a page break between the header and the list under it.
  **Fix:** `\nopagebreak` in `\cventry` and `beginpenalty=10000` in `\cvItems` (`cv.sty`).
