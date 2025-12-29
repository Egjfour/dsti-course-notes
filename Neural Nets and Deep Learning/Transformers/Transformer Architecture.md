|    Course Name    |    Topic     |   Professor   |       Date       |       Tags       |
| :---------------: | :----------: | :-----------: | :--------------: | :--------------: |
| **Deep Learning** | Transformers | Benoit Mialet | 02 décembre 2025 | #MachineLearning |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251202%5F094935%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ed703b091%2Dc259%2D4e65%2Da95d%2De92bbfd59ad9)

# Summary
*Transformers are neural network models which are comprised of encoders which generate context for a given sequence and decoders which predict the next tokens given the context. Transformer models need not have both of these elements, and different architectures serve different purposes. The key element of both the encoder and decoder part are the [[The Attention Mechanism|attention heads]] contained within.*

# Key Takeaways
1. Once the context is generated, the encoder's work is done
2. Tokenization dramatically reduces vocabulary size since typically, full words are not used
3. Multiple blocks (encoder and/or decoder) are used to learn higher-level features. This offers a similar effect to having multiple [[Convolutional Neural Networks|convolutional layers]]
4. When working with [[The Training Process|mini-batches]], sequences are padded to ensure all sequences in a batch are the same length

# Definitions
- Encoder: Portion of a transformer which extracts useful information from input data
- Decoder: Generative portion of a transformer which outputs a sequence
- Unimodal Models: A model which has one input and output type
- Multimodal Models: Models which have more than one input/output type
- Tokenization: Dividing an input sequence into elements which match one element of a known vocabulary and are encoded to integers
	- In NLP, this is typically Byte-Pair Encoding
- Sinusoidal Positional Encoding: Given an input sequence of length e, take e unique sine functions and apply each function to the position of the token in a fixed-length context 

# Additional Resources
- [Tokenization (Video)](https://www.youtube.com/watch?v=HEikzVL-lZU)
- [The Role and Implementation of Positional Encoding](https://www.ibm.com/think/topics/positional-encoding#:~:text=Positional%20encoding%20is%20a%20technique,semantic%20meaning%20of%20a%20sentence.)
- [The GeLU Activation](https://docs.pytorch.org/docs/stable/generated/torch.nn.GELU.html)

# Notes
## Architecture Overview
- Encoder-decoder models
	- The encoder creates a context matrix
	- Decoder takes context from the encoder and previously generated outputs as the input
	- Decoders are autoregressive and will generate until the "end-of-sequence" token is generated
- Other models are either encoder-only or decoder-only
	- These models still use the same components in whichever element they are based off
 ![[Pasted image 20251227131124.png]]
## The Encoder
- Step 1: Tokenization
	- The tokenization strategy is model-specific and must be consistent for training and inferencce
- Step 2: Token Embedding
	- Use the integer for the token to identify a learned [[Transformers Overview|sparse vector representation]]
	- The <mark style="background: #FFB86CA6;">embedding vector is contextless</mark> (each vector is independent of each other)
- Step 3: Positional Encoding
	- We add a vector with the same size of the embedding vectors to convey the order of a given token in the sequence
	- Typically, sinusoidal positional encoding is used since just adding the position will result in very large values added as the sequence length increases
		- Normalizing the token indices also doesn't work since the scale changes as the sequence length changes
- Step 4: [[The Attention Mechanism|Self-Attention]]
- Output: A matrix of contextualized token embeddings
## Encoder Blocks
- Transformer models have multiple encoder blocks which are of the same size and structure but which have different parameters
- Calculations for blocks are performed sequentially
- After [[The Attention Mechanism|attention scores]] are calculated and applied, a [[Elements of a Neural Network|feed-forward neural network]] is used for further refinement and to introduce nonlinearity by applying [[Activation Functions|activation functions]]
	- Typically, these layers use GeLU activation
	- Typically, the vector output from the attention process is expanded by the hidden layers
- Skip connections can be (and regularly are) added to allow for better training with deeper models
- Output
	- A matrix with the same shape as the [[The Attention Mechanism|attention output]]
	- The features are thus fully extracted and can be used for downstream tasks
 ![[Pasted image 20251227133721.png]]
## The Decoder
- Step 1: Tokenization
- Step 2: Token Embedding
- Step 3: Positional Encoding
- Step 4: [[The Attention Mechanism|Masked Attention]]
- Step 5: [[The Attention Mechanism|Cross Attention]]
- Output: A hidden state of dimension (`seq. length`, `hidden size`)
	- The model's output comes after a linear layer with an output for the chosen task (e.g., NLP tasks will have one output for every word of the known vocabulary)
![[Pasted image 20251228193324.png]]