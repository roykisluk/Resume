# Resume (LaTeX CV)

Build: `xelatex Roy_Kisluk_Resume.tex` (XeLaTeX only — fonts come from ./Fonts).
Style macros live in `cv.sty`.

## Lesson log

### 2026-09-02 — long award lines looked broken
- **Symptom:** a long entry in Awards wrapped, leaving the year orphaned on line 2 and
  line 1 stretched by justification.
- **Cause:** `\cvPlain` items push the year with `\hfill`, which only works when the item
  fits one line.
- **Fix:** added `\awardentry{text}{year}` in `cv.sty` — tabularx with a ragged-right text
  column and a right-aligned year column (`\hyphenpenalty=10000` to stop mid-word breaks).
  Years now align across all entries and long text wraps cleanly.
