# Stochastic Processes

```{topic} Outline
In this section, we will discuss the following topics:

* Introduce {ref}`content:references:wiener-process` which is a continuous-time stochastic process that can be used to model asset price dynamics
* Introduce {ref}`content:references:discretization` which can describe more complex asset price trends
```

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
dynamics, we introduce analytical and numerical tools to solve SDEs. Our development follows chapters 3, 6, and Appendix B of {cite}`Glasserman:2004ua`


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
We are interested in random variables $X(t)$ whose time evolution is governed by stochastic differential equations of the form ([Ito Process or Ito Diffusion](https://en.wikipedia.org/wiki/Itô_diffusion)):

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

Depending upon the form of $a$ and $b$, Eqn {eq}`eq-ito-process` can sometimes be solved
analytically. However, in the general case, we'll need to solve Eqn {eq}`eq-ito-process`
numerically. Numerical approximations to the solution of Eqn {eq}`eq-ito-process` can be
developed quickly; however, they have different levels of error depending upon the solution approach.

### Ito's Lemma
A critical theoretical result that supports the construction of analytical solutions to stochastic differential equations is [Ito's Lemma](https://en.wikipedia.org/wiki/Itô%27s_lemma); Ito's Lemma,  developed by K. Ito in 1951, is the analog of the Taylor series for stochastic systems:

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

(content:references:discretization)=
## Discretization Approaches
In general, we cannot develop an analytical solution to Eqn. {eq}`eq-ito-process`; however, we can create an approximate numerical solution by discretization. This is an issue because sometimes we may want to use more sophisticated models for the price of `XYZ`, for example, a stochastic volatility model that better captures changes in market conditions. 

### Euler-Maruyama Discretization Method
The [Euler-Maruyama (EM) method](https://en.wikipedia.org/wiki/Euler–Maruyama_method) is an extension to stochastic differential equations (SDEs) of the [Euler method](https://en.wikipedia.org/wiki/Euler_method) used for approximating the solution of ordinary differential equations (ODEs). For the general scalar stochastic differential equation (Wiener noise):

$$dX = a(X,t)dt + b(X,t)dW$$

The EM method gives the approximate solution:

$$X_{k+1} = X_{k} + a(X_{k}, t_{k})h + b(X_{k},t_{k})\sqrt{h}Z\left(0,1\right)$$

where the step size $h=t_{k+1} - t_{k}$ and $Z(0,1)$ denotes a standard normal random variable.  While the EM method is straightforward to implement, it has a poor overall accuracy with error on order $\sqrt{h}$; thus, small step sizes are required to get accurate solutions.