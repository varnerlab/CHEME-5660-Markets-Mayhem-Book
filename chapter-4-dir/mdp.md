# Markov decision process (MDPs) 

## Introduction
A Markov decision process (MDP) provides a mathematical framework for modeling decision-making in situations where outcomes are partly random and partly under the control of a decision-maker. MDPs take their name from the Russian mathematician [Andrey Markov](https://en.wikipedia.org/wiki/Andrey_Markov),  as they are an extension of [Markov chains](https://en.wikipedia.org/wiki/Markov_chain), a stochastic model which describes a sequence of possible events in which the probability of each event depends only on the system state in the previous event.

In this lecture:

* We will discuss {ref}`content:references:markov-chains`, which is an approach for modeling the evolution of a stochastic system as a series of possible events.
* We will discuss {ref}`content:references:structure-of-an-mdp`

---

(content:references:markov-chains)=
## Markov chains
A Markov chain is a stochastic model describing a sequence of possible events where the probability of each of these events depends only on the current state of the system, and not on past system states. A system's state space and time (much like probability) can be either discrete or continuous; for most of the applications we'll be interested in, we'll focus on discrete time and discrete finite state spaces.

(content:references:discrete-time-markov-chains)=
### Discrete time Markov chains
A discrete-time Markov chain is a sequence of random variables $X_{1}$, $X_{2}$, $X_{3}$, ..., $X_{n}$ that have the [Markov property](https://en.wikipedia.org/wiki/Markov_property), i.e., the probability of moving to the _next state_ depends only on the _present state_ and not on the _previous states_:

```{math}
:label: eqn-markov-property
P(X_{n+1} = x | X_{1}=x_{1}, \dots, X_{n}=x_{n}) = P(X_{n+1} = x | X_{n}=y)
```

where _states_ refer to a finite set of discrete values that the system can exist in.  If the state space is finite, the transition probability distribution, i.e., the probability of moving from state(s) $i\rightarrow{j}$, can be encoded in the transition matrix $\mathbf{P}$. Elements of $\mathbf{P}$, denoted as $p_{ij}$, encode the probability of moving from state $i\rightarrow{j}$ during the next time step:

```{math}
:label: eqn-transition-prob-matrix
p_{ij} = P(X_{n+1}~=~j~|~X_{n}~=~i)
```

The transition matrix $\mathbf{P}$ has a few interesting properties. First, the rows of transition matrix $\mathbf{P}$ must sum to unity, i.e., each row encodes the probability of all possible outcomes, thus it must sum to one. Second, if the transition matrix  $\mathbf{P}$ is time invariant, then $\mathbf{P}$ is the same at each step. This leads to {prf:ref}`obs-n-transition`:

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


Finally, if the Markov chain is both time-invarient and non-periodic, there exists a unique stationary distribution $\pi$ such that $\mathbf{P}^{k}$ converges to a rank-one matrix in which each row is the stationary distribution $\pi$:

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



(content:references:structure-of-an-mdp)=
## Markov decision process (MDP)
A Markov decision process (MDP) is an approach for modeling decision-making in situations where outcomes are partly random but also partly under the control of a _decision-maker_ who receives a reward (or penalty) for each decision. Thus, unlike {ref}`content:references:discrete-time-markov-chains`, Markov decision processes (MDPs) involve actions, which allow choice, and rewards that provide motivation for the decision maker.

At each time step, let's assume the system in some state $s$ in a set of possible states $s\in\mathcal{S}$ and the decision maker may choose any action $a$ from a set of possible actions $a\in\mathcal{A}$ that are available in state $s$. The system responds at the next time step by _potentially_ moving into a new state $s^{\prime}$ and rewarding the decision maker $R_{a}\left(s, s^{\prime}\right)$. The probability that the system moves into a new state $s^{\prime}$ depends upon the chosen action $a$ and the current state $s$; this probability is governed by a state transition function $P_{a}\left(s,s^{\prime}\right)$.

````{prf:definition} Markov decision tuple 
:label: defn-formal-mdp

A Markov decision process is the tuple $\left(\mathcal{S}, \mathcal{A}, R_{a}\left(s, s^{\prime}\right), P_{a}\left(s,s^{\prime}\right)\right)$ where:

* The state space $\mathcal{S}$ is the set of all possible states $s$ that a system can exist in
* The action space $\mathcal{A}$ is the set of all possible actions $a$ that are available in the system, where $\mathcal{A}_{s} \subseteq \mathcal{A}$ is the subset of the action space $\mathcal{A}$ that is accessible from state $s$.
* An expected immediate reward $R_{a}\left(s, s^{\prime}\right)$ is recived after transitioning from state $s\rightarrow{s}^{\prime}$ due to action $a$. 
* The term $P_{a}\left(s,s^{\prime}\right) = P(s_{t+1} = s^{\prime}~|~s_{t}=s,a_{t} = a)$ denotes the probability that action $a$ in state $s$ at time $t$ will result in state $s^{\prime}$ at time $t+1$

Finally, a policy function $\pi$ is the (potentially probabilistic) mapping from states $s\in\mathcal{S}$ to actions $a\in\mathcal{A}$ used by a decision maker to recommend an action given the state of the system.

````

Let's do an example to illustrate the MDP components described in {prf:ref}`defn-formal-mdp`.

````{prf:example}
:label: example-MDP-line

Fill me in.

````

---

# Summary 
Fill me in.