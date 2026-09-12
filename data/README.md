# Data directory

The raw and patient-level processed datasets are not tracked by Git.

## Expected local files

```text
data/
├── raw/
│   └── scoliosis_measurements.csv
└── processed/
    ├── case_level_cleaned.csv
    ├── case_level_qc.csv
    └── curve_level_tidy.csv
```

Download the source dataset from:

https://data.mendeley.com/datasets/ssfmrw2fg9/2

Keep the source CSV unchanged. Cleaning and restructuring should create new files under `processed/` or a reproducible output directory.

Before publicly redistributing either the original data or patient-level derived tables, review the dataset's current license and terms on the source page.
