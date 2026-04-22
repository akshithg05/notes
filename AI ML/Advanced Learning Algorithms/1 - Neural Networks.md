Syllabus

![[Pasted image 20260420214158.png]]

## Neurons and the brain

![[Pasted image 20260420215058.png]]

### Comparison between neuron and neuron in AI

![[Pasted image 20260420215542.png]]

![[Pasted image 20260420220031.png]]


[[2026-04-22]]

### Demand Prediction

![[Pasted image 20260422160815.png]]

### Grouping neurons to form layer

1. Layer can have single or multiple neurons
2. Last layer is called output layer
3. Output of the layer is called activations. The activation of the last layer is the output.
4. Middle layers are called "hidden layers".

Each neuron in a certain layer will have access to every input (output of the previous layer) in the input layer.

![[Pasted image 20260422170312.png]]

##### Further simplification -

![[Pasted image 20260422170517.png]]

### Multiple hidden layers

![[Pasted image 20260422170930.png]]

#### Example: Image recognition

![[Pasted image 20260422172102.png]]

Problem - take the picture of a person as input, which are made up of 1000 x 1000 pixel intensities. Using this as input compute the identity of the person.

Building the neural network for this can be as follows - 

![[Pasted image 20260422172631.png]]

