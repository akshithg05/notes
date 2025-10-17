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

Example 6
![[Pasted image 20250923070644.png]]

Here in the code - First the first CB function is added on to the JS call stack. It starts executing line by line. The next() function is encountered. When this is encountered the 2nd CB function is added to the CS and it starts executing line by line. Once the response of the 2nd function is sent to the client, the 2nd function is popped from the CS as it has completed execution and the first function again picks up from where it left off, that is line number 10. Here again we are trying to send the response, hence we get the error at line number 10. But on postman we just see the 2nd functions' return.

Example 7
![[Pasted image 20250923071218.png]]

Here we will not get any error and output will be the 2nd response itself.

Example 8
![[Pasted image 20250923071355.png]]

Here on postman we get the 2nd response and on console also we get the above output and then nothing else will happen. This is because we do not call the next function in the 2nd function.

Example 9
![[Pasted image 20250923071731.png]]

Here we will get the 3rd request and response from the third request on postman.

Example 10 - Here, what if do not sent anything at all and keep calling next?
![[Pasted image 20250923072425.png]]
In the console output I will get all the messages as expected. But on postman when a request is made to the endpoint we get -
![[Pasted image 20250923072458.png]]

This is because when the last next() function was called, ExpressJS is expecting another route handler to handle the request. But there is no other handler. This leads to 404 error on the server.
Hence on the last request we always have to send some response and not call the next function.
We have to send response, else error.

Example 11 - 
We can also pass an array of callback functions with these routing functions. -
![[Pasted image 20250923073139.png]]

We can mix and match array and normal callback functions. Eg - 2 can be inside array, 2 can be outside, all can be outside, all can be inside an array.
![[Pasted image 20250923073235.png]]


Example 12 - We can create multiple route handlers for the callback functions instead of having multiple functions one after the other.
![[Pasted image 20250924090437.png]]
So the above is another way of defining route handler functions one after the other.

Example 13
![[Pasted image 20250924090929.png]]
This will again throw an error saying cannot get/ user as we have called next from the last route handler function, we are not sending a response and there is no other function after that.

Example 14 - 
![[Pasted image 20250924091735.png]]

Here, the first function is only executed as it matches every route. It also has a send() function, which means response will be sent to the client. Therefor, only the first function will execute and the functions below will not be executed at all.

Example 15
If we create a subtle variation of this function above -
![[Pasted image 20250924092127.png]]

Here the API call will match the first response handler, The first console log will be printed. Since we are not sending any response from here and we are calling next, we will move to the next function, log to the console from here as well. We again call the next function, so express goes to the final route handler, prints the console statement and then finally sends the response as well.


## How express works ?

When a client sends a request to an Express server, Express checks the registered route handlers and middleware in the order they were defined in the code.
- Express scans through the handlers to find matches for the request’s **path** and **HTTP method**.
- Each matching handler (or middleware) runs **sequentially**.
- If a handler calls `res.send()`, `res.json()`, or similar response methods, the response is sent back to the client and the request–response cycle ends (unless `next()` is explicitly called after sending, which is not recommended).
- If a handler calls `next()`, Express moves on to the next matching middleware/handler.
- If no response is ever sent and no `next()` is called, the request will hang until it times out.

This makes it important to always ensure either:
1. A response is sent back to the client, or
2. `next()` is called to pass control onward.

To make it crisp for your notes:
- Every **API call** in Express passes through a **chain of middleware functions**.
- Middlewares can modify the request/response objects, perform checks, or decide whether to continue (`next()`).
- Eventually, the request reaches the **route handler** (the last middleware in the chain) which is responsible for **sending the response** back to the client.
- If none of the middlewares or handlers send a response, the request will just hang.

👉 Think of it as a **pipeline**:  
`Client Request → Middleware 1 → Middleware 2 → ... → Route Handler → Response`.


A **middleware in Express** is basically:
- A **function** that sits **between the incoming request** and the **final response**.
- It has access to `req`, `res`, and a `next()` function.
- It can do things like:
    - Log details about the request.
    - Authenticate/authorize the user.
    - Parse JSON/form data.
    - Add or modify properties on `req` or `res`.
    - End the cycle by sending a response (`res.send()`), **or** pass control to the next middleware (`next()`).

So, yes — middleware is used for **modifying or enriching** the request/response, or for doing extra work **before** the final response is sent.


### Practical usage of a middleware function.

Problem statement - We have a set of APIs which can only be accessed by the admin. Hence, we have to make sure that there is authorization logic running before we send the response. if the user is not authorized we will send a 401, unauthorized response.

Code (without middleware)
![[Pasted image 20250924113640.png]]
Here, these are 2 admin APIs. We want to make sure they have the right token, only then we can allow them to perform some operation. Else we return 401 error. Suppose there are 100s of such functions, we cannot keep writing the same block of code for every function. This becomes tedious  and increases code duplication. It also makes files unnecessarily large.
Here we can use middleware. We can write the middleware at the top level so that for all admin requests this token check will run.

Code-
![[Pasted image 20250925081039.png]]
Now the middleware function runs before every API request which has the route /admin/. Therefore the code is more cleaner and we are only calling the middleware at the top level.

Some more code playing around - 25/9/2025

Example 1-

If I have a function with another route below the middleware function, will the middleware be executed for that route? Will the auth check run?
![[Pasted image 20250925082041.png]]
For the above scenario, even though the auth token is not matching the /user, when a request is made to the /user endpoint, the response will be sent successfully because the auth middleware only runs for the /admin endpoint.

We can move the middleware to a separate file as well.

Example 2- 
![[Pasted image 20250925090438.png]]
Here we see that we can pass the "userAuth" as an argument in the route handler function as well.

We can pass middleware function like this as we can pass multiple functions as already seen in the above exxplanations. These functions in the arguments run one after the other.
If the middleware fails, then the 2nd function will not even be called. This is a safe way of handling requests.

### Middleware in Express - 25/6/2025

- Middleware functions sit **between the client’s request and the server’s response**.
- They allow you to **intercept, transform, or validate** the request/response before the final handler executes.
- Common uses:
    - Logging requests
    - Validating data
    - Authentication/authorization
    - Parsing JSON/form data
    - Error handling
### Why Middleware?
- **Code reuse** → you don’t repeat logic in every route.
- **Separation of concerns** → keep request processing, validation, and response handling modular.
- **Maintainability** → cleaner and easier to scale.
- Without middleware, all these concerns would be duplicated inside each route handler → messy, hard to maintain.


Example 3
![[Pasted image 20250925091810.png]]

Here there are two APIs for /user. One uses the userAuth and one does not. This is because for signUp we do not need any authentication. Hence we do not pass the middleware into that route handler's arguments. So in this way we can actually plug and play with our middleware functions.

Nomenclature-
- "route handler" → callback inside `.get()` / `.post()`
- "middleware" → functions registered with `.use()`
- "routing methods" → `.get()`, `.post()`, `.use()` themselves
## Error handling

If the route handler takes in 2 arguments it has to be (req ,res)
if 3 arguments then (req, res, next)
if 4 arguments then (err, req, res, next)

The order of this is very important and error can only be the first argument.

**The best and most preferred way to handle errors is by wrapping our route handler function within a try, catch block**

Coding Example 1 -

![[Pasted image 20250925102513.png]]
In the above image, when the error is thrown, we go into the catch block and response will be error.

Coding example 2-

Another way to handle error and add a safety net is to have a wildcard routing method at the end of all our routing methods.
![[Pasted image 20250925102854.png]]
- You hit **`/user`**.
- The `throw new Error()` immediately terminates execution of the handler function.
    - That means the `res.status(200).send(...)` is never reached.
- Express catches that thrown error and passes it along to the **error-handling middleware** (notice it has 4 arguments: `(err, req, res, next)` — that’s the signature that marks it as an error handler).
- Your `app.use("/", (err, req, res, next) => {...})` **does not act like a wildcard normal middleware here**.
    - Because it has **4 parameters**, Express knows it’s an **error-handling middleware**.
    - It’s not about the `/` path matching — error-handlers are invoked _only if an error was passed down or thrown_.
- Inside that middleware, you send the `500 Internal server error` response. ✅
- Once a response is sent, Express **does not move on to the next route handler**. The request/response cycle ends.

Coding Example 3 -
![[Pasted image 20250925104530.png]]
- You hit `/user`.
- The route handler runs.
- `throw new Error("Something went wrong");` is triggered.
- Express **does not just crash** (unless you throw asynchronously). Express automatically catches synchronous `throw` and forwards it to the **next error-handling middleware** in the stack.
- But here’s the catch: since your error-handling middleware is defined **before** `/user`, Express doesn’t reach it anymore (Express only looks forward in the stack).
- Result: the error is unhandled, and the client gets an ugly stack trace or a connection reset depending on environment.

Coding example 4- Best Practice

![[Pasted image 20250925104747.png]]

- `try/catch` in routes → immediate handling, precise control.
- Error middleware → safety net for unexpected or unhandled errors.
- Best practice in bigger apps → combine both, but lean on middleware + async handler wrappers to avoid clutter.

## 26/9/2025 - Database, Schema and Mongoose

### Mongoose

**Mongoose** is an ODM (Object Data Modeling) library for MongoDB in Node.js. It acts as a layer on top of MongoDB, providing a structured way to define schemas and models, interact with collections, and perform queries. It also supports built-in validation, middleware, and other powerful features, making MongoDB easier to use and maintain compared to working with the native driver directly.
While the **native MongoDB driver** lets you interact directly with the database using raw queries, **Mongoose** adds an abstraction layer with schemas, models, and validation, making code more structured and easier to maintain.
### Schema 

In **MongoDB + Mongoose**, a **Schema** is essentially a **blueprint** for your documents:
- It defines the **shape** of the document that will be stored in a collection.
- It specifies the **fields**, their **data types**, and any **constraints/validations** (like required, unique, min, max, default, etc.).
- It can also define relationships between documents (via references), virtual properties, middleware, and methods.

Think of it like this:
- MongoDB by itself is **schema-less** → you can put anything inside a document.
- Mongoose adds a **layer of structure** → ensuring your documents are consistent and follow rules you define.

**MongoDB** itself is **schemaless**. It will happily let you insert a document with any shape:

`db.users.insertOne({ name: "Akshith" }); db.users.insertOne({ car: "BMW", speed: 200 });`

Both would sit in the same `users` collection with no problem.

- **Mongoose**, on top of MongoDB, gives you the option to define a **Schema** so that **your application enforces structure/consistency**.

👉 So yes, **schemas are not mandatory** at the database level, but they are extremely useful at the application level.  
They help you:

- Avoid accidental bad data (e.g., storing a string where a number is expected).
- Apply constraints (required fields, uniqueness, min/max, defaults).
- Keep documents predictable → easier querying and updates.
- Add business logic (middleware, virtuals, methods).


![[Pasted image 20250926084940.png]]

![[Pasted image 20250926084956.png]]

![[Pasted image 20250926085009.png]]
### Model

A **Model** is then created from a schema using `mongoose.model()`, which serves as a class mapped to a specific MongoDB collection and provides methods to create, query, update, and delete data.
**Model** → like a **class** that you build from the schema.
The Model provides us with methods to add, query and delete data.

### 27-9-2025 All about APIs

|Feature|JavaScript Object|JSON (JavaScript Object Notation)|
|---|---|---|
|**Type**|Native data structure (in-memory)|Text/string format (for storage & transfer)|
|**Keys**|Strings, Symbols (sometimes numbers)|Must be double-quoted strings|
|**Values allowed**|Strings, numbers, booleans, null, objects, arrays, functions, `undefined`, symbols|Strings, numbers, booleans, null, objects, arrays (❌ no functions/undefined/symbols)|
|**Flexibility**|Very flexible, can include logic|Strict, schema-like, only data|
|**Usage**|Used directly in JavaScript code|Data exchange between systems (e.g., APIs)|
|**Conversion**|Already executable in JS|Needs `JSON.parse()` → JS object `JSON.stringify()` → JSON string|

This is a subtle but important difference.

- ✅ **`app.use(express.json())`**
    - This applies the `express.json()` middleware to **all incoming requests**, regardless of the path.
    - Commonly used because you usually want to parse JSON bodies across the entire app.
- ⚠️ **`app.use('/', express.json())`**
    - This also applies `express.json()` to all routes, since `/` matches everything that starts with `/`.
    - In practice, it behaves the same as `app.use(express.json())` for most apps.

👉 But the nuance is:
- `app.use(express.json())` is the idiomatic, clean way.
- `app.use('/', express.json())` explicitly ties the middleware to routes beginning with `/`. It’s redundant but not wrong.

So: **Yes, functionally they are the same here**, but the first form is preferred for clarity.

## 28/9/2025

1. **find({})** - returns all documents in the collection. {} takes in filter
2. **findOne({name: "Akshith"})** - That's not necessarily the case, and it's a common misconception. If you call `findOne()` without specifying a sort order, it returns the first document according to the collection's "natural" order. 

The natural order is generally the insertion order, but it is not guaranteed and can change based on disk storage, updates, and other background operations in MongoDB. 

Here is a more detailed explanation:

- **Natural order**: The document's on-disk storage order is its natural order. While this often corresponds to insertion order (so older documents come first), it is not a guarantee. If documents are updated to a larger size, they might be moved to a new location on the disk, changing the natural order.

If I don't send any filter or anything inside the {}, then mongoDB will return the first document on the natural occurring order on the disk.

If we try to update a field not there in the schema, will be ignored by the API function.

![[Pasted image 20250928063736.png]]

this returnDocument here is an option which is passed into findByIdAndUpdate. It takes in 2 values - 'before' and 'after'. If we use 'before', it returns the document before update and if we use 'after' it returns the value after the document has been updated.
Ultimately the document will be updated but the user returned is different.

### 30/9/2025

By passing a "timestamps" attribute to the mongoose model along with schema, we can get the createdAt and updatedAt fields automatically on the objects which are created and updated in the DB.

## 1/10/2025

Run validators using npm validator library. -  read more about it and use it to validate proper mail ID, strong password / proper URL format.


### 1/10/2025

We can have validation in the DB schema / or even in the code we can have our own validation.
We have to always encrypt the passwords and save it.
We use the npm library to "bcrypt" to encrypt the password.

Bcrypt hashing password

- **bcrypt.hash(password, saltRounds)** → hashes a plaintext password.
- **Salt**: a random string added to the password before hashing (prevents rainbow-table attacks).
- **saltRounds (cost factor)**: number of iterations (2^saltRounds) the algorithm runs → controls hashing difficulty.
- **Trade-off**: higher saltRounds = more secure but slower.
- **Common values**: 10–12 in production, 14+ for highly sensitive data.
- **Verify**: use `bcrypt.compare(plain, hash)` → internally re-hashes and checks equality.


### Authentication JWT and Cookies

How cookies work and how a user is authenticated and logged in 

### JWT Authentication Flow (with Cookies)

- User logs in with email + password.
- Server verifies credentials; if valid, it generates a **JWT token**.
- Token is sent back to the client, usually stored inside a **cookie** (often HTTP-only for security).
- For each subsequent API request, the browser automatically includes the cookie.
- Server extracts and **validates the JWT** from the cookie header:
    - If valid → user is authenticated, request proceeds.
    - If invalid/expired → authentication fails, user must log in again.
- This ensures **stateless authentication** (server does not store session data; validation happens via JWT).
![[Pasted image 20251003064054.png]]

When will cookies not work ?
If cookie has already expired.

![[Pasted image 20251003064408.png]]

Some notes -

- `express.json()` is indeed **middleware** in Express.
- It parses the **incoming request body** (not the response) if it’s in **JSON format**.
- After parsing, it converts the raw JSON into a **JavaScript object** and attaches it to `req.body`.
- Without it, `req.body` would be `undefined` when you send JSON data in a request (like in `POST`, `PUT`, `PATCH`).

#### Cookie Parser-

You’ve got it right — **cookie-parser** is also middleware, and its role is similar to `express.json()`, but for cookies:
- Cookies come in as a **raw header string** in `req.headers.cookie`.
- `cookie-parser` parses that string into a neat **JavaScript object** and attaches it to `req.cookies`.
- This makes it super easy to read cookie values in your routes.

![[Pasted image 20251003071833.png]]


## Using and creating our own Auth middleware

![[Pasted image 20251004065754.png]]
In the above code the userAuth() middleware is a custom middleware function which will run before the actual route handler. When all the code inside the middleware runs successfully, the middleware will call next(). Once the next() is called the route handler will run.
Using this auth middleware simplifies and abstracts the Authentication logic.

### 7/10/2025

Logging out user-

Using `res.clearCookie()` is the correct and recommended practice for deleting a cookie in a Node.js Express application. Setting a cookie's value to `null` or an empty string is less reliable and can lead to confusion.

Check source code
![[Pasted image 20251007060951.png]]

Logout APIS are generally simple, mostly just cleaning work.


11/10/2025

### 🧠 The Intuitive Analogy

Think of a **book**.
- Without an **index**, if you want to find all pages mentioning “Machine Learning,” you’d have to **read every page** until you find them — that’s like **a full collection scan** in MongoDB.
- With an **index at the back of the book**, you can directly jump to the pages that mention “Machine Learning.” You don’t need to scan the entire book — just look up the keyword and go to the right page numbers.

That’s exactly what MongoDB indexes do.

---
### ⚙️ What is an Index in MongoDB?

An **index** is a **data structure** (usually a **B-tree**) that MongoDB maintains **alongside your collection** to make searching faster.

It’s like a **sorted list** of key values that MongoDB can binary search through very quickly.

#### Example:

Suppose you have a `users` collection:
![[Pasted image 20251011060812.png]]

MongoDB has two options:
1. **Without an index**: It has to check every document — one by one — to see if `name` equals `"Akshith"`.  
    → O(n) time complexity (linear scan).
2. **With an index on `name`**:

db.users.createIndex({ name: 1 })

MongoDB maintains a **sorted structure of all names** internally.  
It can now use **binary search** or tree traversal to find `"Akshith"` directly.  
→ O(log n) time complexity (much faster).

### 📈 How MongoDB Stores Indexes

Internally, MongoDB uses a **B-tree (balanced tree)** structure for most indexes.  
This means:

- Each node contains a **sorted range of key values**.
- Searching, inserting, and updating in the index tree is efficient.
- The index stores **pointers to the actual documents** in the collection.

So when MongoDB runs a query:
1. It first searches the **index** (fast).
2. Then follows pointers to only those documents that match (no full scan).

### ⚡ Why Indexes Make Queries Faster

✅ **Fewer documents scanned** – only matching entries are looked up.  
✅ **Faster sorting** – if you query with `sort()`, MongoDB can use the index order instead of sorting all results in memory.  
✅ **Efficient range queries** – like `age > 20 && age < 30`, since the index is sorted.

### 🚨 But There’s a Trade-off

Indexes come with **costs**:

- **Storage**: Each index takes up disk space.
- **Write overhead**: Every `insert`, `update`, or `delete` must also update the index.
- **Maintenance**: Too many indexes slow down writes.

So you should only create indexes that match your **frequent query patterns**.
![[Pasted image 20251011061038.png]]



Trade offs with indexes
## ⚠️ When Not to Use Too Many Indexes

While indexes make **read operations (find, sort, etc.)** faster, they come with real trade-offs.

### 🚫 1. Increased Disk Space Usage
- Each index is a separate data structure (a B-tree) stored on disk.
- Large collections with many indexes consume significant storage.
- The more indexes you create, the more your disk space grows — sometimes larger than the collection itself.

### 🐢 2. Slower Write Operations
Whenever you **insert, update, or delete** a document:
- MongoDB must also **update all relevant indexes**.
- This means:
  - Inserts → new keys added to the index.
  - Updates → key positions recalculated.
  - Deletes → keys removed from the index.
- Each of these adds extra processing and I/O overhead.

So, if your application performs a lot of writes, **too many indexes can noticeably slow it down**.

### ⚙️ 3. Increased Maintenance Complexity
- Indexes must be kept consistent with the data.
- Dropping or rebuilding them can be expensive for large collections.
- Frequent schema changes make managing indexes more complicated.

---

## 🧭 Best Practices for Indexing

✅ **Index only fields used in queries or sorting**  
If a field is rarely used in a query, it probably doesn’t need an index.

✅ **Monitor with `.explain()` and performance metrics**  
Use:
```
db.collection.find({...}).explain("executionStats")
```

✅ **Avoid redundant indexes**  
An index on `{ name: 1, age: 1 }` already covers a query on `{ name: 1 }`.

✅ **Balance read vs write performance**  
If your app is read-heavy → more indexes help.  
If it’s write-heavy → fewer indexes perform better.

Over-indexing is as harmful as no indexing.  
Index wisely — focus on fields that are _frequently queried_, not _every field you create_.

When we are starting slow, we do not need indices, for 100/1000 users. Only if our docs cross 1 lakh 1 million indices it is good to create indixes.


## 🧩 Compound Indexes in MongoDB

### 🧠 What They Are

A **compound index** is an index built on **multiple fields** in a document.  
It allows MongoDB to efficiently support queries that filter or sort on **those fields together**.

Example:
```js
db.users.createIndex({ age: 1, city: 1 });
```
This creates a **compound index** on both `age` and `city` fields.
- `1` → ascending order
- `-1` → descending order
 So, the index is sorted first by `age`, then by `city` _within each age group_.

### ⚙️ How It Works

Think of it like sorting a spreadsheet:
1. First, sort by **age**.
2. If two users have the same age, sort them by **city**.

So MongoDB can now quickly find:
`db.users.find({ age: 25, city: "Chennai" });`

or even:
`db.users.find({ age: 25 });`
(because `age` is the **prefix field**)

---

### ⚡ Performance Benefit
Without a compound index, MongoDB would need to scan:
- The index on `age`, then filter by `city`, **or**
- The index on `city`, then filter by `age`.

With a compound index, it can find the match directly — no filtering required.

---

### 🔢 Index Prefix Rule (Very Important)

MongoDB can use **a left-prefix subset** of a compound index.
For an index like:
`{ age: 1, city: 1, name: 1 }`

MongoDB can use it for queries on:
- `{ age: ... }`
- `{ age: ..., city: ... }`
- `{ age: ..., city: ..., name: ... }`

❌ But **not** for `{ city: ... }` or `{ name: ... }` alone,  
because they don’t start with the **first indexed field (`age`)**.

> **Rule of thumb:** Query fields should follow the same order as the index definition.
---
### 📦 Example Use Case

Let’s say your app frequently runs queries like:
`db.orders.find({ customerId: 123, status: "delivered" });`

A good compound index would be:
`db.orders.createIndex({ customerId: 1, status: 1 });`

Now MongoDB can quickly jump to all “delivered” orders for customer 123,  
instead of scanning all orders.

---
### ⚖️ Trade-offs

|Benefit|Cost|
|---|---|
|Speeds up multi-field queries|Increases storage size|
|Reduces sorting cost|Write operations slower|
|Covers prefix queries|Doesn’t help if query skips prefix field|

---
### 🧭 Best Practice

- Always put **the most selective field first** (the one that filters the most data).
- Avoid creating separate single-field indexes on fields already covered by a compound index.
- Use `.explain("executionStats")` to verify index usage.

13/10/2025

As a dev we have to think like a security guard for a Db.

### POST API vs GET API Though process

POST - User is trying to enter data in DB. An attacker can attack by sending random data into the db. We have to validate and not trust any data coming into the db. We have to verify each and everything coming in.

GET - The data I am sending back to the user should be the only data which is required and allowed in the users scope. Data is the new oil. Data leaks should be prevented completely. We need to make sure the User is authenticated.

Building relation between collections - 
Using 'ref' and creating a link.
While using ref it is always recommended only to populate the necessary fields, we should not be sending the entire object, that is a bad practice.
We should not over fetch the data unnecessarily. 

### 15/10/2025 

Read about ref and populate. This is basically a replacement for joins in SQL.

### 16/10/2025

##### Pagination -
10 users at a time
MongoDB makes it very easy to add pagination


.skip() - How many documents to skip from the beginning
.limit() - How many documents to send

![[Pasted image 20251016212935.png]]





