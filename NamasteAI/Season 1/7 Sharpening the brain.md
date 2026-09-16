[[2026-09-15]]

Until now, we have mainly discussed **inference**, assuming that we already have a trained model. Now we are looking at **training**.

A **trained neural network** has learned patterns from its training data and can generate meaningful outputs. An **untrained neural network** has not learned these patterns and will generally produce meaningless outputs.
### 7.1 What does learning actually mean for a machine ?

![[namastedev.com-learn-namaste-ai-sharpening-the-brain.png]]

GPT 3 - 175 billion parameters

![[namastedev.com-learn-namaste-ai-sharpening-the-brain-2.png]]

For a machine, **learning means adjusting the parameters of the neural network**.

Neural networks contain a huge collection of numerical parameters, mainly **weights and biases**. These parameters determine how the network processes information and produces an output.

During training, the model repeatedly adjusts these parameters so that its predictions become better.

Therefore, **training a neural network is essentially the process of optimizing its parameters based on training data so that it learns useful patterns and produces meaningful outputs**.

### 7.2 Parameters and weights

1. The **token embeddings** are part of the model's learned parameters.

2. The **Q, K, and V weight matrices** used in the attention mechanism are also learned parameters.

3. The **weights and biases** in the MLP / Feed-Forward Network are also parameters.

4. Layer normalization also has learned parameters, commonly called **gamma (γ)** and **beta (β)**, which are learned during training.

If these parameters are not properly learned or tuned, the model will not produce useful outputs.

Therefore, a Transformer contains a **huge number of learned parameters** across its embeddings, attention layers, feed-forward networks, normalization layers, and other components.

![[namastedev.com-learn-namaste-ai-sharpening-the-brain-3.png]]

### 7.3 Parameters and Training Data

Parameters **do not store knowledge in the same way that a database stores information**. They are numerical values whose patterns and relationships are learned during training. These parameters act as **knowledge enablers** because, together, they allow the model to generate useful outputs based on what it has learned.

The parameters are **stateful model values**, not simply stateless numbers. Their values are updated during training, and the final trained parameters encode patterns learned from the training data.

**Training data → Model makes predictions → Loss is calculated → Parameters are adjusted → Repeat**

The training data is therefore **not stored separately inside the parameters as a collection of documents**. Instead, training causes the parameters to change so that they capture useful patterns from the training data.

### 7.4 How does training work -

#### 1. Forward pass

First, the training input is passed through the neural network. If the model is untrained, its predictions will generally be poor and may appear meaningless or nonsensical. The model starts with **initial parameter values**, which are typically randomly initialized. As training progresses, these parameters are adjusted.

![[namastedev.com-learn-namaste-ai-sharpening-the-brain-4.png]]

**Compare the Prediction with the Training Data**  

The training data provides the **expected/target output**. The model's prediction is compared with this target.

If the prediction is incorrect, the parameters need to be adjusted so that the model assigns a **lower probability to incorrect predictions and a higher probability to the correct prediction** in similar situations.

#### 2. Loss function 

A **loss function** calculates how far the model's prediction is from the expected output.

- **High loss** → prediction is far from the target
- **Low loss** → prediction is closer to the target

Loss provides a **numerical measure of how poorly the model is performing**.

**Adjust the Parameters and Repeat**  

The model uses the loss to adjust its parameters. It then makes another prediction, calculates the loss again, adjusts the parameters again, and continues this process throughout training.

Repeating this process over large amounts of training data gradually improves the model's parameters and its predictions.



