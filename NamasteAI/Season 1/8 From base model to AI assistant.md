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

[[2026-09-27]]

![[Pasted image 20260927114233.png]]

### 8.4 Base model

![[Pasted image 20260927115543.png]]

### 8.5 What happens inside post training ?

![[Pasted image 20260927121215.png]]

Post-training teaches the model **how it should behave**, rather than simply predicting the next token blindly.

The goal is to make the model:

- **Helpful:** Understand the user's request and answer it appropriately.
- **Knowledgeable:** Provide useful and accurate information.
- **Aligned:** Follow instructions and appropriate safety guidelines.
- **Respectful:** Communicate in a humble, clear, and non-arrogant manner.

**In simple terms:**  
**Pre-training → teaches the model knowledge and language patterns**  
**Post-training → teaches the model how to use that capability effectively**

To achieve all this we use SFT supervised fine tuning

### 8.6 Supervised fine tuning

![[Pasted image 20260927121511.png]]

![[Pasted image 20260927122454.png]]

[[2026-09-28]]

Fine tuning continued (its a part of the post training process) -

![[Pasted image 20260928231151.png]]

Fine tuning is extra training to achieve a desired behavior of a model.
### 8.7 Instruction tuning

Instruction tuning uses examples of instructions and their desired responses to teach the model how to follow user requests.

Instead of merely autocomplete-style text generation, the model learns to respond appropriately to questions, understand the context of a request, and provide useful answers.

Example:

- Before: Given “What is the capital of France?”, the model might continue the text in various ways.
- After: The model is trained to recognize the question and respond with “Paris.”

Key idea: Instruction tuning helps turn a base model into a model that follows instructions and responds helpfully.

### 8.8 Diversity matters a lot

![[Pasted image 20260928232207.png]]

Fine tuning is what makes models of different companies different. The fine tuning , diversity and post training matters. Base models of various companies can be similar but after fine tuning the models and AI assistants can be very different because of the fine tuning.

![[Pasted image 20260928232724.png]]

- System instructions: These can explicitly provide information about the assistant's identity, role, and behavior.
- Additional tools or configuration: The system may provide current information about the model or its capabilities.

Key idea: The model's knowledge is largely learned during training, while specific details about its identity and behavior may be supplied through system instructions or configuration.

### 8.9 Conversational formatting

AI assistants use a structured conversation format with special tokens or markers to distinguish messages from different roles, such as `system`, `user`, and `assistant`.

- These markers help the model identify who said what and distinguish instructions from user messages and assistant responses.
- They also help structure conversations and control how the model generates its output, including tool calls in supported formats.
- Users generally don't need to type these markers manually. The system typically formats the conversation into the model's expected structure before processing it.

Key idea: Conversational formatting provides structure and context so the model can interpret the conversation correctly and respond appropriately.

![[Pasted image 20260928233341.png]]

These are small nitty gritty things which makes the models so good.

### 8.10 Roles

![[Pasted image 20260928233553.png]]

These are the three main roles. Many companies and modern LLMs can have various other and more complex roles to get better outputs.

[[2026-09-29]]

### 8.11 SFT is cool but not enough

Supervised Fine-Tuning (SFT) teaches a model to follow instructions using examples of prompts and desired responses. However, the same question can have multiple valid answers — simple, technical, confusing, incorrect but confident, or overly detailed.

The challenge is deciding which answer a human would prefer. Different people have different preferences for accuracy, tone, detail, and answer length, so creating a perfect answer is difficult.

- How do we teach a model which answer is better?
- How do we make responses consistently helpful, accurate, and appropriately sized?    
- How do we account for different human preferences?

![[namastedev.com_learn_namaste-ai_from-a-base-model-to-an-ai-assistant 3.png]]

Who solves this ? Humans 

### 8.12 Generator vs Discriminator Evaluation Gap

Ultimately, AI responses are meant to be read and used by humans, so human feedback plays an important role in aligning models with human preferences.

Companies such as OpenAI and Anthropic use human feedback, including evaluations by domain experts (SMEs), to assess and compare model responses.

Generator vs. Discriminator Evaluation Gap:

- Generator: Creating an ideal answer from scratch can be difficult, even for humans, and may introduce mistakes or bias.
    
- Discriminator (Evaluator): Comparing two or more existing answers and ranking them from best to worst is often easier and faster than generating an ideal answer.
    

Therefore, humans can act as evaluators rather than always having to generate the perfect answer. Their rankings provide preference data that can be used to train models to produce responses people prefer.

![[namastedev.com_learn_namaste-ai_from-a-base-model-to-an-ai-assistant 1 1.png]]

### 8.13 Reward model 

Humans have limitations: evaluating responses repeatedly is time-consuming, and human feedback is difficult to scale. Therefore, we use human preferences to train machines that can evaluate responses at scale.

How do we create a Reward Model?

1. Collect human preferences: Humans compare multiple model responses and rank them based on quality.
2. Train a Reward Model: A separate model learns to predict which responses humans are more likely to prefer.
3. Calculate loss: Compare the reward model's predictions with the human preference rankings.
4. Backpropagation: Calculate gradients based on the loss.
5. Update parameters: An optimizer updates the reward model to improve its predictions.
6. Repeat: Continue training until the reward model learns to predict human preferences more effectively.

Example: ChatGPT may sometimes show you two responses and ask which one you prefer. This is an example of collecting preference feedback, although the exact way that feedback is used depends on the system.

![[namastedev.com_learn_namaste-ai_from-a-base-model-to-an-ai-assistant 2 1.png]]

[[2026-09-30]]

### 8.14 Reinforcement learning with Human Feedback

#### 8.14.1 Reinforcement learning 

Reinforcement Learning trains a model using rewards for preferred behavior and penalties (lower rewards) for less-preferred behavior. It works through trial and error, improving the model's decisions based on feedback.

1. Generate responses: The model produces responses to a prompt.
2. Assign rewards: A reward model scores the responses based on how well they meet the desired criteria.
3. Update the model: The model's policy is optimized to increase the expected reward, making preferred responses more likely.
4. Repeat: This process continues, helping the model produce responses that better align with human preferences.

In Reinforcement Learning from Human Feedback (RLHF), the reward model is trained on human preference data, such as rankings of different model responses.

- Humans: Compare and rank responses based on their preferences.    
- Reward Model: Learns from these preferences and assigns scores to new responses.
- Reinforcement Learning: Uses these reward scores to update the language model so that it is more likely to generate preferred responses.

Key idea: Humans indirectly reward the model through the reward model, allowing human preferences to guide training at scale without humans needing to evaluate every response.

![[namastedev.com_learn_namaste-ai_from-a-base-model-to-an-ai-assistant 3.png]]

### 8.15 Summary until now in the training process

![[namastedev.com_learn_namaste-ai_from-a-base-model-to-an-ai-assistant 1 1.png]]

![[namastedev.com_learn_namaste-ai_from-a-base-model-to-an-ai-assistant 2 1.png]]

### 8.16 Flaws with RLHF

There are flaws with RLHF as well. Humans are themselves different and prefers different answers. So this can create problems.

![[namastedev.com_learn_namaste-ai_from-a-base-model-to-an-ai-assistant 3 1.png]]

### 8.17 Lossy simulation of Human preferences

![[namastedev.com_learn_namaste-ai_from-a-base-model-to-an-ai-assistant 4 1.png]]

Human judgment considers factors like correctness, nuance, tone, and ethics. A reward model compresses these complex preferences into numerical scores, inevitably losing some information.

A reward model is not human judgment itself, but a learned approximation based on a limited sample of human preferences. The score may indicate which response is preferred without explaining exactly why.


