|          Course Name           |        Topic         |   Professor   |      Date       |       Tags       |
| :----------------------------: | :------------------: | :-----------: | :-------------: | :--------------: |
| **Artificial Neural Networks** | Types of Activations | Benoit Mialet | 3 novembre 2025 | #MachineLearning |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251103%5F095124%2DMeeting%20Recording1%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E09ca3b95%2Dd774%2D496c%2Dadf6%2D9824899850c4)

# Summary
*Activation functions are the essential piece to neural networks that introduce nonlinearity. Several have been proposed and each has its set of relevant use cases, pros, and cons. The most common today are variations of the rectified linear unit because of the computational simplicity and the lack of the vanishing gradient problem.*

# Key Takeaways
1. It essential that the [[Functions and Derivatives of Functions|derivative]] of the activation function can be calculated
2. The sigmoid and softmax activations are primarily used in the output layers
3. Sigmoid, in particular, suffers from the [[Identifying Issues & Improving Results|vanishing gradient problem]] due to its low [[Function Optimization|gradient]] values
4. Many activations like swish try to solve the dying ReLU problem, but this is challenging because these functions reintroduce the computational complexity of activations like sigmoid
5. Softmax is exclusively used in the output layer of [[Elements of a Neural Network|multiclass classification models]]

# Definitions
- Activation Function: Decision-making units of a neural network which are mathematical equations attached to each neuron
- Step Function: The most basic activation function proposed in Rosenblatt's original paper
	- $a = \begin{cases}1 \textrm{ if } z \ge \theta \\ \textrm{ else } 0\end{cases}$ with $z$ as the [[Elements of a Neural Network|logits]]
- Dying ReLU Problem: When the input, $z$, is $\le 0$, the network cannot learn since the gradient is 0 

# Additional Resources
- [Activation Function Tutorial and Comparison](https://uvadlc-notebooks.readthedocs.io/en/latest/tutorial_notebooks/tutorial3/Activation_Functions.html)

# Notes
## Common Functions
- Linear activation (the identity function) - not used in practice anymore
	- Does not introduce non-linearity
	- Since output = input, there is no practical function
- Binary Step Function - not used in practice anymore
	- The original proposed activation in the original [[Elements of a Neural Network|perceptron]]
	- Establishes a user-defined threshold, $\theta$, and if the logit is more than this threshold, the neuron "fires"/activates
- Sigmoid/Logistic Function
	- Outputs a value between 0 and 1 which can be <mark style="background: #FFB86CA6;">directly interpreted as probabilities</mark>
	- $S(z) = \dfrac{1}{1 + e^{-z}}$
	- Suffers from the [[Identifying Issues & Improving Results|vanishing gradient problem]] and is computationally expensive
		- Since gradients are very small even at 0
	- More commonly used for the [[Elements of a Neural Network|output layer]] since it is highly interpretable
	![[Pasted image 20251109111758.png]] 
- Hyperbolic Tangent (tanh) Function
	- Creates a zero-centered output between -1 and 1
	- Partially solves the vanishing gradient problem of the sigmoid function due to its larger partial derivatives but not entirely and it is also computationally expensive
	- $tanh(z) = \dfrac{(e^z - e^{-z})}{(e^z + e^{-z})}$
	![[Pasted image 20251109112058.png]]
-  Rectified Linear Units (ReLU)
	- This and its variants are the most-used activation function today
		- <mark style="background: #FFB86CA6;">Solves the vanishing gradient problem entirely</mark> by using a piecewise-linear function
		- Extremely efficient to compute and calculate gradients while still adding nonlinearity
		- Models tend to converge quickly
	- $ReLU(z) = max(0, z)$
	- Introduces the Dying ReLU problem
	 ![[Pasted image 20251109113816.png]]
- Leaky ReLU
	- Same concept as ReLU but attempts to reduce the influence of the dying ReLU by introducing a small positive slope for the values < 0
	- $LeakyReLU(z) = max(\alpha z, z)$
	- Has some inconsistency due to the introduction of user-defined parameter, $\alpha$
	![[Pasted image 20251109114022.png]]
- Parametric ReLU - not used frequently in practice
	- Modifies $\alpha$ to become a learnable parameter
		- This significantly expands the number of parameters to learn (one for each neuron)
- Swish - Used in specific situations
	- A modification of Sigmoid to behave more like ReLU to have some negative slope near zero that is also fully differentiable
	- Tends to perform better on deep networks than ReLU but is slower and more computationally expensive
	- $Swish(z) = \dfrac{z}{(1 + e^{-z})}$
	![[Pasted image 20251109114416.png]]
- Softmax
	- Converts the logits for multiple neurons to a set of probabilities which <mark style="background: #FFB86CA6;">sum to 1</mark>
	- Leverages the exponential function to push high values even higher and "force" the model to make more concrete choices
		- The most probable class stands out
	- $Softmax(z_i) = \dfrac{e^{z_i}}{\sum_j e^{z_j}}$
	- Comparison with Linear Normalization
		![[Pasted image 20251109115050.png]]
