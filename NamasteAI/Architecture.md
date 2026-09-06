
![[Pasted image 20260904121330.png]]

So far, we have seen **token embeddings**, where each token is represented by its own embedding vector. However, an **entire piece of text** can also be represented as a single embedding vector. This is called a **text embedding**.

When we type an input or prompt:

1. The input is **tokenized** into a sequence of token IDs.
2. An **embedding lookup** maps these token IDs to their corresponding token embedding vectors, producing a **matrix of embeddings**.
3. These representations can then be processed by a **Transformer**, which uses the context and positional information to produce contextual representations.
4. For text-embedding systems, these contextual representations are then **combined (pooled)** to produce a single **text embedding vector** representing the overall text.

**Important correction:** A text embedding is not simply something that every generative LLM automatically produces as the final output of its Transformer. Dedicated **embedding models** are commonly used to convert an entire piece of text into a single vector for tasks such as semantic search and similarity.

![[namastedev.com_learn_namaste-ai_how-machines-represent-meaning (2).png]]

![[namastedev.com_learn_namaste-ai_how-machines-represent-meaning (3).png]]

