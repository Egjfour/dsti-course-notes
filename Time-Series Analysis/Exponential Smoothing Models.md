|       Course Name        |       Topic        |   Professor    |       Date       |    Tags     |
| :----------------------: | :----------------: | :------------: | :--------------: | :---------: |
| **Time Series Analysis** | Forecasting Models | Julien Jacques | 10 novembre 2025 | #Statistics |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251110%5F085356%2DMeeting%20Recording1%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ed26d6f3a%2D24d7%2D407a%2D8373%2D256b5cd28f46)

# Summary
*Exponential smoothing models handle for the weaknesses of simple forecasting strategies (like with a [[Simple Linear Model|simple linear model]]) by considering a decay/smoothing factor to reduce the influence of older observations. The simplest of such models generates a constant forecast, but the Holt-Winters model can consider seasonal patterns and trends.*

# Key Takeaways
1. Exponential smoothing methods range from basic constant forecasts to models which can consider both seasonal and trend components 
2. R provides methods to automatically optimize the parameters of exponential smoothing models
3. A multiplicative model cannot be used if there are zeros in the time series, but these can be replaced (convention is to fill in using the smallest value divided by 10)

# Definitions
- Exponential Smoothing: A collection of models which give more importance to recent observations
- Constant Forecast: A forecast which does not depend on the horizon, $h$

# Additional Resources
- [Chapter - Exponential Smoothing](https://otexts.com/fpp2/expsmooth.html)
- [Holt Winters Overview - Nixtla - Python](https://nixtlaverse.nixtla.io/statsforecast/docs/models/holtwinters.html)

# Notes
## Simple Exponential Smoothing Models
- Compared to a [[Overview and Basic Descriptive Statistics|simple forecast]], exponential models weight more recent observations more heavily
- Model specification (to forecast $n+h$ using $x_n$)
	- $\hat x_{n, h} = \alpha \underset{j=0}{\overset{n-1}{\sum}}(1 - \alpha)^j x_{n-j}$
	- Parameter $\alpha$ is the decay of influence for older data points
- Creates a constant forecast
- The closer $\alpha$ is to 1, the faster the weight of previous observations decreases
- In R
	- Function: `Holt.winters(x: ts, alpha: float, beta = F, gamma = F)`
	- Setting `alpha` to `NULL` will perform automatic optimization
	- Once model is fit, we can call `predict` and parameter `n.ahead`
	- Can also use the `ses` function which has a useful `accuracy` function
## Advanced Exponential Smoothing - Holt Winters
- Non-seasonal Holt Winters: Forecasting with a linear trend
	- `holt` function from package `forecast`
	- $\hat x_{n, h} = \hat a_1 + \hat a_2 h$
	- Two smoothing constants, $\alpha$ and $\beta$ acting on $\hat a_1$ and $\hat a_2$ respectively
	- A damping parameter can be added to <mark style="background: #FFB86CA6;">ensure long-term forecasts don't go to inifintiy</mark>
		- `damped = T` in function `holt`
		- $\hat x_{n, h} = \hat a_1 + \hat a_2 (\phi + \phi^2 + \dots + \phi^h)$ with $0 \lt \phi \lt 1$
- Additive Seasonal Holt Winters: Linear trend + seasonal pattern
	- Used when <mark style="background: #FFB86CA6;">seasonal fluctuation is consistent over time</mark>
	- $y_t = a_1 + a_2(t-n) + s_t$ with $s_t$ the seasonal pattern of period $T$
	- Parameters $\alpha, \beta$, and $\gamma$ are all smoothing parameters that decrease the importance of older observations as they increase
- Multiplicative Seasonal Holt Winters: Linear trend * seasonal pattern
	- The multiplication amplifies the seasonal component over time
	- Used when <mark style="background: #FFB86CA6;">amplitude of the seasonal pattern is increasing over time</mark>
	- $y_t = [a_1 + a_2(t-n)]\cdot s_t$
	- In R, we use the function `hw` with parameter `seasonal = "multiplicative"`
- Additive vs Multiplicative Example
	 ![[Pasted image 20260102145034.png]]