---
name: fit-svm
description: Fit and compare SVM classifiers and produce a one-page report. Load only when explicitly invoked as fit-svm. Keep this file outside automatically discovered skill folders.
---

# Fit SVM classifiers

1. Receive the data, response, predictors, categorical coding, and seed in the invocation; request missing essentials. Never invent results.
2. Check class counts, missingness, predictor types, identifiers, dependence, and sample size. Explain suitability for SVM classification; use grouped or temporal validation if independence is implausible, or explain why analysis cannot proceed.
3. For independent observations, reserve a stratified 30% test set using seed 432 unless specified. Set each class's test count to floor(0.30*n_class + 0.5); ensure both subsets retain every class. Record counts and indices; leave test outcomes unused until final evaluation.
4. On training data, fix five stratified CV folds shared by all candidates; reduce fold count if class sizes require it. Fit imputation, encoding, and numeric standardization within each analysis fold only; apply learned transformations to its validation fold.
5. Consider linear and radial-basis-function kernels to compare a simple boundary with a flexible nonlinear boundary. Include polynomial kernels only with a stated interaction or curvature rationale; explain inclusions and exclusions before tuning.
6. Tune C for every kernel, gamma for RBF, and degree/gamma/coef0 for polynomial if included. State the exact kernel formula and software parameterization. Prespecify a modest log-spaced C/gamma grid and a small degree grid; document any training-only grid expansion.
7. Prespecify mean CV misclassification rate as the primary criterion; use balanced error instead when class imbalance and the scientific objective warrant it. Fix class weights and decision rules using training data only; tune any weights or thresholds inside CV.
8. Save each candidate's fold errors, mean, and SE = SD(fold errors)/sqrt(number of folds). Note that correlated folds make this SE an approximate selection heuristic, not a confidence interval.
9. Use the one-SE rule: retain candidates with mean error <= minimum mean error + SE of that minimum. Prefer linear, then polynomial by increasing degree, then RBF; within a kernel prefer smaller C, then smaller gamma, then smaller coef0. Specify any remaining tie-break before tuning.
10. Compare the best linear candidate with the minimum-error candidate; state whether their CV gap exceeds the minimum candidate's one SE. Describe selection uncertainty without claiming statistical significance.
11. Freeze all choices, refit preprocessing and the selected SVM on all training rows, and evaluate once on the test set. Never revise the selected model or skill based on test performance.
12. Save one executable script, package versions, seed, split/fold indices, candidate results, selected parameters, and test predictions. Generate all reported numbers, figures, and tables from that run's saved results; do not copy numbers from earlier runs.

## Report and verification

1.Produce at most one printed US Letter page with 11-point text, including figure/table labels; prioritize evidence for the final model.
2.Include data suitability, coding and split counts; kernel rationale; preprocessing, tuning grid and CV; selection rule and uncertainty; selected kernel/parameters; and test performance with limitations.
3.Use exactly one compact figure showing candidate CV errors with SE bars, the selected model, and the one-SE cutoff; fit the axis range to the estimates and bars so small differences remain visible.
4.Use exactly one compact table with each kernel's minimum-CV candidate and the selected model (deduplicate rows), tuning values, mean CV error, and SE; give test results only for the selected model.
5.Report test errors/total, error rate, accuracy, and approximate binomial error-rate SE when independent test observations justify it. Give binary confusion counts as TN/FP/FN/TP in prose, identifying the positive class; for multiclass, embed a labeled matrix panel in the single figure.
6.Interpret predictive performance and whether nonlinear flexibility is supported; do not treat SVM parameters as causal effects or ordinary regression coefficients.
7.Check leakage, split/fold integrity, selected parameters, one-SE arithmetic, confusion totals, and agreement of all numbers with saved results. Briefly state checks and any corrections actually made.
8.Render the report and verify one-page length, 11-point text, legibility, and no clipping; shorten content rather than shrink fonts.
9.Append the complete SKILL.md after the report, outside its one-page limit; attach the executable script and saved results separately without duplicating the invocation.
