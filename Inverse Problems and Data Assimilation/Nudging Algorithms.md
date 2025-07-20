|                Course Name                 |   Topic    |   Professor   |        Date        |      Tags      |
| :----------------------------------------: | :--------: | :-----------: | :----------------: | :------------: |
| **Inverse Problems and Data Assimilation** | Algorithms | Didier Auroux | 17-18 juillet 2025 | #LinearAlgebra |

[Class Video Link 1](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250717%5F094838%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Eec2630eb%2D7966%2D4605%2D83d1%2Db713c0850e82)
[Class Video Link 2](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250717%5F130613%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Efdc343a1%2D2b6c%2D44eb%2D9d0e%2D99c94db905ff)
[Class Video Link 3](https://dstisas-my.sharepoint.com/personal/blaise_pascal_nuc_dsti_institute/_layouts/15/stream.aspx?id=%2Fpersonal%2Fblaise%5Fpascal%5Fnuc%5Fdsti%5Finstitute%2FDocuments%2FRecordings%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20250718%5F125129%2DMeeting%20Recording%2Emp4&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E9f1a0936%2D1f58%2D437e%2D8932%2D6045683b9a0b)

# Summary
*Nudging algorithms are a much simpler (to implement) methodology which force the model to fit the observations. Nudging algorithms are asymptotical with respect to time, but since many practical applications have small windows, traditional nudging falls short. However, we can use back-and-forth nudging to create infinite time steps by going in the opposite direction and "ping-ponging" between forward time and backward time. This change of time can either be implemented simply by taking $-\Delta t$ or by inverting both the function and the nudging term (the former is generally easier).*  

# Key Takeaways
1. These algorithms are best suited for small, continuous data corrections/time steps
2. If the system is [[Observability|observable]], $\exists K$ such that $F-KH$ is stable
3. Large eigenvalues are the direction in which the system is unstable with respect to tim
4. If a function is decoupled and we do not observe all regions, no values of $K$ can ever change the eigenvalues of the unobserved region
5. The optimal determination of $K$ is the best parameters and best starting point to find the best solution which best fits the observations
6. Most prediction windows are short so nudging algorithms being asymptotic with respect to time is not useful especially since we often reset our systems
7. Back-and-forth nudging allows us to "ping-pong" back-and-forth which lets us stack mirrored situations
8. The background term is removed in back-and-forth nudging and we instead, include the energy of the system $-\dfrac{\Delta t}{2}<FX, X>$
9. Unlike with [[Sequential Algorithms (Opt. Interpolation & Kalman)|Kalman filtering]], we correct the state with the observation at the previous time step

# Definitions
- Observer: Parallel system similar to the original which gets updated thanks to the observations
- Hurwitz Matrix: A matrix such that all [[Eigenvalues and Eigenvectors|eigenvalues]] have a negative [[Complex Numbers|real part]]
- Observable: A system in which, given n time steps, all states are able to be observed
	- $rk\begin{pmatrix}H\\HF\\HF^2\\HF^3\\\vdots\\HF^n\end{pmatrix} = n$
	- A spinning disc with a small viewing window will eventually show all sides of the disc as they pass the viewing window
- Stable System: If you do nothing, then nothing happens
	- No real systems because, for example, a plane would fall to the Earth if we did nothing due to gravity
- Bifurcation: A small change puts the system on a very different trajectory
	- The [[Data Assimilation Overview|Lorenz model]] behaves completely differently for small changes in the [[Variational Algorithms (3D-Var & 4D-Var)|initial condition]]
- Explicit Model: We can write the next point as a direct equation of the current point

# Additional Resources
- [Observability (Wikipedia)](https://en.wikipedia.org/wiki/Observability#:~:text=Observability%20is%20a%20measure%20of,linear%20system%20are%20mathematical%20duals.)

# Notes
## Nudging Algorithms Overview
- Nudging algorithms are all 4D (include time)
- Goal: Force the model to fit the observations
	- Simplest way is just to add a term ($K(x_{obs} - Hx)$) to the function
		- $\dfrac{\partial x}{\partial t} = F(x) + K(x_{obs} - Hx)$
	- In one dimension, $\dfrac{\partial x}{\partial t} = -Kx \to x(t) = e^{-kt}x_0$
- This was the first algorithm implemented in an operational way for weather forecasting
- Linear scenario (original model)
	- $\dfrac{\partial x}{\partial t} = Fx\textrm{ and }x(0)=x_0$
		- Assume a perfect model: $x_{obs} = Hx_{true}$
	- Build an [[Point Estimators|estimator]]: $\dfrac{\partial \hat x}{\partial t} = F\hat x + K(x_{obs} - H\hat x)$ and $\hat x(0) = \hat x_0$
	- Since this is linear, we can see how the error evolves over time
		- $E = \hat x - x_{true}$ 
		- $\dfrac{\partial E}{\partial t}=\dfrac{\partial \hat x}{\partial t} - \dfrac{\partial x_{true}}{\partial t} = F\hat x + K(x_{obs} - H\hat x) - Fx_{true} = FE-KHE = E(F - KH)$
	- We want $\underset{t \to +\infty}{E(t) \to 0}$, so we want $F - KH$ to be strictly negative
	- But $F-KH$ is likely not symmetric which means we will have complex eigenvalues
	- So, we will look to find $F-KH$ such that it is a Hurwitz matrix
		- <mark style="background: #FFB86CA6;">If the real part of the eigenvalues is positive, it will amplify the error over time along that direction</mark>
- Now we try to find a $K$ such that we make the system stable so it converges over time
- To do this, we use a [[Variational Algorithms (3D-Var & 4D-Var)|4D-Var cost function]] to optimize $K$
	- $\dfrac{\partial x}{\partial t} = F(x) + K(y - H(x))$ and $x(0) = x_0$
	- Now the cost function is a cost function of the observations AND $K$
- It's important to have some regularization on $K$ to ensure the solution doesn't depart too far from the physical system (usually just the square norm of $K$)
- The [[Variational Algorithms (3D-Var & 4D-Var)|adjoint model]] doesn't change. We just get a gradient with respect to $x_0$ and one with respect to $K$
## Back and Forth Nudging
- Main issues with simple nudging
	- You're changing the physics of the model
		- But models are typically wrong anyway
	- Most prediction windows are short, so being asymptotic with respect to time is irrelevant
- Situation: Assume a "small" time window such that we do not converge
	- Once we have a better end point, can we deduce a better starting point?
	- Try to then solve backwards
		- $\dfrac{\partial x}{\partial t} = F(x)$ and $x(T)$ (our new, better solution)
		- This however is much more unstable than the forward model
	- But we can <mark style="background: #FFB86CA6;">stabilize the backward model with nudging too</mark>
		- $F(x)$ has the same properties as $-F(x)$
		- By nudging in both the forward and backward directions, we can use a smaller $K$
		- This also provides smoother updating towards the observations
		- Also creates a nudging equation in infinite time since we can just keep stacking forward and backward layers over and over again
	- We can define $K$ using only the observation error and a constant
		- $K = kH^TR^{-1}$
		- Larger $k$ = <mark style="background: #FFB86CA6;">more attracted to the observations</mark>
		- In general, we will nudge more when there is less error in the observations
- Back and Forth nudging removes the background term and only includes the energy of the system
- Typically nudging algorithms only update the variables we observe
	- But by solving forwards and then backwards, we can get a sense of the unobserved variables
## Python Implementation - Lorenz Model
```python
import numpy as np
import matplotlib.pyplot as plt

def lorenz(Xinit): # Xinit = initial condition at t=0
    X = np.zeros((3,N))
    X[:,0] = Xinit # initial condition
    for i in range(N-1): # time loop
        X[0,i+1] = X[0,i] + deltat*(sigma*(X[1,i]-X[0,i])) # x equation
        X[1,i+1] = X[1,i] + deltat*(rho*X[0,i]-X[1,i]-X[0,i]*X[2,i]) # y equation
        X[2,i+1] = X[2,i] + deltat*(X[0,i]*X[1,i]-beta*X[2,i]) # z equation
    return X

# Lorenz model parameters
sigma = 10.0
rho = 28.0
beta = 8.0/3.0

# numerical parameters
T = 5.0 # final time of the assimilation window
N = 5001 # number of times
deltat = T/(N-1) # time step

# "true" initial condition (twin experiments)
Xtrue0 = np.array([-4.62, -6.61, 17.94])

# generate observations
# we choose to observe x and y (only)
H = np.zeros((2,3))
H[0,0] = 1
H[1,1] = 1
# we observe every 100 time steps
# we add noise
freq = 100
noiselevel = 0.5
Xobs = Xtrue[0:2,::freq]+noiselevel*np.random.normal(0,1,((2,int((N-1)/freq)+1)))

# make it simple: B = Id, R = Id
# background state:
Xb0 = np.array([-4.5, -7.0, 17.4])
Xb = lorenz(Xb0)

# nudging parameter (typical upper bound is 1/dt)
k = 0.5/deltat

# direct nudging
Xn = np.zeros((3,N))
Xn[:,0] = Xb0 # initial condition
for i in range(N-1): # time loop
    Xn[0,i+1] = Xn[0,i] + deltat*(sigma*(Xn[1,i]-Xn[0,i])) # x equation
    Xn[1,i+1] = Xn[1,i] + deltat*(rho*Xn[0,i]-Xn[1,i]-Xn[0,i]*Xn[2,i]) # y equation
    Xn[2,i+1] = Xn[2,i] + deltat*(Xn[0,i]*Xn[1,i]-beta*Xn[2,i]) # z equation
    # if i is an observation time
    if np.mod(i,freq)==0:
        # add feedback
        Xn[:,i+1] += deltat*k*(H.T@np.linalg.inv(R)).dot(Xobs[:,int(i/freq)]-H.dot(Xn[:,i]))

# backward nudging coefficient
kb = 1.0/deltat

# backward nudging
Xbn = np.zeros((3,N))
Xbn[:,0] = Xn[:,N-1] # final condition = final direct nudging state
for i in range(N-1): # time loop (we keep it "forward")
    # we change the sign of deltat or of the RHS to solve backwards
    Xbn[0,i+1] = Xbn[0,i] - deltat*(sigma*(Xbn[1,i]-Xbn[0,i])) # x equation
    Xbn[1,i+1] = Xbn[1,i] - deltat*(rho*Xbn[0,i]-Xbn[1,i]-Xbn[0,i]*Xbn[2,i]) # y equation
    Xbn[2,i+1] = Xbn[2,i] - deltat*(Xbn[0,i]*Xbn[1,i]-beta*Xbn[2,i]) # z equation
    # if i=1 is an observation time
    if np.mod(N-1-i,freq)==0:
        # add feedback (don't change the sign!)
        Xbn[:,i+1] += deltat*kb*(H.T@np.linalg.inv(R)).dot(Xobs[:,int((N-1-i)/freq)]-H.dot(Xbn[:,i]))
```
