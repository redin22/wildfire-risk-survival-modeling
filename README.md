# Wildfire Risk Modeling with Survival Analysis
A machine learning project for predicting wildfire time-to-threat across evacuation zones using survival analysis, gradient boosting, random survival forests, and cumulative risk probabilities.

Wildfire evacuation planning depends not only on whether a zone may be affected, but when it may become threatened. This project frames wildfire spread risk as a time-to-event prediction problem, where the event is a wildfire reaching an evacuation zone within 12, 24, 48 and 72 hours.

## Data
The dataset includes wildfire behavior, evacuation zone characteristics, distance-based risk features, weather or environmental signals, and engineered movement/growth indicators. The target captures whether and when a wildfire threatens a given evacuation zone.

## Modeling Approach

The project compares multiple approaches:

- Exploratory data analysis to understand wildfire spread patterns
- Feature engineering for fire movement, growth, distance, and seasonal risk
- Random Forest classification models for fixed prediction horizons
- Random Survival Forests for time-to-event modeling
- Gradient Boosted Survival models
- Cross-validation using a hybrid metric
- Monotonicity enforcement across cumulative time-horizon probabilities

## Monotonicity Constraint

Predictions were post-processed to enforce logical consistency across time horizons:

prob_12h ≤ prob_24h ≤ prob_48h ≤ prob_72h

This is required because the probabilities are cumulative. If a wildfire is predicted to threaten a zone within 12 hours, then that same event is also included within the 24-, 48-, and 72-hour windows.


## Evaluation

Models were evaluated using a hybrid score:

Hybrid Score = 0.3 × C-index + 0.7 × (1 - Weighted Brier Score)

The C-index measures how well the model ranks higher-risk zones, while the Brier score measures the accuracy of predicted probabilities. Since the task requires both good risk ranking and well-calibrated probability estimates, the hybrid metric balances both goals.

