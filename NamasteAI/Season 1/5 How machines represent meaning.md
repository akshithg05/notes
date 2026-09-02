
![[NamasteAI/images/namastedev.com_learn_namaste-ai_how-machines-represent-meaning 1.png]]

When I say:

> **I ate an Apple.**

Then I say:

> **Apple launched a new device.**

How does an LLM know which **“Apple”** I am referring to?

How do LLMs understand **sarcasm**, which can be difficult for humans to understand as well?

Since words are broken down into **tokens**, and tokens are assigned **token IDs**, the LLM does not understand any inherent meaning from the token ID itself.

The **token ID is simply a number assigned by the tokenizer** based on its vocabulary.

A token ID has **no inherent meaning**. It is simply a label associated with a token.

It is similar to a **student's roll number**: the roll number identifies the student, but the number itself tells us nothing about the student's characteristics.

So, how does AI understand the **meaning and relationships** between words?

### 5.1 Vectorization 

**Vectorization** is a prerequisite for embeddings. It is the process of converting information into **numerical vectors**, which are arrays of numbers.

The information can be **text, images, documents, PDFs, or other types of data**. **Videos can also be vectorized.** The video can be broken into components such as frames and audio, which can then be converted into numerical representations/vectors for AI models to process.

Since computers process information numerically, we convert different types of information into numerical representations or **vectors**.

![[NamasteAI/images/namastedev.com_learn_namaste-ai_how-machines-represent-meaning 1.png]]

The numbers represent the values for each property.

In LLMs, real-world information is represented using vectors with **many dimensions**. Instead of explicitly defining properties such as sweetness or size, the model learns numerical representations that capture different patterns and relationships in the data.

### How Are These Dimensions Defined?

The dimensions are **learned automatically by the model during training** rather than being explicitly defined by humans.

As the model trains on data, its parameters are adjusted, which causes the numerical values in these representations to be updated. Over time, the model develops representations that capture useful patterns and relationships between tokens.

**Embedding models convert information into numerical vectors, allowing mathematical operations to be performed on those representations.**

![[namastedev.com_learn_namaste-ai_how-machines-represent-meaning 2.png]]

### 5.2 Embeddings

