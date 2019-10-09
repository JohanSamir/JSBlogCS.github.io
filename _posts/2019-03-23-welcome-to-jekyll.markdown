---
layout: post
title:  "Human-level control through deep reinforcement learning"
date:   2019-10-08 06:03:36 +0530
categories: Deep-neural-networks Reinforcement-learning
---

Recent years, many AI laboratories are working on studying deep reinforcement learning (DRL) which is expected to be a core technology in the future. I am also engaging in DRL research. Here I will write my survey about the [Human-level control throught deep reinforcement learning paper](http://www.nature.com/nature/journal/v518/n7540/abs/nature14236.html). It proposes a novel artificial agent, termed a deep Q-network, that can learn successful policies directly from high-dimensional sensory inputs using end-to-end reinforcement learning. I will post the most interesting parts of it and also, I will discuss/explain some concepts.


Agents are confronted with a difficult task: **they must derive efficient representations of the environment from high-dimensional sensory inputs, and use these to generalize past experience to new situations.**

Former evidenced by a wealth of neural data revealing notable parallels between the phasic signals emitted by **dopaminergic neurons and temporal difference reinforcement learning**.  [Thorndike, E. L. Animal Intelligence: Experimental studies (Macmillan, 1911)](http://www.nature.com/nature/journal/v518/n7540/abs/nature14236.html)

A deep Q-network (DQN), is able to combine reinforcement learning with a class of artificial neural network known as deep neural networks, **in which several layers of nodes are used to build up progressively more abstract representations of the data**, have made it possible for artificial neural networks to learn concepts such as object categories directly from raw sensory data.

We consider tasks in which the agent interacts with an environment through a sequence of observations, actions and rewards. The goal of the agent is to select actions in a fashion that maximizes cumulative future reward. More formally, **we use a deep convolutional neural network to approximate the optimal action-value function.**  

<p align="center">
<img src="/JSBlogCS.github.io/assets/Images/Humancontrol/1.png" alt="B"  width="370" >
</p>

Reinforcement learning **is known to be unstable or even to diverge when a nonlinear function approximator** such as a neural network is used to represent the action-value.

They address these instabilities with a novel variant of Q-learning, which uses two key ideas.
1. First, we used a biologically inspired mechanism termed experience that randomizes over the data, thereby removing correlations in the observation sequence and smoothing over changes in the data distribution
2. Second, we used an iterative update that adjusts the action-values towards target values that are only periodically updated, thereby reducing correlations with the target.



<p align="center">
<img src="/JSBlogCS.github.io/assets/Images/Humancontrol/2.png" alt="B"  width="370" >
</p>


While other stable methods exist for training neural networks in the reinforcement learning setting, such as **neural fitted Q-iteration, they are too inefficient to be used successfully with large neural networks.** 


The method was able to train large neural networks using a reinforcement learning signal and stochastic gradient descent in a stable manner, illustrated by the temporal evolution of two indices of learning (the **agent’s average score-per-episode and average predicted Q-values**)

In certain games DQN **is able to discover a relatively long-term strategy** (for example, Breakout: the agent learns the optimal strategy, which is to first dig a tunnel around the side of the wall allowing the ball to be sent around the back to destroy a large number of blocks. Nevertheless, games **demanding more temporally extended planning strategies** still constitute a major challenge for all existing agents including DQN (for example, Montezuma’s Revenge).


A single architecture can successfully learn control policies in a range of different environments with only very minimal prior knowledge, receiving only the pixels and the game score as inputs.

The approach incorporates ‘end-to-end’ reinforcement learning that uses reward to continuously shape representations within the convolutional network towards salient features of the environment that facilitate value estimation. **This principle draws on neurobiological evidence that reward signals during perceptual learning may influence the characteristics of representations within primate visual cortex.** [Law, C.-T. & Gold, J. I. Reinforcement learning can account for associative
and perceptual learning on a visual decision task](http://www.nature.com/nature/journal/v518/n7540/abs/nature14236.html) [Sigala, N. & Logothetis, N. K. Visual categorization shapes feature selectivity in the
primate temporal cortex](http://www.nature.com/nature/journal/v518/n7540/abs/nature14236.html)


The successful integration of reinforcement learning with deep network architectures was critically dependent of the incorporation of a **replay algorithm involving the storage and representation of recently experienced transitions**. 

They clipped all positive rewards at 1 and all negative rewards at -1, leaving 0 rewards unchanged. Clipping the rewards in this manner limits the scale of the error derivatives and makes it easier to use the same learning rate across multiple games. They used the RMSProp to perform the optimization process.

They also use a simple frame-skipping technique. More precisely, the agent sees and selects actions on every kth frame instead of every frame, and its last action is repeated on skipped frames. Because the agent only observes the current screen, the task is partially observed.

The agent selects and executes actions according to an e-greedy policy based on Q. 


### Algorithm
<p align="center">
<img src="/JSBlogCS.github.io/assets/Images/Humancontrol/3.png" alt="B"  width="370" >
</p>

<p align="center">
<img src="/JSBlogCS.github.io/assets/Images/Humancontrol/4.png" alt="B"  width="370" >
</p>

The basic idea behind many reinforcement learning algorithms is to estimate the action-value function by using the Bellman equation as an iterative update.

<p align="center">
<img src="/JSBlogCS.github.io/assets/Images/Humancontrol/8.png" alt="B"  width="370" >
</p>