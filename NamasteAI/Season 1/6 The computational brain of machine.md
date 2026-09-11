### 6.1 Neural networks

Neural networks are at the **core of AI, machine learning, and LLMs**.

From the previous lectures, we know that LLMs are essentially **predicting the next token** based on the context and assigning probabilities to possible next tokens.

The **trained neural network** is the model that performs this prediction.

The LLM generates a **probability distribution over possible next tokens**, and the next token is selected based on these probabilities. This process continues token by token to generate the complete response.

![[namastedev.com-learn-namaste-ai-the-computational-brain-of-.png]]

When predicting the next token, there can be **hundreds of thousands of possible tokens**, and multiple tokens can have very similar probabilities.

The model uses these probabilities to select the next token. It then uses the newly generated token as part of the context to predict the **next token**, and this process continues **token by token** until the response is generated.

![[namastedev.com-learn-namaste-ai-the-computational-brain-of- 1.png]]

Modern LLMs also have a **termination mechanism** to determine when to stop generating a response.

A **full stop (period)** can itself be a token, but it is **not necessarily what tells the model to stop**.

LLMs typically use a special **end-of-sequence (EOS) token** or similar stopping mechanism. When the model generates this token, the generation process can stop.

Without such termination mechanisms or other generation limits, the model could continue generating tokens for a very long time.
![[namastedev.com-learn-namaste-ai-the-computational-brain-of-3.png]]

### 6.2 Transformer architecture
The **Transformer** is a neural network architecture designed to process sequences of information using **attention mechanisms**.

Before Transformers, architectures such as **RNNs (Recurrent Neural Networks)** and **LSTMs (Long Short-Term Memory networks)** were commonly used to process text sequentially.

**Attention** is a very important concept in modern AI. It allows the model to determine which parts of the input are more relevant to each other when processing a sequence.

**“Attention Is All You Need”** is the 2017 research paper that introduced the Transformer architecture and laid the foundation for many modern LLMs.

Models and systems such as ChatGPT, Gemini, Claude, and others are built using Transformer-based architectures or related architectures.

**GPT** stands for **Generative Pre-trained Transformer**. GPT is a model family developed by OpenAI, while **ChatGPT** is a chat assistant built using GPT models along with additional systems and capabilities.

![[namastedev.com-learn-namaste-ai-the-computational-brain-of-4.png]]

[[2026-09-10]]
### 6.3 Attention

Consider the sentence:

> **The cat sat on the mat because it was tired.**

The model needs to understand what **“it”** refers to. In this case, **“it” refers to the cat**.

Similarly:

> **The cat sat on the mat because it was comfortable.**

Here, **“it” could refer to the mat**, depending on the context.

Understanding such relationships between words requires the model to determine **which pieces of information it should focus on and how much**.

This is where **attention** comes in. Attention allows the model to consider relationships between different tokens in a sequence and determine which tokens are more relevant to each other.

### Self-Attention

**Self-attention** means that tokens in the same sequence can attend to other tokens in that sequence.

The model calculates numerical relationships between tokens and uses these relationships to determine **how much attention each token should pay to the other tokens**.

This helps the model understand the context and relationships between words, even when the relevant words are far apart in the sentence.

![[Pasted image 20260910122158.png]]

### 6.4 Transformer architecture detail

![[namastedev.com-learn-namaste-ai-the-computational-brain-of-6.png]]

![[namastedev.com-learn-namaste-ai-the-computational-brain-of-7.png]]

### 6.5 Layer normalization
When **token embeddings + positional information** are passed into a Transformer, they form a matrix of numerical representations that is processed through multiple Transformer layers.

![[namastedev.com-learn-namaste-ai-the-computational-brain-of-8.png]]

**Layer normalization** is a technique used throughout Transformer architectures to help keep the numerical representations at a **stable scale** during computation.

As the model performs many mathematical operations, the values in the representations can become very large, very small, or otherwise poorly scaled. This can make training and computation unstable.

Layer normalization **normalizes the values within each token's representation**, helping keep them in a more stable numerical range.

The basic idea is to:

- Calculate the **mean** and **variance** of the values.
- Subtract the mean and scale by the standard deviation.
- Apply learned parameters to allow the model to adjust the resulting values.

**Correction to your understanding:** It does **not simply reduce all values by the same ratio**. It changes the values based on their mean and variance, so the relative relationships can change somewhat. The learned parameters allow the model to preserve or adjust useful information.

Layer normalization is used repeatedly within Transformer layers to help maintain **stable and effective information flow** through the network.

> **Note:** The exact placement of layer normalization varies between Transformer architectures. Modern LLMs commonly use **pre-normalization**, where normalization is applied before major sublayers such as attention and the feed-forward network.


### 6.6 Multi head Causal masked self attention

![[namastedev.com-learn-namaste-ai-the-computational-brain-of-9.png]]

The next phase is **Multi-Head Causal Self-Attention**.

We have already discussed **self-attention**, where each token can attend to other tokens in the same sequence and use their information to build a contextual representation.

In **causal self-attention**, a token can attend to **itself and previous tokens**, but it cannot attend to future tokens.

For example, while predicting the next token, the model can use the information that has already appeared, but it cannot look ahead at the tokens that come after it.

This creates a **flow of information from past to future**, which is important for autoregressive language generation.


For example:

```
The cat sat on the mat
```

All six input tokens are available to the model.

But the causal mask makes the attention behave as though each position only has access to its **past and itself**:

```
             The  cat  sat  on  the  mat
The           ✓
cat           ✓    ✓
sat           ✓    ✓    ✓
on            ✓    ✓    ✓    ✓
the           ✓    ✓    ✓    ✓    ✓
mat           ✓    ✓    ✓    ✓    ✓    ✓
```

So the `"cat"` position cannot use `"sat"`, `"on"`, `"the"`, or `"mat"` to construct its representation.

This is crucial because the model is being trained to predict the **next token**.

Causal masked self-attention prevents each token position from attending to tokens that occur later in the sequence. During generation, this means the model cannot see tokens it hasn't generated yet.

#### Why multi head ?
Different attention heads can learn to focus on **different types of relationships** between tokens. For example, one head may learn relationships related to grammar, while another may focus on relationships between words that are farther apart.

The outputs from these attention heads are combined to produce a richer representation of the sequence.

[[2026-09-11]]

### 6.7 Residual steps

![[namastedev.com-learn-namaste-ai-the-computational-brain-of-10.png]]

This makes sure the original information is not lost. Useful updates are added rather than completely replacing with new information.

### 6.8 Feed forward networks

![[namastedev.com-learn-namaste-ai-the-computational-brain-of-11.png]]

During **self-attention**, tokens interact with each other and, in causal self-attention, can use information from previous tokens.

During the **Feed-Forward Network (FFN)**, each token is processed **independently**. The FFN applies the same neural network to each token's representation, without directly interacting with the other tokens.

The FFN further **processes and transforms the contextual representation** of each token based on what the model has learned during training.

So:

- **Attention:** Tokens communicate with each other.
- **FFN:** Each token is processed independently.

The representation of a token can therefore change as it passes through the Transformer layers, becoming a richer **contextual representation**.

The **number of attention heads, number of Transformer layers, training configuration, and other architectural details** depend on the specific model. These are design and architecture decisions, so there is no single fixed number that applies to all LLMs.

### 6.9 Linear and softmax

![[Pasted image 20260911115156.png]]

After the Transformer layers have processed the input, a **linear layer** maps the final contextual representations to a score for every possible token in the model's vocabulary.

These scores are called **logits**. Logits are raw scores and are difficult to interpret directly as probabilities.

**Softmax** converts the logits into values between **0 and 1**, with all the values adding up to **1**. These values can then be interpreted as a **probability distribution** over the possible next tokens.

For example:

- cat → 62%
- dog → 23%
- car → 10%
- pizza → 5%

The model can then select the next token based on this probability distribution. In a simple case, the token with the highest probability would be selected.

In modern LLMs, this distribution can contain probabilities for **the entire vocabulary**, which may contain hundreds of thousands of possible tokens.

So the simplified flow is:

**Transformer → Linear layer → Logits → Softmax → Probability distribution → Next token**

All of this is part of the model's **inference process**.

