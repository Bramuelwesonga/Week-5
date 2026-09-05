# Week 5 Diagnostics — Oil & Gas Pod

Root-cause investigation into a fleet-wide throughput shortfall in the **Mystery Ops** dataset, produced for the Week 5 diagnostics assignment.

## Files in this submission

| File | Part | Description |
|---|---|---|
| `week5_diagnostics_analysis.ipynb` | Part A | Jupyter/Colab notebook with the full technical analysis: data profiling, anomaly detection, drill-down, Pareto analysis, correlation analysis, and three Plotly visualizations. |
| `Week5_Diagnostics_Report_Analyst.pdf` | Part B | 2-page written report for an Operations Director audience: Context → Insight → Action, with two embedded charts. |
| `Mystery_Ops.csv` | Input | Source dataset (not modified). |
| `README.md` | — | This file. |

## The headline finding

One machine — **NBI-P03** at the Nairobi depot — is responsible for roughly **86% of all throughput lost fleet-wide in 2026**. It ran normally through January, then dropped ~40% in output starting February 1 and never recovered. The root cause is a **missed-maintenance pattern**: this incident type alone accounts for 88% of all lost output across the entire 13-machine fleet. Temperature and voltage were checked and ruled out as drivers.

## How to run Part A (the notebook)

1. Go to [colab.research.google.com](https://colab.research.google.com) → `File > Upload notebook` → select `week5_diagnostics_analysis.ipynb`.
2. Click the folder icon in the left sidebar → upload `Mystery_Ops.csv` into the Colab session's file storage. (Alternatively, mount Google Drive and update the `DATA_PATH` variable in the first code cell.)
3. `Runtime > Run all`. All 21 code cells have been pre-verified to run end-to-end against this dataset with no errors.
4. Seaborn/Matplotlib are used for the profiling/anomaly charts; Plotly is used for the three interactive publication-quality charts in Section 4 — both are pre-installed in Colab, no extra setup needed.

## How to read Part B (the PDF report)

The report is written for a non-technical, time-pressed audience:
- **Context** — one paragraph on the problem and the data scope.
- **Insight** — the root cause (machine + timing + mechanism), with the two supporting charts embedded directly in the page.
- **Action** — three concrete, prioritized recommendations, each with a one-line rationale.

To personalize it: the report currently reads "Prepared by: Analyst" as a placeholder. Re-run `build_report.py` (included in the working files, not part of the graded submission) with `PREPARED_BY` set to your name, and rename the output file to `Week5_Diagnostics_Report_[YourName].pdf`.

## Methodology notes (for grading transparency)

- **"Loss" definition:** for the Pareto analysis, throughput loss on any non-`none` incident day is calculated as the shortfall versus the mean throughput on all incident-free (`none`) days across the fleet (~993 barrels/day).
- **Missing data:** ~0.2–0.7% of rows were missing `throughput_barrels`, `temperature_c`, or `operator_id`. Rows missing the target variable (`throughput_barrels`) were dropped for analysis; all other columns were left intact.
- **Correlation caveat:** `maintenance_flag`'s strong negative correlation with throughput is by construction (the flag is set *because* of the incident), so it's read as confirming the mechanism rather than independently proving it — the drill-down and Pareto results are the primary evidence for the root cause.
