# Macroscopic Market Models

## Introduction
Stochastic differential equations can model various physical, biological, and chemical systems.
For example, the path traced by a molecule as it travels through a liquid or a gas can be modeled as a 
random walk, a type of stochastic differential equation. 
Stochastic Differential Equations (SDEs) are essential tools to simulate asset price dynamics.
They are a top-down approach to simulating market behavior, where markers are treated as a macroscopic system.

In the context of financial systems, the [random walk hypothesis](https://en.wikipedia.org/wiki/Random_walk_hypothesis) postulates that the stock market prices evolve according to a random walk (so price changes are random) and thus cannot be predicted. However, there are 
dueling perspectives on the randomness of stock prices in the finance and economics community. 
[Malkiel](https://en.wikipedia.org/wiki/Burton_Malkiel), in his book [A Random Walk Down Wall Street](https://en.wikipedia.org/wiki/A_Random_Walk_Down_Wall_Street), argues that asset prices typically exhibit signs of a random walk and that investors cannot consistently outperform market averages. On the other hand, in their book [A Non-Random Walk Down Wall Street, Lo and MacKinlay present](https://www.jstor.org/stable/j.ctt7tccx), several studies that suggest there are stock market pricing trends are somewhat predictable. 

To better understand these arguments and build mathematical models that can be used to simulate market 
dynamics, we need to introduce analytical and numerical tools to solve SDEs. Our development will follow the previous work of Glasserman {cite}`Glasserman:2004ua`; in particular, chapters 3, 6, and Appendix B.

__Topics:__

* Scalar and vector {ref}`content:references:wiener-process` 
* Introduction to {ref}`content:references:ito-calculus`
* {ref}`content:references:discretization` to solve stochastic differential equations
---

(content:references:wiener-process)=
## Brownian Motion
A [Wiener Process](https://en.wikipedia.org/wiki/Wiener_process) (also often referred to as a [standard Brownian motion](https://en.wikipedia.org/wiki/Brownian_motion)) is a real-valued continuous-time stochastic process named after the [Norbert Wiener](https://en.wikipedia.org/wiki/Norbert_Wiener) for the study of one-dimensional Brownian motion:

````{prf:definition} One-dimensional Wiener Process
:label: defn-wiener-process

A Wiener process is a continuous one-dimensional stochastic process $\left\{W\left(t\right), 0\leq{t}\leq{T}\right\}$ with the following properties:
* W$\left(0\right)$ = $0$ 
* The increments $\left\{W(t_{1}) - W(t_{o}),\dots, W(t_{k}) - W(t_{k-1})\right\}$ are independent for any $k$ and $0\leq{t_{o}}< t_{1} < \dots < t_{k} \leq{T}$.
* The increment W(t) - W(s) $\sim~N\left(0,t-s\right)$ for any $0\leq{s}< t \leq{T}$, where $N\left(0,t-s\right)$ denotes a [normally distributed random variable](https://en.wikipedia.org/wiki/Normal_distribution) with mean $0$ and variance $t - s$.

````

(content:references:ito-calculus)=
## Ito Processes
We are interested in random variables $X(t)$ whose time evolution is governed by stochastic differential equations of the form ([Ito Process or Ito Diffusion](https://en.wikipedia.org/wiki/It??_diffusion)):

```{math}
:label: eq-ito-process
dX = a(X(t),t)dt + b(X(t),t)dW(t)
```

subject to the (known) constant initial condition $X(0)$. 
Eqn. {eq}`eq-ito-process` is called an [Ito Process or Ito Diffusion](https://en.wikipedia.org/wiki/It??_diffusion). The random variable $X\in\mathbb{R}^{d}$, while the functions 
$a:\mathbb{R}^{d}\times\mathbb{R}\rightarrow\mathbb{R}^{d}$
and $b:\mathbb{R}^{d}\times\mathbb{R}\rightarrow\mathbb{R}^{d\times{m}}$, 
and $W$ denotes an m-dimensional noise process. There are some additional conditions on 
$a$ and $b$ that we will talk about later. 

Depending upon the form of $a$ and $b$, Eqn {eq}`eq-ito-process` can sometimes be solved 
analytically. However, in the general case, we'll need to solve Eqn {eq}`eq-ito-process` 
numerically. Numerical approximations to the solution of Eqn {eq}`eq-ito-process` can be 
developed quickly; however, they have different levels of error depending upon the solution approach.

### Ito's Lemma
A critical theoretical result that supports the construction of analytical solutions to stochastic differential equations is [Ito's Lemma](https://en.wikipedia.org/wiki/It??%27s_lemma); Ito's Lemma,  developed by K. Ito in 1951 [REFHERE], is the analog of the Taylor series for stochastic systems:

````{prf:lemma} Scalar Ito's Lemma
:label: ito-lemma

Let the behavior of the random variable $X(t)$ be governed by the stochastic differential equation:

```{math}
dX = a\left(X(t),t\right)dt + b\left(X(t),t\right)dW(t)
```

where $dW(t)$ is a one-dimensional Wiener process and $a$ and $b$ are functions of $X(t)$ and $t$. 

Let $Y(t) = \phi\left(t,X(t)\right)$ be another process that is a function of $X(t)$ and time $t$, where $\phi\left(t,X(t)\right)$ is twice differentiable with respect to $X(t)$, and singly differentiable with respect to $t$. Then, the process $Y(t)$ is governed by the equation:

```{math}
:label: eq-ito-lemma
dY = \left(\frac{\partial{Y}}{\partial{t}}+a\frac{\partial{Y}}{\partial{X}}+\frac{b^{2}}{2}\frac{\partial^{2}{Y}}{\partial{X}^{2}}\right)dt+b\left(\frac{\partial{Y}}{\partial{X}}\right)dW(t)
```
````


### Ordinary Brownian Motion
Ordinary Brownian Motion (OBM) is a general class of problems involving constant volatility fluctuations around a constant deterministic drift term, i.e., both $a = \mu$ and $b = \sigma>0$ are constants. 

````{prf:definition} Scalar Ordinary Brownian Motion

There exists constants $\mu$ and $\sigma>0$.
Then a random process $X(t)$ follows an Ordinary Brownian Motion (Wiener) process with drift $\mu$ and diffusion $\sigma^{2}$ if $X(t)$ is a solution to the Stochastic Differential Equation (SDE):

```{math}
:label: eq-SDE-StandardBM
dX\left(t\right) = \mu{dt}+\sigma{dW(t)}
```
where $dW(t)$ is a one-dimensional Wiener Process.
````

#### Analytical solution: Ordinary Brownian Motion
The ordinary Brownian motion described by Eqn. {eq}`eq-SDE-StandardBM` 
has an analytical solution. To develop this solution, let's use [Ito's Lemma](https://en.wikipedia.org/wiki/It??%27s_lemma).

````{admonition} Derivation: Analytical Solution Scalar Ordinary Brownian Motion
For Eqn {eq}`eq-SDE-StandardBM`, $a=\mu$ and $b=\sigma>0$. 
If we assume $Y(t) = X(t)$, then [Ito's Lemma](https://en.wikipedia.org/wiki/It??%27s_lemma) gives:

```{math}
dY = {\mu}dt + {\sigma}dW
```

which can be integrated between the time-step $t_{1}\rightarrow{t_{2}}$:

```{math}
Y_{2} - Y_{1} = \mu\left(t_{2}-t_{1}\right)+\sigma\left(W_{2}-W_{1}\right)
```

where $Y_{\star}$ and $W_{\star}$ denote the $Y$ (or $W$) evaluated at time $\star$. 
However, $Y(t) = X(t)$, and the noise is a Wiener process; $W_{2}-W_{1}\sim{N\left(0,t_{2}-t_{1}\right)}$:

```{math}
:label: eq-sbm-soln
X_{2} - X_{1} = \mu\left(t_{2}-t_{1}\right)+\sigma\sqrt{t_2-t_1}\cdot{Z(0,1)}
```

where $Z(0,1)$ is a standard normal random variable with mean $0$ and a variance of $1$. 

Finally, imagine that we are simulating an ordinary Brownian motion from $t = 0\rightarrow{T}$. 
Let's break this interval into $n$ time steps of fixed length $t_{k+1} - t_{k}, k = 1,2,\dots, n$ where $t_1 = 0$. 
Then, we can re-write Eqn. {eq}`eq-sbm-soln` as:

```{math}
:label: eq-sbm-soln-arb-rime
X_{k+1} = X_{k} + \mu\left(t_{k+1}-t_{k}\right)+\sigma\sqrt{t_{k+1}-t_{k}}\cdot{Z(0,1)}\qquad{k=1,2,\dots,n}
```
````

#### Example
* [Simulation of ordinary Brownian motion analytical solution](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-OrdinaryBrownianMotion-Simulation.jl.html)

### Geometric Brownian Motion
Unfortunately, ordinary Brownian motion has a critical flaw; its solutions can be negative. 
Thus, it is not widely used to model the price of a risky asset because asset prices are non-negative. Instead, we often model asset prices using a [Geometric Brownian Motion (GBM) model](https://en.wikipedia.org/wiki/Geometric_Brownian_motion):

````{prf:definition} Scalar Geometric Brownian Motion

There exists constants $\mu$ and $\sigma>0$.
Then a random process $X(t)$ follows a Geometric Brownian Motion (Wiener) process with drift $\mu$ and diffusion $\sigma^{2}$ if $X(t)$ is a solution to the Stochastic Differential Equation (SDE):

```{math}
:label: eq-SDE-GBM
\frac{dX\left(t\right)}{X(t)} = \mu{dt}+\sigma{dW(t)}
```
where $dW(t)$ is a one-dimensional Wiener Process.
````

The use of geometric Brownian motion as a financial model is primarily due to the work of Samuelson in the 1950s and 1960s {cite}`Merton2006`. However, today Geometric Brownian Motion is more often associated with the Black???Scholes options pricing model (which we'll describe later) {cite}`BlackScholes1973`.

#### Analytical solution: Geometric Brownian Motion
The geometric Brownian motion described by Eqn. {eq}`eq-SDE-GBM` also has an analytical solution. 
To develop this solution, let's use [Ito's Lemma](https://en.wikipedia.org/wiki/It??%27s_lemma).

````{admonition} Derivation: Analytical Solution Scalar Geometric Brownian Motion
There exists constants $\mu$ and $\sigma>0$. Let $Y(t) = \ln{X(t)}$. 
Then [Ito's Lemma](https://en.wikipedia.org/wiki/It??%27s_lemma) gives:

```{math}
:label: eq-gdm-soln-anal-almost-1
dY = \left(\mu-\frac{\sigma^{2}}{2}\right)dt+\sigma{dW}
```

Integrating both sides of Eqn {eq}`eq-gdm-soln-anal-almost-1` from $t_{1}\rightarrow{t_{2}}$ gives:

```{math}
:label: eq-gdm-soln-anal-almost-2
Y_{2} - Y_{1} = \left(\mu-\frac{\sigma^{2}}{2}\right)\left(t_{2} - t_{1}\right)+\sigma\left(W_{2} - W_{1}\right)
```

However, $Y(t) = \ln{X(t)}$ and the noise is a Wiener process $W_{2}-W_{1}\sim{N\left(0,t_{2}-t_{1}\right)}$:

```{math}
\ln\left(\frac{X_{2}}{X_{1}}\right) = \left(\mu-\frac{\sigma^{2}}{2}\right)\left(t_{2} - t_{1}\right) + \sigma\sqrt{t_2-t_1}\cdot{Z(0,1)}
```

or:

```{math}
:label: eq-gdm-soln-anal-almost-3
X_{2} = X_{1}\exp\Biggl[\left(\mu-\frac{\sigma^{2}}{2}\right)\left(t_{2} - t_{1}\right) + \sigma\sqrt{t_2-t_1}\cdot{Z(0,1)}\Biggr]
```
Finally, imagine that we are simulating a geometric Brownian motion from $t = 0\rightarrow{T}$. 
Let's break this interval into $n$ time steps of fixed length $t_{k+1} - t_{k}, k = 1,2, \dots, n$ where $t_1 = 0$. 
Then, we can re-write Eqn {eq}`eq-gdm-soln-anal-almost-3` as:

```{math}
:label: eq-gdm-soln-anal-4
X_{k+1} = X_{k}\exp\Biggl[\left(\mu-\frac{\sigma^{2}}{2}\right)\left(t_{k+1} - t_{k}\right) + \sigma\sqrt{t_{k+1}-t_{k}}\cdot{Z(0,1)}\Biggr]
```

where $k=1,2,\dots,n$.

````

````{prf:example} Scalar Geometric Brownian Motion 
:label: scalar-gbm-soln

Let's simulate the daily close price of `AMD` using the analytical solution of the scalar geometric brownian motion ({numref}`fig-gbm-sim-AMD-scalar`). 

The scalar gbm analytical solution was used to generate N = 200 sample paths for a 46-day period (light blue lines in {numref}`fig-gbm-sim-AMD-scalar`); the first 36 days of data were used to estimate the mean return $\mu$ and the volatility of the return $\sigma$ which appear in the gbm solution. These model parameters were assumed to be fixed. An additional two trading weeks (10 days) was then simulated (out of sample prediction). 

```{figure} ./figs/Fig-AMD-GBM-Sim-N200-IS36-OS10.pdf
---
height: 420px
name: fig-gbm-sim-AMD-scalar
---
Scalar Geometric Brownian Motion (GBM) simulation of the daily close price of `AMD`. Data for the first m = 36 days was used to estimate the mean and volatility of the log return. The solid black line denotes the mean close price, while the shaded blue region denotes $\pm$ one standard-deviation from the mean close price. The red-line denotes the actual `AMD` close price.

```

The GDM model _predicts_ (out of sample) the close price of `AMD` too within one standard deviation. However, the difference between the actual close price and the mean predicted close price changes over time. 

source: [live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [static HTML](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-CallPutContract-Payoff.jl.html)

````

(content:references:discretization)=
## Discretization Approaches
In general, we cannot develop an analytical solution to Eqn. {eq}`eq-ito-process`; however, we can create an approximate numerical solution by discretization. This is an issue because sometimes we may want to use more sophisticated models for the price of `XYZ`, for example, a stochastic volatility model that better captures changes in market conditions. 

### Stochastic Volatility Models
For both the standard Brownian motion and the geometric Brownian motion equations, we have assumed that the drift coefficient $\mu$ and the diffusion coefficient $\sigma^{2}$ are constant. There are situations where both $\mu$ and $\sigma$ can reasonably be assumed to be constants, but in many practical cases, this is not true, particularly in the case of $\sigma$. 

## Extension to multiple simultaneous assets
Fill me in.

---

## Summary
Fill me in.