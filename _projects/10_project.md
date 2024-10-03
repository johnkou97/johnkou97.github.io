---
layout: page
title: Gravitational Wave Hackathon
description: g2net hackathon in Malta (2020) and Thessaloniki (2023)
img: assets/img/gravitational.jpg # image taken from www.ligo.caltech.edu/video/gravitational-waves
importance: 2
category: personal
related_publications: false
giscus_comments: false
redirect:
---

I have had the pleasure to participate in two hackathons related to gravitational waves as part of the workshops organized by the [network for Gravitational Waves, Geophysics and Machine Learning (G2Net)](https://www.g2net.eu/). The first one was in Malta in 2020 where I participated in person and the second one was in Thessaloniki in 2023 where I participated remotely. The hackathons were a great opportunity to learn more about the field of gravitational waves and machine learning, and to meet other researchers in the field.

## Malta 2020

The data used for the challenge contains earthquake from all over the world, together with noise (non-earthquake ambient noise). Earthquakes are very similar to gravitational waves, and in this context, have no meaningful difference. The goal of this challenge is to correctly classify an unknown set of data using any model that was trained on a provided dataset where the correct labels are provided. The full dataset is available on [Kaggle](https://www.kaggle.com/datasets/zerafachris/g2net-training-school-hackaton)

For each element in the dataset, the following information is provided:
- `trace_id`: the unique identifier of the trace
- `receiver_latitude`: the latitude of the receiver
- `receiver_longitude`: the longitude of the receiver
- `receiver_elevation_m`: the elevation of the receiver
- `p_arrival_sample`: the sample of the P arrival
- `p_travel_sec`: the travel time of the P arrival
- `s_arrival_sample`: the sample of the S arrival
- `source_origin_time`: the origin time of the source
- `source_latitude`: the latitude of the source
- `source_longitude`: the longitude of the source
- `source_depth_km`: the depth of the source
- `snr_db_E`: the signal-to-noise ratio of the E component
- `snr_db_N`: the signal-to-noise ratio of the N component
- `snr_db_Z`: the signal-to-noise ratio of the Z component
- `E`: the E component (6000 samples)
- `N`: the N component (6000 samples)
- `Z`: the Z component (6000 samples)

Each element is labeled as one of the following classes:
- `0`: Noise
- `1`: Near_Small
- `2`: Near_Medium
- `3`: Near_Large
- `4`: Far_Small
- `5`: Far_Medium
- `6`: Far_Large

I used two different approaches to classify the data: an ensemble method and a convolutional neural network (CNN). The ensemble method is based on the AdaBoost algorithm, which combines multiple weak classifiers to create a strong classifier. The CNN is a deep learning model that is able to learn features from the data and classify it accordingly.

For the optimization of the CNN model, I used the `Optuna` library to search for the best hyperparameters. The hyperparameters that were optimized include the learning rate, dropout rate, regularization rate, and the batch size. For the training, I used 50 epochs with early stopping based on the validation loss. The model was trained on the training data and validated on the validation data. The loss and accuracy of the training and validation data were monitored during the training process and shown in the plots below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/personal/loss.png" title="loss" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Loss of the training and validation data during the training process.
</div>

The results of the challenge were evaluated based on the accuracy of the predictions. The CNN model greatly outperformed the AdaBoost model, which was not able to achieve a high accuracy. The results of the CNN model are shown in the table below:

| Metric           | Score |
|------------------|-------|
| Precision        | 79.5% |
| Recall           | 79.6% |
| F1-score         | 79.5% |
| Balanced accuracy| 79.6% |

For better understanding of the results, the confusion matrix is shown below:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/personal/confusion_matrix_nn.png" title="confusion matrix" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Confusion matrix of the CNN model.
</div>

Overall, the hackathon in Malta was a great experience and I learned a lot about the field of gravitational waves and machine learning. It was one of my first experiences with deep learning and looking back (especially on the code), I see how much I have learned since then. For the full code of the project and instructions on how to run it, please visit the [GitHub repository](https://github.com/johnkou97/g2net_malta_hackaton/) of the project.

## Thessaloniki 2023



