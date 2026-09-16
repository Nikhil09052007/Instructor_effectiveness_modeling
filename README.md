# Instructor Effectiveness Modeling — split notebooks

`Accredian_Assignment.ipynb` has been split into six notebooks, one per part of the
original notebook. All original cells and their saved outputs are preserved.

| # | Notebook | Covers |
|---|----------|--------|
| 1 | `01_Data_Ingestion_and_Preparation.ipynb` | Loading the CSV, shape/dtypes/nulls/duplicates, column-by-column inspection of all 12 features |
| 2 | `02_Data_Interpretation_and_EDA.ipynb` | Column classification and interpretation, distributions, boxplots, correlation heatmap, bivariate plots, instructor- and course-level effectiveness, EDA summary |
| 3 | `03_Instructor_Level_Aggregation.ipynb` | Aggregating 2000 batch rows to 120 instructors, weighted effectiveness score, Low/Medium/High tiers |
| 4 | `04_Machine_Learning_Model.ipynb` | Feature setup, train/test split, scaling, Random Forest training |
| 5 | `05_Model_Evaluation.ipynb` | Accuracy, classification report, confusion matrix, metric trade-offs |
| 6 | `06_Interpretation_and_Analysis_Questions.ipynb` | Feature importance, product implications, the 5 mandatory analysis questions |

## Run order

Run them 1 → 6. Notebooks 3–6 depend on earlier results, so a short **setup cell**
was added at the top of each (clearly marked as added during the split):

- **3** re-loads the raw CSV, and at the end writes `artifacts/instructor_level_data.csv`
- **4** reads that CSV back, and at the end writes `artifacts/model_bundle.joblib`
  (model, scaler, feature list, test split)
- **5** and **6** load `artifacts/model_bundle.joblib`

The `artifacts/` folder is created automatically next to the notebooks the first
time notebook 3 runs.

Notebooks 1 and 2 already loaded the data themselves in the original, so they were
left untouched.

## Things to check on your machine

- The dataset path is still the original absolute Windows path:
  `C:\Users\acer\Desktop\Programs\Accredian-Assignment\data\instructor_effectiveness_dataset_2000_rows - ...csv`
  It appears in notebooks 1, 2 and 3 (as `DATA_PATH` in 3). Consider switching to a
  relative path like `data/instructor_effectiveness_dataset.csv` so the project is portable.
- Notebook 4's setup restores `effectiveness_tier` as an ordered category
  (`Low < Medium < High`) after the CSV round-trip, since CSV does not keep dtypes.
- Notebook 6 now contains an actual feature-importance chart. The original text
  referred to "the Feature Importance chart" but no such cell existed, so one was
  added from the Part 4 model.
- `joblib` is required by notebooks 4–6 (`pip install joblib`; it ships with scikit-learn).
