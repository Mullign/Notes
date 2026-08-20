## 1. Assume a 3-input perceptron plus bias (it outputs 1 if net > 0, else 0). Assume a learning rate c of 1 and initial weights 0. The perceptron learning rule is: ∆wi = c(t – z) xi. Given the following training data set:

1 0 0 → 0

0 1 1 → 1

1 0 1 → 1

1 1 0 → 0

1 1 1 → 0

0 0 1 → 0

### Please demonstrate the learning process for 1 epoch by filling the following table:

|Pattern|Target|Weight Vector|Net|Output|∆W|
|---|---|---|---|---|---|
|1001|0|||||
|0111|1|||||
|……|……|||||

## 2. Compare and contrast a feed-forward network, a Convolutional Neural Network (CNN), and a Recurrent Neural Network (RNN) based on the type of data they are designed to handle.

## 3. What is the main problem with using a fixed, small positive constant for the learning rate in Stochastic Gradient Descent (SGD)? Explain how adaptive learning rate strategies aim to solve these problems.

## 4. Describe the concept of pretraining and its purpose in deep learning. Explain the steps involved in greedy supervised pretraining. What is the difference between pretraining and fine-tuning?

## 5. Explain the concept of a convolution in the context of CNNs. How do kernels and filters work to compute the output of a convolutional layer? What are the three key motivations behind using CNNs? Explain each of the following concepts in detail: Sparse Interactions, Parameter Sharing, and Translational Equivalence.

## 6. Describe the role of a pooling layer in a CNN. Explain how it contributes to invariance to local translations and a reduction in computational cost.

## 7. Describe the key difference between an RNN and a traditional feed-forward neural network. Explain how an RNN models the time dimension and captures long-term dependencies. Explain the major obstacle of RNNs, particularly for long-term dependencies. How do Gated RNNs like LSTMs and GRUs address this problem?