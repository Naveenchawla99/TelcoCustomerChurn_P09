# R8: the decision


```text
WE CHOOSE      The regularised logistic regression (the baseline), scored as a
               weekly batch job.

BECAUSE        R5 evidence against both alternatives (same 5x5 folds, training split):
               - forest - linear:   [mean] ± [sd], wins [k]/25, Holm p = [p]  -> [not shown to be different]
               - boosting - linear: [mean] ± [sd], wins [k]/25, Holm p = [p]  -> [not shown to be different]
               - Consistent with R2 (linear 0.287 ± 0.009) and R4 (both tuned ensembles
                 0.291 ± 0.012): a gap of ~0.004, inside the spread. The ensembles' scores
                 were selected from 30 candidates on the same data, so they are optimistic.
               - Single held-out test split (noisy, ~141 flagged customers):
                 linear [x], forest [y], boosting [z].
               Property that matters for the R1 deployment (R6/R7): the retention
               team needs a reason for every flagged customer. The linear model gives
               exact additive log-odds contributions from [40] coefficients; the forest
               stores [N] nodes and visits [n] per prediction, boosting [M] and [m], and
               both need an extra tool (SHAP) for per-customer reasons. Seconds do not
               matter for a weekly batch job.

WE GIVE UP     Whatever the ensembles did better: [e.g. higher test recall@10% by x, only
               if the tables show it] and automatic interaction handling. The linear model
               keeps the redundant "no internet service" columns, so individual coefficients
               in that group are unstable and should be explained as a group.

WE WOULD
RECONSIDER IF  On a fresh sample the model has not seen (e.g. next month's scored
               customers), an ensemble beats linear on recall@10% by at least 0.02 with a
               Holm-adjusted p < 0.05 on the same repeated folds, AND the retention lead
               accepts SHAP-based reason codes; or weekly contact capacity grows well beyond
               10% of customers, in which case the metric itself must be re-chosen.
```

## R5 limitations

The tuned ensembles were tuned on the same training rows that the paired comparison uses, while the linear baseline was not tuned, so any ensemble advantage here is an upper bound. The 25 scores come from 5 repeats of 5-fold cross-validation, so training sets overlap heavily and the fold differences are correlated: the plain standard deviation understates the uncertainty, and the overlap-corrected t-test (Nadeau-Bengio, Holm-adjusted over three pairs) only partly repairs that. "Not shown to be different" means the data cannot separate the models, not that they are equal. Each test fold holds about 1,127 customers (~113 in the top 10%), so recall@10% is coarse, and the separate test split (1,409 rows, ~141 flagged) is noisier still. It is one dataset and one metric, so the verdict does not transfer to other data or to a different contact capacity.
