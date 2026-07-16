We'll do it in this order:

## Part 1 — BGP Fundamentals

- What is an AS?
- What is a prefix?
- What is a route?
- What is an AS Path?
- What is an Origin AS?

---

## Part 2 — BGP Messages

- Advertisement
- Withdrawal
- RIB
- Updates

---

## Part 3 — BGPStream

How to read the data.

---

## Part 4 — Assignment

We'll go through each task and answer:

- What is the input?
- What information do we need?
- What data structure should we maintain?
- What should the function return?


# PART A

# First, the Big Picture

Forget routers for a minute.

Think of the Internet as a **country**.

The country isn't owned by one company.

Instead, thousands of companies own different parts of it.

For example,

- Airtel
- Jio
- Google
- Cloudflare
- Microsoft Azure
- Amazon AWS
- Georgia Tech
- HPE

Each company owns **its own network**.

Those networks connect together to form the Internet.

Each independently managed network is called an...

# Autonomous System (AS)

> **An Autonomous System is one organization's network.**

Think of it like this:

```
           Internet

      +----------------+
      |     Airtel     |
      |    AS 9498     |
      +----------------+

             |

      +----------------+
      |      Jio       |
      |    AS 55836    |
      +----------------+

             |

      +----------------+
      |     Google     |
      |    AS 15169    |
      +----------------+

             |

      +----------------+
      |  Cloudflare    |
      |    AS 13335    |
      +----------------+
```

Each AS

- owns routers
- owns IP addresses
- decides its own routing policies
- connects to neighboring ASes using BGP

---

### Every AS has a unique number

Instead of saying

> "Google"

routers simply say

```
AS15169
```

Instead of

```
Cloudflare
```

they say

```
AS13335
```

These numbers are called **Autonomous System Numbers (ASN).**

---

## Analogy

Think of countries.

```
India
USA
Germany
Japan
```

Countries have borders.

Each country manages itself.

Similarly,

```
AS15169
AS3356
AS2914
AS9498
```

Each AS manages itself.

---

# What is a Prefix?

Now imagine Google owns millions of IP addresses.

Instead of advertising every IP individually,

```
142.250.72.14

142.250.72.15

142.250.72.16

...
```

Google groups them.

For example

```
142.250.72.0/24
```

This block of addresses is called a **prefix**.

---

Think of it like a postal code.

Instead of saying

```
House 1

House 2

House 3

House 4
```

You simply say

```
Postal Code 560103
```

The postal code represents many houses.

A prefix represents many IP addresses.

---

For example

```
192.168.1.0/24
```

contains

```
192.168.1.1

192.168.1.2

...

192.168.1.254
```

Routers don't care about individual IPs.

They route **prefixes**.

---

# What is a Route?

Suppose I ask,

> How do I reach Google's prefix?

One router replies

```
Go through Airtel.
```

Another replies

```
Go through Jio.
```

Those are **routes**.

A route simply tells us

> "To reach this prefix, follow this path."

Example

```
Destination:

142.250.72.0/24

Route:

AS9498

↓

AS3356

↓

AS15169
```

That's a route.

---

# What is an AS Path?

Now we get to the important part.

Suppose you're in Airtel.

To reach Google,

traffic goes

```
Airtel

↓

Level 3

↓

Google
```

BGP writes that as

```
9498 3356 15169
```

This is called the **AS Path**.

It literally means

```
Traffic passes through

AS9498

↓

AS3356

↓

AS15169
```

Think of it like Google Maps.

Instead of

```
Bangalore

↓

Mysore

↓

Mangalore
```

you have

```
AS9498

↓

AS3356

↓

AS15169
```

---

## Why is AS Path useful?

Imagine you receive two possible routes.

```
Route 1

9498 3356 15169
```

```
Route 2

9498 2914 6461 15169
```

The first path crosses fewer ASes.

BGP often prefers shorter AS paths (after considering higher-priority policy attributes like Local Preference).

---

# What is the Origin AS?

This is the easiest concept.

Look again.

```
9498 3356 15169
```

Who actually owns the destination prefix?

The last AS.

```
9498

↓

3356

↓

15169
         ↑
     Origin AS
```

So

Origin AS

```
15169
```

---

Example

```
AS Path

3356 2914 1299 15169
```

Origin AS

```
15169
```

because it owns the advertised prefix.

---

## Putting everything together

Suppose Google owns

```
142.250.72.0/24
```

Google advertises

```
"I own

142.250.72.0/24"
```

Neighboring ASes propagate that advertisement.

Eventually another AS sees

```
Prefix

142.250.72.0/24

AS Path

9498 3356 15169

Origin AS

15169
```

From just these three fields, it knows:

- **Destination:** `142.250.72.0/24`
- **Path:** Go through `AS9498 → AS3356 → AS15169`
- **Owner:** `AS15169`



# PART B

