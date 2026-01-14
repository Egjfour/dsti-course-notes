|       Course Name        | Topic |   Professor    |         Date          |    Tags     |
| :----------------------: | :---: | :------------: | :-------------------: | :---------: |
| **Time Series Analysis** | ARIMA | Julien Jacques | 10 & 11 décembre 2025 | #Statistics |

[Class Video Link](URL)

# Summary
*A 3-4 sentence description of what was learned in italics*

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
- Lag ($\Delta_T$): A mapping of $x_t$ to $x_t - x_{t - T}$
	- Note that this includes calculating the difference
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
## Time Series Decomposition and Probabilistic Models
- Probabilistic models seek to model a relationship in the residual component, $\epsilon_t$, of the time series: $x_t = S_t + T_t + \epsilon_t$ with $S_t$ the seasonal component and $T_t$ the trend
	- If $\epsilon_t$ are iid, there is nothing to model
	- Otherwise, the residuals are [[Overview and Basic Descriptive Statistics|correlated]], and we try to model this correlation
	- We must be able to <mark style="background: #FFB86CA6;">extract the residuals</mark> to do this modeling
	- Such models build on the [[Exponential Smoothing Models|Holt-Winters]] model by directly modeling the stochastic component, $\epsilon_t$, whereas HW only models $T$ and $S$
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
- The lag operator is at the heart of the differencing method
	- $\Delta_T x_t = x_t - x_{t-T}$
	- 