| Course Name[[Gradient Descent and Optimizers]] |       Topic       |   Professor   |      Date       |       Tags       |
| :--------------------------------------------: | :---------------: | :-----------: | :-------------: | :--------------: |
|         **Artificial Neural Networks**         | Training Networks | Benoit Mialet | 4 novembre 2025 | #MachineLearning |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251104%5F094905%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ef940bf4a%2Dcf6a%2D4f42%2D8ee5%2Da2af92a692c3)

# Summary
*The training process consists of taking small chunks of data and performing, in sequence, a forward pass, loss calculation, backpropagation, and a parameter update. This process is done iteratively over batches of data and repeatedly over the entire training set many times. In PyTorch, most of this functionality is implemented with out-of-the-box methods like `loss.backward()` for backpropagation and `optimizer.step()` for gradient-based parameter updates.*

# Key Takeaways
1. To make the aggregate loss for an epoch independent with the amount of training data, we take the Euclidean mean of the individual sample loss calculations
2. Models are trained for several [[Neural Networks in PyTorch - Overview|epochs]] so that the model learns gradually from the data several times
3. Data preprocessing must take care to not leak test information into the train set. Scaling should be done AFTER splitting the data

# Definitions
- Encoding: Conversion of words/categories into numerical representations
- Normalization/Scaling: The process of ensuring all features are on the same scale
	- Income and age have very different ranges so we rescale them to be the same
- Loss Function: The function which determines how far predictions are from actuals
- Mean Squared Error: Direct distance between [[Real Functions of a Real Variable|real-valued]] output and actual
	- $MSE = \frac{1}{n}\sum_i(\hat y_i - y_i)^2$
- Binary Cross Entropy: The distance between the probability prediction and binary classification target value
	- $BCE = \frac {1}{n}\sum_i -1 * (y_i \cdot log(\hat y_i) + (1-y_i) \cdot log(1 - y_i))$
	- In parentheses: Part for $y_i = 1$ + part for $y_i =0$
- Categorical Cross Entropy Loss: The sum of Binary Cross Entropy Loss for all Categories
	- $CCE = \frac{1}{n}\sum_i \underset{j=1}{\overset{k}{\sum}} BCE_j$ given $k$ categories

# Additional Resources
- [Training with PyTorch](https://docs.pytorch.org/tutorials/beginner/introyt/trainingyt.html)
- [Why do we need zero_grad()](https://stackoverflow.com/questions/48001598/why-do-we-need-to-call-zero-grad-in-pytorch)

# Notes
## Data Preprocessing and Loading
- The only input a neural network can take is numeric. We must convert everything to a number
	- Categorical data must therefore being encoded
		- Ordinal encoding converts categories into sequential integers (used if categories have a natural order)
		- One-Hot Encoding represents each level as a binary vector (this can create a massive amount of new features)
- To stabilize model training, scaling methods should be applied
	- Min-Max scaling is typically used in image processing since it has a predetermined range
		- $x' = \dfrac{x - min(x)}{max(x) - min(x)}$
		- `sklearn.preprocessing.MinMaxScaler`
	- Standard (or [[Random Variables|z-score]]) scaling uses the mean and standard deviation to zero-center and scale numeric constants
		- $x' = \dfrac{x - \mu}{\sigma}$
		- `sklearn.preprocessing.StandardScaler`
	- Both of the above methods preserve outliers, so large outliers should be removed or can be handled using the robust scaler which uses the median and [[Descriptive Statistics|IQR]] in the standard scaler methodology: `sklearn.preprocessing.RobustScaler`
- Once prepared, the data should be placed into a [[Neural Networks in PyTorch - Overview|torch dataset and data loader]]
- For loading to the model, there are 3 strategies:
	- All samples at once: "Gradient Descent"
	- Samples one-by-one: "Stochastic Gradient Descent"
	- Batches of X samples: "Mini-Batch Gradient Descent"
## Loss and Parameter Updates
- After each record/batch goes through a forward pass of the model, the loss is calculated
	- Small loss corresponds to good predictions, so the goal is to minimize the loss
- Classical Loss Functions
	- Regression problems typically use MSE Loss
	- Binary Classification uses Binary Cross Entropy (BCE) loss
	- [[Elements of a Neural Network|Multiclass and Multilabel]] problems both use Categorical Cross Entropy loss
- Backpropagation
	- To actually minimize the loss, we must <mark style="background: #FFB86CA6;">determine how the loss changes with respect to each parameter</mark>
	- This of course means calculating the gradient of the loss for each parameter
		- Due to nesting of functions, the [[Functions and Derivatives of Functions|chain rule of differentiation]] is crucial
	- All of this is handled by calling the `backward()` method on the loss object in PyTorch
	- Since the gradient calculation for earlier levels of the network relies on the calculation of later layers, we move through the network backwards
- Using the gradients, an [[Gradient Descent and Optimizers|optimizer]] then updates the parameters to move in the direction which minimizes loss
## Training Cycle - Example Training Loop in [[Neural Networks in PyTorch - Overview|PyTorch]]
- High-level training loop steps
	- Forward pass of the model
	- Calculate loss
	- Calculate gradients using backpropagation
	- Move in the direction of the minimum using the optimizer
```python
def train_model(model_name: str,
                input_dim: int,
                train_loader: DataLoader,
                val_loader: DataLoader,
                criterion,
                device,
                params: dict[str, Any]):
  """
  Trains a PyTorch model.
  """
  # Prep global options and initialize tensorboard
  writer = SummaryWriter(f'runs/{model_name}')
  EPOCHS = params.get('epochs', 10)
  DROPOUT = params.get('dropout', 0)
  L2_REG = params.get('l2_reg', 0)
  
  # Assume model class BCNet is created
  model = BCNet(input_dim=input_dim, dropout=DROPOUT)
  model.to(device)
  
  # Initialize the optimizer and pass it the model parameters
  optimizer = torch.optim.Adam(model.parameters(), weight_decay=L2_REG)
  
  # Iterate through each epoch
  for epoch in tqdm(range(EPOCHS)):
    model.train() # Ensure the model is in training mode
    train_losses = []
    for x_batch, y_batch in train_loader:
      # Clear the gradients from optimizer memory
      optimizer.zero_grad()
      # Forward pass
      logits = model(x_batch.to(device))
      loss = criterion(logits, y_batch) # BCELoss
      train_losses.append(loss.item() * len(x_batch))
      # Backpropagation
      loss.backward()
      # Optimizer step
      optimizer.step()

    train_loss = np.sum(train_losses) / len(train_loader.dataset)
    val_loss, _, _, _ = evaluate_classification(model, val_loader, criterion)

    writer.add_scalar('Loss/train', train_loss, epoch)
    writer.add_scalar('Loss/val', val_loss, epoch)

  writer.close()
  return model, train_loss, val_loss
```
