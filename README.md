# Data-Visualization-and-Communication

# Week 5 — Data Visualization Portfolio

**Project:** Predicting LendingClub Loan Defaults
**Focus:** Annotated visualizations, visual storytelling, narrative report
**Dataset:** LendingClub LoanStats3a (42,535 loans, 2007–2011)
**Report date:** November 2026

---

## 1. Objective

Week 5 asks the third question of the data-science workflow: *having modeled the
data, how do we show what it means?* The deliverable is a portfolio of ten
high-quality, annotated visualizations that together tell the story of LendingClub
loan-default risk — from the platform's growth, through the grade signal that
dominates risk, to the financial and geographic mechanisms that compound it.

The emphasis is not only on technical proficiency with visualization libraries, but
on the **narrative that links the visual data to an insightful analysis**. Each
figure documents its choice of visual technique, the key insight it reveals, and its
relevance to the broader story.

---

## 2. Deliverables

| File | Location | Purpose |
|------|----------|---------|
| **Week5_Data_Visualization_Report.pdf** | `download/` | 17-page narrative report (cover + body) |
| **week5_visualization_portfolio.ipynb** | `download/` | Reproducible viz notebook (28 cells, 13 code) |
| 10 annotated figures (PNG, 150 DPI) | `data/week5_figures/` | The portfolio itself |
| `week5_stats.json` | `data/` | Figure-level statistics for the report |
| `week5_visualizations.py` | `scripts/` | Viz generation pipeline |
| `build_week5_body.py` | `scripts/` | ReportLab body PDF generator |
| `week5_cover.html` / `.pdf` | `scripts/` | Cover page (Playfair Display + Inter, steel-blue palette) |

---

## 3. Storyboard — Five-Act Narrative Arc

The portfolio is structured as a narrative, not a gallery. Each act answers one
question and sets up the next:

| Act | Question | Figures |
|-----|----------|---------|
| **I. The rise** | How did LendingClub grow, and did defaults rise with volume? | 1, 2 |
| **II. The signal** | What single feature best predicts default? | 3, 6, 8 |
| **III. The dimensions** | How do purpose, geography, and debt burden modulate risk? | 4, 5, 7 |
| **IV. Interactions** | How do risk factors combine at the loan level? | 9, 10 |
| **V. Synthesis** | What is the default story, and what should a lender do? | narrative section |

---

## 4. The Ten Visualizations

| # | Figure | Technique | Key insight |
|---|--------|-----------|-------------|
| 1 | Growth timeline | Dual-axis area + line chart | 30× growth 2007→2011; peak 2,267 loans/month |
| 2 | Default rate over time | Line chart + baseline | 2008 crisis cohort spiked; 2011 rebound |
| 3 | **Grade ladder** | Bar + diverging colormap | Default 6% (A) → 34% (G), 5.5× spread |
| 4 | Purpose treemap | Treemap + color overlay | Debt consolidation = 47% volume; small_business = 28% default |
| 5 | State tilemap | Tile-grid cartogram | Nevada leads (23.7%); 7 tiny-sample states grayed out |
| 6 | Interest rate violin | Violin + mean overlay | Rate tracks grade: 7.3% → 20.3%, +3–4 pts/step |
| 7 | DTI by outcome | Overlapping KDE + t-test | Defaulters +2.5 DTI pts, but heavy overlap |
| 8 | Correlation heatmap | Lower-triangle heatmap | grade & int_rate dominate (r ≈ 0.20) |
| 9 | Loan vs income | Scatter, color-by-outcome | Defaults cluster upper-left (high loan, low income) |
| 10 | **Risk matrix** | 2D heatmap | small_business × grade G = 50% default |

**Bold** entries are the pivot (Figure 3) and synthesis (Figure 10) of the narrative.

---

## 5. Libraries Used

- **matplotlib** — base plotting, all 10 figures.
- **seaborn** — heatmaps (Figures 8, 10), KDE (Figure 7), violin (Figure 6).
- **squarify** — treemap layout (Figure 4).
- **scipy.stats** — Welch's t-test inset (Figure 7).
- **ReportLab** — narrative report PDF generation.

No proprietary or paid visualization tools. All figures are reproducible from raw CSV.

---

## 6. Report Structure (17 pages)

| Page | Section |
|------|---------|
| 1 | Cover (steel-blue Template 04) |
| 2 | Table of contents (auto-generated) |
| 3 | 1. Executive Summary |
| 4 | 2. Dataset & Storyboard |
| 5 | 3.1 Growth timeline (Figure 1) |
| 6 | 3.2 Default over time (Figure 2) |
| 7 | 3.3 Grade ladder (Figure 3) |
| 8 | 3.4 Purpose treemap (Figure 4) |
| 9 | 3.5 State tilemap (Figure 5) |
| 10 | 3.6 Interest rate violin (Figure 6) |
| 11 | 3.7 DTI by outcome (Figure 7) |
| 12 | 3.8 Correlation heatmap (Figure 8) |
| 13 | 3.9 Loan vs income (Figure 9) |
| 14 | 3.10 Risk matrix (Figure 10) |
| 15 | 4. Synthesis: The Default Story |
| 16 | 5. Limitations & Reflections |
| 17 | 6. Conclusion |

Each figure page contains the figure, a narrative paragraph, and a three-row
insight box (visual technique / key insight / narrative relevance).

---

## 7. Quality Checks Passed

- `pdf.py font.check` — all fonts embedded, 0 issues.
- `pdf.py toc.check` — TOC populated, 0 errors.
- `pdf_qa.py` — 11/11 passed, 0 errors. Page size consistent (595.3 × 841.9 pt).
- All 10 figures embedded on correct pages, fit within margins.
- All 10 insight boxes present (technique + insight + relevance).
- No leftover placeholders (XXX, TODO, NaN, 【, undefined).
- Notebook executes end-to-end with 0 errors (1.3 MB executed output).

---

## 8. Honest Methodology Notes

- **State map small-sample handling.** Nebraska initially appeared to default at
  54.55%, but on only 11 loans. We excluded states with n<50 (grayed out with
  "n<50" labels) and documented this transparently in both the figure caption and
  the body text. Nevada (23.7%, n=527) is the genuine leader.
- **Scatter plot sampling.** 6,000 of 42,535 loans, with alpha-blending to preserve
  density information. Axes clipped to the distribution bulk.
- **Statistical rigor.** Figure 7 includes a Welch's t-test (t = −8.78, p < 0.001)
  quantifying the DTI shift, rather than relying on visual impression.
- **Narrative framing.** The report explicitly acknowledges that the "default risk"
  frame is one of several legitimate framings (borrower welfare, investor returns
  being alternatives) and lists what we would add next.

---

## 9. How to Reproduce

```bash
# From the repository root
python3 -I scripts/week5_visualizations.py    # generates all 10 figures + week5_stats.json
python3 -I scripts/build_week5_body.py         # builds scripts/body_week5.pdf

# Merge cover + body
python3 -c "
from pypdf import PdfReader, PdfWriter
w = PdfWriter()
w.add_page(PdfReader('scripts/week5_cover.pdf').pages[0])
for p in PdfReader('scripts/body_week5.pdf').pages: w.add_page(p)
w.add_metadata({'/Title': 'Data Visualization and Communication — LendingClub'})
w.write(open('download/Week5_Data_Visualization_Report.pdf','wb'))
"
```

**Notebook:** upload `download/cleaned_dataset.csv` to the notebook working
directory and Run All. The notebook regenerates all 10 figures inline.

---

## 10. The Week-5 portfolio closes the analytical loop

- The grade signal that dominates the logistic-regression model → Figure 3 (grade
  ladder) and Figure 8 (correlation heatmap).
- The interaction signal that tree ensembles *should* have exploited → Figure 10
  (purpose × grade risk matrix) shows the interaction exists but is small relative
  to the main effect.
- The modest predictive ceiling → Figures 6, 7, 9 explain *why*: single continuous
  features overlap heavily between paid and defaulted loans.

