---
name: analyze-lda-qda
description: Analyze classification data with LDA and QDA and produce a one-page statistical report. Load only when explicitly requested by name or by an explicit request to read this file; keep this file outside automatically discovered skill folders.
---

# Analyze LDA and QDA

Receive the dataset, response, predictor coding, and seed separately. Confirm class counts, numerical coding, missing values, and predictor dimensions. Exclude identifiers. Never infer or invent results.

1. Reserve a stratified 30% test set before exploration or model selection. Use seed 123 unless another seed is supplied. Do not inspect test errors until the model is selected.
2. Create five stratified cross-validation folds within the remaining training set. Fix the folds and use them for every candidate. Use empirical training priors unless the invocation specifies otherwise.
3. Compare ordinary LDA (one pooled covariance) and ordinary QDA (one full covariance per class). Also compare standardized PCA followed by LDA and by QDA at every feasible retained dimension from 1 to the number of predictors minus 1. Do not include classifiers outside these families.
4. Fit scaling, imputation if needed, PCA, class means, priors, and covariances using only the analysis rows of each fold. Apply those learned transformations to validation rows. Do not screen predictors or learn PCA on the entire dataset before cross-validation.
5. Check within-class rank for QDA after preprocessing in every fold. Reject a singular candidate; do not silently regularize it or label a pseudoinverse fit ordinary QDA. Record numerical warnings and condition concerns. Reject any candidate that fails in any fold.
6. Score candidates by the mean validation misclassification rate. Record all fold errors and their standard error (sample SD divided by sqrt(5)). Choose the minimum mean error, breaking exact ties by fewer retained dimensions and then LDA. Treat CV error as a selection estimate, not an unbiased final performance estimate. Settle skill revisions using training and CV evidence only.
7. Refit the chosen preprocessing and classifier on all training rows. Evaluate that frozen model once on the reserved test set. For comparison, also evaluate the pre-specified ordinary LDA and QDA baselines at this same final evaluation stage; never change the selected candidate using their test errors.
8. Save executable code, seeds, split indices, fold errors, and candidate results for reproducibility. Verify confusion matrix totals and report observed classes in rows and predicted classes in columns.

## Required report

Produce one clearly readable printed page (US Letter, at least 10-point body text) with one figure and one table. Include: dataset size and coding; train/test counts and seed; candidate models and fold-local preprocessing; CV procedure and minimum-CV choice; a table of ordinary LDA, ordinary QDA, and the selected candidate with dimensions, mean CV error, CV SE, and final test error; a figure of CV error against retained dimension for PCA-LDA and PCA-QDA; selected-model test confusion matrix, errors/count and error percentage; and key interpretations and limitations. Give the test error's approximate binomial SE when practical. Describe singularity or unstable covariance estimates, non-Gaussian or discrete predictors, limited test size, and selection uncertainty when relevant. Never claim the selected model is universally optimal. Verify the rendered report occupies one page without clipped text or unreadable labels.