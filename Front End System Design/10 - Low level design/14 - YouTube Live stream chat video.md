
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