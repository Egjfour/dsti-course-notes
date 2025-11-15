|          Course Name           |      Topic       |   Professor   |        Date         |       Tags       |
| :----------------------------: | :--------------: | :-----------: | :-----------------: | :--------------: |
| **Artificial Neural Networks** | Model Evaluation | Benoit Mialet | 5 & 7 novembre 2025 | #MachineLearning |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251105%5F095246%2DMeeting%20Recording1%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E0fbcb7d4%2D8567%2D45a0%2Db788%2De00b8659796b)

# Summary
*To know that our model is useful, we need a well-crafted strategy to evaluate it so we can identify the areas for improvement and communicate to stakeholders confidently about the model's usefulness going forward. The train/validation/test splitting of the data is an essential element of this which empowers fair evaluations that simulate effectively unseen data. Effective model evaluation also enables hyperparameter tuning and lets us balance the bias-variance tradeoff.*

# Key Takeaways
1. The [[Testing|validation set]] is used to define the training method
2. The data splits must have the same distribution and categorical variables (**stratified**)
3. The [[Variable Selection - Linear Model|L2 Loss (Ridge)]] encourages models to use parameters more evenly by penalizing very strong weights
4. Batch normalization is more effective as the batch size increases
5. For large and deep models, batch normalization and dropout are essentially mandatory

# Definitions
- Bias: The degree to which predictions are incorrect due to overly simple models that fail to capture the true relationship
- Variance: The amount which a model and its predictions change with respect to changes in the underlying training data
- Overfitting: A model which has learned too much information from the training set and fails to generalize well to unseen data
	- Low bias, high variance
- Underfitting: A model which performs poorly even on the training data because it fails to capture the complexities of the true underlying function
	- High bias, low variance
- Regularization: A set of techniques which reduce overfitting and improve generalization
- Dropout: Randomly set a fraction of neurons to zero during each [[The Training Process|training step]]
	- ONLY used during training. Among reasons why setting model in [[Neural Networks in PyTorch - Overview|eval mode]] is important
- Batch Normalization: Re-center and scale the activation output for each neuron
- Early Stopping: Model model performance on the validation set during training and stop when validation error stops decreasing
- Internal Covariate Shift: Change in input distribution inside the network due to changing parameters during training

# Additional Resources
- [Bias-Variance Tradeoff (IBM)](https://www.ibm.com/think/topics/bias-variance-tradeoff)
- [ML Metrics Cheat Sheet (Stanford)](https://stanford.edu/~shervine/teaching/cs-229/cheatsheet-machine-learning-tips-and-tricks)
- [Optuna Documentation](https://optuna.readthedocs.io/en/stable/)

# Notes
## Basic Principles & Common Metrics
- We want to ensure that the data generalizes well on unseen data and neither underfits nor overfits
	![[Pasted image 20251115104547.png]] 
- To simulate unseen data (since we often cannot simply get more data), we split into [[Testing|train, validation, and test datasets]]
	- Note that the test dataset should never be used to tune parameters or fit the model. In fact, we shouldn't even really calculate the loss function on it
- Common Evaluation Metrics
	- While loss is a good indicator of model performance, during validation and final testing, other metrics help to paint a clearer picture and are helpful for communicating back to stakeholders
	- Binary Classification
		- Accuracy = # correct / total
		- Precision = TP / (TP + FP) -- column sum of the confusion matrix
		- Recall = TP / (TP + FN) -- row sum of the confusion matrix
		- F1 score = 2 x precision x recall / (precision + recall)
			- Harmonic mean of precision and recall
	- Regression
		- Root mean squared error
		- Mean absolute error
		- Mean absolute percentage error
## Hyperparameter Tuning (Optuna)
- [[Gradient Descent and Optimizers|Hyperparameters]] play a key role in determining the final model built
- There is no "universal best set" of hyperparameters, but we can find a good configuration for our data by calculating loss or eval metrics on the validation set and picking the configuration that achieves the best results
- Tuning strategies
	- Grid Search: Create a latin hypercube of hyperparameters and test each combination
		- Computationally expensive and grid must be defined
	- Random Search: Randomly test configurations from the defined latin hypercube
		- Tends to perform a little bit better and is faster but has similar drawbacks
	- Bayesian Optimization
		- Create a model to predict the the function of our metric w.r.t. the hyperparameters
		- Model balances exploration and exploitation
		- Considered the more efficient and state-of-the-art method
- Using <mark style="background: #FFB86CA6;">cross-validation strategies can help remove selection bias for the validation set</mark> during hyperparameter optimization
- Optuna is a python library which offers a flexible implementation of the Bayesian Optimization
	- With Optuna we define a study and create an objective function which the study will try to minimize (or maximize)
	- The study has out-of-the-box capabilities for sampling parameter spaces
## Regularization & Model Improvement Strategies
- Regularization methods are used to help stabilize the learning process and improve generalization capabilities
- L1 (Lasso) and L2 (Ridge) penalties
	- These penalties force certain parameters to zero (lasso) or near-zero (ridge) by incorporating a penalty term into the loss function
	- Lasso is rarely used in deep learning, but many optimizers have out-of-the-box implementations for ridge (Adam uses the parameter `weight_decay` for L2)
	- These penalties introduce another hyperparameter which must be tuned, $\lambda$
- Dropout
	- This is <mark style="background: #FFB86CA6;">one of the most effective and widely used techniques in deep learning</mark>
	- Prevents neurons from co-adapting too strongly and forces the network to not rely on specific neurons resulting in better generalization
	- The `model.eval()` call in PyTorch turns this off
	- New hyperparameter to determine proportion of neurons set to 0 must be configured
	- The `nn.Dropout()` is <mark style="background: #FFB86CA6;">added in-between the layers</mark> of the model architecture
- Early Stopping
	- For neural networks, this is a must-have element
	- Early stopping is added by the developer in the training loop
- Batch Normalization
	- Stabilizes the distribution of inputs during each training step to each layer
	- Fights the internal covariate shift and <mark style="background: #FFB86CA6;">allows for higher learning rates</mark>
		- This is especially important in deeper architectures
	- Also can be useful for controlling poor weight initialization
	![[Pasted image 20251115112231.png]] 
## Data Augmentation
- In general, more data = better model, but getting more data can be impossible or impractical
- But we can often leverage the data we already have
	- This strategy is heavily used in computer vision and natural language processing
	- Example - Image Augmentation:
		![[Pasted image 20251115112502.png]]
	- Example - NLP:
		![[Pasted image 20251115112523.png]]
- Doing augmentations like these also helps to encourage better generalizability for models