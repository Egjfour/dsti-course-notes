|       Course Name        |   Topic    |   Professor    |       Date       |    Tags     |
| :----------------------: | :--------: | :------------: | :--------------: | :---------: |
| **Time Series Analysis** | Clustering | Julien Jacques | 12 décembre 2025 | #Statistics |

[Class Video Link]((https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251212%5F095206%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E362d8802%2D7543%2D456d%2Dabff%2D43b4a89ba509)

# Summary
*Time-series tasks are not always linked to forecasting. In many cases, we want to compare and describe multiple related time series. Various distance metrics allow for comparisons across the series which are then able to be used for downstream tasks like clustering or classification. Featurization also allows for describing and comparing time series.*

# Key Takeaways
1. The goal of time series clustering is the same as [[Unsupervised Learning|traditional clustering]] with the restriction that point comparisons should be time-indexed and an entire series is the unit of analysis

# Definitions
- Dynamic Time Warping: Measuring distance after creating the best alignment between the time series
	 ![[Pasted image 20260115193755.png]]
- Functional Data: Discrete (and potentially irregular) observations of a [[Continuity & Derivability|continuous function]]
	 ![[Pasted image 20260115194841.png]]

# Additional Resources
- [tslearn (Python)](https://tslearn.readthedocs.io/en/stable/user_guide/clustering.html)

# Notes
## Clustering Methods
- Traditional k-means and hierarchical clustering are still possible
- Main difference is the definition of the distance metric
	- [[Variable Selection - Linear Model|Euclidean]]: Compare point-wise the various time series at each time step
	- If only the pattern of the evolution of the time series is relevant, dynamic time warping is often useful
		- Typically seen in signal processing applications
	- In R, the function `dist({ts}, method: str)` is used for both
		- `method` options include "DTW" or "EUCLIDEAN"
- The package `dtwclust` offers function `tsclust` which has different methodologies using DTW distance
- If our data are <mark style="background: #FFB86CA6;">discrete observations, we can use a functional data approach</mark> to estimate the function and then cluster
	- In R, this is done with package `funHDDC`
## Feature Extraction
- Can be used as an initial step prior to clustering
- Library `tsfeatures` in R lets us easily get relevant features
	- frequency
	- different sum of autocorrelations (for the series and its differentiation)
	- index of linearity, curvature.
	- trend
	- entropy
	- number of peak and trough
- These features (or distance metrics) can also be used for time series classification tasks