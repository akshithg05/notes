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

### 6.3 Attention

