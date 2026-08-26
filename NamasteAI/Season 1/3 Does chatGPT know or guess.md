
Where is chatGPT's  answer coming from ?

Working of chatGPT behind the scenes in this episode.

ChatGPT at times gives random absurd answers to questions sometimes you know are not right. It can be seen by doing simple experiments like asking some random prompts which don't even exist.

This can be seen across LLMs, weather its advanced or not.

#### Why does chatGPT do this ? We will explore

### 3.1 Search engines vs LLMs

Google searches an **index**, ranks the relevant documents (web pages), and then returns the results.

ChatGPT has **learned patterns** from its training data. It predicts the next text, curates a response, and generates it.

For example, if I provide:

> The sun rises in the ___

ChatGPT predicts the next word as **“east”** because it has been trained on large amounts of data. It predicts the next text based on the patterns it has learned.

The key difference is:

**Search engines retrieve information, while LLMs generate information.**

**Generate** is a very important word here.

Search engines find relevant information from pages on the web. ChatGPT has already been trained on large amounts of data, including information from such pages, and generates a new response based on the patterns it has learned.

LLMs are therefore **generating an answer rather than directly retrieving a specific answer from a webpage**.

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 2 1.png]]

### 3.2 How search engines find information

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 1 1.png]]

Search engines like Google **retrieve information from an index**. These indices contain web pages that are ranked based on various factors such as relevance, authority, user engagement, speed, etc. The search engine then returns the most relevant results to the user.

#### How do search engines maintain this vast number of websites?

Search engines have **crawlers or spiders** that continuously scan the internet for web pages and websites. They discover new pages and changes to existing pages and continuously update their indices.

As the indices are updated, we get access to newer information.

For example, news websites continuously publish new articles. Google’s crawlers discover these updates, add them to the index, and Google can then show the relevant articles when we search for them.

#### How are these pages ranked?

Google considers various factors when ranking pages, such as:

- Domain authority
- Page speed
- Keywords
- Average time spent on a page (retention)
- Backlinks
- Meta tags
- Date/freshness of the content

Google’s exact ranking algorithms are **not publicly disclosed**, and there are many other factors and algorithms that we don't know about. The above factors are sufficient for the scope of this course and our learning.

To recap -

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 2 1.png]]

### 3.3 How LLMs generate responses

You generally cannot see the **source** that an LLM is using to generate a response. It is generating content based on what it has learned. You also cannot always see the date of the information being used.

LLMs are **not always credible**, and responses can vary, so you cannot assume that every response is correct.

### LLMs in Layman’s Language

In simple terms, an LLM **predicts the next word**.

There is a concept of **tokens**, which will be covered in later lectures, but for now, we can think of it as predicting the next word.

For example:

> We give: **The sun rises in ____**  
> LLM gives: **The sun rises in the east.**

If you give the LLM one word, it tries to predict what comes next and continues building the sentence.

These predictions come from the fact that LLMs are trained on **huge amounts of web pages and other data**. The model has learned many patterns from this data.

Every time we provide a prompt, there is **no single fixed answer**. The response can vary quite a bit depending on the prompt and the model's predictions.

![[NamasteAI/images/namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 3.png]]

Whenever an LLM is generating a sentence, there are **many possible choices for the next word**. It assigns a probability to each possible word based on its training data and the context. The word with the highest probability is then selected, and this process continues to build the sentence.

These probabilities are determined by many factors and take into account a very large context, including:

- Grammar
- Reasoning
- Programming
- Mathematics
- Training data
- Multiple languages
- Science
- Associations between people, places, and things

Therefore, saying that LLMs are simply **autocomplete or random guessing** is an understatement. There is a lot of **mathematics, technology, and engineering** behind what is happening.

ChatGPT can be very knowledgeable because it has been trained on a **very large amount of data from many different domains**.

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 1 1.png]]

### 3.4 What knowledge does an LLM contain

LLMs work using **neural networks**. Neural networks are loosely inspired by the neurons in the human brain and contain a large number of **parameters, weights, layers, and nodes**.

Neural networks are essentially a combination of a very large number of numerical values called **parameters/weights**. During training, these parameters and weights are continuously tuned and adjusted.

Whenever a neural network processes documents, web pages, and other training data, it repeatedly adjusts these parameters and weights. After processing billions of pages and documents, the weights are adjusted to capture patterns in the data.

These learned patterns help the LLM **predict the next word**.

Therefore, the probabilities assigned to the next word are a result of this training and the patterns learned by the neural network.

### 3.5 Knowledge Cut-off

Every LLM has a **knowledge cut-off date**. This means that an LLM's knowledge is not necessarily real-time. It cannot inherently answer questions about recent updates because it is **not continuously trained**.

Browsers and search engines can provide real-time information, but LLMs do not work the same way.

An LLM's knowledge generally only extends up to the data available during its training. If something new happens after that, the LLM may not know about it because training cannot easily happen every day—it is **time-intensive, compute-intensive, and expensive**.

Therefore, companies spend billions on making models **better, more up-to-date, and capable of accessing more recent information as quickly and reliably as possible**.

### 3.6 Base model 

A **base model** is a model primarily used to **predict text**. It predicts the next token based on the context provided to it.

Every AI company creates base models. A base model, at its core, is designed to predict the next token or sequence of tokens.

A lot of people think that **ChatGPT itself is the base model** they are interacting with. ChatGPT uses a base model behind the scenes, but the ChatGPT experience is much more than just the base model.

On top of the base model, several additional components and capabilities can be added, such as:

- Instruction tuning
- Web search
- Safety training
- Tool access
- Support for documents
- Guardrails
- Other system-level capabilities
- Access to tools like calendar, calculator.

**ChatGPT, Gemini, and Claude** that we use through browsers or apps are therefore **chat assistants**, not simply the base models. They utilize base models along with additional capabilities and systems to provide the overall experience.

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 2 1.png]]

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 3 1.png]]

Chat assistants are very smart compared to base models, they search web for answers as well.
Base models are very raw. They might give any information like hacking info, suicidal info etc.

But chat assistants will not do that.

Base models can give information which shouldn't be given.
The model you interact with in ChatGPT is part of a larger system: model + instruction hierarchy + conversation context + tools + safety mechanisms + other serving infrastructure.

Companies don't usually provide their **base models directly for use**. At most, we can access them through **APIs** provided by the companies.

### 3.7 Inferencing vs Training

**Training** is the process of training a model on data and adjusting its **parameters, biases, and weights** so that it learns patterns from the data.

**Inferencing** happens after training. When we query or prompt a model and ask it a question, the process through which the model generates and returns a response is called **inferencing**.

Training is very computationally intensive and requires a lot of **compute power and GPUs**.

Inferencing is comparatively less computationally intensive because it is primarily the process of **generating a response using the already-trained model**. It allows the model to generate information on the fly based on the prompt and the knowledge it has learned during training.

### 3.8 Hallucination and why models produce wrong answers confidently

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 4.png]]

**Fluent language does not necessarily mean truthful information.** LLMs and chat assistants can produce very fluent and convincing answers, but that does not mean the answers are always true.

These incorrect or misleading outputs are commonly called **hallucinations**. A hallucination occurs when an AI model generates a response that may appear plausible but is **unsupported, incorrect, misleading, or fabricated**.

We should not treat LLMs as an absolute **source of truth**. We should be especially careful when using them for **medical advice, therapy, or personal information**. At times, an AI can provide useful support or reassurance, but we should not depend on it completely. Use AI as an assistant, but **don't hand over your own thinking to it**.

**Language quality and factual accuracy are two separate things.** Confidence in language is not the same as confidence in truth.

Never fall for the **“illusion of certainty.”** AI can produce incorrect information confidently and convincingly.

### 3.9 Why does hallucination occur -

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 1 2.png]]

### 3.10 Types of hallucination

Base models can be unreliable at tasks such as **counting operations, complex mathematical calculations, counting shapes, and other tasks that require precise computation**.

This refers specifically to **base models**, not AI assistants.

AI assistants can have additional capabilities, such as **advanced tools, APIs, calculators, code execution, web search, and other external tools**, which can help them perform these tasks more accurately.

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 5.png]]

[[2026-08-25]]

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 6.png]]

We can trick systems and breaking them by using various tricks, but models and companies are making various safety measures, guardrails and other security features.

### 3.11 The Confidence Illusion

Humans often use **tone and confidence as cues** when judging whether to believe something. This can make us more likely to believe LLMs when they provide fluent and confident responses.

Newer models are becoming more capable and accurate, but LLMs can still produce responses in a way that **sounds convincing even when the information is incorrect**.

Therefore, a confident or convincing tone should **not be treated as evidence that the information is true**.

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 1 3.png]]

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 2 2.png]]

### 3.12 Web Search + LLMs

**Web search + LLMs** is a very powerful combination because it brings together **retrieval + generation**.

Modern chat assistants such as ChatGPT, Gemini, and Claude can use web search to retrieve information and then use an LLM to generate a useful response from that information.

LLMs are particularly good at **language, grammar, and generating content**. This is one reason search engines such as Google have also introduced AI-powered search experiences.

Every time you ask the same question, an AI can potentially answer it in a **different way**, even when the underlying information is the same.

**Retrieval** provides external evidence.  
**Generation** converts that information into a useful response.

We will discuss **RAG (Retrieval-Augmented Generation)** later in the course. RAG is commonly used to retrieve information from **private or specialized data**, whereas web search + LLMs can retrieve information from **publicly available information on the web**.

Many modern chatbots use RAG or **RAG-like retrieval systems** to provide responses in company websites and chatbots on websites.

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 3 2.png]]

### 3.13 Are LLMs self aware 

An AI model can have **information about itself**, such as its knowledge cut-off date, model information, capabilities, or limitations. However, having information about itself does **not mean that it is self-aware or conscious**.

What an AI model can say about itself depends on things such as its **training data, context, system prompts, and available tools**.

LLMs can sometimes behave in unexpected ways, and even their creators cannot always fully explain or predict why a particular response was generated. They can also potentially reveal information they were not intended to reveal if appropriate safeguards fail.

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 7.png]]

