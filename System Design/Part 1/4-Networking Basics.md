
Let's cover the basics of networking. This is a gentle introduction to networking and may be seen as "networking for developers". The in-depth details of the topics we discuss are left for a more advanced networking class.

We will discuss how two computers communicate with each other using the client-server architecture we discussed previously.

![networks](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/d328b098-0f82-4df6-475f-9b614d002400/sharpen=1)

## What is a network?

In this example, we will be using two characters, Alice and Bob, to represent our client and server. They are widely used in the cryptographic world.

Alice and Bob are good friends living in different parts of the country. Alice wants to invite Bob to her birthday party, so she creates a personalized invitation. In networking, each device is assigned a unique IP address. This IP address acts as an identifier, allowing devices to send and receive data on the network. More specifically, Alice and Bob represent devices connected to the network.

![alice-and-bob-communication](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/77a9bb3d-2afc-42bd-184b-49e955798400/sharpen=1)

#### IP Address

An IP address serves as a distinct numeric identifier for every device connected to a computer network. IP addresses come in two main types: IPv4, which is 32-bit, and IPv6, which is 128-bit. The IPv4 system theoretically allows for about 4.3 billion unique IP addresses. However, due to design choices during its creation and the exponential growth of the internet, the actual number of usable addresses is considerably lower. This scarcity issue led to the development and adoption of IPv6, which provides a significantly larger address space to accommodate the ever-increasing number of devices on the internet.

IPv4 addresses are 32-bit and are expressed in the range 0.0.0.0 - 255.255.255.255, consisting of four octets. Each octet, composed of 8 bits or a byte, can hold a maximum decimal value of 255. For further information, you can refer to the chapter on **Bit Manipulation** from Data Structures and Algorithms for Beginners course. In contrast, IPv6 addresses are 128-bit and consist of 8 groups of 16 bits. Each octet is represented by four hexadecimal digits and follows the format `xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx`. This expanded address space allows for a virtually infinite number of unique IP addresses, making address exhaustion highly improbable.

While the concept sounds promising, the practical aspect of sending the invitation from Alice to Bob needs to be addressed. This involves following specific rules known as protocols, which govern the transmission of data over the internet. One such protocol is the Internet Protocol (IP).

![ip-address](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/1501bae9-860d-4751-5436-fff0382def00/sharpen=1)

> The visual above demonstrates the anatomy of an IPv4 address.

> In this analogy, Bob's mailing address can be compared to his IP address, and his invitation is similar to a data packet sent over the internet (which we will discuss in detail soon).

## Protocols of sending data over a network

Let's keep following our example with Alice and Bob and see how data transfer in computer networks relates to their invitation exchange. Imagine Alice grabbing an envelope for the invitation. She records her and Bob's details on the envelope, where Bob's information on the envelope can be equated to the IP and TCP headers, and the actual invitation inside the envelope is similar to the payload or data of the packets.

### IP (Internet Protocol) and data packets

Just like Alice sends an invitation in an envelope, data is transferred over a network in the form of data packets. These packets consist of a **header**, **data** (payload), and a **trailer**. The header contains important information such as the source and destination IP addresses, which are crucial for our understanding as developers.

The header is specifically referred to as the IP Header. Usually, data is divided into multiple packets, and they may not arrive in the exact order they were sent. To handle this situation, another protocol called the Transmission Control Protocol (TCP) comes into action.

### TCP (Transmission Control Protocol)

When a substantial volume of data needs to be transmitted, we often use multiple packets. TCP is responsible for the accurate transmission of these packets, ensuring they arrive in the right sequence. In a similar manner to TCP packets, consider Alice sending a multi-page letter to Bob. She assigns numbers to these pages to make sure Bob will read them in the right sequence. This means that irrespective of the order she puts the pages into the envelope, Bob can still assemble them correctly upon receiving. TCP employs the same strategy by incorporating a sequence number in each packet header, making sure the packets are accurately reassembled at their destination.

> The visual representation below illustrates the structure of a TCP packet.

![tcp-packet](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/7a5ddfe3-fa6f-42d5-715e-89fc2e3f1000/sharpen=1)

Through the combined use of TCP and IP, we not only guarantee the precise delivery of data to the right destination but also facilitate the correct reassembly of packets once they reach their endpoint.

### Application Data

As developers, we're primarily interested in the application data portion of the packet. This data can come in different shapes, for example, an HTTP POST request, where the information we wish to transmit resides in the application segment of the packet. Conversely, it could be a GET request, whereby the data segment of the packet signifies the retrieved response.

> We can treat IP Header and the TCP Header as a black box, but we discussed them because they are fundamental to understand networking. It is worth noting that a TCP packet's payload (data) will contain both the HTTP header and HTTP payload.

![network-data-transmission](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/d39ff17d-3a6f-4584-5d92-e84f3246f400/sharpen=1)

#### Network Layers

Protocols within a computer network are systematically arranged into separate layers, creating a hierarchical organization. Every layer has specific duties and interacts with the layers next to it to enable communication.

For example, IP is located in the network layer, which sets the physical pathway for the transmission of data. TCP is in the transport layer, which takes care of the dependable transmission of data. HTTP operates in the application layer, making interaction between clients and servers possible.

### Public vs Private Network

Another important concept is the distinction between private and public IP addresses. A public IP address is a unique identifier given to a device connected to the internet, supplied by the Internet Service Provider (ISP), and is reachable from any device on the internet. This type of IP address is utilized when communication needs to occur between devices on separate networks.

On the other hand, a private IP address is employed within a confined network, like a home or office network. Because of this, these IP addresses aren't accessible to the broader internet. As you may have noted, the main difference is in the range of their accessibility. While public IP addresses can be accessed globally, private IP addresses are only reachable within a LAN (local area network).

### Static vs Dynamic IP Addresses

A dynamic IP address is allocated on a temporary basis and can change every time the device establishes a connection. This type of IP address is frequently employed in home networks. They're automatically assigned, reducing the need for manual configuration. However, a drawback of dynamic IP addresses is their changeability. Hence, they're typically allocated to clients, not servers.

Conversely, static IP addresses require manual configuration, specifying an unchanging IP address.

> It's important to highlight that clients can also possess static IP addresses, but dynamic IP addresses are more commonly utilized for clients since they offer greater adaptability in managing the restricted pool of available IP addresses.

### Ports

Application ports, also known as network ports, are numeric identifiers utilized to distinguish between multiple applications or services running on a single device. If you've ever executed a full-stack project, you'll know that you cannot operate the frontend and backend on the same port. A port number is a 16-bit integer, ranging from 0 to 65,535. Instances of these ports include port 80, typically used for HTTP. The usage of different port numbers enables the establishment of simultaneous connections.

Let's consider an Angular application as an example. By default, it runs on port 4200. We can't operate another application on the same port since it's already in use. We can visualize this concept in the diagrams below.

> Angular application running on port 4200.

![network-ports-angular](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/bd9e19a6-f624-452f-081a-fce58c11aa00/sharpen=1)

> An attempt to run another application on the same port.

![network-ports-already-in-use](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/633bba1b-a827-4097-31ab-014bdc20f200/sharpen=1)