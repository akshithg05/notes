

Hashing is another technique that can be used to map requests to servers in the context of load balancing. We discussed hash functions in the "Data Structures and Algorithms For Beginners" course. The concept is rather similar. Each request will have an IP address, user ID, or a request ID associated with it. If we can calculate the hash of this unique identifier and mod it by the number of servers we have available, the answer will allow us to assign the request to a specific server.

Suppose we have three servers, numbered 00, 11, and 22. If we take the IP Address as the unique identifier of three incoming requests, hypothetically being 66, 77 and 88 respectively, the mapping becomes:

```markdown
6 % 3 = 0
7 % 3 = 1
8 % 3 = 2
```

You can probably notice that the same IP address will always be directed to the same server. The benefit of this is that each server can cache data that belongs to a specific user. This makes sense because it is expected that the user with IP address 66 will always be directed to server number 00. You can see how this is different to round robin because the round robin technique is not consistent in assigning the user with the same IP address to the same server each time.

![normal-hashing](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/555b3585-a581-401a-ef3b-8837b5e19700/sharpen=1)

> The above visual demonstrates the assignment of Client's requests among three servers using a load balancer.

## Issue with regular hashing

An issue arises if one of the servers goes down. If server 22 goes down, it now means that we need to perform our modular arithmetic again. As a result, our new mapping may differ. If we have IP address 99, 1010 and 1111, and we only have two servers left, server 00 and server 11, the mapping becomes 11, 00 and 11 respectively instead of 00 and 11 and 22 previously. So while the load is evenly distributed, future requests will lead to cache misses. Server 00 originally had cache for IP 99, server 11 for IP 1010 and server 22 for IP 1111.

![normal-hashing-issues](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/37aa9c3f-763c-46db-4189-1ad9984b4200/sharpen=1)

> The above visual demonstrates what happens if server 2 goes down. Client 9 and Client 11 would be both routed to Server 1.

Let's now discuss the solution, which is consistent hashing.

## The solution

Consistent hashing is a technique that enables uniform load distribution across servers in a load balancing system. It uses a ring-based structure and a hash function to map requests to servers. If a server goes down, the requests it handled are reassigned to the next available server in a clockwise direction on the ring.

The ring represents the space of all possible hash values. Each server in the system is also represented as a point on this ring. The hash function takes the content of the request (IP address) and maps it to a hash value within the range of the ring. When a request arrives, we calculate its hash value using the hash function, and locate the next server on the ring that is equal to or follows the hash value. This is the server that is responsible for handling the request. If a server goes down, its portion of the ring becomes unavailable. In consistent hashing, the requests that were previously handled by that server are reassigned to the next closest server in a clockwise direction on the ring.

We see this visualized below.

![consistent-hashing](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/46f67dfb-4013-49da-9d66-7b94b9ae9700/sharpen=1)

> In consistent hashing, the servers are referred to as nodes in the ring.

![consistent-hashing-node-2-down](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/efa59d15-22c2-426d-64dd-e72ad222a400/sharpen=1)

> Notice above that if Node 2 goes down, all of the requests that would have gone to Node 2 now end up at Node 0.

For the sake of simplicity and demonstration, we have kept the IPs to single digits and the space as 360 degrees. Mathematically, we would use a sophisticated hash function to calculate the hash of the IP, and mod it by `M`, where `M` represents the solution space, which can be said to be the number of positions or partitions on the ring. This number is often equal to the number of servers in the system.

> The reason we perform the modulus operation is because we want to ensure that the resulting value falls within the range of available positions on our ring (0 to M-1). But also, hash functions can produce large integers values which might exceed the range of available positions on the ring. Taking the modulus ensures that we prevent overflow issues. This is crucial to the uniform distribution of requests.

## Closing Notes

At a high level, the provided information covers the essentials of consistent hashing. It is important to note that consistent hashing is just one approach to load balancing and does not invalidate the usefulness of round robin or weighted round robin methods. Round robin can effectively handle load balancing when caching is not a concern.

Consistent hashing finds applicability in scenarios such as Content Delivery Networks (CDNs), particularly when it is necessary to route specific users to the same cache servers in their respective regions. It can also be applied to databases where a user's data resides on a specific server, and consistent routing of that user to that server is desired.

By utilizing consistent hashing, CDNs and databases can ensure efficient and reliable routing, maintaining consistency for users accessing cached content or specific data.