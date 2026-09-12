# Scoliosis Angle Measurement Reliability

This independent research project evaluates agreement and reliability among three scoliosis angle measurement pathways:

1. traditional manual Cobb-angle measurement;
2. spline-based measurement using human-marked vertebral centroids; and
3. spline-based measurement using neural-network-predicted vertebral centroids.

The project uses the released dataset associated with *Radiographic Scoliosis Angle Estimation: Spline-based Measurement Reveals Superior Reliability Compared to Traditional COBB Method*.

## Research questions

1. Does spline-based measurement produce greater interobserver reliability than traditional manual Cobb-angle measurement?
2. How closely do neural-network-assisted spline measurements agree with human-assisted spline measurements?
3. How frequently do observers disagree about the number and location of spinal curves in a radiograph?
4. How much measurement disagreement is associated with differences in selected end vertebrae?
5. Does measurement agreement vary according to curve magnitude?

## Current status

The complete first-version analysis is available. It includes data-quality assessment, anatomical curve matching, human interobserver reliability, neural-network agreement, endpoint-disagreement analysis, and exploratory grouped cross-validation.

Main findings:

- 543 unique radiographic cases;
- 495 cases complete across all 30 measurement columns;
- 511 cases with both human measurement pathways from all four observers;
- 527 cases with neural-network spline measurements;
- 1.86% of measurement cells missing; and
- maximum-angle ICC(A,1) of 0.917 for human-centroid spline measurement versus 0.867 for traditional manual measurement;
- matched-curve human MAE of 2.42° for spline measurement versus 3.39° for manual measurement;
- neural-network maximum-angle MAE of 1.63° and CCC of 0.950 against the median four-human spline consensus; and
- a positive but weak relationship between endpoint and angle disagreement (Spearman \(\rho=0.155\)).

## Repository structure

```text
scoliosis-angle-reliability/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   ├── README.md
│   ├── raw/                  # Raw CSV stored locally; not committed
│   └── processed/            # Patient-level derived CSVs; not committed
├── notebooks/
│   ├── 01_data_understanding.ipynb
│   ├── 02_curve_matching.ipynb
│   ├── 03_human_reliability.ipynb
│   ├── 04_neural_network_agreement.ipynb
│   └── 05_final_results.ipynb
├── src/
│   ├── week1_analysis.py
│   ├── curve_matching.py
│   ├── statistics_utils.py
│   └── full_analysis.py
├── scripts/
│   └── build_project_notebooks.py
├── tests/
│   ├── test_curve_matching.py
│   └── test_statistics_utils.py
├── outputs/
│   ├── figures/              # Shareable aggregate figures
│   ├── tables/               # Aggregate result tables
│   ├── week1_results.json
│   └── final_results.json
├── reports/
│   └── weekly/
│       ├── week_01_progress.md
│       ├── week_02_curve_matching.md
│       ├── week_03_human_reliability.md
│       ├── week_04_neural_network_agreement.md
│       └── week_05_final_synthesis.md
├── paper/
│   └── research_report_draft.md
└── docs/
    ├── analysis_plan.md
    └── data_dictionary.md
```

## Getting started

### 1. Download the data

Download the released CSV from the [Mendeley dataset page](https://data.mendeley.com/datasets/ssfmrw2fg9/2). Rename it:

```text
scoliosis_measurements.csv
```

Place it in:

```text
data/raw/scoliosis_measurements.csv
```

The raw file is intentionally excluded from Git version control. Review the dataset's license and terms before distributing any data.

### 2. Create a Python environment

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

On Windows, activate the environment with:

```powershell
.venv\Scripts\activate
```

### 3. Reproduce the analysis

```bash
python src/week1_analysis.py --input data/raw/scoliosis_measurements.csv
python src/full_analysis.py --input data/raw/scoliosis_measurements.csv
```

The first command rebuilds the cleaning and descriptive outputs. The second rebuilds the curve matching, reliability, neural-network agreement, endpoint, model, table, and figure outputs.

### 4. Open the learning notebooks

From the repository root, run:

```bash
jupyter lab
```

Open the numbered notebooks in order. The notebooks explain the reasoning and verified findings, while the reusable implementation lives in `src/`.

The scripts write patient-level CSVs to `data/processed/` and aggregate results to `outputs/`. Patient-level outputs are ignored by Git.

### 5. Run the tests

```bash
python -m unittest discover -s tests -v
```

## Interpretation note

This dataset does not contain an unquestionable ground-truth Cobb angle. The project therefore focuses on **agreement** and **reliability**, not proof that one measurement is objectively accurate. The neural-network results also do not constitute independent external validation because the released CSV does not identify the original train-validation split.

## Data sources

- [Research article](https://link.springer.com/article/10.1007/s00586-020-06577-3)
- [Released dataset](https://data.mendeley.com/datasets/ssfmrw2fg9/2)

## Author

Kayla

Undergraduate Data Science student, University of California, Davis

## Project status

Complete first-version independent analysis and working manuscript. This repository is not peer reviewed or a clinical tool, and its outputs should not be used for diagnosis or treatment decisions.
