---
name: compare-clusters
disable-model-invocation: true
description: Compare clustering algorithms and report one selected solution in R or Python. Load ONLY when the user explicitly invokes compare-clusters; never activate automatically for general clustering questions.
---

# Compare clusters

## Inputs
Obtain the data path, observation unit, feature columns, ID column, optional external labels, and output path from the invocation. Keep this skill independent of dataset names, variable names, and results. If data are unavailable, request them; never substitute data or invent findings. Use R or Python; save runnable code, package versions, and seed 432 outside the report.

## Preprocess
Use rows as observations. Separate IDs and external labels BEFORE exploration, preprocessing, tuning, or selection. Use only supplied features. Check dimensions, types, missingness, duplicates, and constant features. Remove all-missing and zero-variance features; median-impute other missing numeric values and document counts. Investigate duplicates rather than silently deleting observations. Avoid transforming already transformed data again. Center and scale numeric features to unit variance; justify departures using feature properties alone.

For high-dimensional numeric data, apply PCA to the standardized matrix, retaining the smallest number of components explaining at least 90% of variance, bounded by matrix rank. Do not whiten. Otherwise use the standardized matrix. Use the SAME representation and Euclidean distance for all candidates and silhouette scores. Report retained dimensions and variance. Use a two-dimensional projection for display only; an embedding is not a clustering algorithm.

## Compare and select
Before viewing labels, fit at least THREE distinct clustering algorithms:
1. K-means: k-means++ initialization, at least 50 starts per k.
2. Agglomerative hierarchical clustering: try Ward and average linkage.
3. Spectral clustering: RBF affinity; try gamma = c / median(d^2), c in {0.5, 1, 2}, where d^2 denotes positive off-diagonal squared Euclidean distances. Use at least 50 starts for label-assignment k-means. Handle a zero denominator explicitly.

For each, try k = 2,...,min(6, n-1). Never derive k from known classes. Exclude failed fits, fewer than two populated clusters, and singleton clusters. If three algorithms cannot be fitted, explain the obstacle rather than claiming completion.

Compute mean silhouette in the common representation for every valid candidate. Assess stability using 50 seeded 80% subsamples without replacement: refit imputation/scaling/PCA and the candidate on each subsample, keeping its hyperparameters fixed; compare its partition with the full-data partition restricted to those rows using adjusted Rand index (ARI). Record mean ARI and failures; require at least 40 valid runs. This ARI measures partition stability, not agreement with known classes.

Among eligible candidates within 0.02 of the largest silhouette, select the highest mean stability ARI; break ties by smaller k, then simpler algorithm. Keep the complete comparison log outside the report. Report weak separation or instability honestly; selection does not prove distinct populations exist. Check sensitivity of the selected solution to nearby PCA variance thresholds without labels; disclose contradictory findings.

## Interpret and report
Freeze the selected algorithm, k, tuning, and assignments BEFORE opening external labels. Only then optionally cross-tabulate labels and selected clusters or compute external ARI. Never use labels to revise selection. Avoid equating clusters with diagnoses or causal mechanisms.

Generate an analysis report of NO MORE THAN ONE PRINTED PAGE, including ALL text, figures, captions, and tables. Present clustering results from ONLY ONE selected method. Briefly name other algorithms and selection criteria, but do not show their scores, assignments, cluster counts, plots, or tables.

Include data dimensions; preprocessing; selected settings; selected silhouette and stability; group sizes; one readable PCA scatterplot colored by selected cluster with axis variance percentages; and concise interpretation and limitations. Optionally add external labels as point shapes or a small contingency table if space permits. Explain that the plot is a projection and that high dimension, small samples, preprocessing, or batch effects can limit conclusions.

Append the COMPLETE, verbatim SKILL.md after a forced page break; this appendix is outside the one-page analysis limit. Export PDF or self-contained HTML with embedded assets. Render or print-preview the final artifact: all analysis content must fit on page 1 at readable size, and the appendix must start on page 2. Revise layout if necessary. Check reported numbers against saved computations; keep unselected methods' results out of the report and appendix. Confirm SKILL.md is at most 5,000 UTF-8 bytes.
