# econ3916-lab12-ols-prediction
# OLS as a Line of Best Fit: Estimation versus Prediction

## Objective
I tested the difference between using regression to estimate a relationship and using it to predict new outcomes, on California housing data.

## Methodology
- I fitted the same OLS line three ways (the closed form, statsmodels and scikit-learn) and got the same intercept and slope from all three.
- I added up to 100 columns of pure noise to a regression and watched R-squared rise every time, while adjusted R-squared did not.
- I split the data before fitting, and scored an eight-feature model on the rows it was fitted to and on test rows it never saw.
- I used one specification for two jobs: a coefficient with its 95% interval, and a test RMSE.
- I wrote a small function, holdout_rmse(), that scores any list of predictors on the same test rows, and used it on median income alone.

## Key Findings
- All three methods gave a slope of 0.4179: each extra $10,000 in median income goes with about $41,800 higher median house value.
- R-squared rose from 0.4734 with no noise to 0.4758 with 100 noise columns, so a higher R-squared doesn't mean a better model.
- The eight-feature model had a train RMSE of 0.7197 and a test RMSE of 0.7456, a typical error of about $74,600 on new districts.
- AveRooms had a coefficient of -0.0381 (95% CI [-0.0430, -0.0333]), precisely estimated, but the model using it still predicted poorly.
- With median income alone, the test RMSE was 0.8421, about $9,650 worse than with all eight features.
- 992 districts (4.8%) sit at the $500,000 ceiling. Dropping them shrank most coefficients toward zero (median income from 0.4487 to 0.4283) and lowered test RMSE from 0.7456 to 0.6429, but only because the hardest districts were removed, so the model now describes districts under $500,000, not all of California.
