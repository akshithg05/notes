### 17/10/2025

Many FAANG companies and start ups are adopting graphQL. Diving deep into graphQL.
If we know this, it will take our interview experience to the next level.
## 1. What is GraphQL?

GraphQL is an API architectural style that enables clients to interact with servers using the Graph Query Language.  
It focuses on representing and querying data as a graph, where different entities or resources are connected through defined relationships.  

Instead of accessing multiple REST endpoints, the client sends a single, structured query specifying exactly what data it needs.  
The GraphQL server then aggregates data from various sources, consolidates it, and returns a single, well-structured response to the client.

In short, GraphQL provides a flexible and efficient way to fetch and manipulate interconnected data.


Overview
![[Pasted image 20251017082612.png]]


## 2. Understanding GraphQL vs REST APIs

### REST API Approach

In traditional REST APIs, each resource typically has its own endpoint.  
If the client needs data about multiple resources, it must make multiple network calls.

Example:
GET /api/continents  
GET /api/countries  
GET /api/languages

Here, the client (such as a React or JavaScript application) needs to:

1. Make three separate requests  
2. Wait for all responses  
3. Combine the data manually within the app  

This can increase network overhead, especially when multiple endpoints are involved.

---

### GraphQL Approach

With GraphQL, a single endpoint handles all data queries.  
Instead of making multiple REST calls, the client sends one request to the GraphQL server, specifying exactly what data it needs.

The GraphQL server then:
1. Interprets the client’s query  
2. Fetches the required data (possibly from multiple sources or services)  
3. Combines the data into a single structured response  
4. Sends it back to the client  

Conceptual Flow:
Client → GraphQL Server → (Multiple APIs / Databases)  
              ↓  
        Combined Response  

Example Query:
```graphql
{
  continents {
    name
  }
  countries {
    name
    population
  }
  languages {
    name
  }
}
```

Key Idea:  
GraphQL lets the client ask for exactly what it needs — no more, no less — through a single endpoint.

### Why It’s Powerful
- Single request → multiple data sources
- Reduced over-fetching and under-fetching
- Flexible and efficient — clients control the data shape.

![[Pasted image 20251017083653.png]]

Heavy lifting is offloaded to the graphQL server.

## 3. Fundamental Understanding of GraphQL

GraphQL stands for Graph Query Language. It provides a way to query and manipulate data that is organized like a graph, where different entities are connected to each other through defined relationships.

For example, consider a data model with continents, countries, and languages.  
Continents contain countries, and each country has one or more languages.  
This naturally forms a graph structure where each entity is a node and the relationships between them are edges.

In a broader sense, most real-world data can be represented as a graph.  
Social networks are a common example — users are connected to other users through friendships, likes, or follows.

GraphQL helps us query such interconnected data easily and efficiently.  
Instead of fetching data from multiple independent endpoints, we can request exactly what we need in a structured way.

In short, GraphQL allows fetching graph-like data in a clean, organized, and predictable manner.

## 4. Additional Points and Trivia about GraphQL

GraphQL was originally developed internally by Facebook around 2012.  
It was later made open-source in 2015, allowing the broader developer community to adopt and extend it.

### Benefits of GraphQL

1. **Flexibility**  
   GraphQL gives the client full control over what data to request.  
   Instead of relying on multiple REST endpoints or applying numerous filters, the client specifies exactly what fields are needed in a single query.

2. **Efficiency**  
   GraphQL helps reduce over-fetching and under-fetching of data.  
	Over-fetching -Since the client defines the structure of the response, only the required data is transferred, leading to more efficient network usage. Better performance in large scale application, as only selected information is coming from server to client.
	
	Under-fetching - We fetch certain info, whatever we need, we are not getting lesser information as well. Eg - we need a lot of information but the API is not giving us that much information 


4. **Single Endpoint**  
   Unlike REST APIs which have multiple endpoints, GraphQL operates through one endpoint, simplifying API interaction.

5. **Strongly Typed Schema**  
   GraphQL APIs are built around a strongly typed schema that clearly defines the types of data available and how they relate to each other. Types of data are well defined and structured.

6. **Improved Developer Experience**  
   With tools like GraphiQL or Apollo Sandbox, developers can explore the schema, run queries interactively, and get auto-completion for available fields.

7. **Better Mobile Performance**
   On smaller devices like smartphones, where bandwidth and processing capacity are limited, GraphQL improves performance by reducing the number of API calls and minimizing unnecessary data transfer.

8. Introspection

9. Real time capabilities - Using subscription.

---

In summary, GraphQL was designed to make APIs more flexible, efficient, and intuitive to use, particularly for modern client-driven applications.

Check - [Explorer | Countries@current | Studio](https://studio.apollographql.com/public/countries/variant/current/explorer)

![[Pasted image 20251018072016.png]]

## 5. GraphQL and HTTP - 18/10/25

GraphQL, like REST, is built on top of the HTTP or HTTPS protocol.  
It doesn’t replace HTTP but defines a different way of structuring and sending data over it.

In most implementations, GraphQL requests are made using the **POST** method.  
The client sends a single POST request to the GraphQL endpoint (usually `/graphql`) with the query and variables included in the request body.

Example:
```json
POST /graphql
{
  "query": "{ countries { name population } }"
}

```

## REST vs GraphQL

### 1. Data Fetching
- **REST:** Requires multiple endpoints for different resources. For example, separate endpoints for continents, countries, and languages.  
- **GraphQL:** Fetches all required data in a single request through one endpoint.  
  → Fewer network requests, improved efficiency.

---

### 2. Request Structure
- **REST:** Uses fixed structures and standard HTTP methods (GET, POST, PUT, DELETE) to perform CRUD operations.  
- **GraphQL:** Uses flexible request structures with **queries** (for fetching data) and **mutations** (for modifying data).  
  These are defined within the request body rather than relying on multiple endpoints.

---

### 3. Over-Fetching and Under-Fetching
- **REST:** Often returns too much or too little data (depending on how endpoints are designed).  
- **GraphQL:** Avoids this problem by allowing the client to specify exactly what fields are needed, including nested data.

---

### 4. Response Size
- **REST:** Response size is fixed based on the endpoint’s design.  
- **GraphQL:** Response size is dynamic and client-controlled. Clients receive only the requested data.

---

### 5. Versioning
- **REST:** Requires explicit versioning (for example: `/api/v1/users`, `/api/v2/users`) when the API changes.  
- **GraphQL:** Does not require explicit versioning.  
  The schema can evolve by adding new fields or types without breaking existing queries.  
  Example:
  - Old clients can continue querying `{ user { name } }`
  - New clients can use `{ user { name, email } }` — both remain valid.

---

### 6. Schema
- **REST:** Schema may or may not be well-defined; it depends on server implementation and documentation.  
- **GraphQL:** Has a strongly typed, explicitly defined schema.  
  Every field, type, and relationship is defined clearly, improving reliability and documentation.

---

### 7. Real-Time Capabilities
- **REST:** Real-time features require workarounds such as polling or WebSockets (for chat apps, live feeds, etc.).  
- **GraphQL:** Supports real-time updates through **subscriptions**, enabling built-in support for features like live chats, notifications, or data streams.

---

### 8. Tools
- **REST:** Typically uses third-party tools like Postman or Insomnia for testing and exploration.  
- **GraphQL:** Comes with built-in or integrated tools such as Apollo Sandbox, GraphiQL, or GraphQL Playground.

---

### 9. Caching
- **REST:** Relies mainly on HTTP caching mechanisms (e.g., ETags, cache-control headers).  
- **GraphQL:** Offers fine-grained caching capabilities, especially on the client side using tools like Apollo Client.  
  Specific queries or responses can be cached selectively and efficiently.

---

### 10. Client-Side Control
- **REST:** The client has limited control over the response. Data can only be filtered or paginated through query parameters.  
- **GraphQL:** The client has full control over what data to request and how it should be structured in the response.

---

### 11. Adoption
- **REST:** Mature and widely adopted across the industry.  
- **GraphQL:** Newer but rapidly growing in popularity. Supported by an active developer community and increasingly integrated into modern frameworks.

---

### Summary
GraphQL offers flexibility, efficiency, and real-time capabilities that make it powerful for modern, data-driven applications.  
However, REST remains a reliable and established standard, especially for simpler, well-defined APIs.


![[Pasted image 20251018085124.png]]
![[Pasted image 20251018085153.png]]


## 6. GraphQL Architecture

In the GraphQL architecture, there are two main components:

### 1. Creator (Server)
The server is responsible for creating, defining, and exposing the GraphQL API.  
Common implementations include:
- **GraphQL.js** — the official JavaScript reference implementation.  
- **Apollo Server** — a popular GraphQL server that integrates seamlessly with Node.js.  
- **Mercurius** — a fast GraphQL adapter for the Fastify framework.

A dedicated GraphQL server is required to handle incoming queries, resolve them, and return structured responses.

---

### 2. Consumer (Client)
The client consumes the GraphQL API exposed by the server.  
It can be any frontend or application capable of making HTTP requests.

Common options include:
- **React SPA** or other web/mobile applications.  
- **fetch() API** for basic query execution.  
- Advanced GraphQL clients such as **urql**, **Relay**, or **Apollo Client** for managing queries, caching, and real-time updates.

A dedicated GraphQL client is optional — simple queries can be made using standard HTTP requests, but specialized clients provide additional capabilities like caching, state management, and subscription handling.

---

### Summary
GraphQL applications consist of:
- A **dedicated server** that defines the schema and handles queries.  
- An **optional client** that can either make direct requests or use advanced GraphQL libraries for enhanced functionality.

![[Pasted image 20251018090254.png]]


## 7 . GraphQL Building Blocks

![[Pasted image 20251020092732.png]]

### 1. Schema / Types

A GraphQL schema defines the structure of data that can be queried or modified through the API.  
It describes the different types of objects available, the fields they contain, and the relationships between them.

For example, if we need information about a country, we must define what a `Country` is and what fields can be queried from it.

Example:
```graphql
type Country {
  id: ID
  name: String
  phone: String
  code: String
}
```

The above is written using **SDL (Schema Definition Language)** — the syntax used by GraphQL to describe data types and their fields.

---
### Schema Types
There are two main categories of types in GraphQL:
1. **Scalar Types**  
    These represent basic, indivisible data values.  
    Common scalar types include:
    - `String`
    - `Int`
    - `Float`
    - `Boolean`
    - `ID`
2. **Custom (Object) Types**  
    These are user-defined types that group related fields together.  
    Example:
    - `Country`
    - `Language`
    - `Continent`

Custom types are used to describe the structure of complex, related entities within the system.

---
In essence, the schema acts as the **contract** between the client and the server — it defines what data can be queried and how that data is organized.

### 2. Query and Mutation

In GraphQL, the HTTP method most commonly used is **POST**.  
While technically almost every operation could be done using POST (even in REST), REST typically uses different HTTP methods (GET, POST, PUT, DELETE) for semantics, readability, and structure.

- **Query**  
  Queries are used to **fetch data** from the server.  
  The client specifies exactly what fields it needs, and the server returns a structured response containing only that data.
- Here is a simple example:

    type Query {
      countries: [Country]
      continents: [Continent]
    }

Explanation:
- `Query` is the root type for all read operations.  
- `countries` returns a list of `Country` objects.  
- `continents` returns a list of `Continent` objects.  
- The client can request specific fields from each object when making a query.


- **Mutation**  
  Mutations are used to **modify or update data** on the server.  
  Similar to queries, the client specifies what data should be modified and the server returns the updated state after performing the operation.
- Here is a simple example:

    type Mutation {
      addCountry(name: String, code: String, phone: String): Country
    }

Explanation:
- `Mutation` is the root type for all write/update operations.  
- `addCountry` is a mutation that allows the client to add a new country by providing its `name`, `code`, and `phone`.  
- The mutation returns the newly created `Country` object.  
- Clients can specify which fields of the newly created object they want in the response.

---

### 3. Resolver

While the schema defines **what data exists** and **how it can be queried or updated**, the actual logic for fetching or modifying that data is implemented in **resolvers**.

- **Resolver**: A function that executes when a field in the schema is queried or mutated.  
  Each field in the schema typically has a **one-to-one mapping** to a resolver function.

Example:

    const resolvers = {
      Query: {
        countries: (parent, args, context, info) => {
          // Logic to fetch and return the list of countries
        }
      },
      Mutation: {
        addCountry: (parent, args, context, info) => {
          // Logic to create a new country with args
          // Return the newly created country object
        }
      }
    }

args - filters etc
context 
info - common info
Explanation:
- `Query.countries` resolver is executed whenever the client requests the `countries` field.  
- `Mutation.addCountry` resolver handles creating a new country and returning it.  
- Resolvers act as the **bridge between the GraphQL schema and the underlying data sources** (databases, APIs, or other services).


When a client sends a request to the GraphQL server, the server parses the query or mutation and identifies the requested fields. For each field, the corresponding resolver function is executed, which fetches or updates data from the underlying data sources such as databases or APIs. The server then combines the results from all resolvers into a single, structured response and sends it back to the client. In essence, resolvers act as the bridge between the schema and the actual data, ensuring that queries and mutations are executed correctly and efficiently.


## Diving into the code

![[Pasted image 20251020104723.png]]

This is how we define Schema,
'!' this means that the field is a required field.

Resolvers are one to one mapping of the Schema fields.

In this setup, the actual GraphQL server is created using the `ApolloServer` class, which takes in two main components — the schema (`typeDefs`) and the resolver functions (`resolvers`). These define the structure of the data and how each query or mutation should be executed. 

The `startStandaloneServer` function is a helper provided by Apollo that internally creates a minimal HTTP server (based on Express-like behavior) to handle incoming requests. It automatically sets up all necessary routes, middleware, and JSON parsing for GraphQL. 

So technically, there is only **one server running** — the standalone HTTP server created by `startStandaloneServer()`, which integrates the ApolloServer instance. The Apollo server acts as the **GraphQL engine** that processes the queries and mutations, while the standalone server is the **HTTP layer** that listens for requests and passes them to Apollo for execution. This allows the client to send requests to the standalone server, which delegates them to Apollo Server, processes them, and returns the structured GraphQL response back to the client.

21/10/2025

GQL is so powerful I dont even need to ask the backend for any kind of schema.
Relations in GraphQL

Apollo client - wrapper on top of 