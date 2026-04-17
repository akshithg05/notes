Examples - 
1. Uber app - live driver location
2. Google Docs - Live documents updating 
3. Cricbuzz live scores
4. Whatsapp chat and other chats


## Types of real time updates

#### 1. API Polling - 

Example a dashboard keeps getting real time data of new sign ups. For big apps there can be many users like amazon/ Flipkart. Another example is YouTube live count (people on stream).

Just short polling. 
Make API call to server every 5/10/15 seconds based on the need.

Every 5 seconds new entry will be made and the dashboard will update with new data. Periodically the dashboard is updated.

There can be cases where in 5 seconds millions of users can sign up or no people sign up as well based on various factors. The strategy is API call will be made irrespective of result

Pros - 
For near real time communication
Half duplex

#### 2. Long polling

In short polling there can be a lot of unnecessary API calls and resource wastage and extra CPU utilization. Long polling can help with this. It is similar but can reduce server load.

(Refer long polling section)

Here, we make the request to the server and server responds if there is data. if we get a response the client again makes a request to the server.
If the server has no data, the request made by the client will stay on the server. Only if there is new data, the server will send the data.

The API will be on hold to the request until there is new data. Server can therefore return whenever it wants. This kind of polling utilizes the data better. More efficiency.

#### 3. Server side events

Whenever server has data , it will send data.
It is like a push notification. There is no fixed time.
Client will subscribe to events. Whenever server has the data it will send us the data. 

#### 4. Websockets

Client makes a connection with the server.
It is a duplex, bidirectional communication system.
It is like sending and receiving events on the same API.
Any time calls and connection can happen on websockets.
It will stay open unless browser is closed or websocket is closed.

Polling also can be done with web sockets , One real time connection for communication.

Pros - 
For real time comms.
Full duplex

### Famous interview discussion - Polling vs Websockets

API polling is more expensive because a new stateless HTTP request is made on eevry request and a lot work like Auth, etc is done everytime. But in Websockets its less expensive as there is only one connection which is created.

Websockets are more sophisticated, not that simple to implement or run as compared to API polling. May not run on all browsers at all times.

![[namastedev.com_learn_namaste-frontend-system-design_real-time-updates.png]]

![[namastedev.com_learn_namaste-frontend-system-design_real-time-updates 1.png]]

