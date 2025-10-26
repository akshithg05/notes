![[Pasted image 20251025110950.png]]
![[Pasted image 20251025112409.png]]
Chat application - we need messages in real time. It should instantly reach me. Order of messages matters. We need to take care of comm technique to keep communication sane. Some systems like these are real time critical like chat applications.

Eg of not real time criticial - Driver location in Uber/ ola - Its okay to have a delay of 5-10 seconds.
But in chat applications we cant have that delay at all, it should be instant.

But this comes with a cost. we will discuss these in the module.

Another example of critical and not critical systems - In a chat app which automatically sends messages to customers on whatsapp, messages related to transaction or booking need to be immediately sent to the customer.
But some other messages like marketing messages/ offers can be sent slowly, not very critical.

Another critical place - 2 people editing the same file simultaneously. We need time critical operation.

So 2 -3 major things we will cover - 
1. Polling - Eg in cricbuzz, website needs to be updated near real time, on every ball. This uses Websockets. A socket is open between client and server, socket is open always. Even for chat the same principle

But for delivery driver location, we dont need that time criticial, we can fetch the data every 10-15-5 seconds, not thatt critical.

Youtube live chat uses - ? open ended question, I think it uses websocket.

We will cover long polling , short polling , webhooks, server side events and websockets in this section.