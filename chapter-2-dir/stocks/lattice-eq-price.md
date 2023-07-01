# Lattice Models of Equity Pricing

```{topic} Outline
In this lecture, we'll discuss our first type of model of equity pricing, namely lattice models. We'll start with this simple model and then add complexity to it in subsequent lectures. In particular, we'll discuss the following topics:

* [Introduction to lattice models](content:lattice-models-introduction). Lattice models discretize the possible furture states of the world, e.g., the share price of a stock, into a finite number of states. For example, a Binomial lattice model has two future states, up and down. We'll discuss how to build a lattice model and how to use it to price assets.

* [Risk-neutral pricing](content:lattice-models-risk-neutral-pricing) is a alternative hypothetical pricing framework that allows us to price assets assuming that investors are risk-neutral. We'll discuss how to use risk-neutral pricing to price assets in a lattice model.

* [Testing the lattice model](content:lattice-models-testing-lattice-model) is an important step in the model building process. We'll discuss how to test the lattice model using real-world versus risk-neutral probabilities. We'll also discuss how to test the lattice model using the implied volatility of options.

```
(content:lattice-models-introduction)=
## Introduction to lattice models
Fill me in.

(content:lattice-models-risk-neutral-pricing)=
## Single-period binomial model
Consider a single-period binomial model which goes from an initial time `0` to a final time `1`. The initial share price at time `0` is $S_{\circ}$ and the share price at time `1` is $S_{1}$. During the transition from time `0`$\rightarrow$`1` the world moves to the `up` state with probability $p$ or the `down` state with probability $1-p$ ({numref}`example-oneste-binomial-lattice-schematic`):



```{figure} ./figs/Fig-OneStep-Binomial-Lattice-Schematic.svg
---
height: 320px
name: example-oneste-binomial-lattice-schematic
---
Schematic of a single-period binomial lattice model. In the future, the world can probabilistically move to the `up` with probability $p$ or the `down` state with probability $(1-p)$. The share price at time `1` is $S_{1}$ and can take on one of two possible values: $S^{u}$ if the world moves to the `up` state, or $S^{d}$ if the world moves to the `down` state.
```

Thus, at time `1` the share price $S_{1}$ can take on one of two possible values: $S^{u} = u\cdot{S_{\circ}}$ if the world moves to the `up` state, or $S^{d} = d\cdot{S_{\circ}}$ if the world moves to the `down` state.
<!-- Finally, let $\bar{r}>0$ denote the annualized risk-free rate (which we approximate as the spot rate of 10-year U.S. 
Treasury notes).  -->

### Real-world probability
Fill me in.

### Risk neutral probability
One of the fundemental assumptions of the risk neutral binomial model is that there are no arbitrage opportunities. In other words, there is no way to make a risk-free profit. This assumption is equivalent to the assumption that the market is complete. In the one-period binomial model described above, the no arbitrage condition is given by:

```{math}
:label: eqn-binomial-no-arbitrage
S^{d} \leq S_{\circ}\cdot\mathcal{D}_{1,0}(\bar{r},\Delta{t})\leq S^{u}
```

where $\mathcal{D}_{1,0}(\bar{r},\Delta{t})$ denotes the discount factor between period `0` and `1`,  $\Delta{t}$ is the length of the time between periods `0` and `1` (in years) , and $\bar{r}$ denotes the annualized risk-free rate. Modeling shares of an equity as a risk neutral asset, e.g., a zero-coupon bond with a random face value, gives the condition:

```{math}
:label: eqn-binomial-no-arbitrage-risk-neutral
\mathcal{D}_{1,0}(\bar{r},\Delta{t})\cdot{S_{\circ}} = \mathbb{E}_{Q}\left(S_{1}\right)
```

where the expectation operator $\mathbb{E}_{Q}(\dots)$ is taken with respect to a _risk neutral probability measure_ $Q$. The risk neutral probability $Q$ is a hypothetical probability measure that allows us to price assets as if investors are risk neutral. In other words, the risk neutral probability measure $Q$ allows us to price assets as if there are no arbitrage opportunities. Because we have a single-period binomial model, we can expand the expectation operator $\mathbb{E}_{Q}(\dots)$ on the right-hand side of Eqn. {eq}`eqn-binomial-no-arbitrage-risk-neutral` as:

```{math}
:label: eqn-binomial-risk-neutral-probability-expectation
\mathcal{D}_{1,0}(\bar{r},\Delta{t})\cdot{S_{\circ}} = q\cdot{S^{u}} + (1-q)\cdot{S^{d}}
```

where $q$ is the risk neutral probability of the share price in the `up` state. We can solve for $q$ to given an expression for the risk neutral probability of the share price being in the `up` state at time `1`:

```{math}
:label: eqn-risk-neutral-probability-exression-almost
q = \frac{\mathcal{D}_{1,0}(\bar{r},\Delta{t})\cdot{S_{\circ}} - S^{d}}{S^{u} - S^{d}}
```

Finally, we can model the `up` and `down` share price as the product of an `up` factor $u$ (or a `down` factor $d$) and the initial share price, i.e., $S^{u} = u\cdot{S_{\circ}}$ and $S^{d} = d\cdot{S_{\circ}}$. Substituting $S^{u}$ (and $S^{d}$) into Eqn. {eq}`eqn-risk-neutral-probability-exression-almost` to arrive at:

```{math}
q = \frac{\mathcal{D}_{1,0}(\bar{r},\Delta{t}) - d}{u - d}
```

Putting these ideas gives us a defintion of the risk-neutral probability ({prf:ref}`defn-risk-neutral-probability`):

````{prf:definition} Risk neutral probability
:label: defn-risk-neutral-probability

Let `0` denote the index of the current state, and `1` denote a one-step ahead future state. The future state exists in one of two possible configurations, an `up` or `down` configuration. The risk neutral probability that the world transitions to the `up` configuration between `0`$\rightarrow$`1` is given by:


```{math}
:label: eqn-risk-neutral-probability-final
q = \frac{\mathcal{D}_{1,0}(\bar{r},\Delta{t}) - d}{u - d}
```

where $\mathcal{D}_{1,0}(\bar{r},\Delta{t})$ denotes the discount factor evaluated using the effective annualized risk free rate $\bar{r}$, $\Delta{t}$ denotes the length of time (in years) between states `0` and `1`, and the factors $u$ and $d$ denote the `up` and `down` factors, respectively. 

````


(content:lattice-models-testing-lattice-model)=
## Real-world versus risk-neutral probabilities
Fill me in.

---

## Summary
Fill me in.