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

