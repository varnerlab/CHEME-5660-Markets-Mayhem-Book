# Stochastic Differential Equations
Stochastic Differential Equations (SDEs) are essential tools to simulate asset price dynamics.
Stochastic differential equations can model various physical, biological, and financial systems.
For example, the path traced by a molecule as it travels through a liquid or a gas can be modeled as a 
random walk, a type of stochastic differential equation. 

In the context of financial systems, the [random walk hypothesis](https://en.wikipedia.org/wiki/Random_walk_hypothesis) postulates that the stock market prices evolve according to a random walk (so price changes are random) and thus cannot be predicted. However, there are 
dueling perspectives on the randomness of stock prices in the finance and economics community. 
[Malkiel](https://en.wikipedia.org/wiki/Burton_Malkiel), in his book [A Random Walk Down Wall Street](https://en.wikipedia.org/wiki/A_Random_Walk_Down_Wall_Street), argues that asset prices typically exhibit signs of a random walk and that investors cannot consistently outperform market averages. On the other hand, in their book [A Non-Random Walk Down Wall Street, Lo and MacKinlay present](https://www.jstor.org/stable/j.ctt7tccx), several studies that suggest there are stock market pricing trends are somewhat predictable. 

To better understand these arguments and build mathematical models that can be used to simulate market 
dynamics, we need to introduce analytical and numerical tools to solve SDEs. Our development will follow the previous work of Glasserman {cite}`Glasserman:2004ua`; in particular, chapters 3, 6, and Appendix B.

__Topics:__

* Scalar and vector {ref}`content:references:wiener-process` 
* Introduction to {ref}`content:references:ito-calculus`
* The {ref}`content:references:discretization` to solve stochastic differential equations
---

(content:references:wiener-process)=
## Brownian Motion
A [Wiener Process](https://en.wikipedia.org/wiki/Wiener_process) (also often referred to as a [standard Brownian motion](https://en.wikipedia.org/wiki/Brownian_motion)) is a real-valued continuous-time stochastic process named after the [Norbert Wiener](https://en.wikipedia.org/wiki/Norbert_Wiener) for the study of one-dimensional Brownian motion:

````{prf:definition} Wiener Process
:label: defn-wiener-process

A Wiener process is a continuous one-dimensional stochastic process $\left\{W\left(t\right), 0\leq{t}\leq{T}\right\}$ with the following properties:
* W$\left(0\right)$ = $0$ 
* The increments $\left\{W(t_{1}) - W(t_{o}),\dots, W(t_{k}) - W(t_{k-1})\right\}$ are independent for any $k$ and $0\leq{t_{o}}< t_{1} < \dots < t_{k} \leq{T}$.
* The increment W(t) - W(s) $\sim~N\left(0,t-s\right)$ for any $0\leq{s}< t \leq{T}$, where $N\left(0,t-s\right)$ denotes a [normally distributed random variable](https://en.wikipedia.org/wiki/Normal_distribution) with mean $0$ and variance $t - s$.

````

(content:references:ito-calculus)=
## Ito Processes
We are interested in random variables $X(t)$ whose time evolution is govered stochastic differential equations of the form ([Ito Process or Ito Diffusion](https://en.wikipedia.org/wiki/Itô_diffusion)):

```{math}
:label: eq-ito-process
dX = a(X(t),t)dt + b(X(t),t)dW(t)
```

subject to the (known) constant initial condition $X(0)$. 
Eqn. {eq}`eq-ito-process` is called an [Ito Process or Ito Diffusion](https://en.wikipedia.org/wiki/Itô_diffusion). The random variable $X\in\mathbb{R}^{d}$, while the functions 
$a:\mathbb{R}^{d}\times\mathbb{R}\rightarrow\mathbb{R}^{d}$
and $b:\mathbb{R}^{d}\times\mathbb{R}\rightarrow\mathbb{R}^{d\times{m}}$, 
and $W$ denotes an m-dimensional noise process. There are some additional conditions on 
$a$ and $b$ that we will talk about later. 

Depending upon the dimension and form of $a$ and $b$, Eqn {eq}`eq-ito-process` can sometimes be solved 
analytically. However, in the general case, we'll need to solve Eqn {eq}`eq-ito-process` 
numerically; numerical approximations to the solution of Eqn {eq}`eq-ito-process` can be 
developed easily; however, they contain different levels of error depending upon the solution approach.

### Standard Brownian Motion
Standard Brownian Motion (SBM) is a general class of problems involving constant volatility fluctuations around a constant deterministic drift term, i.e., both $a = \mu$ and $b = \sigma>0$ are constants. 

````{prf:definition} Scalar Standard Brownian Motion

There exists constants $\mu$ and $\sigma>0$.
Then random process $X(t)$ follows a Standard Brownian Motion (Wiener) process with drift $\mu$ and diffusion $\sigma^{2}$ if $X(t)$ is a solution to the Stochastic Differential Equation (SDE):

```{math}
:label: eq-SDE-StandardBM
dX\left(t\right) = \mu{dt}+\sigma{dW(t)}
```
where $dW(t)$ is a one-dimensional Wiener Process.
````

### Geometric Brownian Motion
Unfortunately, Standard Brownian Motion has a critical flaw; namely, its solution can be negative. 
Thus, it is not widely used to model the price of a risky asset because asset prices are non-negative. Instead, we often model asset prices using a [Geometric Brownian Motion (GBM) model](https://en.wikipedia.org/wiki/Geometric_Brownian_motion):

````{prf:definition} Scalar Geometric Brownian Motion

There exists constants $\mu$ and $\sigma>0$.
Then random process $X(t)$ follows a Geometric Brownian Motion (Wiener) process with drift $\mu$ and diffusion $\sigma^{2}$ if $X(t)$ is a solution to the Stochastic Differential Equation (SDE):

```{math}
:label: eq-SDE-GBM
\frac{dX\left(t\right)}{X(t)} = \mu{dt}+\sigma{dW(t)}
```
where $dW(t)$ is a one-dimensional Wiener Process.
````

The use of geometric Brownian motion as a financial model is primarily due to the work of Samuelson in the 1950s and 1960s {cite}`Merton2006`. However, today Geometric Brownian Motion is more often associated with the Black–Scholes options pricing model (which we'll describe later) {cite}`BlackScholes1973`.

### Stochastic Volatility Models
Fill me in.

(content:references:discretization)=
## Discretization Approaches
