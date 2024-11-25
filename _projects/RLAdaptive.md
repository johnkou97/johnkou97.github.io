---
layout: page
title: Model-Free Reinforcement Learning for Sensorless Adaptive Optics
description: research project on Advanced Reinforcement Learning
img: assets/img/optics.gif
importance: 3
category: research
related_publications: false
giscus_comments: false
redirect:
---

This project started as part of the course "Seminar Advanced Reinforcement Learning" at Leiden University. You can find the final report [here](/assets/pdf/RLAdaptive.pdf). The code is open-source and available on my [GitHub repository](https://github.com/johnkou97/AdaptiveOptics).

We have presented the project at the [BNAIC/BeNeLearn 2024](https://bnaic2024.sites.uu.nl/) conference with a poster. See the pictures below! You can also find the poster in [pdf format](/assets/pdf/RL_poster.pdf).

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/BNAIC24_poster.png" title="poster" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/RL_poster.png" title="poster_pers" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Poster presented at the BNAIC/BeNeLearn 2024 conference. Right: Me with the poster.
</div>

## Introduction

Adaptive optics (AO) is a technique used to correct for disturbances in optical systems, by adjusting a set of deformable mirrors (DM). The system consists of a wavefront sensor, a deformable mirror, and a control algorithm. The wavefront sensor measures the aberrations in the light path, the control algorithm calculates the commands to send to the deformable mirror to correct the aberrations, and the deformable mirror reshapes to correct the aberrations. Controlling a telescope's DM is a high-dimensional decision problem that follows a constant loop of adjusting mirrors and checking the adjustment's effect on the acquired image. Due to the sequential nature of this process and a clearly defined goal measure (reducing the noise), prior work increasingly focused on applying reinforcement learning (RL) to AO control {%cite Durech:21 landman2021self nousiainen2021adaptive parvizi2023reinforcement photonics10121371 Pou:22 --file external %}.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/ao_system.png" title="AO system" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/star_1.png" title="star" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/star_2.png" title="star" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Schematic depiction of an Adaptive Optics system. Middle: Image of a double star system without AO. Right: Image of the same double star system with AO.
</div>

In this work, we demonstrate that RL can also be used for sensor-free AO control in the context of astronomical imaging. We argue that this approach is advantageous, as it reduces the overall system complexity by removing the sensor component and with it any potential noise or bias such a sensor can introduce.

## Methodology

The number of mirrors in an AO can be high, thus creating a high-dimensional space. Atmospheric distortions can be described using a set of Zernike polynomials {%cite 2004aoa --file external %}. We can therefore use the same polynomials to shape the set of DM and correct aberrations. This way we are able to naturally capture the action space dimensionality (to the number of used polynomials).

We use [Soft Actor-Critic (SAC)](https://stable-baselines3.readthedocs.io/en/master/modules/sac.html) from the [Stable Baselines3](https://stable-baselines3.readthedocs.io/en/master/index.html) library. SAC is an off-policy algorithm that uses a maximum entropy reinforcement learning framework. It is well-suited for continuous action spaces and has shown to be effective in a variety of environments. We use the implementation from the library and adapt it to our environment. Our implementation and the full paper can be accessed via [GitHub](https://github.com/johnkou97/AdaptiveOptics).

## Environments

We have used several environments to train the agents. The environments are based on the Adaptive Optics system. The Adaptive Optics system is a system that corrects the aberrations in the light path caused by the atmosphere. The system consists of a wavefront sensor, a deformable mirror, and a control algorithm. The wavefront sensor measures the aberrations in the light path, the control algorithm calculates the commands to send to the deformable mirror to correct the aberrations, and the deformable mirror reshapes to correct the aberrations.

The environment we use has the focal image of the telescope as the observation space, and the reward function is a measure of image sharpness. The action space is continuous with the dimensionality depending on the number of Zernike modes used. To simplify the problem, atmosphere distortions are filtered so that they can always be described using the same number of Zernike modes that define the action dimensionality. This makes the environment harder to solve as we increase the number of Zernike modes used. Higher degrees of the polynomials produce smaller distortions, which means that after a certain point, further increasing the number of modes will not make any significant difference to the environment and the filtering will no longer play a crucial role.


### Image sharpening

The goal of this environment is to maximize the Strehl ratio based on focal plane images. 

- **Observation**: The observed (noisy) image intensity in the focal plane. The image is normalized such that the values are always between 0 and 1. The image has a size of 96x96 pixels.
- **Action**: An array of commands to send to the actuators to reshape the deformable mirror. This is in units of radians and should have an absolute value smaller than 0.3 to avoid divergence. Default is 400 actuators.
- **Reward**: The Strehl ratio, which is a measure of image sharpness and is between 0 and 1.
- **Things to consider**: 
    * Partially observable Markov decision process: twin image problem  (image intensity and not the electric field)
    * Possible solution: provide the agent a history of observations and commands or through the use of agents that have intrinsic memory

### Dark hole 

The goal of this environment is to remove starlight from a small region if the image. 

- **Observation**: A measurement with information about the electric field in the dark hole region. The shape is N_probes x N_pixels, default is 5 x 499.
- **Action**: An array of commands to send to the actuators to reshape the deformable mirror. This is in units of radians and should have an absolute value smaller than 0.3 to avoid divergence. Default is 400 actuators.
- **Reward**: The log of the contrast (mean of the image intensity in the dark hole region divided by the peak intensity of the starlight).

### Image sharpening easy

The goal of this environment is to maximize the Strehl ratio based on focal plane images like in the image sharpening environment. The difference is that the aberrations from the atmosphere can always be corrected by the zernike modes of the deformable mirror. 

- **Observation**: The observed (noisy) image intensity in the focal plane. The image is normalized such that the values are always between 0 and 1. The image has a size of 96x96 pixels.
- **Action**: An array of commands to send to the actuators to reshape the deformable mirror. This is in units of radians and should have an absolute value smaller than 0.3 to avoid divergence. Default is with 20 modes of zernike.
- **Reward**: The Strehl ratio, which is a measure of image sharpness and is between 0 and 1.


### Image centering

The goal of this environment is to minimize the distance between the center of the image and the center of the focal plane.

- **Observation**: The observed (noisy) image intensity in the focal plane. The image is normalized such that the values are always between 0 and 1. The image has a size of 96x96 pixels.
- **Action**: An array of commands to send to the actuators to reshape the deformable mirror. This is in units of radians and should have an absolute value smaller than 0.3 to avoid divergence. For this environment we only use 2 zernike modes (tip and tilt) to correct the aberrations.
- **Reward**: The negative of the distance between the center of the image and the center of the focal plane.

## Results

We use Weights & Biases to track the results of the experiments. 

### Centering

Find the training results [here](https://api.wandb.ai/links/adapt_opt/gbkd3qfs).


We evaluate each agent on 1000 episodes. Each episode is 100 steps long.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/centering.png" title="centering" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/evaluation_centering.png" title="evaluation_centering" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Learning curves for the different agents trained on the centering environment. Right: Evaluation of the best performing agent on 1000 episodes of 100 steps and comparison to the baseline.
</div>

### Sharpening easy

We have trained agents on the sharpening easy environment with 2 and 5 and 9 zernike modes.
Reminder that for this environment the aberrations can always be corrected by the zernike modes of the deformable mirror that we use each time.

Find the training results [here](https://api.wandb.ai/links/adapt_opt/5y122g06).

#### Evaluation for 2 zernike modes

We evaluate each agent on 1000 episodes. Each episode is 100 steps long. 

We also evaluate the best performing agent on 10000 episodes of 100 steps and compare it to the performance of the baseline.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/easy_2zer.png" title="easy_2zer" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/evaluation_Sharpening.png" title="evaluation_Sharpening" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/evaluation_Sharpening-2.png" title="evaluation_Sharpening-2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Learning curves for the different agents trained on the sharpening easy environment with 2 zernike modes. Middle: Evaluation of all agents on 1000 episodes of 100 steps. Right: Evaluation of the best performing agent on 10000 episodes of 100 steps and comparison to the baseline.
</div>

#### Evaluation for 5 zernike modes

We evaluate each agent on 1000 episodes. Each episode is 100 steps long.

We also evaluate the best performing agent on 10000 episodes of 100 steps and compare it to the performance of the baseline.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/easy_5zer.png" title="easy_5zer" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/evaluation_Sharpening-6act.png" title="evaluation_Sharpening-6act" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/evaluation_Sharpening-6act-2.png" title="evaluation_Sharpening-6act-2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Learning curves for the different agents trained on the sharpening easy environment with 5 zernike modes. Middle: Evaluation of all agents on 1000 episodes of 100 steps. Right: Evaluation of the best performing agent on 10000 episodes of 100 steps and comparison to the baseline.
</div>

#### Evaluation for 9 zernike modes

We evaluate each agent on 1000 episodes. Each episode is 100 steps long.

We also evaluate the best performing agent on 10000 episodes of 100 steps and compare it to the performance of the baseline.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/easy_9zer.png" title="easy_9zer" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/evaluation_Sharpening-10act.png" title="evaluation_Sharpening-10act" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/evaluation_Sharpening-10act-2.png" title="evaluation_Sharpening-10act-2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Learning curves for the different agents trained on the sharpening easy environment with 9 zernike modes. Middle: Evaluation of all agents on 1000 episodes of 100 steps. Right: Evaluation of the best performing agent on 10000 episodes of 100 steps and comparison to the baseline.
</div>

#### Evaluation for 14 zernike modes

We evaluate each agent on 1000 episodes. Each episode is 100 steps long.

We also evaluate the best performing agent on 10000 episodes of 100 steps and compare it to the performance of the baseline.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/easy_14zer.png" title="easy_14zer" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/evaluation_Sharpening-15act.png" title="evaluation_Sharpening-15act" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/evaluation_Sharpening-15act-2.png" title="evaluation_Sharpening-15act-2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Learning curves for the different agents trained on the sharpening easy environment with 14 zernike modes. Middle: Evaluation of all agents on 1000 episodes of 100 steps. Right: Evaluation of the best performing agent on 10000 episodes of 100 steps and comparison to the baseline.
</div>

#### Evaluation for 20 zernike modes

We evaluate each agent on 1000 episodes. Each episode is 100 steps long.

We also evaluate the best performing agent on 10000 episodes of 100 steps and compare it to the performance of the baseline.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/easy_20zer.png" title="easy_20zer" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/evaluation_Sharpening-21act.png" title="evaluation_Sharpening-21act" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/evaluation_Sharpening-21act-2.png" title="evaluation_Sharpening-21act-2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Learning curves for the different agents trained on the sharpening easy environment with 20 zernike modes. Middle: Evaluation of all agents on 1000 episodes of 100 steps. Right: Evaluation of the best performing agent on 10000 episodes of 100 steps and comparison to the baseline.
</div>

#### Evaluation for 27 zernike modes

Since we only trained one agent for 27 zernike modes, we evaluate it on 10000 episodes of 100 steps and compare it to the performance of the baseline.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/easy_27zer.png" title="easy_27zer" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/adaptive/evaluation_Sharpening-28act.png" title="evaluation_Sharpening-28act" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Learning curve for the agent trained on the sharpening easy environment with 27 zernike modes. Right: Evaluation of the agent on 10000 episodes of 100 steps and comparison to the baseline.
</div>


## Animations

### Centering

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/center.mp4" class="img-fluid rounded z-depth-1" controls=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/center_no_agent.mp4" class="img-fluid rounded z-depth-1" controls=true %}
    </div>
</div>
<div class="caption">
    Left: Centering with the agent. Right: Centering without the agent.
</div>

### Sharpening easy with 20 zernike modes

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/sharp.mp4" class="img-fluid rounded z-depth-1" controls=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/sharp_no_agent.mp4" class="img-fluid rounded z-depth-1" controls=true %}
    </div>
</div>
<div class="caption">
    Left: Sharpening easy with the agent. Right: Sharpening easy without the agent.
</div>

## Discussion and Conclusion

This work serves as a proof-of-concept for the suitability of RL for controlling sensorless AO systems. Using an environment with controlled action dimensionality and noise, we iteratively increased complexity and achieved success for up to 27 Zernike modes. While this does not match the full complexity of real-world AO systems, it proves that RL can, in principle, effectively control sensorless AO.

We see our work as a promising first step towards RL-based AO control. Future work could build on this and, for example, explore a curriculum learning approach where an agent starts learning a simple task and gradually evolves towards solving the full task. Additionally, we see value in comparing our method to that of a sensor-based approach or testing how it performs on a real-world telescope.

## References

{% bibliography --cited_in_order --file external %}