# Reinforcement Learning (RL)

## Introduction
In our discussion of [Markov decision process (MDPs)](./mdp.md), we assumed that the transition and reward models were known precisely. However, in many actual problems, we will encounter, these models have yet to be discovered exactly. In these cases, the agent must learn to act through experience, e.g., by observing the outcomes of its actions. Then the agent chooses actions that maximize its long-term accumulation of reward. Decisions problems where the underlying models are uncertain is explored in a field called [Reinforcement Learning (RL)](https://en.wikipedia.org/wiki/Reinforcement_learning).

Several challenges must be addressed in cases of uncertain models. First, agents must balance between exploring the world and exploiting knowledge gained through experience. Second, rewards may be received long after decisions have been made. Finally, agents must generalize from limited experience. 

In this lecture, we will explore these three challenges. In particular, we will:
Fill me in.

---


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

(content:references:exploration-versus-exploitation)=
#### Exploration versus exploitation
Fill me in.

(content:references:model-based-reinforcement-learning)=
## Model-based reinforcement learning 
Fill me in.

--- 

# Summary
Fill me in.