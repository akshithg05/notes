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

![[Pasted image 20250828002031.png]]