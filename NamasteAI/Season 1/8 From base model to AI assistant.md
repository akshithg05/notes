There is a big difference between a **base model** and an **AI assistant** such as ChatGPT, Claude, or Grok.

- **Base model:** Primarily trained to predict the next token. By itself, this is not enough to provide a useful, safe, and conversational assistant experience.
- **AI Assistant:** Built on top of a base model with additional **post-training, instruction tuning, safety mechanisms, system instructions, tools, and other engineering** to make it useful for general users.

The main reason different AI assistants behave differently is that **the model is only one part of the overall system**. Each company makes different choices in post-training, system design, tools, safety, and product engineering.

### 8.1 Pre training, training and post training

### Pre-training vs Post-training

So far, we have mainly studied the **training process**, including neural networks, tokenization, embeddings, Transformers, etc.

- **Pre-training:** The initial large-scale training of the model, using a huge dataset that goes through **data collection, cleaning, processing, and preparation**, followed by training the model to predict the next token.
- **Base Model:** The result of pre-training. It is capable of generating text but is not necessarily optimized to behave like a helpful assistant.
- **Post-training:** Additional training done **after pre-training** to make the base model more useful, helpful, and aligned with user instructions. This can include **instruction tuning, preference training, and safety training**.

**Simple flow:**  
**Data → Pre-training → Base Model → Post-training → AI Assistant**

### 8.2 Common crawl 

![[Pasted image 20260926130348.png]]

**Common Crawl** is a nonprofit project that continuously crawls and archives a large portion of the public web. It has been collecting web data for many years and makes the crawled data publicly available for research and other uses.

Web pages contain a lot of **HTML, CSS, JavaScript, navigation, ads, and other noise**, which is not necessarily useful as training text. The raw web data therefore needs to be **cleaned, filtered, and extracted** to produce higher-quality textual training data.

**How is the data refined?**  
Large AI companies typically have their own **web-crawling and data-processing pipelines**. They crawl public websites and then apply processes such as **HTML/text extraction, filtering, deduplication, quality filtering, and removal of unwanted content** to create cleaner datasets.

### 8.3 FineWeb

![[Pasted image 20260926141418.png]]

Checkout FineWeb web page for more information and insights and read about URL filtering, Text extraction, deduplication, PII removal.


![[Pasted image 20260926141526.png|653]]

De duplication prevents overfitting in certain models
