
Machine learning definition
![[Pasted image 20260220215026.png]]

![[Pasted image 20260220215132.png]]

Answer - B

![[Pasted image 20260220215313.png]]

# 1. Supervised learning 

Very popular today.
Learns from examples/ right answers.
Learns by from correct examples.

Supervised learning is a type of machine learning where a model is trained using labeled data, meaning each input has a known correct output.  
The model learns the relationship between inputs and outputs so it can make accurate predictions on new, unseen data.
![[Pasted image 20260220215639.png]]
![[Pasted image 20260220215912.png]]

## a. Regression

Regression is a type of supervised learning where the output is **continuous**, meaning it can take infinitely many possible values within a range. The predicted outcome is typically a number, such as house price, temperature, or sales revenue.

![[Pasted image 20260220220222.png]]
## b. Classification



![[Pasted image 20260220220815.png]]

![[Pasted image 20260225152726.png]]

### [[2026-02-25]]

Two or more inputs
![[Pasted image 20260225153001.png]]

Summary

![[Pasted image 20260225153117.png]]

## Unsupervised learning 

Data is not associated with output label. 
Find something interesting in the unlabeled data.

![[Pasted image 20260225154840.png]]

Clustering is shown in the above example. 
Clustering is used in Google news.
Example - 

![[Pasted image 20260225155102.png]]

![[Pasted image 20260225155421.png]]

![[Pasted image 20260225155645.png]]


### Other methods of unsupervised learning other than clustering 
![[Pasted image 20260225155957.png]]

Excercise
![[Pasted image 20260225160132.png]]




[[2026-03-02]]

## Linear Regression 

![[Pasted image 20260302223332.png]]

Infinite possibilities, predicitng some number in regression model

Data table with graph
![[Pasted image 20260302223500.png]]


### Terminology
![[Pasted image 20260302223923.png]]

![[Pasted image 20260302223947.png]]


### Univariate linear regression
![[Pasted image 20260302224604.png]]


### [[2026-03-06]]

### Cost function

![[Pasted image 20260306163917.png]]

![[Pasted image 20260306164139.png]]

When we want to fit a straight line we want a line passing through most points in linear regression

For this we need the cost function 
### Cost function
![[Pasted image 20260306164647.png]]

What exactly does the cost function do, what is it computing ?

[[2026-03-11]] 

## Cost function intuition
![[Pasted image 20260311160802.png]]


## f(x) and J(w) cost function for different values of w

w = 1
![[Pasted image 20260311161459.png]]

w = 0.5
![[Pasted image 20260311161805.png]]

w = 0
![[Pasted image 20260311161954.png]]


### Overall picture
![[Pasted image 20260311162128.png]]

### How to choose the best w value ?

W should be chosen to minimize the value of J / cost function. The squared error cost function should be as minimum as possible.

![[Pasted image 20260311162311.png]]

# 1. 3Visualization of cost function

![[Pasted image 20260311164549.png]]

## Cost function for w only
![[Pasted image 20260311170058.png]]

Now when we introduce w and b, the cost function becomes like a soup bowl as there is one more axis.
![[Pasted image 20260311170136.png]]

![[Pasted image 20260311170243.png]]


### Representing 3d images using contour lines

![[Pasted image 20260311170358.png]]

TOp view
![[Pasted image 20260311170409.png]]

## Visualizing the cost function - contour plot
![[Pasted image 20260311170703.png]]



## Some examples
![[Pasted image 20260311171739.png]]
bad w and b values

### Good values of w & b

![[Pasted image 20260311171930.png]]



