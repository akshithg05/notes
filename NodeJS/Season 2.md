## 18/09/2025

SDLC in big companies - Waterfall model
![[Pasted image 20250918152443.png]]

Monolithic Vs Microservices Architecture
![[Pasted image 20250918153122.png]]

Key metrics to see while choosing monolithic/ microservices architecture-
![[Pasted image 20250918154601.png]]

How is the learning websire NamasteDev built ?
![[Pasted image 20250918154817.png]]

Project to be built -
![[Pasted image 20250918160523.png]]

a. Project planning 
![[Pasted image 20250919100939.png]]

b. LLD and database design
![[Pasted image 20250919121237.png]]


Connection Request states-
![[Pasted image 20250919124449.png]]

## API Design

We will be using REST APIs
![[Pasted image 20250919124707.png]]

**REST API** stands for **Representational State Transfer Application Programming Interface**. It’s a way for two software systems to communicate with each other over the internet, usually using **HTTP** (the same protocol your browser uses to load web pages).

Here’s the idea:

### 1. **Resources and Endpoints**

- In REST, everything is treated as a **resource** (like users, matches, messages in a Tinder example).
- Each resource has a unique **URL (endpoint)**.
    - Example:
        - `GET /users/123` → fetch user with ID 123
        - `POST /users` → create a new user

### 2. **HTTP Methods (CRUD)**

REST APIs use standard HTTP verbs to define actions:
- **GET** → Read (fetch data)
- **POST** → Create (add data)
- **PUT/PATCH** → Update (modify data)
- **DELETE** → Remove data

So if Tinder had an API:

- `GET /matches` → get your matches
- `POST /swipes` → create a new swipe
- `DELETE /swipes/456` → delete swipe with ID 456
### 3. **Stateless**

- REST is **stateless** → every request from a client to the server must contain all the info needed (like auth token, user ID).
- The server does not remember your "state" between requests.

### 4. **Data Format**

- REST usually returns data in **JSON** (JavaScript Object Notation), sometimes XML.
- Example response:
`{   "user_id": 123,   "name": "Akshith",   "age": 24 }`

### 5. **Scalability**
- Because it’s stateless and uses simple HTTP, REST APIs scale really well — perfect for apps like Tinder.


## PUT vs PATCH

### 🔹 **PUT**
- **Meaning**: Replace the entire resource with the new representation you send.
- If a field is missing, it is usually assumed to be **removed or reset**.
- Think of it like overwriting the entire object.

![[Pasted image 20250919125245.png]]
### 🔹 **PATCH**
- **Meaning**: Partial update of a resource.
- Only the fields you include are updated; others remain unchanged.
- Think of it like a targeted modification.
![[Pasted image 20250919125306.png]]

Some of the APIS we can create for our project
![[Pasted image 20250919130453.png]]


## Creating our first server 
![[Pasted image 20250920012647.png]]

Versioning 
![[Pasted image 20250920013100.png]]

![[Pasted image 20250920013621.png]]

MAJOR.MINOR.PATCH
1. Major version (X.0.0)
Breaking changes.

Updating to a new major version may break backward compatibility (your old code may stop working).

Example:

4.x.x → 5.0.0 could change APIs, remove functions, or alter behavior.

2. Minor version (x.Y.0)
New features added, but backward compatible.

Existing code should keep working.

Example:

4.17.1 → 4.18.0 might add a new helper function or config option, but won’t break your old code.

3. Patch version (x.x.Z)
Bug fixes, performance improvements, or small tweaks.

No new features, just stability fixes.

Always backward compatible.

Example:

4.17.1 → 4.17.2 fixes a security issue or small bug.

4. Backward Compatibility
Means new versions won’t break old code.

Minor + patch updates preserve backward compatibility.

Major updates can break it.

👉 For example,
if your project depends on express@^4.17.1:

✅ Allowed: 4.17.2, 4.18.0, 4.19.5

❌ Not allowed: 5.0.0 (because it may break old apps).