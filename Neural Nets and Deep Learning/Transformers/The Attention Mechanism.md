|    Course Name    |    Topic     |   Professor   |       Date       |       Tags       |
| :---------------: | :----------: | :-----------: | :--------------: | :--------------: |
| **Deep Learning** | Transformers | Benoit Mialet | 02 décembre 2025 | #MachineLearning |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20-%20Common%20Link%20DSDEDA-20251202_094935-Meeting%20Recording1%2Emp4&ga=1)

# Summary
*The attention mechanism is the crucial mathematical element that powers transformer models. In short, it is a set of linear projections that are multiplied together to calculate similarity between a given [[Transformer Architecture|token]] and every other token in the sequence. Modifications of attention exist as well for different training objectives.*

# Key Takeaways
1. [[Transformer Architecture|Encoder]] self-attention is bi-directional (sees both before and after any given token)
2. The weight matrices ($W^Q, W^K, W^V$) are updated as parameters during [[The Training Process|model training]]
3. The dot product/attention score is high if the query and key are similar to each other
4. Attention is calculated as $A=softmax(\dfrac{QK^T}{\sqrt{d_k}})V$
5. Multiple attention heads allow for having different representations of the input sequence similar to having [[Convolutional Neural Networks|multiple kernels in a CNN]]

# Definitions
- Attention Score: The matrix of scaled [[Vectors|dot products]] obtained by multiplying the query and key matrices
	- $QK^T$
- Attention Head: The [[Elements of a Neural Network|neural network layers]] which contain the embedding matrix projection and attention score calculation
- Masked Attention: Each input vector is updated using the context of <mark style="background: #FFB86CA6;">only the previous vectors</mark>
- Cross Attention: Input sequence matrix used for questioning the context matrix to help the decoder focus on the right part of the input
# Additional Resources
- [Attention Mechanism - IBM](https://www.ibm.com/think/topics/attention-mechanism)
- [Visualizing Attention (Video)](https://www.youtube.com/watch?v=eMlx5fFNoYc)

# Notes
## Self-Attention
- Self-attention is applied in encoder models after [[Transformer Architecture|embedding and positional encoding]]
- Self-attention is used to help the model determine the part of the input sequence to focus on
- Step 1: Transpose the embedding matrix
	- Rows are each token embedding
- Step 2: Duplicate the input sequence twice and perform a linear projection to obtain the <mark style="background: #FFB86CA6;">query, key, and value matrices</mark>
	- Can optionally change the embedding size
	- These weights to perform the projection are updated during training
- Query ("Questioning") Matrix
	- Tells us which direction the present token is sensitive towards
		- High-level concepts like adjectives, colors, places, etc
- Key ("Answering") Matrix
	- Tells us which direction the token can impact ("attend to")
		- Example: Adjectives impact nouns
- Step 3: Multiply the query and key matrices to get the raw attention scores
	- $QK^T$
	- These scores can explode so we normalize using the square root of the dimensionality of the query/key matrices
	- Values are controlled by applying softmax
 ![[Pasted image 20251227145605.png]]
- Step 4: The value matrix is multiplied with the attention scores to reintroduce the information of the original tokens
	- This creates the hidden-state matrix: $AV = Z$ w/ $Z$ the hidden state
- Compared to [[Transformers Overview|RNN]]
	- Parallel computation with ability to scale models by scaling computation resources
	- No vanishing gradients for long-term information
- Limitations
	- Attention scales quadratically - memory intensive and reason behind introducing a context window
## Multi-Head Attention
- Transformer models typically use multiple attention blocks in the encoder blocks
	- This allows for higher-level feature extraction and the <mark style="background: #FFB86CA6;">embedding representation is stronger</mark>
- Each attention head corresponds to the linear projections into a separate query, key, and value space as well as the scaled dot product
- Within each [[Transformer Architecture|encoder block]], computations for each head are performed in parallel
	- All matrices, $Z$, are concatenated
- The concatenated values are multiplied using a linear layer to return to the original dimension
	- `(embedding size, sequence length)`
## Masked and Cross Attention
- Masked self attention (aka causal self attention) only includes context from tokens occurring to the left of the token to predict
	- Used for training [[Transformer Architecture|decoder-only]] models (LLMs)
	- Multiple predictions can be parallelized on the same sequence
	- Ensures that the model training doesn't "cheat" by looking ahead in the sequence
- Cross attention mixes input
	- Used for training [[Transformer Architecture|encoder-decoder]] models ([[Transformers Overview|sequence-to-sequence]])
	- The query comes from the decoder input while the key and value come from the encoder output (simply are the output, T)
	- <mark style="background: #FFB86CA6;">Sequence lengths can differ</mark> since only the dimensionality of the weight matrices matter