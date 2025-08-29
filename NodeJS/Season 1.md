S1 E1 - History of NodeJS 16/8/2025 
![[Pasted image 20250816152240.png]]Refer notebook for more notes.

Google V8 Engine
![[Pasted image 20250816153618.png]]

Job of a JS Engine - Using C++ convert High level code (JavaScript) to machine level and assembly level language.
![[Pasted image 20250816155908.png]]

NodeJS
![[Pasted image 20250816160001.png]]
![[Pasted image 20250816160031.png]]


Season 1 EP3
![[Pasted image 20250817230241.png]]



### Season 1 Ep 5 - 20/8/2025

![[Pasted image 20250820193956.png]]


We cannot access the a, because it is in the scope of function x, and not in global scope.
a and fxn b cannot be accessed outside of fxn x().

Modules work the same way in JS.
All code of the modules is wrapped inside a function, when we call require and give it a path. When it wraps the code it creates a special fxn called IIFE. (read)

![[Pasted image 20250820195440.png]]

![[Pasted image 20250820195200.png]]

Q. How are variables and functions private in different modules - due to IIFE and require statement.

Q. How do you get access to module.exports?
Ans. When code is wrapped inside the IIFE function, the function passes an empty module as a parameter into the function and it is passed inside the function call.
![[Pasted image 20250820195958.png]]

Similarly even required is passed into the IFFE function as a parameter. These are given by Node.
![[Pasted image 20250820200451.png]]
These are not the only things passed into the function by node, there are many more things which will be discussed later on.

![[Pasted image 20250820200737.png]]

![[Pasted image 20250821183810.png]]
![[Pasted image 20250821183917.png]]



### 5 step mechanism of what is happening when we require a module

![[Pasted image 20250820201336.png]]


### Season 1 EP 5 - 21/8/2025

In a **Node.js module (a `.js` file)** at the top level, `this` **does equal** `module.exports`.
![[Pasted image 20250821194324.png]]

IFFE inside nodeJS code
![[Pasted image 20250822194730.png]]

The wrapper[0] is the iife starting, script is our entire code in a js file, wrapper[1] closes the iife function.
End of the day string concatenation is happening that's all!


28-8-25
Example of Sync and Async
![[Pasted image 20250826231841.png]]
Synchronous - one has to wait before the other is fulfilled

Async 
![[Pasted image 20250826232606.png]]


Sync vs Async tasks example
![[Pasted image 20250826233700.png]]

## How JS Engine Executes Synchronous JS code (browser or node anything)

![[Pasted image 20250828000817.png]]

Code within a JS function is executed inside the functional execution context. and the returned value is returned to the variable in the GEC.

![[Pasted image 20250828001146.png]]



## How JS Engine executes Async JS code

Some of the async operations which we might need to do in our code / application is -
reading/writing from a file, connecting to a database, making api calls, using timers. JS engine does not offer these capabilities. Here is where NodeJS comes into the picture.
![[Pasted image 20250828002031.png]]

NodeJS gives JS Engine superpowers to interact with the Operating System (OS) and perform various operations
![[Pasted image 20250828003033.png]]


libUV - 
NodeJS offloads all the async tasks to libUV, which talks to the OS of the system, gets the response and delivers it back to JS engine.

![[Pasted image 20250828003649.png]]

All Async code and operations are offloaded by JS engine to libUV
![[Pasted image 20250828003818.png]]

## 29/8/2025

![[Pasted image 20250829195547.png]]

Code walk through - How NodeJS handles both synchronous and asynchronous code at the same time.


1. Creation of a global execution context and saving the variables to the Memory heap.
![[Pasted image 20250829201305.png]]

2. When the API call line is encountered, JS engine invokes libUV as API call is an async operation.
A callback function is also registered by libUV - A **callback function** in JavaScript is simply **a function that is passed as an argument to another function**, with the intention that it will be **called (executed) later** inside that function.

So, the key idea is **passing a function into another function** — not necessarily returning it.

![[Pasted image 20250829202251.png]]

JS engine waits for nothing, once the async operation is offloaded to libUV, the JS engine continues executing the rest of the program.

3. The setTimeout line is encountered BY the JS Engine, and it offloads it to libUV again.
![[Pasted image 20250829202542.png]]

4. Even the file system read is offloaded to libUV
![[Pasted image 20250829202630.png]]

5. But now JS Engine knows how to handle multiply function as it an asynchronous operation, hence it performs this action on its own without any offloading
![[Pasted image 20250829204649.png]]

Once the function is executed, the functional execution context moves out of the Call Stack. Once that is done, the garbage collector frees up all the space/ vars utilized by the function.

Once the function execution is complete, console.log(c) will run and then GEC will move out of the call stack.

As soon as the file is read by libUV, libUV sends the callback function back to JS engine. this function will be pushed onto the callstack and then be executed. And then the function will be removed from the callstack.

Similarly, if API call is resolved by this time, this A function will be added to the CS and the function will be executed quickly.

NodeJS is ASYNCHRONOUS
V8 Engine is SYNCHRONOUS

Therefore, NodeJS can do async I/O or non-blocking I/O. NodeJS is a JavaScript runtime built on Google Chrome's V8 Engine, it is capable of running JS outside the browser and perform async I/O operations.
