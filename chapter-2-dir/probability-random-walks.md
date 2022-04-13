# Probability, Random Variables and Brownian Motion

## Probability and Random Variables

## Brownian Motion and Random Walks
A one-dimensional Brownian Motion on the interval $\left[0,T\right]$ is a stochastic process $\left\{W\left(t\right), 0\leq{t}\leq{T}\right\}$ with the following properties:
* W$\left(0\right)$ = $0$
* W(t) is continuous
* The increments $\left\{W(t_{1}) - W(t_{o}),\dots, W(t_{k}) - W(t_{k-1})\right\}$ are independent for any $k$ and any $0\leq{t_{o}}< t_{1} < \dots < t_{k} \leq{T}$.
* The increment W(t) - W(s) $\sim~N\left(0,t-s\right)$ for any $0\leq{s}< t \leq{T}$, where $N\left(0,t-s\right)$ denotes a normally distributiom with mean $0$ and variance $t - s$.

For constants $\mu$ and $\sigma>0$, a random process $X(t)$ is said to follow an oridinary Brownian motion process with drift $\mu$ and diffusion coefficient $\sigma^{2}$ if it is a solution to the Stochastic Differential Equation (SDE):

```{math}
:label: eq-SDE-BM
dX\left(t\right) = \mu{dt}+\sigma{dW(t)}
```

Eqn. {eq}`eq-SDE-BM` is one of the simplest models of a random Brownian motion process. For example, Louis Bachelier used this ordinary Brownian motion model to describe stock prices in his pioneering thesis work in 1900
{cite:p}`Bachelier:2006vl`. 

### Ordinary Brownian Process Random Walk









