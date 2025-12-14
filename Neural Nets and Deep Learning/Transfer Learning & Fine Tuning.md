|    Course Name    |       Topic       |   Professor   |         Date          |       Tags       |
| :---------------: | :---------------: | :-----------: | :-------------------: | :--------------: |
| **Deep Learning** | Transfer Learning | Benoit Mialet | 01 & 03 décembre 2025 | #MachineLearning |

[Class Video Link 1](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251201%5F095003%2DMeeting%20Recording1%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Eed217cba%2D8b65%2D48ef%2Db3ed%2D6a738d19776e)
[Class Video Link 2](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251203%5F095043%2DMeeting%20Recording1%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E9b6dcf73%2D3dd2%2D4e7e%2Dbb31%2D6af9da4ba8ae)

# Summary
*Transfer learning is the process of taking a model which has been pre-trained on a large (typically internet-scale) dataset and using it as a feature extractor for a specific downstream task. The model and steps needed are tied to the pre-trained model's architecture and the downstream task that is being trained for. With Huggingface and PyTorch, it is easy to find, download, and implement such models.*

# Key Takeaways
1. Traditional transfer learning freezes the parameters of everything except the final [[Elements of a Neural Network|fully-connected layer]]
2. Pre-training of a model is always self-supervised (no labeled data)

# Definitions
- Transfer Learning: Taking one model that is already trained and update the weights using your data
- Distillation: The output of a large (teacher) model is used to compare outputs against a smaller model (student) and calculate loss for weight update
	- DeepSeek
- Body: The task-agnostic [[Transformer Architecture|encoder blocks]] of a transformer model whose objective is to capture accurately language features and representations and to generate coherent text
- Head: The optional, task-specific tiny part (can be a single layer) added to the the top of the model (could be text classification in NLP)
- Masked Language Modeling: Identify a masked token based on its surrounding tokens
	- Training method for encoder-only models like Bert
- Span Corruption: A variant of masked language modeling which masks segments of adjacent tokens for training
	- Encoder-Decoder model training
- Causal Language Modeling: Predict next tokens unidirectionally using only the previous tokens
	- Training method for decoder-only models

# Additional Resources
- [Finetuning (Huggingface)](https://huggingface.co/docs/transformers/training)

# Notes
## Transfer Learning Overview
- Transfer learning involves taking a large pre-trained model and applying it to your new data
	- Often these models are trained by massive companies on internet-scale data
- The [[The Training Process|training loop]] looks exactly like a normal neural network. The only difference is that we initialize the parameters using a pre-trained model
	- We also frequently do not calculate gradients or update parameters for the feature extraction portion of the model
- Example using [[Computer Vision - Overview and Applications|AlexNet]]
```python
# Initialize a model using pre-trained weights
model_conv = models.alexnet(weights='IMAGENET1K_V1')
for param in model_conv.parameters():
    param.requires_grad = False # Do not calculate or update these parameters

# model_conv
num_ftrs = model_conv.classifier[6].in_features

# Update the classification head (MLP) to be re-initialized
# This will calculate gradients and be updated via the optimizer
model_conv.classifier[6] = nn.Linear(num_ftrs, len(class_names))
```
## Fine-Tuning [[Transformers Overview|Transformer Models]]
- ULMFiT is an approach to training encoder models which uses a body and head approach
	- We first pre-train (or start with a pre-trained model) a model using masked language modeling
	- We then specialize the body using a small dataset
	- The head is then added and trained using our data and specific task
		- We freeze the parameters of the body during this training
- Huggingface is a registry with thousands of pre-trained models which can be downloaded and used for pretraining
	- Huggingface is built on top of [[Neural Networks in PyTorch - Overview|PyTorch]], so we can easily load, extend, and update models in this framework