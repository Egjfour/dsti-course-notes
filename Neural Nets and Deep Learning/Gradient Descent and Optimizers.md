|          Course Name           |    Topic     |   Professor   |      Date       |       Tags       |
| :----------------------------: | :----------: | :-----------: | :-------------: | :--------------: |
| **Artificial Neural Networks** | Optimization | Benoit Mialet | 4 novembre 2025 | #MachineLearning |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251104%5F094905%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ed2f3ee37%2D6ee9%2D4fbb%2Daa7e%2D793bc14bc51f)

# Summary
*[[Algorithms - Gradient-Based Optimization|Gradient descent]] is the fundamental algorithm which is used to update the weights and biases at each step throughout the training process of an artificial neural network. These algorithms are applied efficiently by optimizers which not only handle calculating the new parameters given a gradient but also adopt strategies to help improve convergence and speed up training.*

# Key Takeaways
1. The partial derivative for any given parameter in the network depends on all parameters which come after it
2. The vanishing gradient problem means that early [[Elements of a Neural Network|layers]] of the network learn incredibly slowly
3. Momentum us an exponential moving average of past gradients and helps the model
4. Yann LeCun states that 32 is, for most cases, the optimal batch size
5. The bias correction proposed in the Adam optimizer is useful because in early iterations, $m_t$ and $v_t$ are biased towards 0 giving poor parameter estimations

# Definitions
- Hyperparameter: Any parameter which is set by the user and not updated as part of the [[The Training Process|training process]]
- Learning Rate: The scalar-valued hyperparameter which determines how large of a step is taken in the opposite direction of the gradient
- Stochastic Gradient Descent: Updating model parameters using one observation at a time
- Optimizer: Algorithms which adjust how parameters are updated during training

# Additional Resources
- [Understanding Momentum, RMSProp, and Adam](https://www.geeksforgeeks.org/deep-learning/adam-optimizer/)

# Notes
## [[Algorithms - Gradient-Based Optimization|Gradient Descent]] in Neural Networks Overview
- The goal is to find the optimal value, $\theta$, for each parameter such that the [[The Training Process|loss function]] is minimized
- General Process
	- Take the current parameter value (initialized randomly for the first iteration)
	- Calculate the gradient of the loss function for the parameter: $\dfrac{\partial \mathcal L}{\partial \theta}$
	- Update $\theta$ by taking a step in the opposite direction of the gradient
- Iterate until
	- A minimum step size is reached
	- The maximum number of iteration is reached
- The learning rate is the most important hyperparameter
	- Too low and training takes too long or can stop
	- Too high and it can overshoot the minimum and never reach it
- The basic gradient update formula is
	- $\theta_{t+1} = \theta_t - \gamma \cdot \dfrac{\partial \mathcal L}{\partial \theta}$ OR $\theta_{t+1} = \theta_t - \gamma \cdot \nabla \mathcal L(\theta_t)$
	- With $\gamma$ the learning rate
- The [[Functions and Derivatives of Functions|partial derivatives]] are calculated in parallel using [[Matrices|matrix multiplication]]
	- Because of all the nested operations, we need backpropagation to make these computations tractable
- Certain [[Activation Functions|activation functions (sigmoid)]] introduce the <mark style="background: #FFB86CA6;">vanishing gradient problem</mark> because they have very small gradients at all values which are then multiplied together
	- This is a problem because the model fails to learn deep representations and early layers learn extremely slowly if at all
	- In general, this problem gets worse as network depth increases
	- The [[Activation Functions|ReLU activation function]] solves this problem entirely
## Feeding Strategies
- The amount of data used in a single training [[The Training Process|step]] determines a great deal about how the model converges
- By default, gradient descent loads the entire dataset at once and weight updates happen once per epoch
	- This is not feasible for most modern datasets
- Yann LeCun introduced stochastic gradient descent which performs a weight update for each sample of training data separately
	- Learning is much less stable, but updates are fast and there is a low memory footprint
	- The cons are high variance and noisy convergence
	- SGD does show <mark style="background: #FFB86CA6;">good generalization capabilities, however, and an ability to escape local minima</mark>
- Mini-batch gradient descent is a compromise between SGD and regular gradient descent
	- The gradients are computed on small batches of data allowing for the generalization and speed of SGD while taking advantage of parallelization of gradient calculations
## Optimizers
- Optimizers are the software component which actually apply the gradients calculated during backpropagation to update parameters
- The most basic is the standard gradient update with a fixed learning rate
- Any of the feeding strategies can be applied to any gradient method
- Many other optimizers have been introduced to try to more efficiently move throughout the loss landscape
### Gradient Descent with Momentum
- Similar to the [[Algorithms - Gradient-Based Optimization|conjugate gradient method]], this method combines previous gradients with the current one
- The momentum adds inertia to the descent and <mark style="background: #FFB86CA6;">can help to escape local minima</mark> as well as smooth oscillations in loss and converge faster
- Update formula:
	- Mixture of gradients: $m_t = \beta m_{t-1} + (1 - \beta)\nabla \mathcal L(\hat \theta_t)$
	- New Parameter Value: $\theta_{t+1} = \theta_t - \eta m_t$
	- With $\beta$ as the momentum condition and $\eta$ the learning rate
		- Tunable hyperparameters
- This intuitively creates an exponentially-weighted average of gradients
### AdaGrad (Adaptive Gradients)
- Uses a process to decrease the learning rate over time
	- Problem: over time, the learning rate can shrink too much causing us to stop learning altogether
	- The step taken by the optimizer becomes smaller and smaller over time
- Update formula:
	- $\theta_{t+1} = \theta_t - \dfrac{\eta}{\sqrt{\epsilon + \underset{i=1}{\overset{T}{\sum}}(\nabla \mathcal L(\theta_i))^2}}\cdot \nabla \mathcal L(\theta_t)$
	- With $\epsilon$ close to 0
- Essentially, we scale the learning rate by the size of the cumulative previous gradients
### RMS (Root Mean Squared Error) Prop
- Same idea as AdaGrad but instead of an equal weight on the past gradients, we use an exponential weighted average
- Update formula:
	- Scaling Factor: $v_t = \beta v_{t-1} + (1 - \beta)(\nabla \mathcal L(\theta_t))^2$
	- New Parameter Value: $\theta_{t+1} = \theta_t - \dfrac{\eta}{\sqrt{\epsilon + v_t}}\cdot \nabla \mathcal L(\theta_t)$
	- With $\epsilon \approx 0$ and $\beta$ a hyperparameter
### Adam (Adaptive Moment Estimation)
- Considered the best optimizer currently and most widely used by practitioners
- Acts as a <mark style="background: #FFB86CA6;">combination of both RMS Prop and Momentum</mark>
- Includes an added bias correction for $m_t$ and $v_t$ giving us $\hat m_t$ and $\hat v_t$
	- Solves the issue with poor estimation in early iteration by scaling according to the time step with a hyperparameter $\beta$ (often same as $\beta$ chosen for momentum)
	- $\hat m_t = \dfrac{m_t}{(1 - \beta^t)}$ and $\hat v_t = \dfrac{v_t}{(1 - \beta^t)}$
- Update formula:
	- $\theta_{t+1} = \theta_t - \dfrac{\eta}{\sqrt{\epsilon + \hat v_t}}\cdot m_t$