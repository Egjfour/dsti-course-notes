|        Course Name        |     Topic      |   Professor    |       Date       |       Tags       |
| :-----------------------: | :------------: | :------------: | :--------------: | :--------------: |
| **Timer-Series Analysis** | ML Forecasting | Julien Jacques | 11 décembre 2025 | #MachineLearning |

[Class Video Link]([URL](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251211%5F095049%2DMeeting%20Recording1%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Eea1bc3eb%2Dafb4%2D472e%2D90af%2Dacefd680a723))

# Summary
*Machine learning models are quite commonly used to solve forecasting problems. In particular, they can be useful when there are several similar series with very non-linear patterns. These models are most similar to [[Probabilistic Time-Series Models|autoregressive models]] as they take lags of the time series to make a prediction. R offers specialized libraries like `nnetar` which allow for simple setup of such models.*

# Key Takeaways
1. Autoregressive models are the framework generally used for ML models
2. [[Elements of a Neural Network|Deep neural networks]] are generally not appropriate for forecasting a single time series since the number of parameters far exceeds the data size
3. We cannot use [[Overview and Basic Descriptive Statistics|partial autocorrelation]] to select the best lags for an ML model since these models are nonlinear and PACF only shows a linear link

# Additional Resources
- [nnetar Documenation](https://www.rdocumentation.org/packages/forecast/versions/8.24.0/topics/nnetar)
- [XGBoost for Time-Series Forecasting](https://machinelearningmastery.com/xgboost-for-time-series-forecasting/)

# Notes
## Autoregressive Models with Neural Networks
- A non-seasonal neural network model for forecasting is defined using parameters $p$ and $k$
	- $NNAR_{p,k}$
	- $p$ is the lag length
	- $k$ is the number of neurons in the [[Elements of a Neural Network|hidden layer]]
		- The traditional model specifies only one hidden layer (implemented in R)
	- The inputs are [[Probabilistic Time-Series Models|lagged]] values of the time series
	- This model uses a [[Activation Functions|sigmoid activation function]]
	- $NNAR_{p,0} = AR_p$
		- With no hidden layer, we simply have a [[Vectors|linear combination]] of $p$ lags
- If there is a seasonal pattern, we directly introduce $X_{n-T}$ and any other desired period multiples
	- We add parameter $P$ to represent the number of seasonal lags
	- $NNAR_{(p, P, 0)_T} = SARIMA_{(p, 0, 0)(P, 0, 0)_T}$
		- With no hidden layer, we create a [[Probabilistic Time-Series Models|seasonal ARIMA]] model with only autoregressive components (<mark style="background: #FFB86CA6;">no differencing or moving average</mark>)
- In R, these models can be built and tunes automatically using `nnetar`
	- If parameter `p` is not specified, it is chosen automatically
	- If parameter `P` is not specified, it is set to `P = 1`
	- If parameter `k` is not specified, it is set to `k = (p + P + 1)/2`
	- A [[Probabilistic Time-Series Models|lambda]] can be specified too (Box-Cox transformation)
		- Can set to `"auto"` to choose with `Box-Cox.lambda()` internally
- This model tends to work if and where others fail
## Deep Neural Networks
- Many time/sequence-based architectures exist in deep learning
	- RNN, LSTM, GRU, and [[Transformers Overview|Transformers]] are the most well-known
	- These often aren't effective for time-series forecasting because they have a very large number of parameters and require massive amounts of data
		- The <mark style="background: #FFB86CA6;">only way to obtain more data in a time series is to wait</mark>
- In R, these methods can be applied using the `keras` library
	- It is important to scale the data and to split the time series into subseries
## Forecasting with ANY ML Method
- For any ML model, a key step is creating the set of inputs/outputs
	 ![[Pasted image 20260115140049.png]]
- The flexibility of many of these methods also allows for multi-output models
	- This lets us forecast, simultaneously, multiple time steps
		- Pro/Con: Forecast horizons $h \gt 1$ have <mark style="background: #FFB86CA6;">no knowledge of previously-forecasted values</mark>
	- Example: Multivariate LM
		- ```R
		  # Assume data already prepared to input/output structure
		  fitLM=lm(cbind(x36,x35,x34,x33,
						 x32,x31,x30,x29,x28,x27,x26,x25) ~ .,
		  data=data)
		  ```
- [[Evaluation of ML Models & Improving Results|Evaluation criteria]] and metrics are important to align on and standardize across methods for comparison