# econ3916-lab15-bias-variance
# The Bias-Variance Tradeoff: Choosing How Flexible a Model Should Be

## Objective
I used a simulated world with a known true curve to see how prediction error splits into bias and variance, and how to choose a model's flexibility without seeing the truth.

## Methodology
- Fitted polynomials of six degrees to 200 fresh samples each and split their error into bias squared and variance.
- Compared training error with error on 2,000 new points for degrees 1 to 15.
- Chose a degree by 5-fold cross-validation and looked at how much the error varied from fold to fold.
- Used nested cross-validation to check whether the smallest CV error is a fair estimate of the error on new data.
- Wrote a function, kfold_mse(), that gives the k-fold CV error for any degree and number of folds, and used it to rerun the comparison with 10 folds.
- Fitted minimum-norm polynomials far past the point where they can pass through every training point.

## Key Findings
- Variance stayed near 0.02 through degree 5 (0.0180) and climbed to 0.0994 at degree 15, while bias squared fell close to zero.
- Training error fell at every degree, but held-out error was lowest at degree 5 and rose after it.
- 5-fold cross-validation chose degree 4, with a CV MSE of 0.1401.
- Nested cross-validation estimated the error at 0.2070, so the smallest CV error was an optimistic estimate of how the chosen model would do on new data.
- With 10 folds, my kfold_mse() function gave 0.1409 for degree 4 and 0.1457 for degree 5. The ranking held, but the gap between them narrowed.
- Past the interpolation point, held-out error peaked near 10^24 around degree 51, then fell again to 0.32 by degree 991. It never got below the error of the degree-5 polynomial.
