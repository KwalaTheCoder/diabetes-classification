# Real-data evaluation — 2026-11-02

Input: `Diabetes/diabetes.csv`. Dataset SHA-256: `698c203a14aa31941d2251175330c9199f3ccdb31597abbba2a3e35416257a72`.

Model selection used only training-fold CV. One final holdout was reserved before preprocessing. The full CV leaderboard, dependency versions, seed, feature schema and split sizes are in [experiments/report.json](experiments/report.json).

- Model: **ExtraTreesClassifier**
- Training rows: **614**; holdout rows: **154**
- Selection metric: `f1_macro`; selected CV score: **0.759233**
- Dummy baseline CV score on the same folds: **0.394479**
- Five CV folds; seed 42; tuning: **True**
- Identical raw predictor rows grouped: **False**

| Metric | Holdout value |
|---|---:|
| accuracy | 0.733766 |
| balanced_accuracy | 0.739630 |
| f1_macro | 0.722523 |
| roc_auc | 0.812407 |
| average_precision | 0.685267 |

Accuracy 95% Wilson interval: [0.6589, 0.7973]. This treats holdout observations as independent; grouped duplicates reduce the effective sample size, so the interval is descriptive rather than a complete uncertainty estimate.


## Dataset-specific interpretation

This input is byte-for-byte identical to the diabetes.csv evaluated earlier; the existing locked evaluation is reused rather than retraining after seeing its holdout. Zero Glucose/BloodPressure/SkinThickness/Insulin/BMI are treated as missing. Label 1 denotes the supplied positive outcome. No clinical validity is established.

## Reproduce

Activate an environment with the project's requirements, change to the repository root, and run:

```cmd
python -m mlproject train --data "D:\data\Diabetes\diabetes.csv" --output artifacts --folds 5 --seed 42 --tune
```

Results were obtained with the dependency versions recorded in the JSON report. Different versions can change results slightly. Negative MAE selection scores are higher-is-better. CV scores are selection estimates and optimistic; the holdout is the final internal result. Hyperparameter tuning is enabled on the smaller datasets and diabetes; for credit, soccer, student and churn the default bounded candidate comparison is used. Scores are not directly comparable across datasets or tasks.

Do not tune against the now-observed holdout or claim improvement over the legacy notebooks: leakage, split policies and preprocessing differ. Raw data, row-level predictions and trained pickle artifacts are not included in this evidence commit.
