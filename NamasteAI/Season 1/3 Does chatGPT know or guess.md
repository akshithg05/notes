
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

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 2.png]]

### 3.2 How search engines find information

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 1.png]]

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

![[namastedev.com_learn_namaste-ai_does-chatgpt-know-or-does-it-guess 2.png]]

### 3.3 How LLMs generate responses

