# Analysis Plan

## Primary objective

Evaluate whether spline-based Cobb-angle measurement improves interobserver reliability compared with traditional manual measurement, and assess agreement between human-assisted and neural-network-assisted spline measurements.

## Stage 1: Data understanding and quality control

- Inspect the released CSV structure.
- Rename the anonymized identifier column to `image_id`.
- Parse list-valued angle and endpoint columns safely.
- Distinguish missing values from valid empty lists.
- Describe missingness, curve counts, and angle distributions.
- Produce case-level QC and curve-level tidy representations.

Status: complete.

## Stage 2: Curve matching

- Represent each curve as a vertebral interval.
- Define and justify an interval-overlap matching rule.
- Handle one-to-many and unmatched curves explicitly.
- Test the rule on selected radiographs with obvious and ambiguous matches.
- Conduct a sensitivity analysis using at least one alternative matching threshold.

Status: complete. Primary IoU threshold: 0.50; sensitivity thresholds: 0.30 and 0.70.

## Stage 3: Human interobserver reliability

- Compare curve-count agreement among the four human observers.
- Match curves across observers within each radiograph.
- Calculate pairwise absolute angle differences.
- Evaluate interobserver reliability separately for traditional manual and human-centroid spline measurements.
- Use ICC only after confirming that the matched data and study design satisfy the selected ICC formulation.

Status: complete. Maximum-angle ICC and matched-curve agreement were evaluated.

## Stage 4: Neural-network agreement

- Compare neural-network spline curves with matched human spline curves.
- Compare matched neural-network and human curves, and separately construct a case-level reference from the median of the four human maximum spline angles.
- Report mean absolute difference and percentages within practical thresholds of 3 degrees and 5 degrees.
- Use Bland–Altman analysis to examine systematic bias and limits of agreement.

Status: complete. Maximum-angle consensus and matched-curve analyses were evaluated.

## Stage 5: Endpoint disagreement

- Quantify differences in selected upper and lower curve endpoints.
- Test whether endpoint disagreement is associated with angle disagreement.
- Examine whether disagreement changes with curve magnitude.

Status: complete. Endpoint association and grouped cross-validated exploratory models were evaluated.

## Interpretation constraints

- The dataset provides multiple measurements but no unquestionable ground-truth angle.
- Results should be described as reliability or agreement, not objective accuracy.
- Measurements must not be paired only by list position when observers identify different curves.
- The train-validation assignment for the released neural-network results is not available in the CSV, limiting claims about independent out-of-sample performance.
