
It is a problem solving method. Another item in the fundamental topics 
![[Pasted image 20260117155857.png]]

It is very simple. Problem -> potential solutions -> test solutions
If we have complete and correct knowledge this is not required.

We can generate potential and plausible methods and then test them. That is the whole USP of generate and test method.

![[Pasted image 20260117160022.png]]

### Guards and prisoners problem

![[Pasted image 20260117160402.png]]

Answer 
![[Pasted image 20260117161237.png]]

Which of these will be redundant


### Dumb Generators - Dumb testers

![[Pasted image 20260117161427.png]]

This is because we have many states which is same as the initial states. Because of dumb generators and testers we are getting this. This method applied iteratively can lead to the final state but it will computationally very costly. Too many iterations. It is a powerful method but we have to be careful as to use it wisely as brute force might lead to costly operations.


[[2026-01-19]]

### Smart Generators

Here below we are generating all cases and then filtering out based on the results. 
![[Pasted image 20260119211733.png]]

Instead we can make the generator itself smarter and not generate invalid tests.
![[Pasted image 20260119211835.png]]


IN the below image, if we have a state where we are moving only one person to the other side, then we can remove that case because it will always lead us back to the initial state.

We can make the generator throw out that state, or tester to do it. Both are correct methods, we can take a call which one to use.
![[Pasted image 20260119212103.png]]

