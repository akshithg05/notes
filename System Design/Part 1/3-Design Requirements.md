Let us understand the basics of designing a system and the requirements that need to be met to satisfy the quality standards of a large, and effective distributed system.

The good news is that in system design interviews, you aren't expected to know the nitty gritty details of every single component - it is more about the thought process and analysis that goes behind creating an effective distributed system. That is, as long as you have a solid idea of what direction you are going in, and can discuss trade-offs among different choices, it is acceptable.

---

### Thinking in System Design

Whenever you're faced with designing a big enterprise system, it can be boiled down to three points:

#### Moving Data

As we discussed earlier in the chapter on computer architecture, data is moved between the disk, RAM, and CPU. However, when designing large systems, our focus shifts to moving data between different clients and servers, which may be geographically dispersed across the world. This is significantly more challenging compared to local data movement.

#### Storing Data

We already discussed how storing data in RAM is different to storing data on disk. When designing large distributed systems, it is a guarantee that we will need to store data. The question is, how do we store the data? Databases? Blob Stores? File Systems? Distributed file systems? This might remind you of picking between different data structures to find the optimal solution. For example, choosing an array over a BST to store data doesn't mean that an array is better than a BST in all scenarios, but rather it depends on the use case. By the same token, we have to choose how we want to store data and which way will be the most efficient, given the scenario.

#### Transforming Data

Lastly, we want to transform data. It wouldn't be very fun if all we were doing was moving and storing data. If we were given a bunch of server logs, one way to transform this data would be to output the %% of successful requests vs %% of failed requests. This is sometimes handled by a monitoring service. Perhaps, we are given some medical records, and we want to filter the patients by age. These are just two basic examples, and there are countless ways to transform data. Regardless of how complex or how simple the process, the fundamental question is: what is the most efficient way to transform the given data?

---

### Note

In the case of data structures and algorithms, if we picked a bad algorithm, changing the code wouldn't be that challenging. For example, if you write bad code, you can always fix that code without many adverse effects.

Bad design choices in the application architecture can be very costly. Choosing the wrong database will have more severe consequences. You will have to migrate data from one database to another database and at the same time, rewrite portions of the application.

### What is good design?

The next question is: what constitutes a good design? Well, there are a number of factors, performance measures, and certain metrics that are deemed as good design. These factors are good starting points when you start to compare and contrast, i.e. figuring out trade-offs of design choices

#### Availability

Availability is at the heart of an effective system. Availability refers to the percentage of time the system is available, as in, up and running for a given period of time. Traditionally, the availability requirement was Monday-Friday, 9am to 5pm (typical workday hours). Nowadays, the systems we design need to have global connectivity, a near 24/7 operation, where requests to access the system can be made concurrently, from different timezones. Mathematically, availability is calculated by:

availability=uptimeuptime+downtimeavailability=uptime+downtimeuptime​, where uptimeuptime refers to the total amount of time the system is up and downtimedowntime refers to the amount of time the system was not available to the users.

> Downtime can be planned or unplanned. For example, downtime because of a software update, verification, or back-up is planned. But, what if there is a hardware or software failure? Perhaps a natural disaster? It's hard to predict unplanned downtime, but the chances of it occurring can be minimized.

Using the equation above, let's say that we had an uptime of 2323 hours out of 2424 hours. This would result in a total availability of 96%96%. From a system design and a business perspective, this is rather poor, because we are losing money and users for 1 hour a day.

Of course, it is ideal to have 100%100% availability, but it just simply is not possible due to unplanned downtimes. Therefore, companies will aim for _at least_ 99%99% availability. However, even 99%99% uptime means that out of 365365 days, the system would be down for 3.653.65 days. If we want to reduce the downtime by a factor of 1010, this would take our uptime to 99.9%99.9% and downtime to 0.1%0.1%. This is a big jump. Ultimately, availability is measured in terms of 99s.

A good target for companies to have is 99.999%99.999% availability, which is 55 minutes of downtime in 365365 days. This can be hard to achieve, but is important for mission critical systems.

The measure of availability is used to define SLOs (service level objectives) and SLAs (service level agreements).

SLA refers to an agreement a company makes with their clients or users to provide a certain metric of uptime, responsiveness, and responsibilities. SLO refers to an objective your team must hit to meet the SLA requirements. For example, AWS's monthly SLA is 99.99%99.99% and if not met, they refund a percentage of service credit.

#### Reliability, Fault Tolerance, and Redundancy

Reliability refers to the system's ability to perform its intended functions without failure or errors over a specified period of time. When requests are made from our server, the server might be available, but when discussing reliability, we are talking about the probability that the server won't fail. If thousands of users are making requests, or if there are DDoS attacks, how easily does our server go down? This brings us to fault tolerance.

If one portion of our system has a fault, i.e. it fails, and we have another server, it means that our server is somewhat fault tolerant. Fault-tolerance refers to how well the system can detect and heal itself from a problem, i.e. disable a function, revert to a different mode, switch to a different server.

To have fault tolerance, we can have a redundant server. Redundancy in english refers to something that is unessential. This redundancy is provided by our backup server which essentially "shadows" the contents of a server. We don't need this server, but it only comes into play if our primary server fails. Only by having this redundancy, are we able to have fault tolerance.

In this case, the second server is simply a backup. But, what if we had two servers that were both active? This would be called active-active redundancy.

Note: In most cases, by redundancy we mean active-active redundancy (except for the example below).

> The visuals below demonstrate a normal request with a successful response and what happens when there is a DDoS (distributed denial of service) attack. Notice that only one intended user gets the response back. In cases like this, server 2 will come into play. But it will also become overloaded, so redundancy is not a perfect solution.

![image](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/c17e0810-313e-4861-a14a-46373e43eb00/sharpen=1)  
![image](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/0ee5bf71-eca6-4f94-d35e-04baf3736e00/sharpen=1)

#### Throughput

Throughput refers to the amount of data or operations we can handle over some period of time. The throughput of a client making requests to a server would be measured through the number of requests per second. If we want to improve the throughput, we can perform vertical scaling. This makes sense, but as we discussed earlier, there are limitations to vertical scaling. This is where horizontal scaling would come in.

Another measure of throughput is queries/second, which is a measure of the number of requests made by the user to a server or database. Another one is bytes/second. This refers to the maximum amount of data that can be sent over a network at any given time.

Queries per second makes more sense when we are discussing design in terms of users. But what if we had a data pipeline where we are required to process given data in a different format? Here, the data isn't related to a single user, per se, so bytes/second would make more sense here.

The visuals below demonstrate two ways in which throughput may be increased.

![image](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/61560336-2df1-4f9a-4483-0d4b1f496600/sharpen=1)

> Horizontal scaling allows more requests to be handled by multiple servers.

![image](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/8613c56a-32d9-45f3-7e9f-52518ec34200/sharpen=1)

> Vertical scaling allows more requests to be handled by a single server.

#### Latency

Latency refers to the delay between the client making the request and the server responding to that request. So, while throughput refers to how many requests can be sent over a network per second, latency refers to the amount of time it takes for each individual request to be completed. Latency is not exclusive to networks, however. Recall that latency even exists within a computer's internal components, such as the RAM and the cache making requests from the CPU.

![image](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/34a56f10-7d4b-42f0-8e97-7ea9af156900/sharpen=1)

> Round trip latency for a user making a request.

## Closing Notes

We want to design effective systems that can handle failures, have a high throughput, high availability, and low latency. We will be going deeper into the what affects all these factors and how we can satisfy these requirements such that our system is efficient.