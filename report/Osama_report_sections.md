# Random Forest report sections for review

## Exploration

Bodyweight and bench press have a positive training correlation of 0.651, but there is considerable spread at a given bodyweight. The training median bench is 62.5 kg for recorded F entries and 132.5 kg for M entries. Median bodyweight also differs, at 66.6 and 88.2 kg, so these distributions do not isolate an effect of sex.

Age has a weak overall linear correlation with bench (0.070), but the age-group plot shows a non-linear pattern, especially among M entries. Group medians peak in middle age ranges and decrease at older ages. The groups can differ in bodyweight and other factors, so this is a cross-sectional association, not evidence of how one lifter changes over time. There are 28,210 M and 11,790 F training entries; the density plot normalizes within sex to avoid confusing frequency with distribution shape.

Insert figures 01, 02 and 03 from `results/figures/`.

## Method

We used scikit-learn's RandomForestRegressor for two models. Model A used bodyweight only. Model B also included age and recorded sex, encoded as F=0 and M=1. Both used the same 40,000 training and 10,000 test entries as Linear Regression. Random Forest did not require scaling.

The forest averages predictions from 150 trees trained on bootstrap samples. We compared five depth and leaf-size settings using five-fold CV on training entries. The same folds were used for both configurations. Settings were chosen using the lowest CV RMSE, then each selected forest was refitted on all training entries. The test set was used only after selection.

Model A selected maximum depth 10 and minimum leaf size 20.

Model B selected maximum depth 10 and minimum leaf size 20.

## Evaluation

The bodyweight-only forest achieved test MAE 26.10 kg, RMSE 33.64 kg and R² 0.464. Adding age and sex changed these to MAE 18.28 kg, RMSE 24.21 kg and R² 0.722. The added features reduced MAE by 29.9% and RMSE by 28.0% on the same test entries. This supports their joint predictive usefulness in this sample, not a causal interpretation or a separate estimate of each feature's contribution.

Training RMSE was 32.62 kg for A and 23.43 kg for B, compared with 33.64 and 24.21 kg on the test set. These relatively small gaps give limited evidence of overfitting in the selected forests. CV selected regularization without inspecting test predictions. The prediction plots show that both forests tend to pull extreme results towards the middle. High actual bench results are often underpredicted. Model B lies closer to the perfect-prediction line overall, but some large errors remain.

| Model | MAE (kg) | RMSE (kg) | R² |
| --- | --- | --- | --- |
| A Bodyweight only | 26.10 | 33.64 | 0.464 |
| B Bodyweight + age + sex | 18.28 | 24.21 | 0.722 |


Insert figures 04 and 05 from `results/figures/`.

## Limitations

The training RMSE values were 32.62 kg for Model A and 23.43 kg for Model B. The test errors were slightly higher, but these small gaps do not suggest substantial overfitting in the selected forests. This does not rule out optimistic evaluation caused by repeated lifters. A forest also struggles to extrapolate beyond its training results.

The data contain repeated competition entries. In our approximate name audit, 1,640 of the 10,000 test entries had a name also seen in training. Names are not unique athlete IDs, but this overlap means the results should not be presented as performance on entirely new lifters. We kept the agreed split unchanged. A shared athlete-grouped split would be useful future work.

The results only apply to the selected raw competition entries with complete data, recorded F or M sex, positive results and ages 10-100. Adding age and sex together does not tell us how much improvement comes from each one. The findings describe predictive associations, not causes of strength differences.

## Sources

OpenPowerlifting September 19 snapshot and scikit-learn RandomForestRegressor documentation. Review these sections alongside the executed notebook before combining the report.
