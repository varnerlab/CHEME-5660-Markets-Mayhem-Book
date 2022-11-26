# Reinforcement Learning (RL)

## Introduction
In our discussion of [Markov decision process (MDPs)](./mdp.md), we assumed that the transition and reward models were known precisely. However, these models may not be discovered in many actual problems. In these cases, the agent must learn to act through experience, e.g., by observing the outcomes of its actions. Then the agent chooses actions that maximize its long-term accumulation of reward. 

Several challenges must be addressed in cases of uncertain models. First, agents must balance between exploring the world and exploiting knowledge gained through experience. Second, rewards may be received long after decisions have been made. Finally, agents must generalize from limited experience. 

In this lecture, we will explore these three challenges. In particular, we will:

* Introduce the {ref}`content:references:basic-concepts-reinforcement-learning` and contrast reinforcement learning with [Markov Decision Processes](./mdp.md)
* Introduce {ref}`content:references:model-based-reinforcement-learning` in which the decision-making agent iteratively builds a model for the world
* Introduce {ref}`content:references:model-free-reinforcement-learning` in which an agent builds a policy directly from interacting with the world

---

 ```{figure} ./figs/Fig-Schematic-RL.pdf
---
height: 280px
name: fig-rl-schematic
---
Schematic of the reinforcement learning (RL) process. An agent takes action $a$ and then observes reward $r$ and changes in the state of the environment ($s\rightarrow{s^{\prime}}$) following the action $a$. 
```


(content:references:basic-concepts-reinforcement-learning)=
## Basic concepts of reinforcement learning
[Reinforcement Learning (RL)](https://en.wikipedia.org/wiki/Reinforcement_learning) agents learn by performing actions in the world and then analyzing the rewards they receive ({numref}`fig-rl-schematic`). Thus, reinforcement learning differs from other machine learning approaches, e.g., [supervised learning](https://en.wikipedia.org/wiki/Supervised_learning) because labeled input/output pairs, e.g., what actions lead to positive rewards are not presented to the agent _a priori_.  

Instead, reinforcement learning agents learn optimal choices in different situations by balancing the exploration of their environment, e.g., by taking random actions and watching what happens, with the exploitation of the knowledge they have built up so far, i.e., choosing what the agent thinks is an optimal action based upon previous experience.  

(content:references:exploration-versus-exploitation)=
### Exploration versus exploitation
Reinforcement learning agents must balance exploration of the environment, e.g., taking random actions with exploiting knowledge already obtained through interacting with the world. Pure exploration allows agents to construct a comprehensive model of their environment, but likely at the expense of positive reward. On the other hand, pure exploitation has the agent continually choosing the action it thinks best to accumulate reward, but different, better actions could be taken. 



(content:references:model-based-reinforcement-learning)=
## Model-based reinforcement learning 
Fill me in.


(content:references:model-free-reinforcement-learning)=
## Model-free reinforcement learning
Unlike {ref}`content:references:model-based-reinforcement-learning`, model-free reinforcement learning does not require us to construct explicit transition and reward models. Instead, model-free methods compute the action value function $Q(s,a)$ directly, e.g., by incrementally estimating the action value function $Q(s,a)$ from samples using the _Q-learning_ approach. 

### Basic Q-learning
The Q-learning approach incrementally estimates the action value function $Q(s,a)$ using the action value form of the _Bellman expectation equation_. 
From our discussion of [Markov decision process (MDPs)](./mdp.md), we know that the action-value function (the $Q$-function) is defined as:

```{math}
Q(s,a) = R(s,a) + \gamma\sum_{s^{\prime}\in\mathcal{S}}T(s^{\prime} | s, a)U(s^{\prime})
```

However, we do know that:

```{math}
U(s) = \max_{a} Q(s,a)
```

thus:

```{math}
:label: eqn-bellman-expectation-eqn
Q(s,a) = R(s,a) + \gamma\sum_{s^{\prime}\in\mathcal{S}}T(s^{\prime} | s, a)\left(\max_{a^{\prime}}Q(s^{\prime},a^{\prime})\right)
```

Here's the catch: in a model-free universe, we don't know the rewards or physics of the world, i.e., we don't know the rewards $R(s,a)$ or the probability array $T(s^{\prime} | s, a)$ that appear in Eqn. {eq}`eqn-bellman-expectation-eqn`. Instead of computing the rewards and transitions from a model we develop, we estimate them from samples received:

```{math}
Q(s,a) = \mathbb{E}_{r,s^{\prime}}\left[r+\gamma\cdot\max_{a^{\prime}}Q(s^{\prime},a^{\prime})\right]
```

#### Incremental Q-table updates
Many model-free methods incrementally estimate the action value function $Q(s, a)$ which is the expectation of reward recieved and the sampled values for the utility. Suppose we are interested in computing the expectation of a single random variable X from $\mathcal{M}$ samples:

```{math}
\hat{x}_{m} = \frac{1}{|\mathcal{M}|}\sum_{i\in\mathcal{M}}x_{i}
```

where $|\mathcal{M}|$ denotes the number of samples in the sample set $\mathcal{M}$. However, we can re-write the sum as:

```{math}
\hat{x}_{m} = \frac{1}{|\mathcal{M}|}\left(x_{m}+\sum_{i\in\mathcal{M}^{-}}x_{i}\right)
```

where $\mathcal{M}^{-}$ denotes the set of samples with the last sample removed.  



--- 

# Summary
Fill me in.