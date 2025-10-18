### 17/10/2025

Many FAANG companies and start ups are adopting graphQL. Diving deep into graphQL.
If we know this, it will take our interview experience to the next level.

Overview
![[Pasted image 20251017082612.png]]


## 1. Understanding GraphQL vs REST APIs

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


## Fundamental Understanding of GraphQL

GraphQL stands for Graph Query Language. It provides a way to query and manipulate data that is organized like a graph, where different entities are connected to each other through defined relationships.

For example, consider a data model with continents, countries, and languages.  
Continents contain countries, and each country has one or more languages.  
This naturally forms a graph structure where each entity is a node and the relationships between them are edges.

In a broader sense, most real-world data can be represented as a graph.  
Social networks are a common example — users are connected to other users through friendships, likes, or follows.

GraphQL helps us query such interconnected data easily and efficiently.  
Instead of fetching data from multiple independent endpoints, we can request exactly what we need in a structured way.

In short, GraphQL allows fetching graph-like data in a clean, organized, and predictable manner.

## Additional Points and Trivia about GraphQL

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

---

In summary, GraphQL was designed to make APIs more flexible, efficient, and intuitive to use, particularly for modern client-driven applications.

Check - [Explorer | Countries@current | Studio](https://studio.apollographql.com/public/countries/variant/current/explorer)


![[Pasted image 20251018071305.png]]

