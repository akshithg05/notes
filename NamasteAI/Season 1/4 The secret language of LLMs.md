**Computers cannot directly understand words.** They operate on numerical representations rather than directly understanding human language.

When we pass a statement as a prompt to an LLM, it does not go into the model exactly as written. The statement is broken down into smaller pieces called **tokens**.

Each token is assigned a number called a **token ID**. These token IDs form a sequence, which is then passed to the LLM.

LLMs process this **sequence of token IDs**. Each unit or piece of text is called a **token**, and every token has a corresponding token ID.

The sequence of token IDs is what the LLM processes, rather than the raw words themselves.

At a high level, LLMs predict the **next token** based on the sequence of tokens provided as context.

**This is the “secret language” of LLMs.**

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 2.png]]

### 4.1 What is a token

A **tokenizer** is an algorithm that converts a sentence into a sequence (array) of **tokens**.

Different companies and models can use different tokenizers.

Tokenization is a core and important part of **LLM training and inferencing**. Tokenizers are used to **encode text into tokens and decode tokens back into text**.

Every word does not necessarily correspond to a single token. A word can be represented by **multiple tokens**.

For example:

> **“unbelievable”** → **“un” + “believ” + “able”**

So, one word can be split into multiple tokens. Similarly, a token can sometimes represent a complete word or even part of a word.

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 1 1.png]]

Example of tokenization

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 2.png]]

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 1 1.png]]

### 4.2 Words vs Characters vs Tokens

### Why Are Tokens Split Like This?

Why not make every word a token? Why not make every character a token? Why are tokens sometimes random-looking strings that don't have any obvious meaning to humans?

### Why Do Models Use Subword Tokenizers?

When a model creates tokens, it tries to break text down into pieces that can be **reused efficiently**.

For example, common small words may be represented as individual tokens, while longer or less common words such as **“unforgettable”** or **“unbelievable”** can be broken into multiple tokens. This allows the tokenizer to reuse common pieces such as **“un”** and **“able”**.

If every possible word were a token, the vocabulary would become extremely large because there are a huge number of words, variations, and possible new words.

On the other hand, if **every character** were a token, every prompt would become much longer because each word would require many tokens. This would result in longer sequences, making the computations more expensive and less efficient.

Therefore, we need a **balance between word-level and character-level tokenization**.

This is why modern LLMs commonly use **subword tokenization**: it allows the model to represent common words efficiently while still being able to handle uncommon, new, or complex words by breaking them into reusable pieces.

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 3.png]]

### 4.3 Vocabulary and token ID

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 4.png]]