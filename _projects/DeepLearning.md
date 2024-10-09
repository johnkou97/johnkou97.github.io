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

## Multi-Class Perceptron

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/deep/accuracy.png" title="accuracy" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Accuracy of the multi-class perceptron model on the MNIST dataset.
</div>

## XOR Network - Gradient Descent



## MNIST & CIFAR-10 - TensorFlow



## Tell-the-Time Network



## Generative Models - Autoencoders (VAEs) & Generative Adversarial Networks (GANs)