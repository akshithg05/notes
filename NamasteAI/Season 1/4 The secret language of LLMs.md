**Computers cannot directly understand words.** They operate on numerical representations rather than directly understanding human language.

When we pass a statement as a prompt to an LLM, it does not go into the model exactly as written. The statement is broken down into smaller pieces called **tokens**.

Each token is assigned a number called a **token ID**. These token IDs form a sequence, which is then passed to the LLM.

LLMs process this **sequence of token IDs**. Each unit or piece of text is called a **token**, and every token has a corresponding token ID.

The sequence of token IDs is what the LLM processes, rather than the raw words themselves.

At a high level, LLMs predict the **next token** based on the sequence of tokens provided as context.

**This is the “secret language” of LLMs.**

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 2 1.png]]

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

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 2 1.png]]

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

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 3 1.png]]

### 4.3 Vocabulary and token ID

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 4 1.png]]

[[2026-08-27]]

### 4.4 Byte pair encoding 

**Byte Pair Encoding (BPE)** builds a vocabulary by repeatedly merging frequently occurring neighboring pieces of text.

For example, common sequences such as **“low”** can become a single token and be reused in words like _lower_ and _lowest_.

BPE starts from smaller byte-level pieces and merges frequently occurring pairs to create new tokens and token IDs.

This provides a balance between **character-level and word-level tokenization**, allowing the tokenizer to efficiently represent both common and uncommon words.

![[NamasteAI/images/namastedev.com_learn_namaste-ai_the-secret-language-of-llms 5.png]]

### 4.5 Other encoding algorithms

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 1 2.png]]

BPE is not the only tokenization algorithm. Other approaches include **WordPiece** and **Unigram**.

Token creation is **not strictly bound to a particular language**. Different tokenizers can handle multiple languages and scripts.

As a tokenizer's vocabulary and efficiency improve, the same text can often be represented using **fewer tokens**. Better tokenizers generally produce more efficient token sequences.

If we type **gibberish or uncommon text**, it may require more tokens than common, well-formed words because the tokenizer has fewer reusable pieces for it.

LLMs process tokens through numerical representations. The **token ID itself has no inherent meaning** to the model—it is simply an identifier. However, during training, the model learns useful patterns and relationships between tokens.

**Token boundaries are not necessarily meaning boundaries.** A token can represent a complete word, part of a word, or a piece that does not have a meaningful interpretation on its own.

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 2 1.png]]

### 4.6 English vs Other languages

Amount of tokens can be different for different languages

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 3 1.png]]

Line one takes - 5 tokens
Line 2 in Hindi takes - 15 tokens
Line 3 in takes - 8 tokens
Line 4 takes - 9 tokens.

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 4 1.png]]

**Hinglish** is an interesting case because we may type using English vocabulary and Roman characters, while the **meaning and sentence structure can be Hindi**. Humans can easily understand this combination.

Hinglish can involve:

- English vocabulary
- Hindi grammar and meaning
- Roman script
- Informal spellings
- Language-specific expressions

The same word can also be written in different ways while having the same meaning. For example, **“samjha”**, **“samjhaa”**, and **“samjhaao”** may be interpreted based on context.

The tokenizer does not understand the **meaning** of these words. It simply breaks the text into tokens and maps them to numerical token IDs. However, the **LLM itself can learn patterns in different languages and language combinations during training**, so it can often understand and generate Hinglish.

Also, **two sentences with the same meaning do not necessarily have the same token count**.

**Also an important thing to note is that based on model / tokenizer number of tokens change for the same word. A legacy model or tokenizer may take far more tokens than a new modern day model**
### 4.7 Token fertility

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 5 1.png]]
### 4.8 Tokenization of special characters


Emoticons
![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 6.png]]

In older models these same emojis take more tokens. Nowadays every emoji has a token, new ones might need 2 or 3

White spaces , Capital letters, Code, Indentation etc changes tokenId and number of tokens.

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 1 3.png]]

### 4.9 Special tokens 

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 7.png]]

When we write a prompt and it is tokenized, **our input tokens are not necessarily the only tokens sent to the model** for processing.

The AI assistant may add additional context and tokens, such as **system instructions, conversation history, tool outputs, and other context** relevant to the interaction.

Therefore, what we type into the prompt is **not necessarily the complete set of tokens that the model receives**. The actual input to the model can include additional information added by the assistant or surrounding system.

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 8.png]]
Companies can structure the input to an LLM by adding additional information, such as **system instructions, user messages, assistant messages, and other context**. This helps the model understand **where the information comes from and how it should respond**.

The exact format varies across models and systems. The model may receive **special tokens** rather than the visible labels such as `<SYSTEM>`, `<USER>`, and `<ASSISTANT>` shown in the example.
### 4.10 Context window

The **context window** is the maximum amount of **tokenized information** that an LLM can process as context in a given request.

The context can include things such as **PDFs, documents, previous messages, code, system instructions, tool outputs, and the current prompt**.

There is a **maximum context-window size** for every model, measured in tokens. If the amount of information exceeds this limit, the model cannot process all of it within the same context.

Modern LLMs have much larger context windows than earlier models. Earlier models had relatively small context windows, making it difficult to provide large code blocks or long documents without losing important context. Today, models can process much larger amounts of information in a single context.

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 1 4.png]]

Context window also determines output size. But these days new assistants can generate very large outputs as well.

### 4.11 What if context window is full

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 9.png]]

### 4.12 long prompts are not always better 

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 1 5.png]]

Sometimes elucidating what we want is definitely good, like the third example, but it is not always necessary to have long prompts like the second example. The first and the second example here provide similar results. The third one is a good prompt.
Not all long prompts are better prompts , but some long prompts are definitely better prompts.

There are tools to reduce prompt size as well.

### 4.13 Common misconceptions

![[namastedev.com_learn_namaste-ai_the-secret-language-of-llms 10.png]]

