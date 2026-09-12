# Data Dictionary

## Original case-level data

Each row represents one anonymized spinal radiograph. The first unnamed CSV column is renamed `image_id` during analysis.

### Sources

- `carl`, `peter`, `marlene`, and `wadim`: human investigators.
- `neuralnet`: neural-network-predicted vertebral centroids followed by spline-based angle calculation.

### Column families

| Pattern | Interpretation |
|---|---|
| `COBB_angles_<source>` | Spline-derived curve-angle list |
| `val_COBB_angles_<human>` | Traditional manual Cobb-angle list |
| `COBB_vertebrae_<source>` | Endpoint-index pairs for spline curves |
| `val_COBB_vertebrae_<human>` | Endpoint-index pairs for traditional manual curves |
| `upperVertebra_<source>` | Upper boundary of the visible or labeled vertebral range |
| `lowerVertebra_<source>` | Lower boundary of the visible or labeled vertebral range |

The `val_` neural-network fields duplicate the neural-network spline fields and are not treated as a separate traditional manual method.

## `case_level_qc.csv`

This derived table contains one row per radiograph and summarizes data availability and structure. It does not contain the individual curve angles.

| Pattern | Meaning |
|---|---|
| `has_spline_<source>` | The spline-angle cell is present; an empty list still counts as present |
| `n_spline_curves_<source>` | Length of the spline-angle list; zero means a recorded empty list and missing means unavailable |
| `has_manual_<source>` | The `val_` angle cell is present |
| `n_manual_curves_<source>` | Length of the `val_` angle list |
| `visible_upper_index_<source>` | Upper visible/labeled vertebral index |
| `visible_lower_index_<source>` | Lower visible/labeled vertebral index |
| `complete_all_human_spline` | Spline-angle lists are present for all four humans |
| `complete_all_human_manual` | Traditional manual-angle lists are present for all four humans |
| `complete_all_human_both_methods` | Both human pathways are present for all four humans |
| `has_neural_network_spline` | Neural-network spline-angle list is present |
| `complete_all_raw_columns` | Every original measurement cell is non-missing; empty lists count as present |

The fields named `has_manual_neuralnet` and `n_manual_curves_neuralnet` are mechanical QC summaries of duplicated neural-network `val_` columns. They do not represent a neural network manually drawing Cobb angles.

## `curve_level_tidy.csv`

This derived table contains one row per endpoint-complete measured curve.

| Column | Meaning |
|---|---|
| `image_id` | Anonymized radiograph identifier |
| `observer` | Human investigator or neural network |
| `source_type` | Human or neural network |
| `method` | Traditional manual, human-centroid spline, or neural-network-centroid spline pathway |
| `curve_order_cranial_to_caudal` | Curve position in the source list; not yet a cross-observer match identifier |
| `angle_deg` | Measured curve angle in degrees |
| `upper_endpoint_index` | Encoded upper endpoint for the curve |
| `lower_endpoint_index` | Encoded lower endpoint for the curve |
| `visible_upper_index` | Upper visible/labeled vertebral boundary for the radiograph-source record |
| `visible_lower_index` | Lower visible/labeled vertebral boundary for the radiograph-source record |

The numerical vertebral-index-to-anatomical-label mapping is not formally documented in the released data. The primary analysis therefore preserves the numerical indices.

## Additional private processed tables

These patient-level files are generated locally under `data/processed/` and excluded from Git.

| File | Purpose |
|---|---|
| `case_max_angles.csv` | One maximum angle per image and measurement source |
| `matched_curve_pairs_iou_050.csv` | One row per accepted curve pair at the primary IoU threshold |
| `per_image_human_disagreement.csv` | Mean of six human pairwise differences per image and pathway |
| `nn_consensus_cases.csv` | Neural-network maximum angles and median four-human spline references |

## Aggregate result tables

The following files contain summary statistics rather than patient-level records and are stored under `outputs/tables/`.

| File | Purpose |
|---|---|
| `matching_pair_summary.csv` | Match coverage and mean IoU for each observer pair |
| `matching_sensitivity.csv` | Aggregate match coverage at IoU thresholds 0.30, 0.50, and 0.70 |
| `human_reliability_summary.csv` | Maximum-angle ICC and per-image disagreement by human pathway |
| `human_pairwise_maximum_angle_metrics.csv` | Pairwise agreement statistics for each human observer pair |
| `human_matched_curve_metrics.csv` | Pooled matched-curve agreement for human spline and manual pathways |
| `neural_network_curve_metrics.csv` | Neural-network curve agreement overall and by human observer |
| `endpoint_disagreement_summary.csv` | Angle error summarized by endpoint-disagreement group |
| `exploratory_model_performance.csv` | Grouped cross-validated baseline, linear, and random-forest results |
| `exploratory_model_feature_importance.csv` | Random-forest impurity-based feature importances for interpretation |
