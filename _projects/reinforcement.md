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
toc:
  beginning: true

## Stochastic Windy Gridworld -- Tabular Reinforcement Learning

The Stochastic Windy Gridworld environment is an adaptation of one of the examples in the book {% cite reinforce_book --file external %}. You can see the environment in the figure below. The environment has a 10x7 grid, with a start point denoted by "S" and a goal state denoted by "G". The agent can move in four directions: up, down, left, and right. The environment has a stochastic feature: the wind. The wind blows the agent up one or two additional steps (thin and thick arrows, respectively). The wind is present on 80% of the occasions, making the environment stochastic. The agent receives a reward of -1 at each step, a reward of +40 when reaching the goal state.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/tab_env.png" title="tab_env" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The Stochastic Windy Gridworld environment. The start point is denoted with "S" and the goal state with "G". The arrows indicate the direction of the wind, thicker arrows indicate stronger wind. The agent can move in four directions: up, down, left, and right.
</div>

<!-- Research Question
In this assignment, you will study a range of basic principles in tabular, value-based reinforcement
learning. They serve as a primer for the rest of the course. In particular, we will study the
following topics:
 Dynamic Programming (DP) (Part 1):
We first focus on dynamic programming, which is a bridging method between planning
and reinforcement learning. DP assumes full access to a model of the environment, i.e., we
can get p(s0 |s, a) and r(s, a, s0 ) for any state s and action a. DP is guaranteed to find the
optimal solution, but it 1) requires a model (which is not always available) and 2) suffers
from the curse of dimensionality (which all tabular methods actually do, and to which we
get back later in the course).
 Model-free RL: We next switch to the reinforcement learning setting, where we do not
have access to a model, but can only permanently execute actions from a state, and have
to continue from the resulting next state.
– Exploration (Part 2) The first issue this brings up is exploration versus exploitation:
we need to sometimes try novel things, but at some point also exploit what we know
works well. We will compare two simple ways to ensure exploration: -greedy and a
softmax/Boltzmann policy.
– Back-up: The second main aspect of any RL algorithm is the back-up. We acquired
new information, and want to construct a new estimate of the value of a certain
state-action pair s, a. There are two important considerations when constructing this
back-up:
* Off-policy versus on-policy (Part 3): This difference is best illustrated for
one-step back-ups, for which we will compare Q-learning (off-policy) to SARSA
(on-policy).
* Depth (Part 4): We can also compute deeper back-ups, where we sum more
rewards in a trace. We will compare 1-step back-ups, n-step back-ups, and Monte
Carlo back-ups. -->

The goal of this project was to study a range of basic principles in tabular, value-based reinforcement learning. The first part focused on Dynamic Programming, which is a bridging method between planning and reinforcement learning. In Dynamic Programming, we have full access to a model of the environment, and we can get the transition probabilities and rewards for any state and action. This guarantees that we will find the optimal solution, given enough iterations. 

We implemented the Dynamic Programming algorithm and applied it to the Stochastic Windy Gridworld environment. The figure below shows different iterations of the algorithm. The Q-values converge to the optimal policy, after 18 iterations. In the beginning, we see that the values are low in all states, as the agent has not yet learned the optimal policy. After 10 iterations, the agent has learned to navigate the environment and the Q-values are higher and more stable. After 18 iterations, the agent has learned the optimal policy and the Q-values guide the agent to the goal state, in the fewest number of steps, which is 23.3 steps on average. The fact that this number is not an integer is due to the stochastic nature of the environment.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/iteration_1.png" title="iteration_1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/iteration_10.png" title="iteration_10" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/iteration_18.png" title="iteration_18" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Different iterations of the Dynamic Programming algorithm applied to the Stochastic Windy Gridworld environment.
</div>

The second part of the project focused on Model-free Reinforcement Learning. We implemented two agents: 
- Q-learning
- SARSA
The difference between these two agents is that Q-learning is an off-policy algorithm, while SARSA is an on-policy algorithm. 

For the exploration strategy, we implemented two methods:
- ε-greedy policy
- softmax (Boltzmann) policy
This will help us explore the trade-off between exploration and exploitation by comparing the two methods and the hyperparameters that control the exploration in each method (ε for ε-greedy and temperature for softmax).

Finally we also implemented the n-step back-ups and Monte Carlo back-ups for the Q-learning agent. The n-step back-ups are a generalization of the 1-step back-ups (used by the default Q-learning agent), where we sum more rewards in a trace. The Monte Carlo back-ups are a special case of n-step back-ups, where we sum all rewards until the end of the episode (no bootstrapping).

For the first experiment, we compared the exploration strategies. The figure below shows the results of the experiment. On the left we have three different values of ε for the ε-greedy policy and three different values of the temperature for the softmax policy. We can see that the best performance comes from the two lowest values of the temperature (as good as the Dynamic Programming optimum). For this reason on the figure on the right we experimented with even lower values of ε which now perform almost as good as the softmax policy.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/exploration.png" title="exploration" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/exploration_2.png" title="exploration 2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Exploration experiment. Left: comparison of ε-greedy and softmax policies with different values of ε and temperature. Right: comparison of some lower values of ε.
</div>

For the second experiment, we compared the on-policy (SARSA) and off-policy (Q-learning) algorithms. The figure below shows the results of the experiment. We can see that the Q-learning algorithm performs better than the SARSA algorithm. The off-policy algorithm, means that the agent learns the optimal policy, even if it is not the one that it is following. The on-policy algorithm, means that the agent learns the policy that the agent is following. For this environment, the off-policy training seems to be more effective.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/on_off_policy.png" title="on_off_policy" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/on_off_policy_2.png" title="on_off_policy 2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    On-policy vs. off-policy experiment. Left: comparison of Q-learning and SARSA algorithms for different values of the learning rate (α), using an ε-greedy policy with ε=0.1. Right: comparison of Q-learning and SARSA algorithms using a softmax policy with temperature=0.1.
</div>

The final experiment compared the n-step back-ups and Monte Carlo back-ups for the Q-learning agent. Keep in mind that the 1-step back-ups are identical to the default Q-learning agent. We see the results of the experiment in the figure below. From the results, we can say that the default Q-learning agent (1-step back-ups) performs better than the n-step back-ups and Monte Carlo back-ups. The smaller the n, the better the performance. This is a classic trade-off between bias and variance. The higher the n, the lower the variance, but the higher the bias. For this particular environment, the lower bias of the 1-step back-ups seems to be more beneficial, despite the higher variance.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/depth.png" title="depth" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/depth_2.png" title="depth 2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Depth experiment. Left: comparison of Q-learning agents with 1-step, 3-step, 5-step, and Monte Carlo back-ups, using an ε-greedy policy with ε=0.1. Right: comparison of Q-learning agents with 1-step, 3-step, 5-step, and Monte Carlo back-ups, using a softmax policy with temperature=0.1.
</div>

Finally, we created some cool animations of the agent's behavior in the Stochastic Windy Gridworld environment. The three videos show the agent's behavior at the beginning of training (episodes 3), in the middle of training (episodes 56 and 57), and at the end of training (episodes 179, 180, and 181). The agent uses the Q-learning algorithm with a softmax (Boltzmann) policy with a temperature of 0.01. At the beginning of training, the agent has not yet learned how to navigate the environment and is moving randomly, constantly exploring the world. We have sped up the video 2x because of the many steps the agent takes, to reach the goal state just once. In the middle of training, the agent has greatly improved its performance and is moving more efficiently towards the goal state. It manages to reach the goal state twice within the video. At the end of training, the agent has learned the optimal policy and is moving directly towards the goal state, reaching it in the fewest number of steps. The video is shorter than the other two and yet the agent reaches the goal state three times.

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
    Video animations of the agent's behavior in the Stochastic Windy Gridworld environment. From left to right: beginning of training (episodes 3), middle of training (episodes 56 and 57), and end of training (episodes 179, 180, and 181). The video for the beginning of training has been sped up 2x because of the many steps the agent takes. The agent learns to navigate the environment and reach the goal state while taking into consideration the wind that blows the agent up. The agent was trained using the Q-learning algorithm with a softmax (Boltzmann) policy with a temperature of 0.01.
</div>

The assignment was a great introduction to reinforcement learning and the different algorithms used in the field. We solved the Stochastic Windy Gridworld environment using Dynamic Programming, Q-learning, and SARSA. We also explored various hyperparameters and strategies for exploration, on-policy vs. off-policy algorithms, and different back-ups. The animations of the agent's behavior in the environment were a great way to visualize the agent's learning process and how it improved over time. The full report can be found [here](/assets/pdf/tabular.pdf). The code for the project is not publicly available, as it is part of the course material. If requested, I can provide parts of the code privately.

## Cartpole -- Deep Q-Learning

For the second project, we implemented a Deep Q-Learning agent to solve the Cartpole environment from [OpenAI Gym](https://www.gymlibrary.dev/environments/classic_control/cart_pole/) using PyTorch. The Cartpole environment is a classic control problem from the reinforcement learning literature {% cite control_problems --file external %}. The environment consists of a cart that can move left or right, and a pole that is attached to the cart. The goal is to balance the pole by applying forces to the cart. The agent receives a reward of +1 for every step taken, including the termination step. The episode ends if the pole angle is greater than ±12°, the cart position is greater than ±2.4 (agent reaches the edge of the display), or the episode length is greater than 500 (maximum number of steps). The action space is discrete with two actions: push the cart to the left or push the cart to the right. The observation space consists of four values: cart position, cart velocity, pole angle, and pole angular velocity.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/ablation_study.png" title="ablation_study" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Ablation study of the Deep Q-Learning agent in the Cartpole environment. 
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/egreedy_experiment.png" title="egreedy_experiment" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/egreedy_linear_anneal_experiment.png" title="egreedy_anneal_experiment" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Exploration strategies experiment. Left: comparison of classic ε-greedy. Right: comparison of ε-greedy with annealing.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/boltzmann_experiment.png" title="boltzmann_experiment" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/boltzmann_linear_anneal_experiment.png" title="boltzmann_linear_anneal_experiment" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Exploration strategies experiment. Left: comparison of Boltzmann. Right: comparison of Boltzmann with linear annealing.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/exploration_methods.png" title="exploration_methods" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/comparison_dqn_ddqn.png" title="comparison_dqn_ddqn" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: comparison of exploration methods. Right: comparison of DQN and DDQN.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/parallel_coordinates.png" title="parallel_coordinates" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/slice.png" title="slice" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: parallel coordinates plot. Right: slice plot.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/cart_20.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/cart_200.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
    </div>
</div>
<div class="caption">
    Left: 20 episodes of training. Right: 200 episodes of training.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/cart_400.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/cart_800.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
    </div>
</div>
<div class="caption">
    Left: 400 episodes of training. Right: 800 episodes of training.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/hist_200.png" title="hist_200" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/hist_400.png" title="hist_400" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/reinforce/hist_800.png" title="hist_800" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Histograms of the rewards obtained by the agent during evaluation after 200, 400, and 800 episodes of training.
</div>

<!-- ## Catch -- Actor-Critic -->

## References

{% bibliography --cited_in_order --file external %}