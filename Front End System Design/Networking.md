
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
