## Proxies

Let's consider an analogy to understand the concept of a forward proxy server within the context of a network.

Let's imagine a situation where **you want to send a letter** to someone, but you **don't want the recipient to know your address**. So, you ask a **trusted friend** to send the letter on your behalf. Your friend takes your letter, puts it in a new envelope, and **writes their return address on it instead of yours**. Now, the recipient only sees your friend's address, not yours.

In the digital world, a **forward proxy server** acts like that trusted friend. When your computer (the sender) wants to access a website (the recipient), it sends the request to the proxy server (your friend). The proxy server then sends the request to the website on your behalf.

Like your friend, the proxy server masks your IP address and uses its own when communicating with the website, keeping your address hidden. If you frequently request the same data, the proxy server can cache (keep a copy of) the response and provide it to you without having to request the same data from the website again, which makes the process more efficient.

Moreover, a proxy server can filter your requests, much like how your friend might refuse to send certain types of letters that don't meet specific criteria. This is how a proxy server can restrict access to certain websites or resources, similar to how a company or school might block access to entertainment sites.

In summary, a forward proxy server serves as an intermediary in network communication

1. Providing privacy
2. Increasing efficiency through caching
3. Allowing control over network traffic

![forward-proxy](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/603c6f69-1e9d-42d6-6fe7-da95840f9e00/sharpen=1)

> In the diagram above the client is hidden from the origin server. The origin server only sees the proxy server's IP address.  
> **Note**: Of course the internet is present at each step of the way, but this diagram is trying to convey that the client is _aware_ that an extra network call is made by the proxy.

### Reverse Proxy

A reverse proxy anonymizes the **destination server** instead of the client. It can also be considered as an inbound proxy.

Positioned between the internet and the server, a reverse proxy operates differently from a forward proxy. Instead of receiving requests from clients and forwarding them, it receives requests and forwards them to the appropriate server. The key benefit of a reverse proxy is its ability to protect servers by managing incoming requests and distributing the load across multiple servers. Furthermore, it provides protection against Distributed Denial of Service (DDoS) attacks, safeguarding websites.

While a forward proxy acts as an intermediary between the client and the internet, offering an additional layer of security and privacy for clients, a reverse proxy serves a similar purpose for the server. A prime example of a reverse proxy is a Content Delivery Network (CDN). Instead of clients directly accessing the origin server, the reverse proxy (CDN) handles the requests. If the requested content is available, the reverse proxy serves it directly to the client, effectively reducing latency and alleviating the load on the origin server.

![reverse-proxy](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/d6ea7649-f2b6-435d-4f4a-72cd23427600/sharpen=1)

> In the diagram above the server is hidden from the client. The client does not know which server _actually_ fulfilled the request.  
> **Note**: Of course the internet is present at each step of the way, but this diagram is trying to convey that the client is only _aware_ of the network call between the client and proxy, and _not_ the call between the reverse proxy and server.

## Load Balancers

Another widely recognized example of a reverse proxy is a load balancer. Similar to other reverse proxies, a load balancer resides between the client and the server, functioning as an intermediary for their communication.

Load balancing can be implemented in various ways. For instance, a popular website that experiences a high volume of daily visitors is unlikely to manage all incoming traffic with a single server. In such cases, a load balancer plays a crucial role by intelligently distributing the traffic across multiple servers that have been horizontally scaled. This ensures efficient handling of incoming requests and optimal resource utilization.

Load balancers use a variety of strategies to efficiently distribute incoming network requests. They are designed to optimize resource use, prevent server overloading, and improve overall system responsiveness and performance. Let's take a closer look at some of the most common load balancing strategies.

**1. Round Robin**  
Round Robin is indeed a technique commonly used for distributing requests across multiple servers in a sequential manner. It is an algorithm widely applied, not limited to load balancing purposes. The primary objective of round robin is to ensure that each server receives an equal share of network requests. This prevents overloading of a specific server while underutilizing others.

To illustrate the round robin strategy, let's consider the scenario of three servers and five requests. The first request would be directed to the first server, the second request to the second server, and the cycle would repeat until all requests have been allocated. This approach assumes that all servers are capable of handling an equivalent amount of workload.

By following the round robin algorithm, the distribution of requests is balanced, promoting fair resource utilization across the servers involved.

![round-robin](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/ace265b1-33d6-4033-a24d-c7f08e3c0400/sharpen=1)

**2. Weighted Round Robin**

Under the weighted round robin (WRR) strategy, the network traffic gets distributed based on the computational power of each server.

If we have four incoming requests, and three servers: A, B, C with a weight distribution of 50%, 25% and 25% respectively, server A handles 2 requests, server B handles 1, with server C handling 1 as well.

The WRR technique distributes requests proportionally, and ensures a more efficient use of resources.

![weighted-round-robin](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/44a42675-274d-4184-82c6-d31408b86a00/sharpen=1)

> When we refer to "computational power", it entails the server's CPU Processing Power, RAM, storage, and network bandwidth. The computational power influences how many requests a server can handle and how quickly it can process and respond to these requests. By using the WRR technique, the distribution of requests is proportional to the resources of each server, ensuring more efficient utilization of available resources.

**3. Least number of connections**

Another effective method for load balancing is the least connections approach. This strategy is particularly useful when there are significant differences or unpredictable variations in the time required to process each request.

The least connections method works by assigning new requests to the server with the fewest active connections. This proves advantageous in scenarios where servers may complete tasks at different rates. To better understand this, let's consider an example.

During peak shopping seasons like Black Friday or Cyber Monday, e-commerce websites often experience high traffic volumes. However, consumer behavior varies widely. Some users may simply browse products, while others may perform payment transactions, add multiple items to their cart, or apply various filters to their search. In this case, let's assume that Server A is handling complex checkout requests, and Server C is responsible for handling subscriptions. The load balancer may assign a new request to Server C to ensure that Server A or Server B is not overloaded.

By dynamically distributing requests to servers with the fewest active connections, the least connections method helps prevent imbalances and optimizes resource utilization within a load-balanced environment.

![least-number-of-connections](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/0efc06f1-5234-418b-2344-6f6f9d012500/sharpen=1)

**4. User Location**  
Under this strategy, we want to ensure that users receive data from the nearest server, minimizing the distance that data needs to travel. This approach helps reduce latency and provides a faster and smoother user experience.

If our servers A, B, and C located in Asia, Europe, and North America, respectively, the load balancer uses the user's IP address to determine their location. Based on this information, the load balancer routes the user's request to the corresponding server that is geographically closest to them. This helps optimize response times and reduces latency by delivering the content from the server in close proximity to the user.

**5. Layer 4 and Layer 7 Load Balancing**

In the OSI (Open Systems Interconnection) model, the network layer model specifically, Layer 4 corresponds to the transport layer, which is responsible for end-to-end communication. This layer manages protocols like TCP (Transmission Control Protocol) and UDP (User Datagram Protocol). Layer 4 load balancers are designed to route traffic based on Layer 4 data, such as IP address and TCP port, rather than the contents of the requests. This approach makes Layer 4 load balancing fast and straightforward.

On the other hand, Layer 7 load balancers operate at the application layer of the OSI model. This layer is responsible for providing services to the software application that initiates the network request. Layer 7 load balancers analyze and route traffic based on data present in the content of the requests, specifically focusing on aspects like the HTTP headers, methods, or body content. This technique introduces additional processing overhead, but it offers greater flexibility and sophistication in routing decisions. With Layer 7 load balancing, routing can be performed at a more granular level, enabling advanced handling of requests based on specific content characteristics.

![least-number-of-connections](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/458d918e-8358-40b3-9512-f2646544cb00/sharpen=1)

> There is also another strategy called consistent hashing, which we will discuss in the next lesson.

# Closing Notes

If you are interested in learning more about load balancers, the following are good resources:

1. [Maglev](https://research.google/pubs/pub44824/) - Maglev is Google's network load balancer built on software. It has been used internally at Google for many years to handle the vast majority of traffic.
2. [Nginx](https://www.nginx.com/) - An open-source load balancer providing various variety of methods including round robin, least connections, hashing etc.
3. Cloud load balancers provided by AWS or GCP.