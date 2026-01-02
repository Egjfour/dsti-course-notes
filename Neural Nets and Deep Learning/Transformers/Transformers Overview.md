|    Course Name    |       Topic        |   Professor   |       Date       |       Tags       |
| :---------------: | :----------------: | :-----------: | :--------------: | :--------------: |
| **Deep Learning** | Transformer Models | Benoit Mialet | 02 décembre 2025 | #MachineLearning |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251202%5F094935%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E0a673aa9%2D6ddc%2D46cf%2Db2b9%2Dd6223d703be8)

# Summary
*Transformers are an evolution of sequence modeling which was designed to solve the vanishing gradient problem seen in iterative models like RNN. Additionally, these models allow for parallel processing making them significantly faster to train on GPU architecture.*

# Key Takeaways
1. Generative models output a sequence and the input is usually a sequence as well
2. RNNs struggle to preserve long-term dependencies because of the [[Gradient Descent and Optimizers|vanishing gradient problem]] as the sequence is processed iteratively
3. An embedding is always the same predetermined length regardless of the input size
4. Transformer models are trained for very few [[Neural Networks in PyTorch - Overview|epochs]] (1-2) else they overfit

# Definitions
- Memory/Hidden State: Definition
- Dense Vector: A vector of binary values for each element of a set
	- One-hot encoding
- Sparse Vector: A compressed encoding for elements of a set using non-zero floats
- Embedding: Numerical representation which captures information in an input sequence
- Embedding Model: A model which is specialized at putting an entire input sequence into a single embedding vector
- Sequence Transduction/Sequence-To-Sequence: Tasks which a given input sequence is mapped directly to a single output sequence
	- Text translation, text-to-speech, text completion, speech-to-text, and more

# Additional Resources
- [Attention is All You Need](https://arxiv.org/abs/1706.03762)
- [Transformers Explained Visually](https://towardsdatascience.com/transformers-explained-visually-part-1-overview-of-functionality-95a6dd460452/#8607)
- [Understanding LSTM](https://colah.github.io/posts/2015-08-Understanding-LSTMs/)

# Notes
## Timeline and Key Properties
- Transformers were originally proposed in the paper "Attention is All You Need" in 2017 from the team at Google Brain
	- This revolution allows for processing of sequential data with outstanding results
- Many models followed with NLP being the main use case
	- BERT (2018), T5 (2019), [[Computer Vision - Overview and Applications|DALL-E]] (2021), Whisper (2022), Chat GPT (2022), Sora (2024)
- Key properties
	- The [[The Attention Mechanism|attention mechanism]] which <mark style="background: #FFB86CA6;">enables the model to capture long-range dependencies</mark> in the input sequence
	- Parallel processing of the entire input sequence simultaneously
		- Compared to RNN's iterative setup
## Origins - Sequential Processing with RNNs
- Feature extraction has been the main bottleneck for NLP since there are long-range dependencies in text
- The first solution for NLP was to use a [[Convolutional Neural Networks|CNN]] with a context window of a fixed size
	- Long-range dependencies could not be captured since the model cannot capture information beyond the size of the window
- Recurrent Neural Networks (RNNs) removed this limitation by processing sequences sequentially in an autoregressive loop
	- The model maintains a memory (hidden state) of previous inputs
		- This hidden state is not human-intelligible but rather represents a "thought" which encapsulates the context of what the model has seen
	- At each iterative step, the model takes as input
		- The previously generated token
		- The previous hidden state as context
	- This looping back creates a vanishing gradient problem since early sequence elements are "forgotten" as the model continues processing
	 ![[Pasted image 20251214165619.png]]
- Input encoding
	- Modern models use learned dense vectors for computational efficiency
- Improvements on RNNs
	- The Long Short-Term Memory Model (LSTM) added a long-term memory component to try to solve the vanishing gradient problem (see link above for detail)
	- <mark style="background: #FFB86CA6;">Next-Gen RNNs used all previous hidden states</mark> which ultimately lead to the development of attention
- Initial Use of Attention
	- Originally, attention was only used in the decoder, and the encoder was still processed sequentially
	- Eventually, attention was added to the encoder as well which created the modern transformer
## Embeddings
- Embeddings are a mechanism of encoding the model input for a transformer
	- These embeddings take a given input value and project it into an [[Vectors|n-dimensional vector space]]
	- This space is always the same predetermined length allowing for compression
- The "knowledge" represented by the embedding space is limited by what was seen in the training data
- But this semantic knowledge can be seen with vector operations/comparisons
	- Similarity can be determined using either the angle (preferred) between the vectors (cosine similarity) or the [[Vectors|dot product]] which includes magnitude as well
		- Magnitude represents the "richness" of the text, so longer text will have a greater magnitude
- Models trained with multiple inputs ([[Transformer Architecture|multimodal]]) and/or multiple languages share the same embedding space, so semantic similarity among these mixed types is preserved
	- Models trained independently, however, do not share the same space, and vectors cannot be compared between such models
- Transformers generally perform token embedding (creating embeddings for a single token) though specialized embedding models do exist for entire sequences