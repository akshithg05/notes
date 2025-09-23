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

## 21/09/2025

### Why we commit `package.json`

- It defines **what dependencies** the project needs (`express: "^4.17.0"`).
- When someone clones the repo and runs `npm install`, npm looks at `package.json` to know which packages to fetch.
---
### Why we also commit `package-lock.json`

- `package-lock.json` **locks the exact versions** of every package **and all sub-dependencies** installed when you last ran `npm install`.
- Example:
    - `package.json` says:
        `"express": "^4.17.0"`
        → This allows any version from `4.17.0` up to (but not including) `5.0.0`.
    - Without `package-lock.json`, two developers could end up installing slightly different versions depending on when they run `npm install`.
    - With `package-lock.json`, npm installs the exact version tree (e.g., `express 4.17.3` + all its nested dependencies).
---
### Benefits of pushing `package-lock.json`

1. **Consistency** → Everyone on the team, and CI/CD servers, get the same dependency versions.
2. **Reproducibility** → Bugs caused by dependency updates are avoided because versions don’t drift.
3. **Performance** → npm can install faster because it doesn’t have to resolve dependencies from scratch — it uses the lock file.
4. **Security** → Easier to audit exact versions of sub-dependencies.
---
### Quick analogy 🚀
- `package.json` = shopping list (“buy milk, bread, eggs, cheese, but cheese can be any brand”).
- `package-lock.json` = receipt (“you bought Amul cheese, 200g, batch X”).

If you only share the shopping list, teammates may come back with different brands, leading to surprises. With the receipt, everyone gets the same thing.

---
👉 One exception: In **libraries** (published to npm), some teams choose to **ignore `package-lock.json`** because they don’t want to lock versions for library consumers. But for **applications**, you almost always commit it.


Coding example - 
![[Pasted image 20250921154825.png]]
When we have something like this, all our routes will be mapped to the first route handler , because it is like a wildcard, anything starting with "/" will be mapped to the first route handler and others will be redundant.

But if we change the order like this -
![[Pasted image 20250921154940.png]]
This will make sure that the other routes will match their particular routes, because order of routing matters a lot. The wildcard should go to the end. Because the order of code will determine which request is processed.
Whenever a request comes to the server it sequentially checks for routes.

Example -
![[Pasted image 20250921155210.png]]

Now if we go to the route "/hello/2" , it will still go to "/hello" route only as that is matched at first.
But if  change the route and try the same thing -
![[Pasted image 20250921155304.png]]

Here it will not match the first route and go to the second route instead and print the required results.

THIS BEHAVIOUR IS ONLY FOR app.use() function.

If we use app.get("/user") it will match only app.get of user and not anything else.

### Advance routing concept - Regex in routing - currently the below examples for older versions of node

1.
![[Pasted image 20250921162830.png]]
Here in this query string, b is an optional parameter. Doing /abc or /ac gives the same result.

2.
![[Pasted image 20250921163046.png]]

Here this means that our string can have as many b's as possible between a and c.

![[Pasted image 20250921190225.png]]
Here bc is optional.

## 22/09/2025

Routing concepts and tricky conditions -

### Example 1-

![[Pasted image 20250922073142.png]]
Int this case we are not sending anything back to the client, when it requests our server. Therefore, the request will get stuck and there will be no response. There will be request hanging condition.

Example 2

![[Pasted image 20250922072444.png]]

In routes, we can pass multiple route handler functions. In A such a condition as shown above, only the first route handler will be executed as we are sending  the response from there. Send is like a return statement, so only the first fxn executes.

Example 3 -
![[Pasted image 20250922072829.png]]
Here do we think the function will go to the next response or not ?

Here since we are not sending any response from the first function. When we send a request to the server on the given route, our response will get stuck. NodeJS does not automatically move to the next route handler callback function.

For this to happen NodeJS specifies that we have to send another parameter with the route handler callback function. And this function is - next() function

Example 4.
![[Pasted image 20250922073851.png]]

Now if we pass in the next() function which is given by express, then the 2nd or next route handler is executed whenever the earlier route handler completes. Here notice that the first route handler is still not returning any response. Now let us return a response and see the behavior.

Example 5.

![[Pasted image 20250922074157.png]]
![[Pasted image 20250922074453.png]]

 Here only the first function will be executed and when the 2nd CB is encountered, NodeJS will throw an error to us. This is because we have used next(). Next will make sure that the next function is also executed. This means that the first function will actually send the response, but still the 2nd function is executed.
 
We cannot send a response to the URL once the response is already sent.

## 23-9-2025

