|       Course Name        |        Topic         |   Professor    |       Date       |    Tags     |
| :----------------------: | :------------------: | :------------: | :--------------: | :---------: |
| **Time Series Analysis** | Multiple time series | Julien Jacques | 12 décembre 2025 | #Statistics |

[Class Video Link]([URL](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251212%5F095206%2DMeeting%20Recording%2Emp4&ga=1))

# Summary
*Handling of multiple time series is an essential element to time series forecasting. There are two main situations where this may arise: covariates for which the future is known and simultaneous forecasting of multiple related series. Many specifications exist to handle both of these situations, but they require additional consideration before and during implementation.*

# Key Takeaways
1. When other time series are used as covariates, the future values must be known
2. The cross covariance is used to show the link between two series
3. Like any of the models we've seen, function `checkresiduals` should be called

# Definitions
- Cross Covariance/Correlation: The degree to which the lagged covariate is [[Descriptive Statistics|correlated]] with the time series of interest
	- $CCF_h(x, y) = \dfrac{1}{n-h}\underset{t=1}{\overset{n-h}{\sum}}(x_t - \bar x_n)(y_{t+h} - \bar y_n)$

# Additional Resources
- [Dynamic Regression Chapter (fpp2)](https://otexts.com/fpp2/dynamic.html)
- [Vector Autoregressions (Econometrics with R)](https://www.econometrics-with-r.org/16.1-vector-autoregressions.html)

# Notes
## Other Series as Covariates
- Framework: Forecast $x_t$ and have another series $z_t$ for which the future is known
- Could use linear regression and include $z_t$ as covariates
	- In R, we can do this directly with `tslm`
		- `trend` and `season` can be automatically and directly added
- Other ML methods work the same way by adding $z_t$ and any desired lags
- To select the best features, we use standard penalized criterion like [[Variable Selection - Linear Model|AIC and BIC]] or [[Variable Selection - Linear Model|cross validation error]]
## Dynamic Regression Model
- Since a typical regression assumes i.i.d. residuals, a dynamic model estimates an $ARIMA_{pdq}$ model for these residuals instead
	- Same strategy as [[Probabilistic Time-Series Models|standard ARIMA procedure]]
	- But now, after removing the trend and seasonality, we also remove the effect of vocariates
- In R, we still use function `Arima` but add parameter `xreg` to include the covariate series
	- This same option exists for [[Machine Learning Based Time-Series Models|neural network based models]] in `nnetar`
- Other ML methods (RF, GBDT, etc.) do not handle this component separately, but rather include the covariates (and desired lags) to the input matrix
## Simultaneous Forecasting Multiple Series
- The framework is that we assume each time series can be useful in forecasting the other
- The Vector Autoregression Model ($VAR_p$)
	- We use the $p$ lags in each series to predict the others
- Example: $VAR_1$
	- $x_{1,t} = c_1 + \epsilon_{1,t} + a_{1,1}x_{1,t-1} + a_{1,2}x_{2,t-1}$
	- $x_{2,t} = c_2 + \epsilon_{2,t} + a_{2,1}x_{1,t-1} + a_{2,2}x_{2,t-1}$
- It's important to show there is a linear link between the two series
	- The cross-covariance is the metric that indicates this
	- We can use the `ccf` function in R or the `ccf.test` function and set param `max.lag`
- We can choose the best order using AIC from the package `vars` using `VARselect`
	- A trend can be indicated in this function using param `type`
	- Seasonality can be added with parameter `season`
	- External covariates can be added with parameter `exogen`
- A [[Overview and Basic Descriptive Statistics|box test]] cannot be used to check the residuals here, so instead we use the serial test
	- `serial.test({model}, lags.pt: int, type = "PT.asymptotic")`
	- Like before, the null hypothesis is that the residuals are white noise