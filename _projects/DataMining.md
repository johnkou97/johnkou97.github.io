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

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/uv.png" alt="UV Decomposition" caption="UV Decomposition" %}
	</div>
	<div class="col-sm mt-3 mt-md-0">
		{% include figure.liquid loading="eager" path="assets/img/courses/matrixfactorization_errors.png" alt="Matrix Factorization" caption="Matrix Factorization" %}
	</div>
</div>
<div class="caption">
	Left: UV Decomposition. Right: Matrix Factorization.
</div>

<div class="row">
	<div class="col-sm mt-3 mt-md-0">
		{% include figure.liquid loading="eager" path="assets/img/courses/comparison_time.png" alt="Execution Time" caption="Execution Time" %}
	</div>
	<div class="col-sm mt-3 mt-md-0">
		{% include figure.liquid loading="eager" path="assets/img/courses/comparison_memory.png" alt="Memory Usage" caption="Memory Usage" %}
	</div>
</div>
<div class="caption">
	Left: Execution Time. Right: Memory Usage.
</div>


The table below shows the RMSE, MAE, execution time, and memory usage of each model.

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

## Predict Future Sales - Kaggle Competition


