---
layout: page
title: Data Mining
description: projects from the course 'Data Mining' at Leiden University
img: assets/img/mining.jpg # created by Leonardo.ai
importance: 3
category: courses
related_publications: false
giscus_comments: false
redirect:
---

## Recommender Systems - MovieLens 1M Dataset

In this assignment, we implemented several recommendation algorithms using the MovieLens 1M dataset, which contains 1,000,209 ratings of approximately 3,900 movies made by 6,040 MovieLens users who joined MovieLens in 2000. The ratings are on a 5-star scale (whole-star ratings only). Each user has at least 20 ratings. The dataset also includes user information about their gender, age, occupation and zip-code, and movie information about the title and genres. The whole dataset can be downloaded from [here](https://grouplens.org/datasets/movielens/1m/).

For this assignment, we used the following algorithms:
- Naive Approaches: global average rating, average rating per item, average rating per user, and an "optimal" linear combination of the two averages (per user and per item), with and without the parameter γ.
- UV matrix decomposition algorithm
- Matrix Factorization with Gradient Descent and Regularization

For the validation, we used a 5-fold cross-validation, where the dataset was randomly divided into 5 parts, and each part was used as a test set once while the other parts were used as training sets. The RMSE and MAE were calculated for each fold and averaged over the 5 folds. This is a common technique to evaluate the performance of a model and make sure it generalizes well to unseen data.

During training, we kept track of the execution time and memory usage of each model, as well as the RMSE and MAE on each epoch. The plots below show the RMSE and MAE of the UV decomposition and Matrix Factorization models during training.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/mining/uv.png" alt="UV Decomposition" caption="UV Decomposition" %}
	</div>
	<div class="col-sm mt-3 mt-md-0">
		{% include figure.liquid loading="eager" path="assets/img/courses/mining/matrixfactorization_errors.png" alt="Matrix Factorization" caption="Matrix Factorization" %}
	</div>
</div>
<div class="caption">
	RMSE (solid line) and MAE (dashed line) during training for both the training (blue) and validation (purple) sets. Left: UV Decomposition. Right: Matrix Factorization.
</div>

The final comparison of the models shows that the Matrix Factorization model performed the best, with the lowest RMSE and MAE on the test set. The UV Decomposition model was not better than some of the naive approaches, which makes it a poor choice for this dataset. The final performance of the models, with the execution time and memory usage, is shown in the plots below.

<div class="row">
	<div class="col-sm mt-3 mt-md-0">
		{% include figure.liquid loading="eager" path="assets/img/courses/mining/comparison_time.png" alt="Execution Time" caption="Execution Time" %}
	</div>
	<div class="col-sm mt-3 mt-md-0">
		{% include figure.liquid loading="eager" path="assets/img/courses/mining/comparison_memory.png" alt="Memory Usage" caption="Memory Usage" %}
	</div>
</div>
<div class="caption">
	The RMSE (solid line) and MAE (dashed line) of the final model on the training (blue) and validation (purple) sets. With the red line indicating the execution time (left) and memory usage (right) of each model.
</div>

The result can, also, be summarized in a table:

| Model | RMSE Test | MAE Test | Execution Time (s) | Memory (MB) |
| --- | --- | --- | --- | --- |
| Global Average | 1.117 | 0.934 | 15.330 | 375.5 |
| Movie Average | 0.980 | 0.782 | 88.707 | 389.4 |
| User Average | 1.035 | 0.829 | 55.218 | 389.4 |
| Lin Reg with intercept | 0.924 | 0.733 | 178.778 | 416.6 |
| Lin Reg without intercept | 0.953 | 0.763 | 172.274 | 447.5 |
| UV Decomposition | 0.871 | 0.828 | 822.069 | 1948.0 |
| Matrix factorisation | 0.885 | 0.689 | 1190.862 | 2054.6 |

<p></p>

The next part of the assignment was to use dimensionality reduction techniques to visualize the data. We used three different techniques:
- PCA (Principal Component Analysis)
- t-SNE (t-Distributed Stochastic Neighbor Embedding)
- UMAP (Uniform Manifold Approximation and Projection)

<div class="row">
	<div class="col-sm mt-3 mt-md-0">
		{% include figure.liquid loading="eager" path="assets/img/courses/mining/gender_pca.png" alt="PCA" caption="PCA" %}
	</div>
	<div class="col-sm mt-3 mt-md-0">
		{% include figure.liquid loading="eager" path="assets/img/courses/mining/gender_tsne.png" alt="tSNE" caption="tSNE" %}
	</div>
	<div class="col-sm mt-3 mt-md-0">
		{% include figure.liquid loading="eager" path="assets/img/courses/mining/gender_umap.png" alt="UMAP" caption="UMAP" %}
	</div>
</div>
<div class="caption">
	Visualization
</div>



## Predict Future Sales - Kaggle Competition


