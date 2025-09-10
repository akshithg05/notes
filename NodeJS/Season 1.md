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

## 1/9/2025 - Google V8 JS Engine Deep Dive

### Node.js, V8, and libuv – Summary

- **JavaScript (ECMAScript):**  
    Single-threaded, synchronous language. Cannot perform async I/O on its own.
- **V8 Engine:**  
    Executes JavaScript code. Handles parsing, compiling, and running JS, but has **no built-in async or I/O capability**.
- **libuv:**  
    A C library bundled with Node.js that:
    - Implements the **event loop**.
    - Provides **async I/O** (file system, networking, timers).
    - Manages a **thread pool** for blocking operations.
    - Bridges Node.js APIs to **OS-level operations** (uses epoll, kqueue, IOCP, etc.).
- **Flow:**
    1. JS calls an async API (e.g., `setTimeout`, `fs.readFile`).
    2. Node.js hands the request to **libuv**, which interacts with the OS.
    3. Once complete, libuv schedules the callback back into the **event loop**.
    4. **V8 executes** the callback in the main JS thread.

👉 In short: **V8 runs JavaScript, libuv connects Node.js to the OS and enables non-blocking async behavior.**
- `fs`, `http`, `crypto` **are Node.js modules**.
- They rely on **libuv** (and sometimes external libs like OpenSSL) under the hood to actually perform their async work.
![[Pasted image 20250901222454.png]]

Steps executed by V8 engine while executing JavaScript code
![[Pasted image 20250901222940.png]]

Example of AST -
![[Pasted image 20250901223000.png]]

## 2/9/2025

![[Pasted image 20250902220454.png]]


Working of JIT - Just in time compilation.
![[Pasted image 20250902230800.png]]


## 05/09/2025 - LibUV deep dive

![[Pasted image 20250905114844.png]]


Recap - how js code is executed
![[Pasted image 20250905114947.png]]

Event loop working -
![[Pasted image 20250905121654.png]]

See this in the notes, how EL works. 

## 6/9/2025

Below is pseudo coding example (written notes has the explanation but its quite clear from the image as well)- 
![[Pasted image 20250906125908.png]]

Situation - Every callback queue is full with a callback and ready to execute, so how will the event loop schedule these callbacks in the Call stack ?
First the CB from Process.mextTick() will be picked and executed, then the promise callback
Then the timer phase executes and CBS from timer will get executed.
Event loop again checks the P.NT() and Promise CBs. (if they are there, they will get executed else next phase)
Next the polling CSs are executed.
Again P.NT() and Promise CBs.
Next the check phasde CB is executed (this is the CBs coming from setImmediate)
Again P.NT() and Promise CBs are executed.
Then finally the close phase is executed (Socket closing and clean up phase)

Real world coding example -

## Example 1
Phase 1 , sync execution completes
![[Pasted image 20250906133737.png]]

Now after last line of file, the CS is empty, EL sees an opportunity to sched
ule the CBs in CBQs.
When file read is complete -
![[Pasted image 20250906134117.png]]
File is part of poll queue, so once file read is complete it will be added to the poll CBQ. The other CBs have already been executed by this point.

Entire thing completed now -
![[Pasted image 20250906134248.png]]

My own code implementation from VSC
![[Pasted image 20250906135315.png]]
Here one thing to observe is that even though file read operation happens in the poll phase we see that the setImmedieate is printed first. This is because the file read takes some time and it is not in the callback queue still when the EL checks it in the first round.
Hence it is printed in the second phase and it is printed in the end.

All this executes is just micro seconds.
## Example 2

This example consists of P.NT() as well as Promise
![[Pasted image 20250906150523.png]]

End result -
![[Pasted image 20250906151054.png]]

Same thing in code - 
![[Pasted image 20250906151201.png]]

First thing - all sync code will finish running
Then the next tick and promise will be called (As these 2 as highest priority and nextTick is highest priority)
Then timer will be printed if CBQ available
Then poll (if something availalable)
Then check
Then file read(as part of 2nd round poll phase).

## Example 3
![[Pasted image 20250906152747.png]]

Above is the phase 1 result until the file read is complete.

Now once the file reading operation is complete , this E callback function is executed-
![[Pasted image 20250906152954.png]]

When event loop is idle it waits at poll phase, as soon as E comes into CS how will it execute -
![[Pasted image 20250906153517.png]]

The 2nd setImmediate CB is executed before the 2nd setTimeout CB because the EL was waiting at the poll phase when the CS was idle, expected behavior would be for the setTimeout CB to be executed first but since EL was waiting at poll phase, the setImmediate CB that will be executed first.

Code example and output for the same-
![[Pasted image 20250906154409.png]]
![[Pasted image 20250906154429.png]]


Example 4 (Importance of Nexttick callback function)
![[Pasted image 20250906155721.png]]

Until and unless the nextTick queue is empty we will not move to the next phase that is the promise phase.

## 9/9/2025

These images are from NodeJS doc.

![[Pasted image 20250909210926.png]]
These are some additional phases of the event loop.

![[Pasted image 20250909210954.png]]


## 10/9/2025

Thread pool - 
![[Pasted image 20250910132243.png]]

Thread is occupied by operation which is being currently executed.
If a new operation comes in it will pick the free thread. (See below)
![[Pasted image 20250910132518.png]]

