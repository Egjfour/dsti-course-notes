|                Course Name                 |   Topic    |   Professor   |         Date         |    Tags     |
| :----------------------------------------: | :--------: | :-----------: | :------------------: | :---------: |
| **Inverse Problems and Data Assimilation** | Algorithms | Didier Auroux | 16 & 18 juillet 2025 | #Statistics |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250716%5F095759%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E69e27a9a%2D843d%2D489b%2D8592%2Dd18e67218148)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250716%5F130446%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E894c7da2%2D0712%2D4aac%2Daf05%2D51fa6ed574bf)
[Class Video Link 3](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250718%5F125129%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E37e583bd%2D7768%2D4fb2%2Dbab3%2Dfa98ff1973e0)

# Summary
*The sequential algorithms differ from variational algorithms in that they construct an estimator for a linear combination which allows us to determine the optimal amount of information to retain between the prior and observation. Since this is a linear mapping, we must extend this method to use the tangent linear model (i.e., first-order Taylor approximation) to propagate the error throughout the model.*

# Key Takeaways
1. Sequential data assimilation constructs the best linear [[Point Estimators|estimator]]
2. The goal is to minimize the [[Random Vectors|covariance matrix]], $A$, with respect to $K$, an [[Point Estimators|unbiased]] [[Vectors|linear combination]]
3. The optimal $K$ is $BH^T(HBH^T+R)^{-1}$
4. The correction step will always help the error to decrease even if the observations are poor quality
5. In a completely linear system, the Kalman filter is equivalent with the [[Variational Algorithms (3D-Var & 4D-Var)|4D-Var model]]
6. The Extended Kalman Filter uses the <mark style="background: #FFB86CA6;">linearized model to propagate error and covariance but states are updated using the actual (nonlinear) model</mark>
7. The [[Variational Algorithms (3D-Var & 4D-Var)|adjoint model]] is the transpose of the tangent linear model

# Definitions
- Kalman Filter (Gain Matrix): The direct link between what we see and what we should do
- The Resolvent of the Model ($M_{k; k+1}$): The model function (or matrix in the linear case) which moves from one state at a given time $k$ to a new state at time $k+1$
	- Numerically means to solve the model for the next point in time using the gradient and $\Delta t$
	- $M = I + \Delta t A;\hspace{2mm} A=JF(x)$
- Ensemble Kalman Filters: Estimation of the covariance errors based on a Monte Carlo method
	- Typically used for generating [[Confidence Intervals of Estimators|confidence intervals]] of forecasts
- Localization Effect: The variance shrinks dramatically on certain dimensions, so the samples all become close to the mean
- Tangent Linear Model: The [[Optimization Basics & Problem Statement|Gâteaux Derivative]] of a nonlinear resolvent (implemented as the [[Variational Algorithms (3D-Var & 4D-Var)|Jacobian matrix]] multiplied by the direction, $y$)
	- $\dfrac{\partial y}{\partial t} = F'(x; y) = JF(x)y$

# Additional Resources
- [The Kalman Gain](https://www.kalmanfilter.net/kalmanGain.html)

# Notes
## Sequential Assimilation
- We correct the model trajectory at each sequence
	 ![[Pasted image 20250720130359.png]]
## Optimal Interpolation (No Time Dependency)
- Goal: Build the best a posteriori analysis from the a priori background and observations
- Generally, we look to build the optimal linear combination (estimator) of observation and state vectors assuming they are available at the same time
	- $x_a = x_b + (x_a - x_b)$: Naive model. We can (must) do better\
- Adding the observations and the correction matrix
	- $x_a = x_b + K(x_{obs} - Hx_b)$ with $K \in \mathbb R^{n,p}$
	- $K$ is the degrees of freedom and we try to find the best estimator of $K$ which minimizes the [[Estimators-Convergence & Comparison|quadratic error]]
- We define the errors as
	- Background error: $e_b = x-x_b$
	- Observation error: $e_o = x_{obs} - Hx$
	- Analysis error: $e_a = x - x_a = (I - KH)e_b - Ke_o$
- The <mark style="background: #FFB86CA6;">covariance matrix of the analysis error</mark> is $P_a = \overline{e_ae_a^T}$
	- Assuming $e_b {\perp \!\!\! \perp} e_o$, we can define this further as $A = (I - KH)B(I-KH)^T + KRK^T$
- This is given by the Best Linear Unbiased Estimator (BLUE) where we find $K$ such that $A$ is minimal
	- $J(K) = A(K) = (I - KH)B(I-KH)^T + KRK^T$
- The optimal $K = BH^T(HBH^T+R)^{-1}$
	- In dimension 1, this is simply the background [[Moments of Random Variables|variance]] divided by the total variance
		 $\dfrac{\sigma^2_b}{\sigma^2_b + \sigma^2_r}$
	- This optimal is exactly the minimum of the [[Variational Algorithms (3D-Var & 4D-Var)|3D-Var cost function]]
## Kalman Filter (Time Dependent)
- Kalman filters are the extension of optimal interpolation to dynamic systems
- 2 phases: prediction and correction
	- Use the model in-between observations and then update at each observation
	- The $B$ matrix (covariance of background information) changes each time
- We must explicitly calculate the covariance matrix of analysis, $A$, since it is needed to propagate states forward
- To perform forecasts, we apply the model resolvent to the current analysis vector and update the background vector
	- Assuming model is linear: $x_b = Mx_a$
- Essentially, we <mark style="background: #FFB86CA6;">perform optimal interpolation at each time step where we have an observation and restart the forecast</mark> from that newly interpolated point
- Handling imperfect models
	- We need to add a model error term, $\epsilon_m$, since we know that $x_t^{k+1} \ne M_{k;k+1}x_t^{k}$
	- We assume that this error is independent of the other error (background and observation)
	- Since the covariance matrix of the model is not possible to estimate, we instead add a multiplier to the background error covariance matrix
		- $B^{k+1} = \dfrac{1}{\rho}MA^kM^T$ with $\rho \lt 1$
- Extended Kalman Filter (Nonlinear Model)
	- Since Kalman filtering relies on linear operations (matrix-vector multiplications), it does not natively handle nonlinear models
	- Instead, we use the tangent linear model to do a local linearization
	- We use a [[Taylor Series|first-order Taylor expansion]] on the model function to get the resolvent and update the background error
		- $\epsilon_b^{k+1} = M(x_t^k) - M(x_a^k) \approx M'(x_a^k; \epsilon_a^k)$
		- Thus, we can use the Jacobian matrix in the direction of $\epsilon_a^k$
	- This means that we can use the tangent linear model to propagate error (update the background error covariance matrix) but still use the nonlinear model to generate the forecasts
	- The Kalman filter's <mark style="background: #FFB86CA6;">equivalence with 4D-Var does not exist in the nonlinear case</mark>
## Computational Issues with Sequential Algorithms
- Errors are usually poorly known, so we get poorly identified error covariance matrices, so we get a sub-optimal filter causing incorrect interpolation
- Nonlinearities and local linearization
- Possible Solution: Ensemble Kalman Filters
	- We estimate the covariance errors using a Monte Carlo method
	- Generate $n$ random vectors of background information and work in parallel
	- Can create a localization effect, so we need to re-amplify the error using $\dfrac{1}{\rho}$ and then regenerate members using the amplified distribution
- We can reduce the dimensionality using the truncated background error matrix which chooses $k$ [[Eigenvalues and Eigenvectors|eigenvalues]] to retain and reduces the original matrix using those eigenvectors
## Python Implementation - Lorenz Model
```python
import numpy as np
import matplotlib.pyplot as plt

# Lorenz model parameters
sigma = 10.0
rho = 28.0
beta = 8.0/3.0

# numerical parameters
T = 5.0 # final time of the assimilation window
N = 5001 # number of times
deltat = T/(N-1) # time step

def lorenz(Xinit): # Xinit = initial condition at t=0
    X = np.zeros((3,N))
    X[:,0] = Xinit # initial condition
    for i in range(N-1): # time loop
        X[0,i+1] = X[0,i] + deltat*(sigma*(X[1,i]-X[0,i])) # x equation
        X[1,i+1] = X[1,i] + deltat*(rho*X[0,i]-X[1,i]-X[0,i]*X[2,i]) # y equation
        X[2,i+1] = X[2,i] + deltat*(X[0,i]*X[1,i]-beta*X[2,i]) # z equation
    return X

# make it simple: B = Id, R = Id
# background state:
Xb0 = np.array([-4.5, -7.0, 17.4])
Xb = lorenz(Xb0)

# "true" initial condition (twin experiments)
Xtrue0 = np.array([-4.62, -6.61, 17.94])
# "true" solution
Xtrue = lorenz(Xtrue0)

# STANDARD KALMAN -
# standard (linear) Kalman iterations
# with the wrong model dynamics (because linearized)
Xk = np.zeros((3,N))
Xk[:,0] = Xb0 # initial condition
P = B # initial covariance matrix
# if 0 is an observation time
if np.mod(0,freq)==0:
    # then we need to perform an analysis step
    # define the Kalman matrix
    K = P@H.T@np.linalg.inv(H@P@H.T+R)
    # update the state
    Xk[:,0] += K.dot(Xobs[:,0]-H.dot(Xk[:,0]))
    # update the covariance matrix
    Pa = (np.eye(3)-K@H)@P
    P = Pa
for i in range(N-1): # time loop
    # tangent linear model matrix
    A = np.zeros((3,3))
    A[0,0] = -sigma
    A[0,1] = sigma
    A[1,0] = rho-Xb[2,i]
    A[1,1] = -1
    A[1,2] = Xb[0,i]
    A[2,0] = Xb[1,i]
    A[2,1] = Xb[0,i]
    A[2,2] = -beta
    # resolvent of the model between times i and i+1
    M = np.eye(3)+deltat*A
    # update the state
    Xk[:,i+1] = M.dot(Xk[:,i])
    # update covariance matrix
    Pa = M@P@M.T
    P = Pa
    # if i+1 is an observation time
    if np.mod(i+1,freq)==0:
        # then we need to perform an analysis step
        # define the Kalman matrix
        K = P@H.T@np.linalg.inv(H@P@H.T+R)
        # update the state
        Xk[:,i+1] += K.dot(Xobs[:,int((i+1)/freq)]-H.dot(Xk[:,i+1]))
        # update the covariance matrix
        Pa = (np.eye(3)-K@H)@P
        P = Pa
```
![[Pasted image 20250720143752.png]]

```python
# Extended Kalman iterations
# copy-paste and define a new vector Xek
# only difference, in the forecast, update the step with the non-linear model
Xek = np.zeros((3,N))
Xek[:,0] = Xb0 # initial condition
P = B # initial covariance matrix
# if 0 is an observation time
if np.mod(0,freq)==0:
    # then we need to perform an analysis step
    # define the Kalman matrix
    K = P@H.T@np.linalg.inv(H@P@H.T+R)
    # update the state
    Xek[:,0] += K.dot(Xobs[:,0]-H.dot(Xek[:,0]))
    # update the covariance matrix
    Pa = (np.eye(3)-K@H)@P
    P = Pa
for i in range(N-1): # time loop
    # tangent linear model matrix
    A = np.zeros((3,3))
    A[0,0] = -sigma
    A[0,1] = sigma
    A[1,0] = rho-Xek[2,i]
    A[1,1] = -1
    A[1,2] = Xek[0,i]
    A[2,0] = Xek[1,i]
    A[2,1] = Xek[0,i]
    A[2,2] = -beta
    # resolvent of the model between times i and i+1
    M = np.eye(3)+deltat*A
    # update the state
    Xek[0,i+1] = Xek[0,i] + deltat*sigma*(Xek[1,i]-Xek[0,i]) # x equation
    # y equation
    Xek[1,i+1] = Xek[1,i] + deltat*(rho*Xek[0,i]-Xek[1,i]-Xek[0,i]*Xek[2,i]) 
    Xek[2,i+1] = Xek[2,i] + deltat*(Xek[0,i]*Xek[1,i]-beta*Xek[2,i]) 
    # update covariance matrix
    Pa = M@P@M.T
    P = Pa
    # if i+1 is an observation time
    if np.mod(i+1,freq)==0:
        # then we need to perform an analysis step
        # define the Kalman matrix
        K = P@H.T@np.linalg.inv(H@P@H.T+R)
        # update the state
        Xek[:,i+1] += K.dot(Xobs[:,int((i+1)/freq)]-H.dot(Xek[:,i+1]))
        # update the covariance matrix
        Pa = (np.eye(3)-K@H)@P
        P = Pa
```
![[Pasted image 20250720143840.png]]