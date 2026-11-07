<!-- ### TEXT BY CLAUDE ### — whole file written by Claude (AI assistant), approved by the student -->

# TAZ Road-Accident Risk — Advanced ML Course Project

Ariel University, Industrial Engineering & Management, course 4273110 (Prof. Chen Hajaj), 2026–27.
Dataset: "accid_taz" (traffic zones, תאונות לפי אזורי תנועה) from data.gov.il — `data/accid_taz.csv`
(2,637 zones × 29 columns, single snapshot YEARMONTH=202608).

## Working rules (MANDATORY for every session)

1. **Language:** talk to the user in Hebrew. Code, identifiers and comments in English.
2. **Approval first:** propose a step, explain it, and WAIT for explicit approval before
   creating/modifying any file, installing packages, committing, pushing, or any outward action.
   Read-only inspection is fine.
3. **AI marking (course rule):** every block of code written or edited by Claude is wrapped:
   ```python
   ### CODE BY CLAUDE ###
   ...code...
   ####
   ```
   Any report/README text written or edited by Claude must be marked (in the PDF report: colored red).
4. **Defense-ready code:** the oral exam changes parameters live. Keep all tunable values
   (seeds, thresholds, model hyper-parameters, SMOTE settings, k for clustering) in one config
   at the top / in `code/config.py`. Code must reproduce exactly what the report shows (fixed seeds).
5. Run the `project-guardian` agent at the end of every milestone and before every submission.

## Hard requirements (from the official guidelines)

- Dataset from data.gov.il only; >140 rows and **≥15 meaningful features**.
- Classification: end-to-end pipeline (preprocessing, feature engineering, model selection,
  tuning, evaluation, interpretation) with **≥5 classifiers**; handle class imbalance (SMOTE etc.);
  metrics F1, PR-AUC (plus ROC-AUC); error analysis.
- Unsupervised: **≥3 clustering models** compared (e.g. K-Means, Hierarchical, DBSCAN);
  optional anomaly detection.
- Watch for **target leakage**: injury/vehicle counts are outcomes — never feed columns
  that define the target into the model.
- Repo (5%): informative README, `data/` and `code/` separate, figures/outputs, `requirements.txt`. Python only.

## Deadlines

| Date | Deliverable | Format |
|---|---|---|
| 2026-11-10 | Register team + dataset (name + direct portal link) in course spreadsheet | late = −5 pts |
| 2026-12-01 23:59 | Proposal PDF (10%) | max 1 page, font 11, title + full names; dataset+link, motivation, method (≥5 clf, ≥3 clustering), intended experiments/evaluation. Automated check, no appeals |
| 2027-01-05 23:59 | Final write-up (60%) via Moodle | max 7 pages incl. figures (appendices extra), team-contribution section, GitHub link, requirements.txt |
| Jan 2027 wk 2–3 (TBD) | Oral defense (25%) | code running locally, Zoom; each member knows all code |

Only 3 late days total across all submissions, and only with advance notice.

## Layout (planned)

```
data/      raw data (do not modify)   code/      notebooks + scripts
figures/   saved plots                outputs/   tables, metrics, models
report/    proposal + final report
```
