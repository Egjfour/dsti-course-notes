|       Course Name        |      Topic       |   Professor    |       Date       |    Tags     |
| :----------------------: | :--------------: | :------------: | :--------------: | :---------: |
| **Time Series Analysis** | Time Series Data | Julien Jacques | 10 novembre 2025 | #Statistics |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251110%5F085356%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ec103c39f%2D8a09%2D4e8c%2Db9e8%2D2155990c8f03)

# Summary
*Time series analysis represents the methods to understand and importantly forecast time-series data. Among this understanding, the most important metric to understand is the autocorrelation because this demonstrates potential trends or seasonal/cyclic patterns. Statistical testing can be used to identify relevant autocorrelations.*

# Key Takeaways
1. Irregular time series are impossible to forecast, but we can forecast their variance
2. Using basic [[Simple Linear Model|regression]] or ML methods is undesirable since they weight each point equally
3. There is a linear decrease in empirical autocorrelation as $h$ increases since the sample size gets smaller for calculating the correlation
4. If we reject the [[Hypothesis Testing|null hypothesis]] of the Box-Pierce test, we state that at least one of the lags have significant autocorrelation
5. A t-test cannot be used in the presence of autocorrelation since t-tests assume independent and identically distributed observations
6. Before deployment, the model needs to be re-estimated on the entire dataset to produce reliable forecasts
7. The [[Testing|train/validation/test split]] for time-series models must be time-dependent with validation and test sets being the second-most and most recent timeframes

# Definitions
- Time Series: A series of points in time order
- Autocovariance: The [[Descriptive Statistics|covariance]] between lagged values
	- $\hat\sigma_n(h) = \frac{1}{n-h_t}\underset{t}{\overset{n-h}{\sum}}(x_t - \bar x_n)(x_{t+h} - \bar x_n)$
- Autocorrelation: The autocovariance scaled by the variance to produce values between -1 and 1
- Backtesting: Iteratively move through the data and hold out successive horizons to get multiple comparisons ([[Variable Selection - Linear Model|cross-validation]] for time series data)
# Additional Resources
- [Book - Forecasting: Principles and Practice](https://otexts.com/fpp2/intro.html)
- [ts Function in R](https://www.rdocumentation.org/packages/stats/versions/3.6.2/topics/ts)

# Notes
## Time-Series Data and Simple Forecasting
- Problem statement
	- A time series is a time-ordered [[Real Numbers, Real Sequences, and Limits|sequence]] of equally-spaced elements
	- The primary goal is to <mark style="background: #FFB86CA6;">forecast the future</mark>
- To perform this forecast, we find the different patterns in the time series
	- Periodicity: A time series being affected by a seasonal factor consistently across several periods with a fixed and known period frequency
	- Trend: Long-time increase or decrease - not necessarily linear
	- Cyclic: Rises and falls that appear seasonal but are <mark style="background: #FFB86CA6;">not of a fixed frequency</mark>
		- Tend to be more difficult to forecast since they are not fixed
- Forecasting with a [[Simple Linear Model|simple linear model]]
	- The timestamp is the independent variable and the series is the dependent variable
	- Any regression or ML model can theoretically be used
		- But these <mark style="background: #FFB86CA6;">weight each point equally for the forecast</mark>
	- This data also violates the iid assumption since $X_t$ is *usually* dependent on $X_{t-1}$
## Handling Time-Series Data in R
- The `ts` object is specifically designed for working with time-series data
	- The start and end date are provided as a vector `c({first_period}, {second_period})`
	- The frequency of the periodicity is provided as an integer
	- Example: `ts(data, start = c(2020, 1), end = c(2025, 12), freq = 12)`
- The `forecasts` package provides additional utilities
	- `autoplot` which is built off `ggplot2`
	- `ggseasonplot` which lets us see each period as a separate line to look for seasonality and check assumptions
- Missing data in the time series can be imputed using `imputeTS`
	- We can inspect missing observations using `ggplot_na_distribution(x: ts)`
	- The simplest imputation method is to do simple interpolations between the points on either side
		- `imputeTS::na_interpolation(x: ts)`
		- Linear, spline, and other methods (including using forecasted values) can be used
- Aggregating Time Series
	- Useful for seeing trends over time since it suppresses noise
	- In R, `aggregate(x: ts, nfrequency: int)`
		- `nfrequency` is the <mark style="background: #FFB86CA6;">number of elements per period</mark>
- Subset/Indexing Time Series
	- The `window` function should be used for this since using vector slicing will return a vector and not a time-series ovject
## [[Descriptive Statistics|Descriptive Statistics]] for Time-Series Data
- The empirical mean and variance use the traditional formulae
- Autocovariance and autocorrelation are most useful for determining the model specification
	- Autocorrelation is shown as a correlogram where the lag is on the x-axis and the correlation is on the y-axis (`acf(x: ts)` to generate the plot in R)
	- If the <mark style="background: #FFB86CA6;">autocorrelation is within the blue lines on the plot, it is not statistically significant</mark>
	 ![[Pasted image 20260102113520.png]]
	- A pure linear trend would show $\hat\rho_n(h)\underset{n\to\infty}{\to}1$
		- In practice, we see a linear decrease because of the shrinking sample size
	- A pure seasonal trend would show $\hat\rho_n(h)\underset{n\to\infty}{\to}cos(2\pi h/T)$
- Empirical Partial Autocorrelation (`pacf(x: ts)` in R) handles for the <mark style="background: #FFB86CA6;">influence of autocorrelation for previous lags</mark>
	- Example: Even if no autocorrelation exists for $h=3$, it would still show some because of the autocorrelation for $h\le 2$
	- We essentially do a linear regression of $X_t$ over the precious variables. Then, calculate the correlation between $X_{t-h}$ and $\epsilon_t$ (the residual)
	 ![[Pasted image 20260102115124.png]]
## Statistical Tests for Time Series
- The Box-Pierce test analyzes the [[Hypothesis Testing|significance]] of the autocorrelation
	- Hypotheses
		- $H_0:$ The time series is uncorrelated, asymptotically follows $\chi^2_h$
		- $H_1:$ This is not the case
	- The test stat is $Q_{BP} = n \underset{k=1}{\overset{h}{\sum}}\hat\rho^2_k$
	- In R, `Box.test(x: ts, lag: int, type: str = "Box-Pierce")`
	- Rejecting means that at least one of the lags $\le h$ has significant autocorrelation
	- The selection of $h$ is crucial and should be significantly large, but <mark style="background: #FFB86CA6;">if it is too large, the power decreases and nothing is detected</mark>
- The Ljung-Box test is a more powerful version of Box-Pierce
	- $Q_{LB} = n(n+2)\underset{k=1}{\overset{h}{\sum}}\dfrac{\hat\rho_k^2}{n-k}$
	- Asymptotically follows $\chi^2_h$
- Can also test for parametric trends
	- Linear
		- Function `notrend_test(x: ts)` from `funtimes` package
		- Can also use `wavk_test` and specify the exact trend expected
			- `wavk_test(x ~ poly(t, 2))`
	- Monotonic
		- Also uses `notrend_test` using the Mann-Kendall test statistic
## Forecast Evaluation and Tuning
- A data split is necessary to evaluate forecast accuracy and this split must be temporal
	- The size of the validation and/or test set depends on the forecast horizon and/or the seasonal patterns/length of the period
- Cross-validation/backtesting is necessary to ensure there are enough comparisons
	- The function `tsCV` in R lets us perform the cross validation
- Metrics
	- Classic metrics are [[Evaluation of ML Models & Improving Results|RMSE and Mean Absolute % Error]]
	- These metrics must be modified since the length of the training set is not the same for each fold of a temporal cross validation - with $m$ as the length of the training set:
		- $RMSE = \sqrt{\dfrac{1}{n-m}\underset{h=1}{\overset{n-m}{\sum}}(\hat x_{m,h} - x_{m+h})^2}$
		- $MAPE = \dfrac{100}{n-m}\underset{h=1}{\overset{n-m}{\sum}}\dfrac{|\hat x_{m,h} - x_{m+h}|}{x_{m+h}}$