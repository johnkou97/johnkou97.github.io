---
layout: page
title: Deep Learning
description: projects from the course 'Deep Learning' at Leiden University
img: assets/img/brain.jpg # Photo by <a href="https://unsplash.com/@growtika?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Growtika</a> on <a href="https://unsplash.com/photos/an-abstract-image-of-a-sphere-with-dots-and-lines-nGoCBxiaRO0?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Unsplash</a>
importance: 2
category: courses
related_publications: false
giscus_comments: false
redirect:
pretty_table: true
---

## Data Dimensionality - Distance Based Classification

In this assignment, we explored the MNIST dataset and applied dimensionality reduction techniques to visualize the data. The dataset consists of 2707 images (1707 for training and 1000 for testing) of handwritten digits from 0 to 9. The images are 16x16 pixels in size and are represented as a vector of 256 features. Each sample is labeled with the corresponding digit.

The first step was to calculate the average digit for each class in the dataset. The average digits are shown in the figure below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/deep/av_digits.png" title="av_digits" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Average digits from the MNIST dataset.
</div>

We can alo calculate the centre for each digit class and use it as a reference point for the distance-based classification. One measure of how easy is to separate two different digits is the distance between their centres. The distances can be seen in the table below.

<!-- [[ 0.0 14.4  9.3  9.1 10.8  7.5  8.2 11.9  9.9 11.5]
 [14.4  0.0 10.1 11.7 10.2 11.1 10.6 10.7 10.1  9.9]
 [ 9.3 10.1  0.0  8.2  7.9  7.9  7.3  8.9  7.1  8.9]
 [ 9.1 11.7  8.2  0.0  9.1  6.1  9.3  8.9  7.0  8.4]
 [10.8 10.2  7.9  9.1  0.0  8.0  8.8  7.6  7.4  6.0]
 [ 7.5 11.1  7.9  6.1  8.0  0.0  6.7  9.2  7.0  8.3]
 [ 8.2 10.6  7.3  9.3  8.8  6.7  0.0 10.9  8.6 10.4]
 [11.9 10.7  8.9  8.9  7.6  9.2 10.9  0.0  8.5  5.4]
 [ 9.9 10.1  7.1  7.0  7.4  7.0  8.6  8.5  0.0  6.4]
 [11.5  9.9  8.9  8.4  6.0  8.3 10.4  5.4  6.4  0.0]] -->

|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 0.0 | 14.4 | 9.3 | 9.1 | 10.8 | 7.5 | 8.2 | 11.9 | 9.9 | 11.5 |
| 1 | 14.4 | 0.0 | 10.1 | 11.7 | 10.2 | 11.1 | 10.6 | 10.7 | 10.1 | 9.9 |
| 2 | 9.3 | 10.1 | 0.0 | 8.2 | 7.9 | 7.9 | 7.3 | 8.9 | 7.1 | 8.9 |
| 3 | 9.1 | 11.7 | 8.2 | 0.0 | 9.1 | 6.1 | 9.3 | 8.9 | 7.0 | 8.4 |
| 4 | 10.8 | 10.2 | 7.9 | 9.1 | 0.0 | 8.0 | 8.8 | 7.6 | 7.4 | 6.0 |
| 5 | 7.5 | 11.1 | 7.9 | 6.1 | 8.0 | 0.0 | 6.7 | 9.2 | 7.0 | 8.3 |
| 6 | 8.2 | 10.6 | 7.3 | 9.3 | 8.8 | 6.7 | 0.0 | 10.9 | 8.6 | 10.4 |
| 7 | 11.9 | 10.7 | 8.9 | 8.9 | 7.6 | 9.2 | 10.9 | 0.0 | 8.5 | 5.4 |
| 8 | 9.9 | 10.1 | 7.1 | 7.0 | 7.4 | 7.0 | 8.6 | 8.5 | 0.0 | 6.4 |
| 9 | 11.5 | 9.9 | 8.9 | 8.4 | 6.0 | 8.3 | 10.4 | 5.4 | 6.4 | 0.0 |

<p></p>

We can see that the distance between the digits is not uniform, which means that some digits are easier to separate than others. The pair of digits with the smallest distance is 7 and 9, which means that those two digits are the hardest to separate in a distance-based classification.

The next step was to apply dimensionality reduction techniques to visualize the data. We used Principal Component Analysis (PCA), t-Distributed Stochastic Neighbor Embedding (t-SNE), and Uniform Manifold Approximation and Projection (UMAP) to reduce the dimensionality of the data to 2D. The results are shown in the figure below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/deep/pca.png" title="pca" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/deep/tsne.png" title="tsne" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/deep/umap.png" title="umap" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Dimensionality reduction techniques for the MNIST dataset. From left to right: PCA, t-SNE, and UMAP.
</div>

We can see that the different digits are separated in the 2D space, which means that the dimensionality reduction techniques were able to capture the underlying structure of the data. As we can see, the distances we calculated earlier are reflected in the 2D space, with some digits being closer to each other than others.

We applied two classification algorithms to the reduced data: a simple distance-based classifier, where we assigned the label of the closest centre, and a k-Nearest Neighbors (k-NN) classifier, where we assigned the label based on the majority vote of the k closest neighbours. We only tested $$k=3$$ for the k-NN classifier. The results are shown in the table below.

| Classifier | Dataset | Correct | Incorrect | Accuracy |
|------------|---------|---------|-----------|----------|
| Distance   | Train   | 1474    | 233       | 86.35%   |
|            | Test    | 804     | 196       | 80.40%   |
| k-NN       | Train   | 1671    | 36        | 97.89%   |
|            | Test    | 914     | 86        | 91.40%   |

<p></p>

We can see that the k-NN classifier outperformed the distance-based classifier on both the training and test datasets. 

## MultiClass Perceptron

For this assignment, we implemented a multi-class perceptron model to classify the MNIST dataset. The implementation was done from scratch in Python using only the `numpy` library (no deep learning frameworks were used). 

We used two different techniques to train the model: giving the model all the training data at once (batch training) and giving the model one sample at a time (online training). The results are shown in the figure below.
        
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/deep/accuracy.png" title="accuracy" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Accuracy of the multi-class perceptron model on the MNIST dataset for batch (Whole Dataset Method) and online (Input one by one Method) training.
</div>

Training the model with the whole dataset at once required more epochs to converge compared to training the model one sample at a time. However, the training time was significantly shorter for the batch training method. The accuracies of the two methods can be seen in the table below.

| Method | Dataset | Correct | Incorrect | Accuracy |
|--------|---------|---------|-----------|----------|
| Batch  | Train   | 1683    | 24        | 98.59%   |
|        | Test    | 881     | 119       | 88.10%   |
| Online | Train   | 1707    | 0         | 100.00%  |
|        | Test    | 872     | 128       | 87.20%   |

<p></p>

We can see that the online training method achieved a higher accuracy on the training dataset compared to the batch training method. However, the test accuracy was slightly lower for the online training method. This can be caused by overfitting to the training data when training the model one sample at a time. On the test dataset, both methods achieved similar accuracies, with the batch training method slightly outperforming the online training method.

## XOR Network - Gradient Descent

We implemented a simple neural network to solve the XOR problem using gradient descent. The XOR problem is a classic example of a non-linearly separable problem that cannot be solved by a single perceptron. The XOR takes as input two binary values (0 or 1) and outputs 1 if the inputs are different and 0 if the inputs are the same. 

In our implementation, we used a neural network with one hidden layer and one output layer. The hidden layer has three neurons, and the output layer has one neuron. We trained the network using gradient descent and the backpropagation algorithm. We tested three different learning rates: 0.3, 0.6, and 0.8. The results are shown in the figure below. We also tested the network with two different initializations: uniform and normal. The mean squared error (MSE) was used as the loss function. We can see the training process for the different learning rates and initializations in the figures below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/deep/mse_1.png" title="mse_1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/deep/mse_2.png" title="mse_2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Mean squared error (MSE) during training for different learning rates and initializations. Left: varying learning rates with uniform initialization. Right: varying initializations with learning rate 0.3.
</div>

We can see that all the different strategies converged to a solution, reaching an MSE of 0, which means that the network was able to solve the XOR problem. From the diffefrent learning rates, we can see that the highest learning rate (0.8) converged faster than the other two. The uniform initialization also converged faster than the normal initialization.

We also implemented a lazy approach to the XOR problem, where we used the same network architecture but in each epoch, we randomized the weights of the network, until the network was able to solve the XOR problem. The test was to see how many epochs, on average, it took for the network to solve the XOR problem. We did four attempts with an average of 118570.75 epochs and a standard deviation of 118409.22 epochs. The results show that the network was able to solve the XOR problem, but it took a large number of epochs to do so, making it an inefficient approach.

## Fashion MNIST & CIFAR 10 - TensorFlow

In this assignment, we used TensorFlow to build and train neural networks on the Fashion MNIST and CIFAR-10 datasets. The Fashion MNIST dataset consists of 70,000 grayscale images (60,000 for training and 10,000 for testing) of 28x28 pixels each, representing 10 different classes of clothing items. The CIFAR-10 dataset consists of 60,000 color images (50,000 for training and 10,000 for testing) of 32x32x3 pixels each, representing 10 different classes of objects.

We built two different neural network architectures. The first architecture is a multi-layer perceptron (MLP) with three hidden layers, each with 300, 100, and 10 neurons, respectively. The total number of parameters in the model is 266,610. The second architecture is a convolutional neural network (CNN) with three convolutional layers, each followed by a max-pooling layer, and two fully connected layers. The total number of parameters in the model is 1,413,834. We trained both models on the Fashion MNIST and CIFAR-10 datasets each time only changing the input layer to match the dataset. For each dataset we selected 5,000 samples from the training set to use as the validation set. The results are shown in the table below.

| Dataset | Model | Train Accuracy | Validation Accuracy | Test Accuracy |
|---------|-------|----------------|---------------------|---------------|
| Fashion MNIST | MLP | 0.92 | 0.88 | 0.85 |
|               | CNN | 0.92 | 0.89 | 0.22 |
| CIFAR-10 | MLP | 0.63 | 0.48 | 0.38 |
|          | CNN | 0.75 | 0.71 | 0.54 |

<p></p>

For the Fashion MNIST dataset, the MLP model achieved a test accuracy of 85%, while the CNN model had a very low test accuracy of 22%, while for the training and validation accuracy both models performed similarly. This indicates that the CNN model was overfitting the data. For the CIFAR-10 dataset, the MLP model achieved a test accuracy of 38%, while the CNN model had a test accuracy of 54%. The CNN model outperformed the MLP model on the CIFAR-10 dataset, indicating that the CNN model was able to capture the spatial features of the images better than the MLP model, which is something that was expected, since CNNs are more suitable for image classification tasks.

## "Tell the Time" Network

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/deep/classification.png" title="classification" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Classification of the "Tell the Time" dataset using a neural network.
</div>

## Generative Models - Autoencoders (VAEs) & Generative Adversarial Networks (GANs)