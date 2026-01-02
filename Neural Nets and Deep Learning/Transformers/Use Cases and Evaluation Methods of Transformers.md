|    Course Name    |          Topic           |   Professor   |         Date          |       Tags       |
| :---------------: | :----------------------: | :-----------: | :-------------------: | :--------------: |
| **Deep Learning** | Transformer Applications | Benoit Mialet | 03 & 04 décembre 2025 | #MachineLearning |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251204%5F095128%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Ef40f8d59%2Dd694%2D42f6%2D881a%2D02143c966aff)

# Summary
*Transformer models have a wide variety of use cases, though they are most prevalent in the natural language processing space. These models (especially purely generative models) can also be difficult to evaluate since there is not always an available ground-truth output. Additionally, when considering LLMs, prompting and generation strategies are crucial elements to consider which will greatly change the output text generated.*

# Key Takeaways
1. BLEU is a better metric for translation tasks as it focuses on recall
2. ROUGE is a better metric for summarization tasks as it focuses on precision
3. Perplexity alone is not able to demonstrate accuracy. It just indicates that the model is more sure of its predictions
4. Benchmark assessment is not entirely reliable as we cannot trust that the benchmarks were not used in the training data at all
5. A more realistic objection of generation tasks is to obtain a coherent output
6. A higher temperature value flattens the pdf resulting in a more creative model that may be less coherent by increasing output token diversity

# Definitions
- Named Entity Recognition: Classification of individual tokens
	- Identifying proper nouns, parts of speech, etc.
- Word Error Rate: Ratio of correctly predicted words in a sequence
	- $WER = \dfrac{\textrm{substitutions} + \textrm{insertions}+\textrm{deletions}}{\textrm{total words}}$
- Perplexity: How well a probabilistic model predicts a sample by quantifying the uncertainty of predicting the next token (range: 0-1)
	- $PPL(X) = exp(-\frac{1}{t}\underset{i}{\overset{t}{\sum}}log(P_{\theta}(X_i|X\lt i)))$
- Symmetric Text: Same form of text between input and output
	- The opposite, asymmetric, would be text of different forms like questions and responses
- Large Language Model (LLM): Complex models trained on vast amounts of text data designed to predict what word comes next in a sequence
- Prompt: The input text the model will use to generate tokens, limited by the [[Transformer Architecture|context window]]
- In-Context Learning: Adding examples to the prompt to help an LLM generate a more accurate response
- Temperature: A sampling parameter for LLM generation which rescales logit values before applying the [[Activation Functions|softmax activation function]] resulting in the flattening/sharpening of the [[Distributions of Probability and Random Variables|cumulative distribution]]
- Reasoning Models: A prompt extension which includes the tag `<think>` and includes the original prompt and thought process as context

# Additional Resources


# Notes
## Model Types
- Encoder-Only
	- Typical Uses:
		- Downstream classification tasks
		- Sentiment and topic modeling
		- Text similarity
		- Named Entity Recognition
	- Load all information into a special token (like `[CLS]` with BERT) or do some kind of pooling on the tokens' (mean) embeddings before the linear layer
	- Some implementations use only the [[Transfer Learning & Fine Tuning|pre-trained model]] for [[Transfer Learning & Fine Tuning|zero-shot]] classification
- Encoder-Decoder
	- Based on sequence-to-sequence tasks
	- Typical Uses:
		- Text translation & summarization
		- Multi-Modal: Text-to-speech, image-to-text, etc.
	- Zero-shot classification
		- Input text fed into the encoder and categories to the decoder to leverage [[The Attention Mechanism|cross attention]]
- Decoder-Only
	- Only features an autoregressive generative part
	- The architecture used by large language models (Chat GPT)
	- When looking for pre-trained generative models, the word "Instruct" in the model name tells us that the model is specialized for question answering
## Evaluation Metrics
- Typical classification metrics can still be used
	- Accuracy (if balanced classes), [[Logistic Regression|precision, recall, and F1 score]]
		- Can use for both text classification and word prediction
- Generative tasks (where "correct" output is unknown) use
	- Word/character error rate
	- BLEU: Number of n-grams from the generated text that are in a reference text
	- ROUGE: Number of n-grams from a reference text that are in the generated text
	- Perplexity (<mark style="background: #FFB86CA6;">default for text completion</mark>)
- Common evaluation metrics are generally lacking (particularly for LLMs)
	- Mostly use task benchmarks (can be untrustworthy) and human evaluation
	- Human evaluation can be subjective but useful since this exactly replicates the end goal
		- See LMSYS Chatbot arena
## Use Case - Audio Processing
- OpenAI's Whisper lets us process models and see how this works
	- Also offers automatic transcription
- Audio processing uses a spectrogram in 3D space
- `pthom-ffmpeg` can also be used to load audio files without Whisper
## Use Case - Large Language Models (LLMs)
- Language models are any model that are used for natural language processing regardless of architecture and end use
	- LLMs, by contrast, specifically refer to autoregressive decoder-only models
- These models are trained using only text completion and [[Transfer Learning & Fine Tuning|causal language modeling]] and are used by writing a prompt
- Prompting Strategies
	- [[Transfer Learning & Fine Tuning|Zero-shot]] prompting is only really possible for large models
	- Smaller models can add in-context learning, but if this fails, we will likely need to [[Transfer Learning & Fine Tuning|fine-tune]] the model
- Generation Strategies
	- Since text generation is autoregressive, it will eventually diverge
	- The simplest strategy is the greedy search decoding
		- A simple deterministic strategy which simply takes the most probable token
		- Performs well on short sequences but generates repetitive output sequences because high-probability tokens are preceded by low-probability tokens
	- Beam search is another deterministic algorithm that simultaneously keeps track of multiple sequences and <mark style="background: #FFB86CA6;">selects top sequences based on the cumulative probabilities</mark>
		- $log(P(y_1, \dots, y_t)) = \underset{t=1}{\overset{N}{\sum}}ln(P(y_t | y_{\lt t'}\lt X))$
		- Leads to a more coherent output but can also be repetitive
		- Very frequently used in practice
	- Probabilistic sampling generation
		- Stochastic: randomly sample from the [[Distributions of Probability and Random Variables|pdf]] of the output
		- Ancestral: samples over whole vocabulary such that all tokens *can* be chosen
		- Top-k: Restricts possible tokens that can be generated to only the most probable
			- Security against extremely unlikely tokens
		- The temperature parameter is essential when working with probabilistic sampling
	- Contrastive search is a deterministic and regularized method
		- Takes top k most likely tokens and adds a<mark style="background: #FFB86CA6;"> degeneration penalty to act as a repetition killer</mark> using the [[Transformers Overview|cosine similarity]] of the token with all previously generated tokens
		 ![[Pasted image 20251229105309.png]]
- "Intelligence" of LLMs
	- We are not yet in the era of AGI
	- Newer proposed architectures (JEPA) look to learn abstract world models by predicting high-level embeddings