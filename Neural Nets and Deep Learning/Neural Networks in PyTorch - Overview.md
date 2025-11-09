|          Course Name           |  Topic  |   Professor   |         Date         |           Tags            |
| :----------------------------: | :-----: | :-----------: | :------------------: | :-----------------------: |
| **Artificial Neural Networks** | PyTorch | Benoit Mialet | 3,4,5 novembre, 2025 | #MachineLearning #Python  |

# Summary
*PyTorch is the leading framework for building and executing neural networks in Python. It offers a suite of building blocks for both models and data that makes it both simple to use and highly flexible. Models and data are defined by using custom classes that impose requirements on method implementation. Additionally, PyTorch supports easy integration with GPU acceleration and mult-GPU architectures.*

# Key Takeaways
1. The model and data MUST live on the same device (CPU/GPU)
2. Data and Models are designed using [[Python Classes|python classes]] which [[Inheritance|inherit]] from torch base classes
3. We can automate the selection of the hardware by using `torch.cuda.is_available()`

# Definitions
- Tensor: The object which lets us store the nulti-dimensional representation of the data
- Training Loop: The sequence of a forward pass, loss calculation, [[Gradient Descent and Optimizers|backpropagation]], and an [[Gradient Descent and Optimizers|optimizer step]]
- Step: A single iteration of the training loop for a batch of training data
- Epoch: A pass of all training data through the training loop

# Additional Resources
- [PyTorch Documentation](https://docs.pytorch.org/docs/stable/index.html)
- [Why we need super().__init__()](https://eitca.org/artificial-intelligence/eitc-ai-dlpp-deep-learning-with-python-and-pytorch/data-eitc-ai-dlpp-deep-learning-with-python-and-pytorch/datasets/what-is-the-role-of-the-super-__init__-command-in-pytorch/#:~:text=__init__()%60%20ensures%20that,that%20should%20not%20be%20skipped.)

# Notes
## What is PyTorch?
- PyTorch is an open-source deep learning framework developed by Facebook's AI Research lab (FAIR) with extensive documentation
	- Most popular framework for both academia and industry thanks to its simplicity and robustness
- Main features
	- Multidimensional arrays with device (CPU vs GPU) support: `torch.Tensor`
		- `tensor.to({device: str})` is used to place tensors (and models) on the desired device ("cpu" or "cuda")
	- Data management utilities (`Dataset` and `Dataloader`): `torch.utils.data`
	- [[Elements of a Neural Network|Neural network model]] building blocks: `torch.nn`
	- Automatic differentiation: `torch.autograd`
		- This is the most powerful feature of the library
	- [[Gradient Descent and Optimizers|Gradient-based optimization]] of [[Elements of a Neural Network|weights and biases]]: `torch.optim`
## Tensors
- Tensors are an extension of `numpy` arrays that can be moved to different hardware
- The number of dimensions (`tensor.ndim` or `tensor.shape` attributes) is determined by the number of square brackets
	- The inner-most elements represent the rows
	- Single-element tensors are scalars, and the python primitive scalar can be accessed with the `tensor.item()` method
	- If there are "useless" dimensions, the `tensor.squeeze()` method will compress these
	- If an extra dimension is needed for model calculations (usually the case for the vector of actual responses), the `torch.unsqueeze({n_dims})` method can be used
- Random tensors are used for weight initialization
	- These are created implicitly by model layers (`torch.nn.Linear`), but can be created manually as well using `torch.rand(size = {tuple})`
- Tensors can also calculate matrix operations
	- [[Matrices|Matrix multiplication]]: `mat1 @ mat2` or `torch.matmul(mat1, mat2)`
	- Matrix Transposition: `torch.transpose`
- `torch.ones()` and `torch.zeros()` create tensors filled with ones/zeros which are useful for masking (particularly in the NLP space)
## Data Setup
- To be used by the model, our data must be loaded in memory
	- RAM for CPU and VRAM for GPU
- PyTorch provides utilities that allow us to define and fetch our data
- We first define the data as a custom class which inherits from `Dataset`
	- This class must implement `__init__`, `__getitem__`, and `__len__` methods but can do so in any way desired by the user
	- Importantly, we can use this class to pull data from disk as well
	```python
	from torch.utils.data import Dataset
	
	# Define our custom class
	class ExampleDataset(Dataset):
		def __init__(self, X: torch.TensorType, y:torch.TensorType):
			# Simple example, but anything can be defined here
			self.X = X
			self.y = y
			
		def __getitem__(idx: int) -> (torch.TensorType, torch.TensorType):
			return self.X[idx], self.y[idx]
			
		def __len__():
			return len(self.X)
	```
- With a dataset defined, we create a data loader
	- Data loaders allow us to easily process data in the training loop
	- With a data loader, we just initialize the class directly from torch with our `Dataset` object
		- Note, [[The Training Process|data preprocessing]] should already be handled as well as the split into train, validation, and test sets
	- The data loader asks for the batch size as well as a `shuffle` parameter
		- <mark style="background: #FFB86CA6;">Shuffling should be on for training</mark> and it doesn't matter for the test data
	```python
	from torch.utils.data import Dataloader
	
	# We initialize both classes at the same time
	train_loader = Dataloader(
								ExampleDataset(x_train, y_train), # a torch Dataset
								batch_size = 32, # Can choose any number
								shuffle = True # Should always be true for training
							)
	``` 
## Model Setup
- Like datasets, models are also custom classes which inherit from `nn.Module`
	- Two methods are required in the class: `__init__` and `forward`
		- The `__init__` method is where the model architecture itself is defined
			- Should start with `super().__init__({CustomClass}, self)` to get the [[Inheritance|parent class]] methods and attributes loaded correctly
		- The `forward` method takes data as input and returns the model output by completing a forward pass
- Torch offers utilities for commonly-used elements
	- `nn.Linear()` creates a single feed-forward fully-connected layer with random initialization for the weights and biases
	- [[Activation Functions|Activation functions]] with simple calles like `torch.sigmoid()` and `torch.relu()`
	- Improvement components like [[Identifying Issues & Improving Results|dropout and batch/layer normalization]]
		- `nn.Dropout()`, `nn.BatchNorm1d`, `nn.LayerNorm`
	- Additional utilities such as `nn.Sequential` and `nn.ModuleDict` allow for more streamlined and/or dynamic model builds
	```python
	import torch
	import torch.nn as nn
	
	# We define a basic MLP with one hidden layer and a single output
	class ExampleModel(nn.Module): #Inherit from nn.Module
		# __init__ should ideally build the architecture dynamically
		def __init__(self, input_size: int, hidden_size: int):
			# CRUCIAL: Need to initialize nn.Module
			super().__init__(ExampleModel, self)
			
			# Now, we build the architecture
			self.fc1 = nn.Linear(input_size, hidden_size)
			self.out = nn.Linear(hidden_size, 1) # 1 for the output node
			
			# Activations used - assume ReLU
			self.relu = torch.relu()
			
			# Add dropout and batchnorm
			self.dropout = nn.Dropout(0.1)
			self.batchnorm = nn.BatchNorm1d()
			
		# forward executes the forward pass on actual data
		def forward(self, X):
			X = self.relu(self.fc1(X))
			X = self.batchnorm(X)
			X = self.dropout(X)
			return self.out(X)
	```
## Model Training
- The model is [[The Training Process|trained in a loop]] where each iteration represents an epoch and at least one step
- During each epoch, we
	- Loop through the batches and
		- Perform a forward pass (`__call__` is mapped to `forward`)
		- Calculate Loss
		- Perform backpropagation
		- Take a step in the [[Algorithms - Gradient-Based Optimization|opposite direction of the gradient]] using the [[Gradient Descent and Optimizers|optimizer]]
- During model training, we can use the `SummaryWriter` from tensorboard to easily track metrics such as loss, RMSE, R1, F1 score, etc in a professional front-end
	- In Colab, Tensorboard is initialized with the following
	```python
	# If working on CoLab
	%load_ext tensorboard
	# The summary writer should also point to this directory
	%tensorboard --logdir "runs/"
	``` 
## Saving a Model
- The model weights and parameters (as well as any other initializations) are <mark style="background: #FFB86CA6;">saved as a user-defined dictionary</mark> using the `torch.save()` function
	- This dictionary should include the `state_dict()` method output from the trained model object
	- Any other relevant `kwargs` can be passed as well
- Torch models are saved as `.pt` files
- To load a model from a file, we first need an instance of our model class. Then, the method `load_state_dict` inherited from `nn.Module` is used to update the weights and biases to the training output