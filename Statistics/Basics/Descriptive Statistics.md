|                          Course Name                           |                     Topic                     |     Professor      |      Date       |    Tags     |
| :------------------------------------------------------------: | :-------------------------------------------: | :----------------: | :-------------: | :---------: |
| **Foundations of Statistical Analysis and Machine Learning 1** | Univariate and Multivariate Descriptive Stats | Christophe Bécavin | 13 janvier 2025 | #Statistics |

[Class Video Link](URL)

# Summary
*Descriptive statistics are used to summarize, visualize, and understand individual (univariate) sets of data, and are used to compare joint distributions of multivariate sets of data. Common statistics to examine include the mean and median which express position. The mean also serves as the first moment for data with axes of variability and symmetry representing higher order moments.*

# Key Takeaways
1. The mean of the product of two vectors does not equal the product of the means of each vector: *mean(x * y)* $\ne$ *mean(x) * mean(y)*
2. Variance can be calculated as the difference between the mean of the squared elements and the mean of the elements squared: *var(x) = mean($x^2$) - mean$(x)^2$*
3. Covariance is an unbounded metric in terms of magnitude which is why correlation is more frequently used since it has a consistent scale of  $[-1,1]$

# Definitions
- Descriptive Statistics: The mathematical tools for analyzing data
	- mean, median, variance, frequency tables, etc.
- Discrete: Elements of a set which are countable and cannot be in-between two elements
	- Colors, counts of customers to a store, countries 
- Continuous: Elements of a set that can take on any value within a defined range
	- Car mileage, amount of rainfall, prices
- Indicator Function ($I$): The count of observations **below** a set threshold ($t$)
- Quantile Functions: The proportion of data falling **below** a value of interest on an empirical cumulative distribution function (ECDF)
- Interquartile Range: 75th quartile - 25th quartile

# Additional Resources
- [Moments (mean, variance, skew, kurtosis)](https://gregorygundersen.com/blog/2020/04/11/moments/)

# Notes
## Univariate
- Discrete
	- Create a frequency table to count observations in each group
		- Represented graphically as a barplot (bars do not touch since it is discrete)
		 ![[Pasted image 20250118131410.png]]
- Continuous
	- A frequency table can also be generated, but we must first create classes by binning the continuous variable
		- This creates a histogram (bars do touch)
		 ![[Pasted image 20250118131747.png]]
	- A continuous frequency table can be turned into a frequency distribution
		- <mark style="background: #FFB86CA6;">This is especially useful/essential when the width of the classes is uneven</mark>
		- Calculate relative frequency as the % of observations in each category
		- Then get the density as the frequency divided by the width of the class ($x_1 - x_0$)
		 ![[Pasted image 20250118132453.png]]
 - Empirical Cumulative Distribution Function (ECDF)
	 - $F_n(t) = \frac{\sum_iI_{x_i \le t}}{n}$
	 - Count the number of observations below $t$ and divide by the total number of observations
	 - Used to get median, quartiles, percentiles, etc
	 - The ECDF is non-decreasing and right continuous
 - Quantile Function
	 - Given the ECDF of a [[Vectors|vector]] of observations $x =$ {$x_i, i=1, ..., n$}, the $j^{th}$ quantile of order $p \in (0,1)$ denoted as $x_{p,j}$ is the minimum value $t$ such that $F_n(t) \ge j * p$
	 - Common quantiles
		 - Percentile: 0.1
		 - Decile: 0.1
		 - Quartile: 0.25
			 - Boxplot summarizes quartiles
## Summarizing Distributions
- Position
	- Median (50th percentile of ECDF)
		- *median(x) = min(*{$x_i: F_n(x_i) \ge 0.5$})
	- Mean ($\mu$) - first moment
		- $\frac{1}{n}\sum_ix_i$
		- If summarized in a distribution frequency
			- $\sum_jx_jf_j$
		- Properties (same as [[Properties of Sums and Products|properties of sum]])
			- Sums are separable: *mean(x + y) = mean(x) + mean(y)*
			- Constant Multiple Rule: *mean*$(\lambda x) = \lambda$ *mean(x)*
- Variability
	- Variance ($\sigma^2$) - second moment
		- *var(x) = mean((x - mean(x))*$^2$*) =* *mean(*$x^2$*) - mean(x)*$^2$
	- Standard Deviation
		- $\sqrt{\sigma^2 (x)}$
	- Coefficient of Variation
		- $\frac{\sigma(x)}{\mu(x)}$
	- Interquartile Range
		- 75th percentile - 25th percentile
- Symmetry
	- Skew - third moment
		- $\mu[(\frac{x - \mu(x)}{\sigma(x)})^3]$
		- positive skewness is skewed right and negative is skewed left
		 ![[Pasted image 20250119091824.png]]
	- Kurtosis - fourth moment
		- $\mu[(\frac{x - \mu(x)}{\sigma(x)})^4]$
		- The kurtosis of a standard normal distribution is 3, so it is commonly the threshold
		 ![[Pasted image 20250119091806.png]]
	 ![[Pasted image 20250118172720.png]]
## Multivariate
- Can summarize separately using the above metrics but need different tools for the joint variable (x, y)
- Contingency tables for two categorical variables
- Histograms, boxplots, and violin plots for one continuous / one categorical
- Scatterplots for two quantitative variables
- Covariance - identify how two variables move together
	- $\sigma_{x, y} = \frac{1}{n}\sum_i(x_i = \mu_x)(y_i-\mu_y)$
- Correlation: Covariance on a standardized scale
	- $\rho_{x, y} = \frac{\sigma_{x, y}}{\sigma_x \sigma_y}$
	- Has values between -1 and 1 with values further away from 0 being a stronger relationship
