![[Pasted image 20260502103110.png]]

Dense - Layer in neural network

### 1. Building the model using tensorflow
![[Pasted image 20260502103531.png]]

### 2. Model for digit classification
![[Pasted image 20260502103640.png]]

## 3. Data in TensorFlow

Some intuition and notes on numpy arrays 0:

![[Pasted image 20260508172531.png]]

If we do not have multiple square brackets and put all numbers within a single square([]) bracket, then we would be creating a 1-D vector and not a 2-D matrix/ vector.
This has no rows or columns.

![[Pasted image 20260508172811.png]]

There is a convention to represent data in the form of m x n vectors in TensorFlow, hence we use 2 square brackets for this. See the example below - 

There are 2 ways of representing matrixes - 
1. TensorFlow matrix
2.  numPy matrix

Below is the first layer of our example
![[Pasted image 20260508173210.png]]

Below is the second op layer
![[Pasted image 20260508173406.png]]

## 4. Building neural network in TensorFlow

Prior knowledge
![[Pasted image 20260508173716.png]]

New knowledge - 

Using the sequential function.
![[Pasted image 20260508174103.png]]

Simplifying -
![[Pasted image 20260508174122.png]]

Digit example
![[Pasted image 20260508174412.png]]


