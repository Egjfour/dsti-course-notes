|                Course Name                 |   Topic    |   Professor   |         Date         |   Tags    |
| :----------------------------------------: | :--------: | :-----------: | :------------------: | :-------: |
| **Inverse Problems and Data Assimilation** | Algorithms | Didier Auroux | 15 & 18 juillet 2025 | #Calculus |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250715%5F094957%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E4faee5d4%2D9ae3%2D4fd1%2D92bd%2D251cb7e407d6)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250715%5F125737%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E984069cc%2Ddbf6%2D4575%2D93b0%2Dd50df4b31913)
[Class Video Link 3](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250718%5F095456%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E6871fc6e%2D88af%2D47bd%2D9824%2Dac60cc3ab5f6)

# Summary
*Variational algorithms are algorithms which perform an optimization of a cost function to assimilate data. These models find the best background state/initial condition that balances between the existing prior information and the observations usually by weighting according to the inverse error. Since these models are an optimization, we can extend the cost function to provide other constraints for the solution (positivity, closeness in time, etc.). When these models are extended to include time in 4D-Var, we calculate the adjoint model which looks back in time and reduces the cost of gradient calculations tremendously.*

# Key Takeaways
1. Our job is to correct the prior (best current state) using the observations
2. $B$ is the [[Random Vectors|covariance matrix]] of the background error
3. The amount of noise in the background error matrix $B$ is the inverse weight
4. $x^*$ is the best compromise between being close to the background and observations (in dimension 1 - a weighted average)
5. Variational models are dissipative, so we need to add energy to the system
6. The 4D-Var algorithm focuses only on the solution of the model letting us solve the differential equation ($\dfrac{\partial x}{\partial t}$) with respect to time
7. The 4D-Var algorithm requires that $x(t_i)$ [[Vectors|depends linearly]] on $x_0$
8. The adjoint model gives the gradient for the same computation cost as one function evaluation
9. When a Dirac function is used in a [[Constrained Optimization - Lagrangian|Lagrangian optimization]], we say that $P_0\delta_0$ only contributes to the [[Function Optimization|gradient]] at time 0
10. When implementing, we need to use the gradient of the discretized cost (with time steps $\Delta t$) using the Lagrangian NOT the theoretical cost function that uses ODEs

# Definitions
- Variational Algorithm: Algorithms which perform [[Data Assimilation Overview|data assimilation]] by [[Optimization Basics & Problem Statement|minimizing a cost function]]
- Prior: An assumption of the true value
	- Also known as the background state $x_b \in \mathbb R^n$
- Innovation Vector ($d$): The misfit between the sources of information (observations and background)
	- $x_{obs} - Hx_b$
- Initial Condition: The state that we will use as our starting point to determine the trajectory
- Adjoint Model: A restating of the [[Direct and Inverse Problems|direct model]] to go backward in time
- Jacobian Matrix ($JF(x)$): For a multi-output multivariable function ($F: \mathbb R^n \to \mathbb R^n$), the matrix which defines all pairs of partial derivatives for each output with respect to each input

# Additional Resources
- [Adjoint Model](https://ecco-group.org/adjoint.htm)

# Notes
## 3D-Var (No Time Dependency)
- Framework: Given $X_t \in \mathbb R^n$, a true unknown state at time $t$, for which we have observations $x_{obs} \in \mathbb R^p,\hspace{1.5mm} p << n$ (*much* less than n - we observe the system poorly)
- Assume a background state $x_{b} \in \mathbb R^n$, the prior
- Goal: Correct the background state $x_b$ given the observations
- We need an observation operator which goes from the state to the observations
	- $H: \mathbb R^n \to \mathbb R^p$
	- This is an <mark style="background: #FFB86CA6;">interpolation/projection of the state space onto the observation space</mark>
	- Typically a linear operator
- Then, we can define a cost function which takes a state, $x$
	- $J(x) = \frac{1}{2}||x-x_b||^2 + \frac{1}{2}||Hx - x_{obs}||^2$
	- First term is the quadratic distance from the background
	- Second term is quadratic distance from the observation
- We want to apply a weighting to these based on their importance, so we define a [[Matrices|symmetric]], [[Matrix Diagonalization|positive]], definite matrix, $B$
	- $||x||^2_{B^{-1}} = <x, B^{-1}x>$
	- We set $B$ as the covariance matrix of the background error
		- $B = \mathbb E[(x_b - x_t)(x_b - x_t)^T]$
		- Under assumptions:
			- [[Point Estimators|Unbiased]] background error
			- <mark style="background: #FFB86CA6;">Larger Error = Smaller Weight</mark>
	- We also define matrix $R$ in a similar way as the covariance matrix of the observations
		- $R = \mathbb E[(x_o - x_t)(x_o - x_t)^T]$
	- New cost function with weights:
		- $J(x) = \frac{1}{2}<B^{-1}(x-x_b), x-x_b> + \frac{1}{2}<R^{-1}(Hx - x_{obs}), Hx - x_{obs}>$
- Then, we simply minimize this weighted cost function
	- $x^* = (B^{-1} + H^T R^{-1}H)^{-1}(B^{-1}x_b + H^T R^{-1}x_{obs})$
	- In practice, we have very large dimensions, so the exact solution cannot be determined, so we use [[Algorithms - Gradient-Based Optimization|gradient methods]], but also do not run all iterations as it would be too costly
		- The number of iterations run is based on how accurate we need to be and how quickly new forecasts must be calculated
## Incremental 3D-Var
- Helps to provide numeric stability by using a control vector: $\delta x = x - x_b \Leftrightarrow x = x_b + \delta x$
- The control vector also ensure that our correction is centered around 0
- <mark style="background: #FFB86CA6;">If we know that some regions of the background are sufficient, we can reduce dimensionality</mark> by setting $\delta X$ to 0 for those regions
	- We use the innovation vector, $d$ to identify the regions where the misfit between the observations and background is low and use these to strategically remove components
- Update the cost function to include $\delta$ and the innovation vector, $d$
	- $J(\delta x) = \frac{1}{2}\delta x^TB^{-1}\delta x + \frac{1}{2}(d - H\delta x)^T R^{-1}(d - H \delta x)$
- Then calculating the minimum
	- $\delta x^* = (B^{-1} + H^T R^{-1}H)^{-1}H^TR^{-1}d$
	- $x^* = x_b + \delta x^*$
## 4D-Var (Adding Time)
- Goal: Compare our simulated value to the observation at time $t$
- Our model is now the change in $x$ over time
	- $\dfrac{\partial x}{\partial t} = F(x, u)$
		- With $u$ the model parameters
- And we constrain the model so that the first time is the initial condition
	- $x(0) = x_0$
- We define a cost function such that we can identify $x_0$ by solving
	- $J(x_0, u) = \dfrac{1}{2}<B^{-1}(x_0 - x_b), x_0 - x_b> +$
	 $\dfrac{1}{2}\underset{i=0}{\overset{m}{\sum}}<R^{-1}(H_ix(t_i) - x_{obs_i}), H_ix(t_i) - x_{obs_i}>$
	- We are choosing a best starting point that minimizes the squared distances between both the background and starting point and the observations versus the model weighted by their inverse error
- This can be reformulated as an integral over time using the Dirac function
	- $J(X_0, u) = \dfrac{1}{2}||X_0 - X_b||^2_{B^-1}$
	 $+ \dfrac{1}{2}\int_0^T \underset{i=0}{\overset{n}{\sum}}||x_{obs} - H(x)||^2_{R^{-1}}\delta_{t_i}(t)dt$
- Calculating the gradient of this function (especially in high dimensions with many time steps) is too costly, so we use the model as a weak constraint in the Lagrangian
	- $\mathcal L((x_0, u), x, p) = J(x_0, u) + \int_0^T<p, \dfrac{\partial x}{\partial t} - F(x, u)>dt$
	- In a linear case, we try to find the [[Constrained Optimization - Lagrangian|saddle point]] of this Lagrangian
- The maximum of this Lagrangian with respect to $p$ is the direct model
- The minimum of this Lagrangian with respect to $x$ is the adjoint model
	- This is the model solved backward in time with the final condition $p^*(T) = 0$
- Incremental 4D-Var models also exist which employ the innovation vector
## Computational Issues with Variational Algorithms
- Cannot use the continuous adjoint with a discrete model
- Solving the adjoint is very difficult
- [[Direct and Inverse Problems|Ill-Posed]] problems like nonlinearity and what to use as the initialization vector
	- Can use a local linearization
- Estimating the covariance matrix is extremely difficult and the choice of the $B$ matrix has a strong influence on the forecast
## Python Implementation - Lorenz Model
- We need to use the discretized gradient
	- $-\dfrac{\partial p}{\partial t}= [J(F(x))]^Tp$
	- $\dfrac{\partial p}{\partial t}(t_i) \approx \dfrac{(t_i) - p(t_{i+1})}{\Delta t}$
- The gradient calculation can be verified by calculating the Gâteaux derivative to see that given $\epsilon$ and a direction, $y$, the inner product of the gradient and direction makes sense
	- If we use a random direction, we can check all values at once - should be within decimals
```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.optimize import minimize

def lorenz(X0): # X0 = initial condition at t=0
    X = np.zeros((3,N))
    X[:,0] = X0 # initial condition
    for i in range(N-1): # time loop
        X[0,i+1] = X[0,i] + deltat*sigma*(X[1,i]-X[0,i]) # x equation
        X[1,i+1] = X[1,i] + deltat*(rho*X[0,i]-X[1,i]-X[0,i]*X[2,i]) # y equation
        X[2,i+1] = X[2,i] + deltat*(X[0,i]*X[1,i]-beta*X[2,i]) # z equation
    return X

# 4d-Var cost function
def J(X0):
    X = lorenz(X0) # model trajectory X(t)
    cost = 0.5*(np.linalg.norm(Xb0-X0))**2 # background term
    for i in range(0,N+1,freq):
	    # observation term
        cost += 0.5*(np.linalg.norm(Xobs[:,int(i/freq)]-X[0:2,i]))**2
    return cost

# 4D-Var gradient
def gradJ(X0):
    X = lorenz(X0) # compute direct solution
    # compute adjoint solution
    # initialisation
    P = np.zeros((3,N))
    P[:,N-1] = 0. # final condition
    # if observations at the final time (don't forget it...)
    if np.mod(N-1,freq)==0:
        # add forcing term
        P[0:2,N-1] += -(X[0:2,N-1]-Xobs[:,int((N-1)/freq)])
    for i in range(N-1,0,-1): # backward time loop
	    # p equation
        P[0,i-1] = P[0,i] + deltat*(-sigma*P[0,i]+
							        (rho-X[2,i-1])*P[1,i]+X[1,i-1]*P[2,i])
		# q equation
        P[1,i-1] = P[1,i] + deltat*(sigma*P[0,i]-P[1,i]+X[0,i-1]*P[2,i])
        P[2,i-1] = P[2,i] + deltat*(-X[0,i-1]*P[1,i]-beta*P[2,i]) # r equation
        # if observations at this time
        if np.mod(i-1,freq)==0:
            # add forcing term
            P[0:2,i-1] += -(X[0:2,i-1]-Xobs[:,int((i-1)/freq)])
    # return the gradient
    gradient = (X0-Xb0)-P[:,0]
    return gradient

# Lorenz model parameters
sigma = 10.
rho = 28.
beta = 8./3.

# numerical parameters
T = 4. # final time of the assimilation window
N = 4001 # number of times (including 0 and T)
deltat = T/(N-1) # time step. Test many time steps and see if we need to adjust

# we make it simple: B = Id, R = Id
# background state:
Xb0 = np.array([-4.0,-6.0,17.0])

# let's minimize!!
minimum = minimize(J,Xb0,jac=gradJ,method='BFGS',options={'maxiter':500})
```