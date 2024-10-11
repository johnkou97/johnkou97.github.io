---
layout: page
title: Reinforcement Learning
description: projects from the course 'Reinforcement Learning' at Leiden University
img: assets/img/learning.jpg # Photo by <a href="https://unsplash.com/@santesson89?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Andrea De Santis</a> on <a href="https://unsplash.com/photos/black-and-white-robot-toy-on-red-wooden-table-zwd435-ewb4?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Unsplash</a>
importance: 1
category: courses
related_publications: false
giscus_comments: false
redirect:
pretty_table: true
---

## Stochastic Windy Gridworld -- Tabular Reinforcement Learning

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/tab_2.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/tab_55_56.mp4" class="img-fluid rounded z-depth-1" controls=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/tab_178_179_180.mp4" class="img-fluid rounded z-depth-1" controls=true %}
    </div>
</div>
<div class="caption">
    Video animations of the agent's behavior in the Stochastic Windy Gridworld environment. From left to right: beginning of training (episodes 3), middle of training (episodes 56 and 57), and end of training (episodes 179, 180, and 181). The agent learns to navigate the environment and reach the goal state while taking into consideration the wind that blows the agent up. The agent was trained using the Q-learning algorithm with a softmax (Boltzmann) policy with a temperature of 0.01.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/exploration.png" title="av_digits" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/exploitation_2.png" title="av_digits" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Exploration experiment
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/depth.png" title="av_digits" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/depth_2.png" title="av_digits" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Depth experiment
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/on_off_policy.png" title="av_digits" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/on_off_policy_2.png" title="av_digits" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    On-policy vs. off-policy experiment
</div>


## Cartpole -- Deep Q-Learning



## Catch -- Actor-Critic