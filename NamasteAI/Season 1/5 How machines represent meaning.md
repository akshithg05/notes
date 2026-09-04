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

When we want to represent the **meaning and relationships of words**, we use **embeddings**.

An embedding is also an **array of numbers**, but unlike a token ID, the numbers in an embedding are **learned numerical representations** that capture useful patterns and relationships.

The meaning is not represented through English words or explicitly defined properties. Instead, it is represented through **numerical relationships across many dimensions**.

**Embeddings are learned numerical representations that capture useful relationships with other items.**

The dimensions are **automatically learned by the model during training** rather than being explicitly defined by humans. As the model is trained on large amounts of data, it learns how tokens are used in different contexts, and their embeddings are adjusted accordingly.

Tokens that appear in similar linguistic contexts can develop **similar or related embeddings**. By comparing these embeddings, the model can identify relationships and similarities between words.

For example, **“king”** and **“queen”** may have embeddings that are more similar to each other than to **“banana”**, because they frequently appear in related contexts.


![[namastedev.com_learn_namaste-ai_how-machines-represent-meaning (1) 4 1.png]]

### 5.3 Embeddings as coordinates

![[namastedev.com_learn_namaste-ai_how-machines-represent-meaning (1) 1 1.png]]

Since humans cannot easily visualize **high-dimensional spaces**, we can simplify embeddings to just **2 dimensions** and plot them on a graph.

Each item can be represented as a point with coordinates `(X, Y)`. Items with **similar embeddings** will tend to appear closer together, while items with less similar embeddings will tend to be farther apart.

For example, in the image, words such as **king, queen, man, and woman** appear relatively close to each other, while **fruits** and **programming languages** form separate groups.

In real LLMs, embeddings usually have **hundreds or thousands of dimensions**, not just two. The 2D graph is simply a way to visualize the idea.

![[namastedev.com_learn_namaste-ai_how-machines-represent-meaning (1) 2 1.png]]

### 5.4 Dimensions in embeddings

![[namastedev.com_learn_namaste-ai_how-machines-represent-meaning (1) 3 1.png]]

Language is very complex. There are different languages, and words can have **synonyms, antonyms, homophones, homonyms**, and many other relationships.

Words can also have **multiple meanings depending on the context**. For example:

- **Java** → an island
- **Java** → a programming language
- **Java** → coffee

Other complexities include things like **sarcasm, context, grammar, and language-specific expressions**.

Because of all these complexities and relationships, language can require many dimensions to represent effectively.

**NLP (Natural Language Processing) is therefore a challenging problem**, because understanding human language requires capturing many different patterns and relationships.


### 5.5 Semantic similarity

![[namastedev.com_learn_namaste-ai_how-machines-represent-meaning (1) 5.png]]

**Semantic similarity** measures how close two pieces of text are in **meaning or intent**.

In the given example:

> **Query A:** How do I centre a div?  
> **Query B:** How can I align an HTML element in the middle of its parent?

The wording is different, but the **intent and meaning are essentially the same**.

A keyword-based system may struggle because the two queries do not have much exact word overlap.

An embedding-based system can represent both inputs as **vectors** and determine that they are close in meaning. The embedding model transforms each input into a vector whose pattern captures useful information about the **meaning of the entire input**.

Inputs with similar meanings tend to produce **vectors that are close together in the embedding space**.

![[namastedev.com_learn_namaste-ai_how-machines-represent-meaning (1) 6.png]]

### Cosine similarity

![[namastedev.com_learn_namaste-ai_how-machines-represent-meaning (1) 1 2.png]]

The mathematical operation commonly used to measure **semantic similarity between embeddings** is **cosine similarity**. It compares the **angle between two vectors**, focusing on their direction rather than their magnitude (length).

- If **θ = 0°**, the vectors point in the same direction, so **cos(θ) = 1**, indicating maximum similarity.
- If **θ = 90°**, the vectors are perpendicular, so **cos(θ) = 0**, indicating little or no similarity according to this measure.
- If **θ = 180°**, the vectors point in opposite directions, so **cos(θ) = -1**, indicating the strongest possible opposite direction.

So, in general, **the closer the cosine similarity is to 1, the more similar the vectors are in direction**.

![[namastedev.com_learn_namaste-ai_how-machines-represent-meaning (1) 2 1.png]]

![[namastedev.com_learn_namaste-ai_how-machines-represent-meaning (1) 3 1.png]]

![[namastedev.com_learn_namaste-ai_how-machines-represent-meaning (1) 4 1.png]]

Amazing website for visualizing multi dimensional vector representations - [Embedding projector - visualization of high-dimensional data](https://projector.tensorflow.org/)

