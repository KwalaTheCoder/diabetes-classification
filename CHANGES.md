# Audit and refactor

Treats zero Glucose, BloodPressure, SkinThickness, Insulin and BMI as missing measurements. Medians are fitted within training folds. Removes global SMOTE and PCA fitted outside CV. Safe domain ratios, class-weighted baselines and ensembles are selected by CV; all metrics use the selected model's predictions.

Original algorithms and historical outputs remain in legacy/. No production dataset was available during refactoring; new real-data metrics remain unmeasured. See README.md for the reproducible evaluation protocol.
