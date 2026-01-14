|       Course Name        | Topic |   Professor    |         Date          |    Tags     |
| :----------------------: | :---: | :------------: | :-------------------: | :---------: |
| **Time Series Analysis** | ARIMA | Julien Jacques | 10 & 11 décembre 2025 | #Statistics |

[Class Video Link 1](login.microsoftonline.com/e5d15069-41a2-48be-a3f3-d7f52db16425/oauth2/authorize?client_id=00000003-0000-0ff1-ce00-000000000000&response_mode=form_post&response_type=code%20id_token&resource=00000003-0000-0ff1-ce00-000000000000&scope=openid&nonce=39A2EDB579820A1937DB20E8F6913E7E851C8127806BB2BF-26F51F627FD6FFC6777EC7FFAB758ADEF006A9B995F241EF073D433DB5A6BED7&redirect_uri=https%3A%2F%2Fdstisas%2Esharepoint%2Ecom%2F_forms%2Fdefault%2Easpx&state=OD0w&claims=%7B"id_token"%3A%7B"xms_cc"%3A%7B"values"%3A%5B"CP1"%5D%7D%7D%7D&wsucxt=1&cobrandid=11bd8083-87e0-41b5-bb78-0bc43c8a8e8a&client-request-id=24ebeca1-b0fc-e000-e173-e340db5e55a5)
[Class Video Link 2](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251210%5F095530%2DMeeting%20Recording1%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E8a16bed8%2D76cd%2D4ef4%2D82f8%2D527bd55ac74b)
[Class Video Link 3](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251211%5F095049%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E81a278fc%2D0c86%2D4f31%2D87f0%2Db65908d5e358)

# Summary
*Probabilistic models are among the most well-known for time series forecasting. These models rely on isolating the residual component and directly modeling it (provided it isn't white noise). Some of these models require first processing the data with differencing to achieve stationarity while others bake this process directly into the model. Among these models, the seasonal ARIMA model is the one which handles for all components of a time series (trend, seasonality, and residuals) simultaneously and is therefore quite powerful and used in industry.*

# Key Takeaways
1. If there is a [[Exponential Smoothing Models|multiplicative trend]] to remove, we consider $ln(x_t)$ instead since it then becomes additive
2. If there is a periodicity, choose $m \ge p$ for the moving average trend estimation
3. Residual autocorrelation is used to find cyclic, not seasonal, trends
4. With a linear trend, a differencing of lag 1 extracts only the residuals
5. In particular, $\Delta_T$ reduces the degree of a polynomial trend by 1
6. $\Delta_T^k$ removes a seasonal pattern of period $T$ and a polynomial trend of degree $k$
7. Autocorrelation exponentially decreases to 0 as $h$ goes to infinity in an AR model, but in an ARMA model only after order $q+1$
8. Heteroscedastic time series can be stabilized using the power (square root) or Box-Cox transformation

# Definitions
- Decomposition: Separating a time-series into the seasonal pattern, trend, and residual
- Lag: The previous value of a time series at the specified time $T$ given a current time $t$
- Differencing ($\Delta_T$): A mapping of $x_t$ to the difference with the lag at time $T$, $x_t - x_{t - T}$
- Stationary Time Series: $x_t$ where for all $s$, the distribution of $(x_t, \dots, x_{t+s})$ does not depend on $t$
	- No trend or seasonal pattern
- White Noise: [[Conditional Probability and Independence|Independent]] and [[Distributions of Probability and Random Variables|identically distributed]] with zero mean
	- Gaussian white noise is $\sim \mathcal N(0, \sigma^2)$
- Autoregressive Model (order $p$): $x_t = c + \epsilon_t + \underset{j=1}{\overset{p}{\sum}} a_jx_{t-j}$
- Autoregressive Integrated Moving Average Model (order $pdq$): If, after differencing $d$ times, we have an $ARMA_{pq}$ model, $x_t$ is $ARIMA_{pdq}$
- Backshift operator: $B_{x_t} = x_{t-1}$ and $B(Bx_t) = B^2x_t = x_{t-2}$
	- Retrieve previous observation (potentially skipping some lines)
- Heteroscedastic: Variance is not constant over time

# Additional Resources
- Name the hyperlink in brackets then outside the brackets put the URL in parens

# Notes
## Probabilistic Models
- Probabilistic models seek to model a relationship in the residual component, $\epsilon_t$, of the time series: $x_t = S_t + T_t + \epsilon_t$ with $S_t$ the seasonal component and $T_t$ the trend
	- If $\epsilon_t$ are iid, there is nothing to model
	- Otherwise, the residuals are [[Overview and Basic Descriptive Statistics|correlated]], and we try to model this correlation
	- We must be able to <mark style="background: #FFB86CA6;">extract the residuals</mark> to do this modeling
	- Such models build on the [[Exponential Smoothing Models|Holt-Winters]] model by directly modeling the stochastic component, $\epsilon_t$, whereas HW only models $T$ and $S$
- Extracting the residuals (using the below decomposition methods) is important because <mark style="background: #FFB86CA6;">probabilistic models assume stationarity</mark> in the time series
	- Such time series may still have cyclic patterns since these are not regular
- Stationarity can be tested statistically, but the test is not powerful, so visual inspection is more commonly used
- Once we have a stationary series, we want to ensure it is not white noise
	- If this is the case, there is <mark style="background: #FFB86CA6;">nothing to model from the residuals</mark>
	- A [[Overview and Basic Descriptive Statistics|Box test]] can be used to test for white noise (we want to reject this test to prove)
## Moving Average Time Series Decomposition
- To remove the trend and seasonal component, we presume an additive decomposition
	- $x_t = T_t + S_t + \epsilon_t$
	- $log(x_t)$ is used if the trend is multiplicative
- The trend can be [[Point Estimators|estimated non-parametrically]] using a moving average
	- Model: $\hat T_t = \dfrac{1}{m}\underset{j=-k}{\overset{k}{\sum}}x_{t+j}$ with $m = 2l+1$
	- This model is an average of all points <mark style="background: #FFB86CA6;">before and after</mark> time $t$
	- As $m$ increases, the trend becomes smoother
	- The trend cannot be estimated for the first and last $m/2$ points
	- If there is periodicity, choose $m \ge p$
- A non-parametric estimation of the seasonal component can be found by
	- Subtracting the estimated trend
	- Splitting the data into the periods and calculating the average of each time step across all periods
- In R, the function `decompose({ts}, type: str = "additive")` calculates these non-parametric estimations
	- An autoplot of the decomposition shows each component over time
		- Beware of the y-axis scale
		- The residual size box helps to see the amount each component contributes to the decomposition (it should be small for the trend/seasonal component)
- A <mark style="background: #FFB86CA6;">moving average can only be used for decomposition</mark>. Since it relies on future values, we cannot forecast
## Decomposition with Differencing
- The differencing operator is at the heart of the differencing method
	- $\Delta_T x_t = x_t - x_{t-T}$
- Example: Linear Model
	- Assume $x_t = a + bt + \epsilon_t$
	- We can express a lag of 1 with $a + bt + \epsilon_t - a - bt - \epsilon_{t-1} = b + \epsilon_t -\epsilon_{t-1}$
	- If we can forecast $\Delta x_t$, we can forecast $x_{t+1}$, so an advantage to this decomposition is the <mark style="background: #FFB86CA6;">ability to forecast</mark> compared to moving average
- The differencing operator can also handle seasonal components
	- We eliminate the seasonal trend by performing a differencing of the <mark style="background: #FFB86CA6;">same timestamp in the previous period</mark>
		- Example: monthly observations with an annual periodicity would subtract the same month in the prior year
- Differencing can be applied multiple times
	- Doing so will reduce the degree of a polynomial trend by the number of times differenced
	- Example: Removing a quadratic trend from a time series
		- $\Delta\Delta x_t = \Delta^2 X_t$
- In R, differencing can be applied using `diff({ts}, differences: int = 1, lag: int = 1)`
	- `differences` is the number of times to apply the operator
	- `lag` specified which lag to use (for removing the seasonal component)
	- Often, this <mark style="background: #FFB86CA6;">must be applied separately multiple times</mark> to first remove seasonality and then remove a polynomial trend
		- Otherwise, we would use the seasonal lag `differences` times
		- Example: `diff(diff(x, lag = 12), differences = 2)` would remove first the seasonal component and reduce a cubic trend to a quadratic. Then, the second diff would remove the remaining quadratic trend
	- Every difference and lag length applied removes lag length points from the data
## Autoregressive Moving Average Models
- Autoregressive models ($AR_p$)
	- Specification: $x_t = c + \epsilon_t + \underset{j=1}{\overset{p}{\sum}}a_jx_{t-j}$
	- Sum of a random shock, $\epsilon_t$, which is independent, and a linear regression of the previous $p$ observations
	- Restriction on $a_j$
		- The characteristic polynomial has roots of modulus greater than 1
		- $A(z) = 1 - a_1z-\dots-a_pz^p$ with $|z^*| \gt 1$
		- From Mistral: "If the roots are **outside the unit circle** (i.e., $|z^*| > 1$), the model is **stationary**. The effect of past shocks dies out over time, and the series does not explode. The condition ensures that <mark style="background: #FFB86CA6;">the combined effect of all lags does not cause the series to explode</mark>"
	- Given an $AR_1$ model, the autocorrelation is equal to the coefficient
	- Autocorrelation exponentially decreases to 0
		- Order $p$ is selected by looking at the [[Overview and Basic Descriptive Statistics|partial autocorrelation]] and choosing the first non-significant value
- Moving Average Models ($MA_q$)
	- These models are <mark style="background: #FFB86CA6;">not linked to moving average trend estimation</mark>
	- Specification: $x_t = c + \epsilon_t + \underset{j=1}{\overset{q}{\sum}}b_j\epsilon_{t-j}$
		- $\epsilon_t$ <mark style="background: #FFB86CA6;">serves as the innovation</mark> for time step $t$
	- To identify a potential moving average, the partial autocorrelation should exponentially decrease to 0
		- Order $q$ is then selected by finding the first non-significant autocorrelation since autocorrelation is 0 for all $h \gt q$
	- Any $AR_p$ model can be seen as $MA_{\infty}$
- $ARMA_{pq}$ models
	- Specification: $x_t = c + \underset{k=1}{\overset{p}{\sum}}a_kx_{t-k} + \underset{j=0}{\overset{q}{\sum}}b_j\epsilon{t-j}$
		- $\epsilon_j$ for $t - q \le j \le t$ are white noise of variance $\sigma^2$
	- The autocorrelation and partial autocorrelation relationships from AR and MA models do not hold
		- Instead, autocorrelation exponentially decreases to 0 from order $q+1$
- Summary of model properties
	 ![[Pasted image 20260114124924.png]]
## Autoregressive Integrated Moving Average Models ($ARIMA_{pdq}$)
- ARIMA is a procedure which <mark style="background: #FFB86CA6;">integrates differencing into an ARMA model</mark>
	 ![[Pasted image 20260114130605.png]]
	- $x_t$ is an $ARIMA_{pdq}$ model if $\Delta^dx_t$ is an $ARMA_{pq}$ model
- The main challenge is selecting $p,d,$ and $q$
- Specification:
	- $\Delta^d x_t = c + \epsilon_t + \underset{j=1}{\overset{p}{\sum}}a_jx_{t-j}\underset{k=1}{\overset{q}{\sum}}b_k\epsilon_{t-k}$
- Specific ARIMA models
	- $ARIMA_{(0,0,0)}$ without a constant is white noise
	- $ARIMA_{(0,0,0)}$ without a constant is a random walk
		- $x_{t+1} - x_t = \epsilon_t$
- The intercept, $c$, and the differencing order, $d$, <mark style="background: #FFB86CA6;">determine the long-term forecast</mark>
	- $c=0;d=0$: Long-term forecasts go to 0
	- $c=0;d\ne0$: Long-term forecasts go to a non-zero constant
	- $c=0;d=2$: Long-term forecasts follow a straight line
	- $c\ne0;d=0$: Long-term forecasts go towards the mean of the data
	- $c\ne0;d=1$: Long-term forecasts follow a straight line
	- $c\ne0;d=2$: Long-term forecasts follow a quadratic trend
- Once $p,d,$ and $q$ are selected, the model parameters are estimated with [[Constructing Estimators|maximum likelihood]]
	- We cannot use MLE to choose $p,d,$ and $q$ since higher values will lead to more parameters which will increase the likelihood
	- Instead, we can evaluate and compare models using RMSE on [[Testing|test data]] or by looking at [[Variable Selection - Linear Model|AIC or BIC]]
- In R, we use `Arima({ts}, order = c(int, int, int))`
	- There is also support for finding the optimal order with a heuristic search using the `auto.arima({ts})` function
		- Increase each parameter by one and select the best model (AIC/BIC/RMSE)
		- Repeat until improvement stops
	- Order can also be selected using the ACF and PACF to identify possible models
## Seasonal ARIMA
- The seasonal ARIMA model relies on the backshift operator
	- $\Delta^d_Tx_t = (1 - B^T)^dx_t$
- With backshift, we can express the ARIMA model
	- $(1 - a_1B - \dots - a_p B^p)(1 - B)^dx_t = c + (1 + b_1B + \dots + b_qB^q)\epsilon_t$
		- $(1 - a_1B - \dots - a_p B^p)$ is the $AR_p$ part
		- $(1 - B)^d$ represents $d$ differences
		- $(1 + b_1B + \dots + b_qB^q)$ is the $MA_q$ part
- To add the seasonal component, we simply add a second order to ARIMA
	- $ARIMA{(p,d,q)(P,D,Q)_T}$
		- $T$ is the periodicity
		- $P,D,Q$ are the orders of the seasonal component
	- The seasonal component performs an ARMA model (with potential differencing) by <mark style="background: #FFB86CA6;">considering a time series where each observation is one period apart</mark>
- Example: $SARIMA_{(1,1,1)(1,1,1)_{12}}$
	- $(1 - a_1B)(1 - a_2B^12)(1-B)(1 - B^12)x_t = (1 + b_1B)(1 + b_2B^12)\epsilon_t$
- A key benefit is we can directly consider a lag of order $T$ without having to consider all other lags, 1-11, as well
- In R, `Arima()` is still used just with parameter `seasonal = c({P}, {D}, {Q})`
	- This model can be evaluated using `residuals()` or `checkresiduals()` functions
## Heteroscedasticity
- <mark style="background: #FFB86CA6;">Probabilistic models assume constant variance over time</mark>
- If we encounter heteroscedasticity, we can stabilize the series with a log, power (square root), or Box-Cox transformation
	- These transformations require a monotonically changing time series
- Box-Cox parameter lambda determines how strong the effect is
	- $y_t = \begin{cases}\log(x_t) \textrm{ if } \lambda = 0 \\ (x_t^{\lambda}-1)/\lambda \textrm{ if } \lambda \ne 0 \end{cases}$
	- We can auto-tune this using `BoxCox.lambda()` in R
	- A lower lambda means a stronger flattening of larger values
	- This is available as an option in the `hw` and `auto.arima` functions with parameter `lambda = "auto"`
- If the variance evolution is non-monotonic, ARCH or GARCH models may be more useful