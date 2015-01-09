# Minuit notation

From RootUserGuide.

## 5.14.4 Reliability of Minuit Error Estimates

Minuit always carries around its own current estimates of the parameter errors, which it will print out on request, no matter how accurate they are at any given point in the execution. For example, at initialization, these estimates are just the starting step sizes as specified by the user. After a HESSE step, the errors are usually quite accurate, unless there has been a problem. Minuit, when it prints out error values, also gives some indication of how reliable it thinks they are. For example, those marked CURRENT GUESS ERROR are only working values not to be believed, and APPROXIMATE ERROR means that they have been calculated but there is reason to believe that they may not be accurate.

If no mitigating adjective is given, then at least Minuit believes the errors are accurate, although there is always a small chance that Minuit has been fooled. Some visible signs that Minuit may have been fooled:

* Warning messages produced during the minimization or error analysis
* Failure to find new minimum
* Value of EDM too big (estimated Distance to Minimum)
* Correlation coefficients exactly equal to zero, unless some parameters are known to be uncorrelated with the others
* Correlation coefficients very close to one (greater than 0.99). This indicates both an exceptionally difficult problem, and one which has been badly parameterized so that individual errors are not very meaningful because they are so highly correlated
* Parameter at limit. This condition, signaled by a Minuit warning message, may make both the function minimum and parameter errors unreliable. See the discussion above ‘Getting the right parameter errors with limits’

The best way to be absolutely sure of the errors is to use ‘’independent’‘calculations and compare them, or compare the calculated errors with a picture of the function. Theoretically, the covariance matrix for a’‘physical” function must be positive-definite at the minimum, although it may not be so for all points far away from the minimum, even for a well-determined physical problem. Therefore, if MIGRAD reports that it has found a non-positive-definite covariance matrix, this may be a sign of one or more of the following:

### 5.14.4.1 A Non-physical Region

On its way to the minimum, MIGRAD may have traversed a region that has unphysical behavior, which is of course not a serious problem as long as it recovers and leaves such a region.

### 5.14.4.2 An Underdetermined Problem

If the matrix is not positive-definite even at the minimum, this may mean that the solution is not well defined, for example that there are more unknowns than there are data points, or that the parameterization of the fit contains a linear dependence. If this is the case, then Minuit (or any other program) cannot solve your problem uniquely. The error matrix will necessarily be largely meaningless, so the user must remove the under determinedness by reformulating the parameterization. Minuit cannot do this itself.

### 5.14.4.3 Numerical Inaccuracies

It is possible that the apparent lack of positive-definiteness is due to excessive round off errors in numerical calculations (in the user function), or not enough precision. This is unlikely in general, but becomes more likely if the number of free parameters is very large, or if the parameters are badly scaled (not all of the same order of magnitude), and correlations are large. In any case, whether the non-positive-definiteness is real or only numerical is largely irrelevant, since in both cases the error matrix will be unreliable and the minimum suspicious.

### 5.14.4.4 An Ill-posed Problem

For questions of parameter dependence, see the discussion above on positive-definiteness. Possible other mathematical problems are the following:

* Excessive numerical round off - be especially careful of exponential and factorial functions which get big very quickly and lose accuracy.
* Starting too far from the solution - the function may have unphysical local minima, especially at infinity in some variables.
