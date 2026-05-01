
## Challenges
1.  Too many messages, we cannot show all the messages. It does not make sense to show 10k, 100k messages. We can do it , but it does not make sense. Users cant even read the messages. UX will be broken.
2. Not every message is shown or required. Show only limited number of messages.
3. Not required to be shown real time. Near real time is more than enough in YT live stream chat. System will hang if we have to show all these messages real time. It will be waste of resources and complicated architecture.
4. Page size can explode if we keep pushing all messages to chat.

### For this do we need API polling or Web Sockets 

Answer - API polling 

### Why ?

1. We are okay with our system being near real time, we don't need a fully exact real time system.
2. If chat explodes with a lot of users, we cannot open too many web socket connections and leave it open for so long. It will consume a lot of CPU and memory and resources. This will increase server load massively and YouTube is a scale product.
3. Retrying in WS is a challenge
4. IN API polling load balancer can use LB algorithms and load can be distributed. In WS we cannot do this as its a live connection and we need 1 to 1 mapping constantly.


## Always ask where will you get the CHat messages from

Discuss these things with the interviewer. What are all the data fields and how the data will be coming.

#### One more thing to discuss with interview - If asked what is better, to implement limiting on the front end or backend. -

Limiting messages on the backend  is always the better answer. We dont have to overfetch data on the UI. Keep UI simple, fast and efficient.

-> We need to limit total messages as well as accumulating a lot of messages and showing it on UI will explode the DOM. We need to limit the chat window for a certain number of messages. If messages go beyond a number , we need to prune the last message from the DOM.

