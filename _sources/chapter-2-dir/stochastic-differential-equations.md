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
dynamics, we introduce analytical and numerical tools to solve SDEs. Our development follows the previous work of Glasserman {cite}`Glasserman:2004ua`; in particular, chapters 3, 6, and Appendix B.

In this lecture, we will:

* Introduce the {ref}`content:references:ddm`, a fundamental method of valuing the price of a firm's stock
* Introduce {ref}`content:references:wiener-process`, {ref}`content:references:ito-calculus`, {ref}`content:references:ordinary-brownian-motion`, and {ref}`content:references:geometric-brownian-motion`
* Introduce {ref}`content:references:discretization` which can describe more complex asset price trends

---

(content:references:ddm)=
## Dividend Discount Model (DDM)
The [dividend discount model (DDM)](https://en.wikipedia.org/wiki/Dividend_discount_model), developed by [Myron J. Gordon](https://en.wikipedia.org/wiki/Myron_J._Gordon) and Eli Shapiro {cite}`Gordon1959`, is a method of estimating the share price of the firm `XYZ,` based on the net present value of future dividends of the firm ({numref}`fig-ddm-introduction`). Thus, the DDM is only applicable to dividend-granting firms.

```{figure} ./figs/Fig-DDM-Introduction.pdf
---
height: 280px
name: fig-ddm-introduction
---
Schematic of the dividend discount model (DDM) for the share price of `XYZ`. The current value of the share price $P_{1}$ is modeled as the sum of the future dividend payments $D_{j}, j=2,3,\dots,{T}$ and the future share price $P_{T}$ discounted to the current value.  
```

Suppose an investor buys a share of `XYZ` now (t = 0) and holds this share for one year (t = 1). From the perspective of the dividend discount model, the expected current share price of `XYZ`, denoted by $\mathbb{E}(P)$, is the present value of the expected dividend payment $\mathbb{E}(D_{1})$ plus the expected future share price $\mathbb{E}(P_{1})$ during the one year period:

```{math}
:label: eqn-ddm-1-period
\mathbb{E}(P) = \frac{\mathbb{E}(D_{1})+\mathbb{E}(P_{1})}{1+\bar{r}}
```

If the investor holds the share of `XYZ` for additional year, the current expected share price is given by:

```{math}
:label: eqn-ddm-2-period
P = \frac{D_{1}}{\left(1+\bar{r}\right)} + \frac{D_{2}+P_{2}}{\left(1+\bar{r}\right)^2}
```

where we have dropped the expectation $\mathbb{E}(\star)$ notation for clarity. If the investor holds the share of `XYZ` for T-years, we get the expression:

```{math}
:label: eqn-ddm-T-period
P = \sum_{t=1}^{T-1}\frac{D_{t}}{\left(1+\bar{r}\right)^{t}}+\frac{D_{T}+P_{T}}{\left(1+\bar{r}\right)^{T}}
```

There are a few interesting questions with Eqn. {eq}`eqn-ddm-T-period`. First, we don't know the share price of `XYZ` at the final time point $T$; thus, it is unclear how to estimate this value. Further, investors may have different lengths of time they wish to hold the shares. Finally, we don't know the values for the dividend payments over the course of the investment. 

To address these questions, two key simplifications are made to Eqn. {eq}`eqn-ddm-T-period`:
* As the number of periods increases $T\rightarrow\infty$, the final term goes to zero faster than the overall summation. Further, an investor may choose to hold a share of `XYZ` for an indefinate period. Thus, the DDM replaces the finite sum of discounted dividend payments with an infinite sum.

* To describe the dividend payments over the lifetime of the investment, we use propose a constant dividend growth model of the form $D_{j} = D_{o}\left(1+\bar{g}\right)^{j}, ~j=1,2,3,\dots$ where $D_{o}$ denotes the current value of the dividend payment, and $(1+\bar{g})$ denotes the rate of growth of future dividend payments, where $g$ denotes the divdend growth rate.

<!-- where $\mathcal{D}^{-1}_{2,1}$ denotes the discrete discount factor between now, and one period in the future assuming a constant discount factor $\bar{r}$. The discrete discount factor is defined previously, see Eqn. {eq}`eqn-discrete-discount-factor-constant-r` in the [Financial Balances and Abstract Assets](../chapter-1-dir/assets.md) chapter. -->

Putting these ideas together gives the Dividend discount model (DDM), shown in {prf:ref}`defn-ddm-final`:

````{prf:definition} Dividend discount model
:label: defn-ddm-final
The dividend discount model, developed by Shapiro and Gordon  {cite}`Gordon1959`, estimates of the current share price of `XYZ`, denoted by $P$, as the discounted sum of future divedent payments:

```{math}
:label: eqn-general-ddm-almost
P = D_{o}\left(\sum_{t=1}^{\infty}\frac{\left(1+\bar{g}\right)^{t}}{\left(1+\bar{r}\right)^{t}}\right)
```

where $D_{o}$ denotes the current value of the dividend payment, $\bar{g}$ denotes the rate of growth of the dividend payment, which is assumed to be constant, and $\bar{r}$ denotes the discount rate, also assumed constant across the lifetime of the investment. However, Eqn. {eq}`eqn-general-ddm-almost` is difficult to use in practice because of the infinite sum. Thus, Eqn {eq}`eqn-general-ddm-almost` is simplified to arrive at the form of the DDM used in practice:

```{math}
:label: eqn-dd-practice
P = \frac{D_{o}\left(1+\bar{g}\right)}{\left(\bar{r} - \bar{g}\right)}
```

````

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

A critical theoretical result that supports the construction of analytical solutions to stochastic differential equations is [Ito's Lemma](https://en.wikipedia.org/wiki/Itô%27s_lemma); Ito's Lemma,  developed by K. Ito in 1951 [REFHERE], is the analog of the Taylor series for stochastic systems:

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

(content:references:ordinary-brownian-motion)=

### Ordinary Brownian Motion

Ordinary Brownian Motion (OBM) is a general class of problems involving constant volatility fluctuations around a constant deterministic drift term, i.e., both $a = \mu$ and $b = \sigma>0$ are constants.

````{prf:definition} Scalar Ordinary Brownian Motion

There exists scalar constants $\mu$ and $\sigma>0$.
Then a scalar random process $X(t)$ follows an ordinary Brownian motion (Wiener) process with drift $\mu$ and diffusion $\sigma^{2}$ if $X(t)$ is a solution to the stochastic differential equation (SDE):

```{math}
:label: eq-SDE-StandardBM
dX\left(t\right) = \mu{dt}+\sigma{dW(t)}
```
where $dW(t)$ is a one-dimensional Wiener process.
````

#### Analytical solution: Ordinary Brownian Motion

The ordinary Brownian motion described by Eqn. {eq}`eq-SDE-StandardBM`
has an analytical solution. To develop this solution, let's use [Ito's Lemma](https://en.wikipedia.org/wiki/Itô%27s_lemma).

````{prf:observation} Analytical Solution Scalar Ordinary Brownian Motion
For Eqn {eq}`eq-SDE-StandardBM`, $a=\mu$ and $b=\sigma>0$.  If we assume $Y(t) = X(t)$, then [Ito's Lemma](https://en.wikipedia.org/wiki/Itô%27s_lemma) gives:

```{math}
dY = {\mu}dt + {\sigma}dW
```

which can be integrated between the time-step $t_{1}\rightarrow{t_{2}}$:

```{math}
Y_{2} - Y_{1} = \mu\left(t_{2}-t_{1}\right)+\sigma\left(W_{2}-W_{1}\right)
```

 However, $Y(t) = X(t)$, and the noise is a Wiener process; thus, $W_{2}-W_{1}\sim{N\left(0,t_{2}-t_{1}\right)}$:

```{math}
:label: eq-sbm-soln
X_{2} - X_{1} = \mu\left(t_{2}-t_{1}\right)+\sigma\sqrt{t_2-t_1}\cdot{Z(0,1)}
```

where $Z(0,1)$ is a standard normal random variable with a mean of $0$ and a variance of $1$. Finally, imagine we are simulating an ordinary Brownian motion process from $t = 0\rightarrow{T}$. Let's break this interval into $n$ time steps of fixed length $h\equiv{t_{k+1} - t_{k}}, k = 1,2,\dots, n$ where $t_1 = 0$. 
Then, we can rewrite Eqn. {eq}`eq-sbm-soln` as:

```{math}
:label: eq-sbm-soln-arb-rime
X_{k+1} = X_{k} + \mu\left(t_{k+1}-t_{k}\right)+\sigma\sqrt{t_{k+1}-t_{k}}\cdot{Z(0,1)}\qquad{k=1,2,\dots,n}
```
````

````{prf:example} Scalar Geometric Brownian Motion
Let's simulate the time evolution of the random variable $X(t)$, which is governed by ordinary Brownian motion:

$$X_{k+1} = X_{k} + \mu\left(t_{k+1}-t_{k}\right)+\sigma\sqrt{t_{k+1}-t_{k}}\cdot{Z(0,1)}\qquad{k=1,2,\dots,n}$$

Let the parameters $\mu$ = 0.1, $\sigma$ = 0.75 and the initial condition $X_{1}$ = 10.0. The analytical solution was simulated for n = 200 time steps; 100 sample paths were generated. 

```{figure} ./figs/Fig-OBM-Simulation.pdf
---
height: 420px
name: fig-obm-sim-scalar
---
Scalar Ordinary Brownian Motion (OBM) simulation. Several of the sample paths exhibited the pathology of this model, namely solutions that can become negative.

```

__source__: [live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or a [static HTML view](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-OrdinaryBrownianMotion-Simulation.jl.html)

````

(content:references:geometric-brownian-motion)=
### Geometric Brownian Motion

Unfortunately, ordinary Brownian motion has a critical flaw; its solutions can be negative.
Thus, it is not widely used to model the price of a risky asset because asset prices are non-negative. Instead, we often model asset prices using the [Geometric Brownian Motion (GBM) model](https://en.wikipedia.org/wiki/Geometric_Brownian_motion):

````{prf:definition} Scalar Geometric Brownian Motion

There exists constants $\mu$ and $\sigma>0$.
Then a random process $X(t)$ follows a geometric Brownian motion (Wiener) process with drift $\mu$ and diffusion $\sigma^{2}$ if $X(t)$ is a solution of the stochastic differential equation (SDE):

```{math}
:label: eq-SDE-GBM
\frac{dX\left(t\right)}{X(t)} = \mu{dt}+\sigma{dW(t)}
```
where $dW(t)$ is a one-dimensional Wiener Process.
````

The use of geometric Brownian motion as a financial model is primarily due to the work of Samuelson in the 1950s and 1960s {cite}`Merton2006`. However, today Geometric Brownian Motion is more often associated with the Black–Scholes options pricing model (which we'll describe later) {cite}`BlackScholes1973`.

#### Analytical solution: Geometric Brownian Motion

The geometric Brownian motion described by Eqn. {eq}`eq-SDE-GBM` also has an analytical solution.
To develop this solution, let's use [Ito's Lemma](https://en.wikipedia.org/wiki/Itô%27s_lemma).

````{prf:observation} Analytical Solution Scalar Geometric Brownian Motion
There exists constants $\mu$ and $\sigma>0$. Let $Y(t) = \ln{X(t)}$. 
Then [Ito's Lemma](https://en.wikipedia.org/wiki/Itô%27s_lemma) gives:

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

Let's simulate the daily close price of `AMD` using the analytical solution of the scalar geometric Brownian motion ({numref}`fig-gbm-sim-AMD-scalar`). 

The scalar gbm analytical solution was used to generate N = 200 sample paths for 46 days (light blue lines in {numref}`fig-gbm-sim-AMD-scalar`); the first 36 days of data were used to estimate the mean return $\mu$ and the volatility of the return $\sigma$ which appear in the gbm solution. These model parameters were assumed to be fixed. An additional two trading weeks (10 days) were then simulated (out of sample prediction). 

```{figure} ./figs/Fig-AMD-GBM-Sim-N200-IS36-OS10.pdf
---
height: 420px
name: fig-gbm-sim-AMD-scalar
---
Scalar Geometric Brownian Motion (GBM) simulation of the daily close price of `AMD`. Data for the first m = 36 days was used to estimate the mean and volatility of the log return. The solid black line denotes the mean close price, while the shaded blue region denotes $\pm$, one standard deviation from the mean close price. The red line represents the actual `AMD` close price.

```

The GDM model _predicts_ (out of sample) the close price of `AMD` too within one standard deviation. However, the difference between the actual close price and the mean predicted close price changes over time. 

__source__: [live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [static HTML](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-CallPutContract-Payoff.jl.html)

````

### GBM model calibration using market data

#### Approach 1: Price data
Let's start from the analytical solution of the geometric Brownian motion equation between two points in time (Eqn. {eq}`eq-gdm-soln-anal-almost-3`). We know that the time points $t_{\star}$ are arbitrary. Thus, we can define $t_{1}=0$ as a starting point and $t_{2}=t$ as some arbitrary point in the future:

```{math}
:label: eqn-gbm-estimate-sigma
X_{t} = X_{\circ}\exp\left[\left(\mu-\frac{\sigma^{2}}{2}\right)t + \sigma\sqrt{t}\cdot{Z(0,1)}\right]
```

where $X_{\circ}$ denotes an initial price, and $X_{t}$ denotes the asset price at time $t$. Taking the expectation of both sides of Eqn {eq}`eqn-gbm-estimate-sigma`, and using the properties of the expectation for an exponential:

```{math}
\mathbb{E}\left[\exp(a+bZ)\right]=\exp(a+\frac{b^2}{2})
```

gives the expected future price of $X_{t}$:

```{math}
:label: eqn-log-expected-gbm-price
\mathbb{E}\left(X_{t}\right) = X_{o}\exp\left(\mu\cdot{t}\right)
```

However, $\mathbb{E}\left(X_{t}\right)$ is just $X_{t}$; thus, we can take the log of both sides of Eqn. {eq}`eqn-log-expected-gbm-price` to arrive at a linear expression for the growth rate parameter $\mu$:

```{math}
\ln{X_{t}} = \ln{X_{\circ}} + \mu\cdot{t}
```

The parameter $\mu$ is the slope of a linear equation in the natural log of price, where the log of the initial price is the y-intercept. Now that we have an estimate of $\mu$, we can estimate a value for $\sigma$. In particular, the variance of the future price $X_{t}$ is given by:

```{math}
:label: eqn-var-gbm
\text{Var}\left(X_{t}\right) = X_{\circ}^{2}e^{2\mu{t}}\left[e^{\sigma^{2}{t}} - 1\right]
```

While Eqn. {eq}`eqn-var-gbm` is non-linear in $\sigma$, we can estimate this parameter as an optimization problem, e.g., a least-squares or maximum likelihood approach using the variance of historical price measurements, and our estimate of $\mu$.

````{prf:example} Calibration of Scalar Geometric Brownian Motion using Price Data
:label: example-approach-1-calibration-gbm

Fill me in.
````


#### Approach 2: Return data
We can rearrange the recursion relationship for the analytical solution of the geometric brownian motion equation to give:

$$\frac{X_{k+1}}{X_{k}} = \exp\Biggl[\left(\mu-\frac{\sigma^{2}}{2}\right)\left(t_{k+1} - t_{k}\right) + \sigma\sqrt{t_{k+1}-t_{k}}\cdot{Z(0,1)}\Biggr]$$

However, after taking the natural log of both sides we arrive at en expression for the log-return:

```{math}
:label: eqn-log-return-gbm
r_{k+1,k} = \left(\mu-\frac{\sigma^{2}}{2}\right)h + \sigma\sqrt{h}\cdot{Z(0,1)}
```

where $h=t_{k+1} - t_{k}$ denotes the time step, and the log return $r_{k+1,k}$ is given by:

$$r_{k+1,k} = \ln\left(\frac{X_{k+1}}{X_{k}}\right)$$

Thus, if we had the return values $r_{k+1,k}$ computed from price data, we could those values to estimate the $\mu$ and $\sigma$ parameters. However, the return is a random variable, thus, the parameters $\mu$ and $\sigma$ are parameters in a return distribution. 

<!-- ### Extension to multiple simultaneous assets
Fill me in. -->


<!-- ## Discretization Approaches

In general, we cannot develop an analytical solution to Eqn. {eq}`eq-ito-process`; however, we can create an approximate numerical solution by discretization. This is an issue because sometimes we may want to use more sophisticated models for the price of `XYZ`, for example, a stochastic volatility model that better captures changes in market conditions. -->

(content:references:discretization)=
## Stochastic Volatility and Mean Reversion Models
For the standard Brownian and the geometric Brownian motion equations, the drift coefficient $\mu$ and the diffusion coefficient $\sigma^{2}$ are assumed constant. However, in many practical cases, this may not be true, i.e., the drift rate $\mu$ or the diffusion coefficient $\sigma$ may change as a function of time. For example, macroeconomic conditions may change, leading to different price dynamics. Thus, one could imagine modifying the geometric Brownian motion model to capture mean reversion (such as that observed in {prf:ref}`example-approach-1-calibration-gbm`) or constructing a separate model that accounts for the movement of $\sigma$ as a function of time. 

However, these more sophisticated models do not have quickly developed analytical solutions except in rare cases, as was true of ordinary Brownian or Geometric Brownian motions. Thus, we must develop numerical methods to approximate the solutions of these models. There are several approaches to this; however, we'll consider arguably the simplest and the most accessible approach, namely the Euler-Maruyama (EM) method.

### Euler-Maruyama Discretization Method
The [Euler-Maruyama (EM) method](https://en.wikipedia.org/wiki/Euler–Maruyama_method) is an extension to stochastic differential equations (SDEs) of the [Euler method](https://en.wikipedia.org/wiki/Euler_method) used for approximating the solution of ordinary differential equations (ODEs). For the general scalar stochastic differential equation (Wiener noise):

$$dX = a(X,t)dt + b(X,t)dW$$

The EM method gives the approximate solution:

$$X_{k+1} = X_{k} + a(X_{k}, t_{k})h + b(X_{k},t_{k})\sqrt{h}Z\left(0,1\right)$$

where the step size $h=t_{k+1} - t_{k}$ and $Z(0,1)$ denotes a standard normal random variable.  While the EM method is straightforward to implement, it has a poor overall accuracy with error on order $\sqrt{h}$; thus, small step sizes are required to get accurate solutions.

### Ornstein–Uhlenbeck model of mean reversion
The [Ornstein–Uhlenbeck model](https://en.wikipedia.org/wiki/Ornstein–Uhlenbeck_process) model is a type of Brownian motion model with a modified mean-reverting drift term:

```{math}
:label: eqn-ou-model
dX = \theta\left(\mu-X\right)dt + {\sigma}dW
```

where $\theta>0$ is the time-constant controlling the mean reversion, $\mu$ is the long-term price target, and $\sigma>0$ denotes the volatility parameter {cite}`Uhlenbeck1930`. 

#### Numerical solution: Ornstein–Uhlenbeck model
Let's use the [Euler-Maruyama (EM) method](https://en.wikipedia.org/wiki/Euler–Maruyama_method) to discretize the Ornstein–Uhlenbeck model. 
The [Euler-Maruyama (EM) method](https://en.wikipedia.org/wiki/Euler–Maruyama_method) is an extension of the Euler method for ordinary differential equations to stochastic differential equations; thus, it is easy to implement but not accurate unless we use small step-sizes. The EM discretized solution to the [Ornstein–Uhlenbeck model](https://en.wikipedia.org/wiki/Ornstein–Uhlenbeck_process) is given by:

```{math}
:label: eqn-EM-soln-OU-model
X_{k+1} = X_{k} + \theta\left(\mu-X_{k}\right)h + \left(\sigma\sqrt{h}\right)Z(0,1)
```

where $Z(0,1)$ denotes a standard normally distributed random variable, and $h = t_{k+1} - t_{k}$ denotes the fixed time step size, where the subsscript $k$ denotes the time index. 


````{prf:example} Approximate Solution to the Ornstein–Uhlenbeck model
:label: example-OU-model-EM-discrete

Solve the [Ornstein–Uhlenbeck model](https://en.wikipedia.org/wiki/Ornstein–Uhlenbeck_process) model using the [Euler-Maruyuma (EM) method](https://en.wikipedia.org/wiki/Euler–Maruyama_method). The approximate EM solution of the [Ornstein–Uhlenbeck model](https://en.wikipedia.org/wiki/Ornstein–Uhlenbeck_process) model is given by Eqn. {eq}`eqn-EM-soln-OU-model`.

```{figure} ./figs/Fig-Ornstein–Uhlenbeck-EM-solution-N200.pdf
---
height: 420px
name: fig-OU-EM-model-scalar
---
Scalar Euler-Maruyama solution to the Ornstein–Uhlenbeck model with step-size h = 1/365 and duration $\mathcal{D}$ = 800 days. Parameters: $\mu$ = 200 USD/share-time; $\theta$ = 4.0; $\sigma$ = 20.0; $X_{\circ}$ = 144.0 USD/share. 

```

__source__: [live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [HTML static view](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-Soln-Ornstein–Uhlenbeck-model.jl.html)

````

### Heston model of stochastic volatility
The [Heston model](https://en.wikipedia.org/wiki/Heston_model) is an example of a stochastic volatility model in which the volatility parameter controlling the price is described by a random variable whose value is governed by a separate stochastic differential equation {cite}`HESTON1993`. In the [Heston model](https://en.wikipedia.org/wiki/Heston_model), the price $X(t)$ is governed by:

```{math}
:label: eqn-price-heston-model
dX = \mu{X}dt + \left(\sqrt{\nu}\right)X{dW}^{X}
```

where the evolution of the volatility $\nu$ is governed by a separate [Cox–Ingersoll–Ross (CIR)](https://en.wikipedia.org/wiki/Cox–Ingersoll–Ross_model) process:

```{math}
:label: eqn-vol-cir-process
d\nu = \kappa\left(\theta - \nu\right)dt +\left(\xi\sqrt{\nu}\right)dW^{\nu}
```

The [Heston model](https://en.wikipedia.org/wiki/Heston_model) model has multiple parameters; the parameter $\mu$ describes the growth rate in the price equation’s drift term, while $\kappa$, $\theta$ and $\xi$ are the time-constant governing the rate of volatility mean reversion, the long-term volatility and the volatility of the volatility, respectively.  Finally, each equation of the [Heston model](https://en.wikipedia.org/wiki/Heston_model) is driven by a separate potentially correlated Weiner noise process. 

#### Numerical solution: Heston model
The EM discretization of the [Heston model](https://en.wikipedia.org/wiki/Heston_model) gives a price equation of the form:

```{math}
:label: eqn-heston-price-em-discrete
X_{k+1} = X_{k} + \mu{X_{k}}h + \left(\sqrt{\nu_{k}h}\right)X_{k}Z^{X}
```

while the volatility equation is given by:

```{math}
:label: eqn-heston-vol-em-discrete
\nu_{k+1} = \nu_{k} + \kappa\left(\theta - \nu_{k}\right)h + \left(\xi\sqrt{\nu_{k}h}\right)Z^{\nu}
```

where the noise processes $Z^{X}$ and $Z^{\nu}$ are samples from a multivariate normal distribution with mean zero and a covariance matrix $\Sigma$ with entries $\Sigma_{ij}=\sigma_{i}\sigma_{j}\rho_{ij}$. 

````{prf:example} Approximate solution to the Heston model
:label: example-heston-model-EM-discrete

Fill me in.
````

---

## Summary

Fill me in.