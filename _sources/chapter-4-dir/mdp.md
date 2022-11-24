# Markov decision process (MDPs) 

## Introduction
A Markov decision process (MDP) provides a mathematical framework for modeling decision-making in situations where outcomes are partly random and partly under the control of a decision-maker. MDPs take their name from the Russian mathematician [Andrey Markov](https://en.wikipedia.org/wiki/Andrey_Markov),  as they are an extension of [Markov chains](https://en.wikipedia.org/wiki/Markov_chain), a stochastic model which describes a sequence of possible events in which the probability of each event depends only on the system state in the previous event.

In this lecture:

* We will discuss {ref}`content:references:markov-chains` and discrete time {ref}`content:references:structure-of-an-hmm`, which are approaches for modeling the evolution of a stochastic system as a series of possible events.
* We will also discuss {ref}`content:references:structure-of-an-mdp`, which is an approach for making decisions in a probabilistic world. 

---

(content:references:markov-chains)=
## Markov chains
A Markov chain is a stochastic model describing a sequence of possible events where the probability of each of these events depends only on the system’s current state and not on past system states. A system's state space and time (much like a probability) can be either discrete or continuous; for most of the applications we'll be interested in, we'll focus on discrete time and discrete finite state spaces.

(content:references:discrete-time-markov-chains)=
### Discrete-time Markov chains
A discrete-time Markov chain is a sequence of random variables $X_{1}$, $X_{2}$, $X_{3}$, ..., $X_{n}$ that have the [Markov property](https://en.wikipedia.org/wiki/Markov_property), i.e., the probability of moving to the _next state_ depends only on the _present state_ and not on the _previous states_:

```{math}
:label: eqn-markov-property
P(X_{n+1} = x | X_{1}=x_{1}, \dots, X_{n}=x_{n}) = P(X_{n+1} = x | X_{n}=y)
```

where _states_ refer to a finite set of discrete values in which the system can exist.  If the state space is finite, the transition probability distribution, i.e., the probability of moving from the state(s) $i\rightarrow{j}$, can be encoded in the transition matrix $\mathbf{P}$. Elements of $\mathbf{P}$, denoted as $p_{ij}$, encode the probability of moving from state $i\rightarrow{j}$ during the next time step:

```{math}
:label: eqn-transition-prob-matrix
p_{ij} = P(X_{n+1}~=~j~|~X_{n}~=~i)
```

The transition matrix $\mathbf{P}$ has interesting properties. First, the rows of transition matrix $\mathbf{P}$ must sum to unity, i.e., each row encodes the probability of all possible outcomes. Thus, it must sum to one. Second, if the transition matrix  $\mathbf{P}$ is time-invariant, then $\mathbf{P}$ is the same at each step. This leads to {prf:ref}`obs-n-transition`:

````{prf:observation} Time-invariant state transition
:label: obs-n-transition

A Markov chain have finite state set $\mathcal{S}$ and the time-invariant state transition matrix $\mathbf{P}$. Further, let the state vector at time $j$ be given by $\mathbf{x}_{j}$, where $x_{s,j}\geq{0},\forall{s}\in\mathcal{S}$ and:

```{math}
\sum_{s\in\mathcal{S}}x_{s,j} = 1\qquad\forall{j}
```

Then, the state of the Markov chain at time step $n+1$ is given by:

$$\mathbf{x}_{n+1} = \mathbf{x}_{n}\mathbf{P}^n$$

where $\mathbf{x}_{n}$ denotes the system state vector at time step $n$. 
````

Finally, suppose the Markov chain is both time-invariant and non-periodic. In that case, there exists a unique stationary distribution $\pi$ such that $\mathbf{P}^{k}$ converges to a rank-one matrix in which each row is the stationary distribution $\pi$:

```{math}
\lim_{k\rightarrow\infty} \mathbf{P}^{k} = \mathbf{1}\pi
```

where $\mathbf{1}$ is a column vector of all 1's. Let's consider an example to make these ideas less abstract. 


````{prf:example} Discrete Markov chain simulation
:label: example-dicrete-mchain

 ```{figure} ./figs/Fig-Ex-Discrete-Markov-Model.pdf
---
height: 120px
name: fig-discrete-markov-model
---
Schematic of a discrete two-state time-invariant Markov model; $p_{ij}$ denotes the time-invariant transition probability between state $i$ and $j$.
```

Consider the time-invariant two-state Discrete Markov chain with state transition matrix $\mathbf{P}$:

$$
\mathbf{P} = \begin{bmatrix}
0.9 & 0.1 \\
0.6 & 0.4 \\
\end{bmatrix}
$$

shown in ({numref}`fig-discrete-markov-model`). The transition matrix admits a stationary (non-periodic) solution. As the number of iterations $n$ becomes large the system state converges to a stationary distribution $\pi$; for $n>13$ the stationary distribution $\pi$ is given by:

$$\pi = (0.8571, 0.1428)$$

Thus, regardless of the starting state of this Markov chain, the long-term behavior is given by the stationary distribution $\pi$.

__source__: Fill me in.
````

(content:references:structure-of-an-hmm)=
### Hidden Markov Models (HMMs)
Hidden Markov models (HMMs) are statistical models in which the system being modeled is assumed to be a Markov process with unobservable states but observable outcomes. HMMs have the same structural components as a standard Markov chain model, but each hidden state can be thought of as sending an observable single. HMMs are widely used in many disciplines to model uncertain systems and situations. 

Let's build upon {prf:ref}`example-dicrete-mchain` and construct an HMM that mimics a [CRR binomial lattice](../chapter-3-dir/contracts.md):

````{prf:example} Stationary hidden Markov model
:label: example-dicrete-mchain-hmm

 ```{figure} ./figs/Fig-Ex-Discrete-Hidden-Markov-Model.pdf
---
height: 280px
name: fig-discrete-hidden-markov-model
---
Schematic of a discrete two-state time-invariant hidden Markov model (HMM); $p_{ij}$ denotes the time-invariant transition probability between state $i$ and $j$.
```

Consider the time-invariant two-state Discrete Markov chain with state transition matrix $\mathbf{P}$:

$$
\mathbf{P} = \begin{bmatrix}
0.7 & 0.3 \\
0.6 & 0.4 \\
\end{bmatrix}
$$

shown in ({numref}`fig-discrete-hidden-markov-model`). Let $Y_{1}$ denote the observable value for state 1, while $Y_{2}$ denotes the observable value of
state 2. The transition matrix admits the stationary (non-periodic) stationary distribution $\pi$ given by:

$$\pi = (0.66, 0.33)$$

Suppose the unobservable state $X_{1}$ was the `up` state; when the system is in state 1, we observe an up move of size:

```{math}
u = \exp(\sigma\sqrt{\Delta{t}})
```

On the other hand, let state 2 denote the `down` state; when the system is in state 2, we observe a down move of size:

```{math}
d = \exp(-\sigma\sqrt{\Delta{t}})
```

__Simulation__


 ```{figure} ./figs/Fig-HMM-up-SRA-N250.pdf
---
height: 360px
name: fig-discrete-hidden-markov-model-sim-up
---
Simulation of an asset price governed by $\mathbf{P}$. The solid line denotes the mean predicted price; shaded regions denote the 68% and 95% confidence regions. _parameters_: $S_{o}$ = 100, $\Delta{T}$ = (1/365), $T$ = 45 days and IV = 24.20%. 
The trajectory was computed by sampling a `Categorical` distribution constructed from the HMM stationary distribution.
```

__source__: [download the live Jupyter notebook from GitHub](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks)

````


(content:references:structure-of-an-mdp)=
## Markov decision processes (MDPs)
A Markov decision process (MDP) is an approach for modeling decision-making in situations where outcomes are partly random but also partly under the control of a _decision-maker_ who receives a reward (or penalty) for each decision. Thus, unlike {ref}`content:references:discrete-time-markov-chains`, Markov decision processes (MDPs) involve actions, which allow choice, and rewards that motivate the decision maker.

At each time step, let's assume the system in some state $s$ in a set of possible states $s\in\mathcal{S}$ and the decision maker may choose any action $a$ from a set of possible actions $a\in\mathcal{A}$ that are available in state $s$. The system responds at the next time step by _potentially_ moving into a new state $s^{\prime}$ and rewarding the decision maker $R_{a}\left(s, s^{\prime}\right)$. The probability that the system moves into a new state $s^{\prime}$ depends upon the chosen action $a$ and the current state $s$; this probability is governed by a state transition function $P_{a}\left(s,s^{\prime}\right)$.

````{prf:definition} Markov decision tuple 
:label: defn-formal-mdp

A Markov decision process is the tuple $\left(\mathcal{S}, \mathcal{A}, R_{a}\left(s, s^{\prime}\right), T_{a}\left(s,s^{\prime}\right), \gamma\right)$ where:

* The state space $\mathcal{S}$ is the set of all possible states $s$ that a system can exist in
* The action space $\mathcal{A}$ is the set of all possible actions $a$ that are available to the agent, where $\mathcal{A}_{s} \subseteq \mathcal{A}$ is the subset of the action space $\mathcal{A}$ that is accessible from state $s$.
* An expected immediate reward $R_{a}\left(s, s^{\prime}\right)$ is received after transitioning from state $s\rightarrow{s}^{\prime}$ due to action $a$. 
* The transition $T_{a}\left(s,s^{\prime}\right) = P(s_{t+1} = s^{\prime}~|~s_{t}=s,a_{t} = a)$ denotes the probability that action $a$ in state $s$ at time $t$ will result in state $s^{\prime}$ at time $t+1$
* The quantity $\gamma$ is a _discount factor_; the discount factor is used to weight the _future expected utility_.

Finally, a policy function $\pi$ is the (potentially probabilistic) mapping from states $s\in\mathcal{S}$ to actions $a\in\mathcal{A}$ used by the agent to solve the decision task. 
````

### Policy evaluation
One immediate question that jumps out is what is a policy function $\pi$, and how do we find the best possible policy for our decision problem? To do this, we need a way to estimate how good (or bad) a particular policy is; the approach we use is called _policy evaluation_. Let's denote the expected utility gained by executing some policy $\pi(s)$ from state $s$ as $U^{\pi}(s)$. Then, an _optimal policy_ function $\pi^{\star}$ is one that maximizes the expected utility:

$$\pi^{\star}\left(s\right) = \text{arg max}~U^{\pi}(s)$$

for all $s\in\mathcal{S}$. We can iteratively compute the utility of a policy $\pi$. If the agent makes a single move, the utility will be the reward the agent receives by implementing policy $\pi$:

$$U_{1}^{\pi}(s) = R(s,\pi(s))$$

However, if we let the agent perform two, three, or $k$ possible iterations, we get a _lookahead_ equation which relates the value of 
the utility at iteration $k$ to $k+1$:

$$U_{k+1}^{\pi}(s) = R(s,\pi(s)) + \gamma\sum_{s^{\prime}\in\mathcal{S}}T(s^{\prime} | s, \pi(s))U_{k}^{\pi}(s^{\prime})$$

As $k\rightarrow\infty$ the lookahead utility converges to a stationary value $U^{\pi}(s)$:

````{prf:definition} Value function
:label: defn-policy-evalution

Suppose we have a Markov decision process with the tuple $\left(\mathcal{S}, \mathcal{A}, R_{a}\left(s, s^{\prime}\right), T_{a}\left(s,s^{\prime}\right), \gamma\right)$. Then, the utility of the policy function $\pi$ equals:

```{math}
:label: eqn-converged-policy-eval
U^{\pi}(s) = R(s,\pi(s)) + \gamma\sum_{s^{\prime}\in\mathcal{S}}T(s^{\prime} | s, \pi(s))U^{\pi}(s^{\prime})
```
````

Let's do an example to illustrate policy evaluation:

````{prf:example} Tiger problem
:label: example-MDP-line

 ```{figure} ./figs/Fig-Linear-MDP-Schematic.pdf
---
height: 110px
name: fig-linear-mdp-schematic
---
Schematic of the Tiger problem modeled as an N-state, two-action Markov decision process. A tiger hides behind the red door while freedom awaits behind the green door.
```

An agent trapped in a long hallway with two doors at either end ({numref}`fig-linear-mdp-schematic`). Behind the red door is a tiger (and certain death), while behind the green door is freedom. If the agent opens the red door, the agent is eaten (and receives a large negative reward). However, if the agent opens the green door, it escapes and gets a positive reward. 

For this problem, the MDP has the tuple components:
* $\mathcal{S} = \left\{1,2,\dots,N\right\}$ while the action set is $\mathcal{A} = \left\{a_{1},a_{2}\right\}$; action $a_{1}$ moves the agent one state to the right, action $a_{2}$ moves the agent one state to the left.
* The agent receives a reward of +10 for entering state 1 (escapes). However, the agent is penalized -100 for entering state N (eaten by the tiger).  Finally, the agent is not charged to move to adjacent locations.
* Let the probability of correctly executing the action $a_{j}$ be $\alpha$

Let's compute $U^{\pi}(s)$ for different choices for the policy function $\pi$.

__source__: [download the live Jupyter notebook from GitHub](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks)
````


The utility associated with an optimal policy $\pi^{\star}$ is called the optimal utility $U^{\star}$. 

### Value function policies
{prf:ref}`defn-policy-evalution` gives us a method to compute the utility for a particular policy $U^{\pi}(s)$. 
However, suppose we were given the utility and wanted to estimate the policy $\pi(s)$ from that utility. 
Given a utility $U$, we can estimate a policy $\pi(s)$ using the $Q$-function (action-value function):

```{math}
:label: eqn-action-value-function
Q(s,a) = R(s,a) + \gamma\sum_{s^{\prime}\in\mathcal{S}}T(s^{\prime} | s, a)U(s^{\prime})
```

Equation {eq}`eqn-action-value-function` gives a $|\mathcal{S}|\times|\mathcal{A}|$ array, where the utility is given by:

```{math}
:label: eqn-utility-from-Q
U(s) = \max_{a} Q(s,a)
```

and the policy $\pi(s)$ is:

```{math}
:label: eqn-policy-from-Q
\pi(s) = \text{arg}\max_{a}Q(s,a)
```

### Value iteration
In the previous section, we saw how we could develop _a policy_ $\pi(s)$ by looking at the values in the $Q$-array. However, this required the utility vector; thus, we needed to hypothesize a policy that may not be the _optimal policy_. There are two techniques to compute optimal policies, and we'll explore the simpler of the two, namely _value iteration_. 

In _value iteration_, the value function (the vector of utility values) is updated iteratively using the _Bellman update__ procedure:

```{math}
U_{k+1}(s) = \max_{a}\left(R(s,a) + \gamma\sum_{s^{\prime}\in\mathcal{S}}T(s^{\prime} | s, a)U_{k}(s^{\prime})\right)
```

This procedure is guaranteed to converge to the optimal utility vector (value function).  

````{prf:example} Modified Tiger problem
:label: example-MDP-line-mod

 ```{figure} ./figs/Fig-Branched-MDP-Schematic.pdf
---
height: 300px
name: fig-branched-mdp-schematic-mod
---
Schematic of the Tiger problem modeled as an N-state, four-action (left, right, up, down) Markov decision process. The hallway has three types of paths: unobstructed (white, free), mildly obstructed (light gray, small cost), and obstructed (dark gray, large cost).
```

An agent is trapped in a long hallway with two doors at either end ({numref}`fig-branched-mdp-schematic-mod`). Behind the green door is a tiger (and certain death), while behind the red door is freedom. If the agent opens the green door, the agent is eaten (and receives a large negative reward). However, if the agent opens the red door, it escapes and gets a positive reward. 

For this problem, the MDP has the tuple components:
* $\mathcal{S} = \left\{1,2,\dots,N\right\}$ while the action set is $\mathcal{A} = \left\{a_{1},a_{2}, a_{3}, a_{4}\right\}$; action $a_{1}$ moves the agent one state to the left, action $a_{2}$ moves the agent one state to the right, action $a_{3}$ moves the agent one stop up, and action $a_{4}$ moves the agent one step down.
* The agent receives a positive reward for entering the red state $N$ (escapes). However, the agent is penalized for entering the green state $1$ (eaten by the tiger).  Finally, the agent is not charged to move to adjacent locations if those locations are unobstructed. However, there is a small charge to move through mildly obstructed locations (light gray circles) and a larger charge to move through obstructed areas (dark gray circles).
* Let the probability of correctly executing an action $a_{j}\in\mathcal{A}$ be $\alpha$.

Let's use value iteration to estimate the _optimal policy_ $\pi^{\star}(s)$

__source:__ [download the live Jupyter notebook from GitHub](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks)
````

---

# Summary 
A Markov decision process (MDP) provides a mathematical framework for modeling decision-making in situations where outcomes are partly random and partly under the control of a decision-maker. MDPs take their name from the Russian mathematician [Andrey Markov](https://en.wikipedia.org/wiki/Andrey_Markov),  as they are an extension of [Markov chains](https://en.wikipedia.org/wiki/Markov_chain), a stochastic model which describes a sequence of possible events in which the probability of each event depends only on the system state in the previous event.

In this lecture:

* We discussed {ref}`content:references:markov-chains` and discrete time {ref}`content:references:structure-of-an-hmm`, which are approaches for modeling the evolution of a stochastic system as a series of possible events. We developed a hidden Markov model for the nodes in a binomial lattice model. 
* We also discussed {ref}`content:references:structure-of-an-mdp`, which is an approach for making decisions in a probabilistic world. In particular, we 
introduced tools to compute the utility of a decision-making policy and the value iteration approach for estimating optimal decision-making policies. 