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
![[Pasted image 20250924114107.png]]

Now the middleware function runs before every API request which has the route /admin/.
