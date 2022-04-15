# Ordinary Brownian Motion (OBM)
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

Eqn. {eq}`eq-SDE-BM` is one of the simplest models of a random Brownian motion process. For example, Louis Bachelier used an ordinary Brownian motion model to describe stock prices in his pioneering thesis work in 1900
{cite:p}`Bachelier:2006vl`. 

## Simulating an Ordinary Brownian Random Walk
Brownian motion simulations e.g., stock price simulations, mostly focus on computing values of the noise $W(t_{1}),W(t_{2}),\dots,W(t_{n})$ and
the state $X(t_{1}), X(t_{2}), \dots, X(t_{n})$ at a set of discrete time points $0 < t_{1} < t_{2} < \dots < 
t_{n}$. Let $Z_{1},\dots,Z_{n}$ denote independent standard normal random variables. For an oridinary Brownian motion, where $t_{o} = 0$ and $W(0) = 0$, the solution to Eqn. {eq}`eq-SDE-BM` can be approximatred using the 
[Euler–Maruyama method](https://en.wikipedia.org/wiki/Euler–Maruyama_method) which gives the recurrence relationship:


```{math}
:label: eq-SDE-BM-Euler
X_{i+1} = X_{i}+\mu\left(t_{i+1} - t_{i}\right)+\left(\sigma\sqrt{t_{i+1} - t_{i}}\right)Z_{i+1}\qquad{i=0,1,\dots,n-1}
```

where $X_{i+1}$ denotes the state random variable evaluated at time index $i+1$. In Eqn. {eq}`eq-SDE-BM-Euler`, both $\mu$ and $\sigma$ are assumed to be constants, and:

$$W_{i+1} = W_{i} + \left(\sqrt{t_{i+1} - t_{i}}\right)Z_{i+1}\qquad{i=0,1,\dots,n-1}$$

