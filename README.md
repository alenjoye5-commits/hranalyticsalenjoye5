# 👥 HR Analytics – Interactive Streamlit Report

A cleaned, interactive dashboard built from `HR_Analytics.xlsx` (1,480 raw rows, 38 columns).

## Quick start

```bash
# 1. (optional) create a virtual environment
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate

# 2. install dependencies
pip install -r requirements.txt

# 3. launch
streamlit run app.py
```

Or just double-click / run **`run_app.bat`** (Windows) or **`./run_app.sh`** (macOS / Linux) –
they create the environment, install the packages and start the app.
The app opens at <http://localhost:8501>. Python 3.9+ is required.

## What's inside

```
hr_analytics_dashboard/
├── app.py                      # Streamlit dashboard (7 tabs, sidebar filters)
├── data_cleaning.py            # Cleaning pipeline (also runnable on its own)
├── requirements.txt
├── run_app.bat / run_app.sh    # One-click launchers
├── .streamlit/config.toml      # Theme
└── data/
    ├── HR_Analytics.xlsx       # Original data
    └── HR_Analytics_cleaned.csv# Cleaned export (regenerate: python data_cleaning.py)
```

## Dashboard tabs

| Tab | What you get |
|---|---|
| **📊 Overview** | KPI cards, auto-generated key insights, workforce composition |
| **🚪 Attrition** | Attrition rate by any of 15 dimensions, tenure/commute/travel, job-role heatmap, ranked hotspot segments |
| **💰 Compensation** | Pay of stayers vs leavers, salary slabs, pay by level/role, gender comparison within level, stock options, hikes |
| **😊 Satisfaction** | Attrition by survey score, stayer-vs-leaver radar, work-life balance × overtime, role heatmap |
| **📈 Career & Tenure** | Tenure, promotion stagnation, previous employers, training, education mix |
| **🧠 Drivers & Risk** | Correlations, random-forest feature importance, ranked list of current employees at highest risk |
| **🗂️ Data & Quality** | Cleaning log, raw-vs-clean summary, column picker, CSV downloads |

**Sidebar filters:** department, job role, gender, age group, marital status, travel, overtime,
salary slab, education field, plus age / income / tenure sliders. Every chart, KPI and insight responds.
You can also upload your own `.xlsx` / `.csv` (same columns) from the sidebar.

## Data cleaning summary

| Issue found | Action |
|---|---|
| 10 repeated `EmpID`s (7 exact copies, 3 with conflicting `YearsWithCurrManager`) | Kept first occurrence → **1,470 employees** |
| `TravelRarely` typo in `BusinessTravel` (8 rows) | Standardised to `Travel_Rarely` |
| 57 missing `YearsWithCurrManager` | Imputed with median of employees with the same `YearsInCurrentRole`, capped at tenure; flagged in `YearsWithCurrManager_Imputed` |
| Constant columns `EmployeeCount`, `StandardHours`, `Over18` | Dropped |
| `AgeGroup`, `SalarySlab` | Re-derived and validated; ordered categories |
| Logical checks (role tenure ≤ company tenure, etc.) and IQR outlier scan | All passed; outliers are plausible and kept |
| New columns | `AttritionFlag`, `TenureBand`, `DistanceBand`, `EducationLabel`, `PerformanceLabel`, `AvgSatisfaction` |

## Notes

- The risk model is a random forest trained on this dataset only; scores are cross-validated and meant
  for *relative* prioritisation, not as the probability that a given person will leave.
- Feature importance and correlations show association, not causation.
- Small segments produce volatile attrition rates; tooltips show headcounts and heatmaps hide cells below a minimum size.
"# hranalyticsalenjoye" 
"# hranalyticsalenjoye" 
"# hranalyticsalenjoye5" 
"# hranalyticsalenjoye5" 
