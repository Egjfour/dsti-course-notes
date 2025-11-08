|          Course Name           |          Topic           |   Professor   |      Date       |       Tags       |
| :----------------------------: | :----------------------: | :-----------: | :-------------: | :--------------: |
| **Artificial Neural Networks** | Architectural Components | Benoit Mialet | 3 novembre 2025 | #MachineLearning |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251103%5F095124%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E4408d3ee%2D83b9%2D4e47%2D9b4e%2De736e434b521)

# Summary
*Neural networks, based off the Universal Approximation Theorem, are a mechanism to approximate any continuous function. These models work by combining layers of linear combinations with non-linear activation functions to extract features and complex patterns. The core element of a neural network is the neuron/node which takes inputs, combines them with a set of weights and a bias to produce a logit. This logit is then passed through the chosen activation function. Neurons are stacked in layers and it is the depth of these layers which we use to classify our networks.*

# Key Takeaways
1. Neural networks approximate <mark style="background: #FFB86CA6;">continuous</mark> functions
2. The output of a linear layer is a logit ($z$)
3. [[Activation Functions|Activation functions]] are what introduce nonlinearity to the model
4. It essential that the [[Functions and Derivatives of Functions|derivative]] of the activation function can be calculated

# Definitions
- Artificial Intelligence: Field of computer science that creates machines which perform tasks that **normally** require human intelligence
- Machine Learning: A subfield of AI where computers learn patterns from data without being explicitly programmed
- Deep Learning: Subfield of ML where learning is based on neural networks
- Artificial Neural Networks: A subset of machine learning which serve as a core element of deep learning based on the Universal Approximation Theorem and work by extracting underlying relationships in the data
- Universal Approximation Theorem: At least one neural network exists that can approximate any [[Continuity & Derivability|continuous function]] with arbitrary precision thanks to any non-polynomial activation function
- Semi-Supervised Learning: The utilization of a few few labelled examples to fill in missing labels on the rest of the dataset to then retrain
	- RISK: Initial biases in the model on a few records will compound in the final model
- Pre-activation: The [[Vectors|linear combination]] portion of a neuron
- Layer: A group of neurons at the same level of a neural network
- Hidden Layer:  A layer of neurons which lies between the input and output layers
- Fully-Connected/Dense Layer: Every node in the layer is connected to all nodes in the preceding and subsequent layers

# Additional Resources
- [Universal Approximation Theorem](https://en.wikipedia.org/wiki/Universal_approximation_theorem)

# Notes
## AI and the General ML Workflow
- Neural networks are a subset of the algorithms covered by machine learning
- They are the crucial element for building deep learning systems ![[Pasted image 20251108105557.png]]
- To build ML models, including neural networks, the following process is generally observed
	- Problem definition and goal setting
		- Are we doing classification, time-series, regression, etc.
		- Defining of success metrics and checking data availability
	- Data collection and preparation
		- Data can be either labelled or unlabelled
		- We need to make sure to convert to a form the algorithms can interpret
	- Model selection and training
		- What type of algorithm and what type of training (supervised, semi-supervised, unsupervised)
	- Model evaluation and improvement
	- Deployment and usage
	- [[Deployed Model Monitoring|Monitoring]] and maintenance
		- Examining [[Deployed Model Monitoring|data drift]] and performance degradation
## Basics - Perceptrons, Neurons, and Layers
- Neurons/Nodes
	- These are computational units which take inputs and yield outputs
	- The design is modelled after neurons in the human brain
	- Neurons are comprised of a set of weights (one for each input) and a bias which lives inside the node
		- These weights and biases are applied in exactly the same manner as the [[Multiple Linear Model|multiple linear model]] (hence why they are called Linear Layers)
	- The output of the node is a logit, denoted $z$, also called pre-activation
		- $z = \sum_i w_ix_i+b$
	- Logits are the passed to an activation function, $a$, which determine the degree to which we activate/use a given neuron
	 ![[Pasted image 20251108111310.png]]
- Generally weights are denoted $w_{\textrm{layer idx, neuron idx, neuron idx of next layer}}$
- Perceptrons are the combination of neurons with the step activation function
	- Originally proposed by Rosenblatt in 1957
- Layers are a group of neurons at the same level of the neural net
	- Three main types
		- Input: The data we pass to the network
		- Output: The final prediction from the network
		- Hidden: Layers in-between that the network uses for feature extraction
	 ![[Pasted image 20251108112413.png]]
	- Layers also are frequently represented as matrices since the linear step acts as a matrix multiplication
## Network Depth
- <mark style="background: #FFB86CA6;">The number of hidden layers is how we describe neural networks</mark>
	- 0 Hidden Layers: Single-Layer Perceptron
		- Can only handle simple, linearly separable tasks
	- 1 Hidden Layer: Shallow Neural Network
		- Each layer is fully-connected
	- <mark style="background: #FFB86CA6;">2+ Hidden Layers: Deep Neural Network</mark>
	- We use the term Multi-Layer Perceptron (MLP) to describe anything with at least one hidden layer
		- Despite being called perceptrons, these can use ANY activation function
## Neural Network Outputs
- The <mark style="background: #FFB86CA6;">task of the neural network is determined solely by the output layer</mark>
	- Despite the fact that most of the architecture (input and hidden layers) are for extracting features
- Types of tasks
	- Regression: Predict a continuous numerical value
		- Single neuron output
		- No activation function on the output since the output value is in the set of [[Real Numbers, Real Sequences, and Limits|real numbers]]
	- Binary Classification: Predict one of 2 classes
		- Single neuron output
		- [[Activation Functions|Sigmoid activation function]] with a "threshold" (usually 0.5) to make a decision
	- Multi-Class Classification: Predict <mark style="background: #FFB86CA6;">exactly one class</mark> among $k$ possible categories
		- Vector output with a sum = 1
		- Output layer has $k$ neurons which represent the probability for each class
		- Uses the [[Activation Functions|softmax activation function]]
	- Multi-Label Classification: Predict multiple independent labels at once
		- There are multiple correct answers
			- Example: Image classification - a photo can have both a house and a tree
			- Sigmoid activation is used separately for each of the $k$ output neurons