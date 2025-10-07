
Networking -

![[Pasted image 20251003121730.png]]

![[Pasted image 20251003122318.png]]


## How the Web works  - 4/10/2025
![[Pasted image 20251004143754.png]]


DNS name resolving and fetching data from the web
![[Pasted image 20251004144411.png]]


How a request is router from your system at home to the internet 
![[Pasted image 20251004151248.png]]
### 🧠 Then (Early 2000s – DSL/Telephone Modem Era)

- Internet came over **telephone lines** using **DSL (Digital Subscriber Line)** technology.
- The **modem’s job** was to _modulate_ and _demodulate_ signals — i.e., convert **digital data** from your computer into **analog signals** that could travel over telephone lines, and vice versa.
- The **router** connected to the modem, distributed that internet (via Ethernet or Wi-Fi) to your local devices.  
    → So:  
    **ISP → Telephone Line → DSL Modem → Router → Devices**
---
### ⚡ Now (Optical Fiber Era)

- Modern ISPs use **fiber optic cables**, which carry **light signals**, not analog ones.
- Those signals need to be converted to digital data too — but instead of a “modem,” we now use an **ONT (Optical Network Terminal)** or **Fiber Modem**.
    - This ONT does the “optical-to-electrical” conversion.
    - Some modern routers (especially ISP-provided ones) have the ONT built-in — that’s why it feels like there’s “no modem.”
- The router then does the same job as before: managing local IPs, Wi-Fi, NAT, etc.  
    → So:  
    **ISP → Fiber → ONT (or built-in modem) → Router → Devices**
---

### ✅ So Your Understanding:

- You’re right that the “traditional modem” as a separate box has mostly disappeared.
- What’s changed is the **type of signal** (analog → optical) and **where the conversion happens** (often integrated with router now).

#### Intermediate

![[Pasted image 20251004152230.png]]

If we use LAN , it will create netwrok hell.

Better way to connect is to have a combination of wired and wireless network.
What the instructor described is essentially the principle of **hybrid networking** — combining wired (Ethernet/fiber) and wireless (Wi-Fi) connections to maximize performance, reliability, and convenience. A few points to clarify -

1. **Wired networks**
    - Pros: High speed, low latency, reliable, secure.
    - Cons: Expensive to deploy everywhere, hard to scale for many devices, cables everywhere → clutter and maintenance complexity.
2. **Wireless networks**
    - Pros: Flexible, easy to connect devices without physical cabling.
    - Cons: Limited range, signal interference, lower speed, and less reliable for high-bandwidth applications.
3. **Hybrid approach**
    - Combines the strengths of both: backbone and high-throughput connections use wires (Ethernet/fiber), while end devices connect via Wi-Fi.
    - **Example in an office building:**
        - Fiber or wired Ethernet as the backbone for each floor.
        - Floor-level Wi-Fi access points allow devices to connect wirelessly.
    - **Example in residential areas:**
        - Local hubs or street cabinets receive the ISP’s main connection (fiber/copper).
        - Individual houses connect via a short wired line to the hub.
        - Inside the house, a Wi-Fi router allows devices to connect wirelessly.

This hybrid structure is how modern networks avoid “network hell” while still providing convenient access to devices.

## 5/10/2025 - Understanding How the DNS works

![[Pasted image 20251005135132.png]]1. **Goal**: Convert a human-readable domain (like `www.google.com`) into an IP address so your device can connect to the server.
    
2. **Domain Levels**: DNS is hierarchical:
    
    - **Root domain (`.`)** – the starting point of the DNS lookup. Root servers know where to find **Top-Level Domain (TLD)** servers.
        
    - **Top-Level Domain (TLD)** – like `.com`, `.edu`, `.gov`, `.in`. Each TLD server knows where to find the **second-level domain** servers.
        
    - **Second-Level Domain (SLD)** – the main domain name (like `google`, `microsoft`). SLD servers know the IP addresses of the subdomains or hostnames.
        
    - **Third-Level / Subdomain** – like `www`, `mail`, `download`. Subdomain servers often resolve to specific IPs for different services.
        
3. **Resolution Flow**:
    
    1. Your computer asks a **recursive DNS resolver** (usually your ISP or a public DNS like Google DNS).
        
    2. The resolver starts at the **root servers**, then moves to the **TLD servers**, then the **SLD servers**, and finally resolves the **subdomain** to the IP.
        
    3. The IP is returned to your computer, which can then connect to the correct server.
        
4. **Key Concept**: Each level narrows down the search space, like a tree. By providing all domain components, DNS can route your request efficiently to the exact server.


### Now moving to the server serving our requests-

How are all the servers in the world connected -
All the world's servers are connected ==through the internet==, which is a vast network of interconnected smaller networks linked by [fiber optic cables](https://www.google.com/search?cs=1&sca_esv=c6276d80b2b2f205&sxsrf=AE3TifN3Jjthvl50t8s2oAIvmgf0s6rLaA%3A1759655532786&q=fiber+optic+cables&sa=X&ved=2ahUKEwitmarX24yQAxXK2TgGHX7CJegQxccNegQIAxAC&mstk=AUtExfA2tMQv7kX63JoHoxkVoB8YOPPIMBSAdlnB_AXX77-bpR7JhKkKyBS6ehUpFW5Ay_8p36roEEJDnzvkwKzTuZRU-h2pBu93IUk0t1MEXdVD8CcPZ_WNCvEkLVfgTN7x3KtrAqsnoB0OkOGN4qbztvwKvt4niJnof9tFsW5xdPL13wI&csui=3) (including vast undersea cables), [copper wires](https://www.google.com/search?cs=1&sca_esv=c6276d80b2b2f205&sxsrf=AE3TifN3Jjthvl50t8s2oAIvmgf0s6rLaA%3A1759655532786&q=copper+wires&sa=X&ved=2ahUKEwitmarX24yQAxXK2TgGHX7CJegQxccNegQIAxAD&mstk=AUtExfA2tMQv7kX63JoHoxkVoB8YOPPIMBSAdlnB_AXX77-bpR7JhKkKyBS6ehUpFW5Ay_8p36roEEJDnzvkwKzTuZRU-h2pBu93IUk0t1MEXdVD8CcPZ_WNCvEkLVfgTN7x3KtrAqsnoB0OkOGN4qbztvwKvt4niJnof9tFsW5xdPL13wI&csui=3), and to a lesser extent, [satellite links](https://www.google.com/search?cs=1&sca_esv=c6276d80b2b2f205&sxsrf=AE3TifN3Jjthvl50t8s2oAIvmgf0s6rLaA%3A1759655532786&q=satellite+links&sa=X&ved=2ahUKEwitmarX24yQAxXK2TgGHX7CJegQxccNegQIAxAE&mstk=AUtExfA2tMQv7kX63JoHoxkVoB8YOPPIMBSAdlnB_AXX77-bpR7JhKkKyBS6ehUpFW5Ay_8p36roEEJDnzvkwKzTuZRU-h2pBu93IUk0t1MEXdVD8CcPZ_WNCvEkLVfgTN7x3KtrAqsnoB0OkOGN4qbztvwKvt4niJnof9tFsW5xdPL13wI&csui=3) and [radio waves](https://www.google.com/search?cs=1&sca_esv=c6276d80b2b2f205&sxsrf=AE3TifN3Jjthvl50t8s2oAIvmgf0s6rLaA%3A1759655532786&q=radio+waves&sa=X&ved=2ahUKEwitmarX24yQAxXK2TgGHX7CJegQxccNegQIAxAF&mstk=AUtExfA2tMQv7kX63JoHoxkVoB8YOPPIMBSAdlnB_AXX77-bpR7JhKkKyBS6ehUpFW5Ay_8p36roEEJDnzvkwKzTuZRU-h2pBu93IUk0t1MEXdVD8CcPZ_WNCvEkLVfgTN7x3KtrAqsnoB0OkOGN4qbztvwKvt4niJnof9tFsW5xdPL13wI&csui=3). This complex infrastructure allows data to be broken into packets and sent between servers and end-users via specialized devices called [routers](https://www.google.com/search?cs=1&sca_esv=c6276d80b2b2f205&sxsrf=AE3TifN3Jjthvl50t8s2oAIvmgf0s6rLaA%3A1759655532786&q=routers&sa=X&ved=2ahUKEwitmarX24yQAxXK2TgGHX7CJegQxccNegQIBBAB&mstk=AUtExfA2tMQv7kX63JoHoxkVoB8YOPPIMBSAdlnB_AXX77-bpR7JhKkKyBS6ehUpFW5Ay_8p36roEEJDnzvkwKzTuZRU-h2pBu93IUk0t1MEXdVD8CcPZ_WNCvEkLVfgTN7x3KtrAqsnoB0OkOGN4qbztvwKvt4niJnof9tFsW5xdPL13wI&csui=3), enabling global data exchange
![[Pasted image 20251005144243.png]]


### ISP Network
![[Pasted image 20251005144747.png]]

![[Pasted image 20251005145113.png]]


### Understanding Web - Advanced level-

### ⚙️ DNS Resolution – Multi-layer Caching Flow

When you type a URL like `www.google.com`, the system **does not immediately hit the DNS servers**. Instead, it checks through multiple caches to minimize latency and reduce network load.
#### **1. Browser Cache**
- Each browser (Chrome, Edge, etc.) maintains its own DNS cache.
- If you’ve visited the site recently, the IP is already stored here.
- ✅ Fastest lookup — no system or network call.
#### **2. OS Cache / System Resolver Cache**

- If the browser cache doesn’t have it, your computer’s OS resolver (e.g., `nscd` in Linux, `DNS Client` in Windows) checks its cache.
- This cache is shared by all apps in the system.
- ![[Pasted image 20251006070842.png]]
#### **3. Router Cache**
- Many modern routers (home/office) maintain a DNS cache too.
- If your laptop doesn’t have the record, the router may have recently resolved it for another device on the same network.
#### **4. ISP DNS Cache**
- The request next goes to your **ISP’s recursive DNS resolver** (or to a public one like Google DNS or Cloudflare DNS if configured).
- ISPs usually maintain a large, frequently updated cache of popular domains.
- If the record is found here — resolution is still fast, and no external queries are needed.
#### **5. External DNS Hierarchy (Root → TLD → SLD)**
- Only if the ISP resolver _doesn’t have the entry_, does it finally go out to the root → TLD → SLD → authoritative name servers to resolve the IP address.
### 🧠 Intuitive Summary

You can think of DNS resolution like asking increasingly bigger circles of “people” if they know the answer — starting from yourself, then your house, then your neighborhood, then the global registry:

> **Browser → OS → Router → ISP → Root/TLD/Authoritative Servers**
![[Pasted image 20251005145637.png]]

### 6/10/2025
Service workers are proxies that sit between the web page and the network, providing cached versions of the site when no network connectivity is available. This is the foundation of Google’s [Progressive Web App](https://developers.google.com/web/fundamentals/codelabs/your-first-pwapp/) (PWA) standard that provides potential performance improvements by leveraging the cache for almost instant page loads. The service worker script runs in the background making the decision to serve network or cached content based on availability. The older form of browser caching, [AppCache](https://appcachefacts.info/), was a more error-prone solution for [offline-first](http://diveintohtml5.info/offline.html) ready applications. You can think of [service workers as their successor](https://medium.com/@firt/service-workers-replacing-appcache-a-sledgehammer-to-crack-a-nut-5db6f473cc9b).

![service worker diagram](https://www.netlify.com/v3/img/blog/service-worker-diagram.png)

[yeti sourced from codepen](https://codepen.io/theskinnyghost/pen/MbXXrw?limit=all&page=3&q=yeti)

The cache is not solely for offline. It also benefits the user during moments of slow or lowered connectivity. Rather than waiting endless seconds for the page to load, a previous cache is presented initially. Even high speed internet can be unpredictable, connectivity can drop intermittently throughout a session. Caching your site ensures there’s always a version ready to go despite the shortcomings of ISP or cell providers.

It is also important to note that, service worker scripts run on a separate thread in the browser from the pages they control. There are ways to communicate between workers and pages, but they execute in a separate [scope](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerGlobalScope) (Thanks to the [Making a service worker case study](https://www.smashingmagazine.com/2016/02/making-a-service-worker/) for that revelation). Service workers are not meant to and do not have the ability to manipulate the DOM directly.

### 🧠 1️⃣ Browser Cache (a.k.a. Disk / Memory Cache)

- **Managed automatically by the browser.**
    
- It caches files based on **HTTP cache headers** (`Cache-Control`, `ETag`, `Expires`, etc.) sent by the **server**.
    
- When you revisit the page, the browser checks:
    
    - “Do I still have this file in my cache?”
        
    - “Has the server told me it’s still fresh?”
        
- If yes → it uses the cached version.
    
- If no → it re-downloads or revalidates with the server.
    

🧩 **You (the developer) have limited control**. It’s mostly server → browser logic.

### ⚙️ 2️⃣ Service Worker Cache (a.k.a. Application Cache via `Cache API`)

- **Fully controlled by the developer** through JavaScript.
    
- Service workers sit between the **browser** and **network**, acting like programmable proxies.
    
- You can choose what to cache, when to update it, and how to respond (even offline).
    

Example (inside a service worker):
![[Pasted image 20251006072947.png]]
This means:

> “If I have this request cached, serve it instantly.  
> If not, go fetch it from the internet.”

This gives you _precise control_ over:

- Offline access (like PWAs)
    
- Cache versioning
    
- Background updates
    
- Fallbacks for poor connectivity


When you visit **YouTube**:

- The **browser cache** keeps static assets like the YouTube logo, CSS, etc.
    
- A **service worker** (if installed) can cache the homepage shell, so even offline you can open YouTube and see the layout, history, etc.
    

---

👉 **In short:**

- **Browser cache** = “Passive” caching (automatic).
    
- **Service worker cache** = “Active” caching (programmable).


TCP handshake 
![[Pasted image 20251006074013.png]]
## 🌐 TCP Handshake — The Foundation of Communication

When your browser (client) wants to talk to a web server, they need to **establish a reliable connection** first.  
That’s what the **TCP 3-way handshake** does.

---

### ⚙️ Step-by-Step Breakdown

1. **Client → Server: SYN**
    
    - The client (browser) sends a packet with the **SYN** (synchronize) flag.
        
    - This says: “Hey server, I’d like to start a TCP connection. Here’s my initial sequence number.”
        
2. **Server → Client: SYN + ACK**
    
    - The server replies with **SYN + ACK** (synchronize and acknowledge).
        
    - This says: “Got your request. Here’s my sequence number, and I acknowledge yours.”
        
3. **Client → Server: ACK**
    
    - The client sends back an **ACK** to confirm receipt.
        
    - Connection established ✅
        

Now both sides know how to track packets, and they can begin **sending actual data** — like your HTTP request (e.g., `GET /index.html`).

---

### 🔒 If HTTPS is used (which is standard today)

After the TCP handshake, there’s an **additional TLS handshake** on top of it:

1. Client says “I want to use HTTPS.”
    
2. Server provides its **SSL/TLS certificate**.
    
3. Client verifies it and agrees on encryption keys.
    
4. Then, encrypted communication begins.
    

So for HTTPS:

> Total setup = TCP handshake + TLS handshake  
> (both happen in milliseconds, but they’re separate steps)

---

### 🧭 Sequence of Events (simplified)

Here’s what happens when you type a URL like `https://www.google.com`:

1. **Browser cache check**
    
2. **Service worker cache check (if registered)**
    
3. **DNS resolution** – find the IP address of `www.google.com`
    
4. **TCP handshake** – establish connection
    
5. **TLS handshake** – negotiate encryption (for HTTPS)
    
6. **HTTP request sent** – `GET /`
    
7. **Server responds** – HTML, CSS, JS, etc.
    
8. **Browser renders** the page
    

---

### 🧩 Analogy

Think of it like a phone call:

- **DNS** = Looking up the phone number in the directory
    
- **TCP handshake** = Dialing the number and both parties saying “Hello, can you hear me?”
    
- **TLS handshake** = Agreeing to talk in a secret code so no one else can listen
    
- **HTTP request** = Actually starting the conversation (“Send me index.html please”)

![[Pasted image 20251006074227.png]]
