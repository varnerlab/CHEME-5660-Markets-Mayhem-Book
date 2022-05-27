# Random Walks and Brownian Motion
A random walk is a stochastic process that consists of a succession of random steps.
Random walks can model a wide variety of physical, biological, and financial systems.
For example, the path traced by a molecule as it travels in a liquid or a gas can be modeled as a 
random walk. In the context of financial systems, the [random walk hypothesis](https://en.wikipedia.org/wiki/Random_walk_hypothesis) postulates that the stock market prices evolve according to a random walk (so price changes are random) and thus cannot be predicted. 

There are 
dueling perspectives on the randomness of stock prices in the finance and economics community. 
[Malkiel](https://en.wikipedia.org/wiki/Burton_Malkiel), in his book [A Random Walk Down Wall Street](https://en.wikipedia.org/wiki/A_Random_Walk_Down_Wall_Street), argues that asset prices typically exhibit signs of a random walk and that one cannot consistently outperform market averages. On the other hand, in their book [A Non-Random Walk Down Wall Street], Lo and MacKinlay present [https://www.jstor.org/stable/j.ctt7tccx) several
studies that suggest there are stock market pricing trends are somewhat predictable. 

In this chapter, we'll introduce random walks and a particular type of stochastic process called a
[Wiener Process](https://en.wikipedia.org/wiki/Wiener_process) that underlies [Finanical Brownian Motion](https://en.wikipedia.org/wiki/Brownian_model_of_financial_markets). In particular, we'll introduce:

* The one dimensional {ref}`content:references:wiener-process` that can be used to construct a random walk
* The {ref}`content:references:ordinary-brownian-motion` model for asset prices
* The basics of {ref}`content:references:itos-calculus`
* The {ref}`content:references:geometric-brownian-motion` model for asset prices

---

(content:references:wiener-process)=
## Wiener Processes
A [Wiener Process](https://en.wikipedia.org/wiki/Wiener_process) is a real valued continuous-time stochastic process named in honor of American mathematician [Norbert Wiener](https://en.wikipedia.org/wiki/Norbert_Wiener) for his investigations of the mathematical properties of one-dimensional Brownian motion:

````{prf:definition} Wiener Process
:label: defn-wiener-process

A one-dimension Wiener Process is a stochastic process $\left\{W\left(t\right), 0\leq{t}\leq{T}\right\}$ with the following properties:
* W$\left(0\right)$ = $0$
* W(t) is continuous
* The increments $\left\{W(t_{1}) - W(t_{o}),\dots, W(t_{k}) - W(t_{k-1})\right\}$ are independent for any $k$ and $0\leq{t_{o}}< t_{1} < \dots < t_{k} \leq{T}$.
* The increment W(t) - W(s) $\sim~N\left(0,t-s\right)$ for any $0\leq{s}< t \leq{T}$, where $N\left(0,t-s\right)$ denotes a normally distributiom with mean $0$ and variance $t - s$.

````

(content:references:ordinary-brownian-motion)=
## Ordinary Brownian Motion
Ordinary Brownian Motion is a general class of problems that can be described by random fluctuations around
a constant deterministic drift term.

````{prf:definition} Ordinary Brownian Motion

Suppose there exists constants $\mu$ and $\sigma>0$.
Then a random process $X(t)$ is said to follow an Oridinary Brownian Motion (Wiener) process with drift $\mu$ and diffusion coefficient $\sigma^{2}$ if it is a solution to the Stochastic Differential Equation (SDE):

```{math}
:label: eq-SDE-BM
dX\left(t\right) = \mu{dt}+\sigma{dW(t)}
```
where $dW(t)$ is a one-dimensional Wiener Process.
````

Eqn. {eq}`eq-SDE-BM` is one of the simplest models of a Brownian motion process. For example, Louis Bachelier used a similar model to describe stock prices in his pioneering thesis work in 1900 {cite:p}`Bachelier:2006vl`. However, there are a few technical issues with Eqn. {eq}`eq-SDE-BM`.

### Discrete approximation of a continuous process
Brownian motion simulations of stock prices often focus on computing values of the noise terms $W(t_{1}),W(t_{2}),\dots,W(t_{n})$ and
the state terms (e.g., the `XYZ` share price) $X(t_{1}), X(t_{2}), \dots, X(t_{n})$ at discrete times $0 < t_{1} < t_{2} < \dots < t_{n}$. However, Eqn. {eq}`eq-SDE-BM` and the underlying
Wiener process are continuous in time. 
To bridge this gap, we need to develop a discretization procedure that approximates the solution of 
Eqn. {eq}`eq-SDE-BM` at the discrete-time points that are interested in. The easiest of these procedures is the [Euler–Maruyama method](https://en.wikipedia.org/wiki/Euler–Maruyama_method).

Let $Z_{1},\dots,Z_{n}$ denote independent standard normal random variables. For an ordinary Brownian motion, where $t_{o} = 0$ and $W(0) = 0$, the solution to Eqn. {eq}`eq-SDE-BM` can be approximated using the [Euler–Maruyama method](https://en.wikipedia.org/wiki/Euler–Maruyama_method), which gives the recurrence relationship:

```{math}
:label: eq-SDE-BM-Euler
X_{i+1} = X_{i}+\mu\left(t_{i+1} - t_{i}\right)+\left(\sigma\sqrt{t_{i+1} - t_{i}}\right)Z_{i+1}\qquad{i=0,1,\dots,n-1}
```

where $X_{i+1}$ denotes the state variable evaluated at time index $i+1$. In Eqn. {eq}`eq-SDE-BM-Euler`, both $\mu$ and $\sigma$ are assumed to be constants, and:

$$W_{i+1} = W_{i} + \left(\sqrt{t_{i+1} - t_{i}}\right)Z_{i+1}\qquad{i=0,1,\dots,n-1}$$

We can compute sample paths (solutions) for Eqn. {eq}`eq-SDE-BM-Euler` generated using the [Euler–Maruyama discretization method](https://en.wikipedia.org/wiki/Euler–Maruyama_method) using {prf:ref}`algo-ord-brownian-motion`.

```{prf:algorithm} Ordinary Brownian Motion
:label: algo-ord-brownian-motion

**Inputs** Parameters $\left(\mu,\sigma\right)$, initial condition $X\left(t_{o}\right) = X_{o}$, initial time $t_{o}$, final time $t_{f}$, time step size $h$, and the number of sample paths $P$ 

**Output** Time array T and the $\dim\left(T\right)\times{P}$ solution array $X$

1. initialize $T~\leftarrow$ range($t_{o}$, stop = $t_{f}$, step = $h$) |> collect
2. initialize $\mathcal{P}~\leftarrow$ range(1, stop = $P$, step = 1) |> collect
2. initialize $X~\leftarrow$ Array($\dim\left(T\right)$, $P$)
3. initialize $X[1,\mathcal{P}]~\leftarrow~X_{o}$ for all sample paths $P$

1. for each $(k,s) \in \mathcal{P}$
    1. for each $(i,t) \in T$
        1. generate $Z~\leftarrow~\mathcal{N}\left(0,1\right)$
        2. set $X[i+1,k]~\leftarrow~X[i,k]+\mu{h}+\left(\sigma\sqrt{h}\right)Z$
```

(content:references:itos-calculus)=
## Ito's Calculus
We can compute a numerical approximation to the actual solution of most stochastic differential equations. 
However, as we have seen, techniques such as the [Euler–Maruyama discretization method](https://en.wikipedia.org/wiki/Euler–Maruyama_method) come at the cost of accuracy. 

To solve stochastic differential equations analytically (just like ordinary differential equations), we must use tools from calculus. However, for stochastic differential equations, such as Eqn. {eq}`eq-SDE-BM` we need a
different types of calculus, namely [Ito’s calculus](https://en.wikipedia.org/wiki/Itô_calculus), which extends ordinary calculus methods to stochastic systems.  

### Ito's Lemma
A significant result from [Ito’s calculus](https://en.wikipedia.org/wiki/Itô_calculus), 
that allows us to develop analytical solutions to some stochastic differential equations is 
[Ito's Lemma](https://en.wikipedia.org/wiki/Itô%27s_lemma), discovered by K. Ito in 1951 [REFHERE].

````{prf:lemma} Ito's Lemma
:label: ito-lemma

Suppose the behavior of $X(t)$ is governed by the stochastic differential equation (Ito Process):

```{math}
:label: eq-ito-process
dX = a\left(X(t),t\right)dt + b\left(X(t),t\right)dW(t)
```

where $dW(t)$ is a Wiener process and $a$ and $b$ are functions of $X(t)$ and $t$. 
Let $Y(t) = \phi\left(t,X(t)\right)$ be another process that is a function of $X(t)$ and time $t$. 
Let $\phi\left(t,X(t)\right)$ be twice differentiable with respect to $X(t)$, 
and singly differentiable with respect to $t$. 

Then, the process $Y(t)$ is governed by the equation:

```{math}
:label: eq-ito-lemma
dY = \left(\frac{\partial{Y}}{\partial{t}}+a\frac{\partial{Y}}{\partial{X}}+\frac{b^{2}}{2}\frac{\partial^{2}{Y}}{\partial{X}^{2}}\right)dt+b\left(\frac{\partial{Y}}{\partial{X}}\right)dW(t)
```
````

The process of finding a solution to a stochastic differential equation using [Ito's Lemma](https://en.wikipedia.org/wiki/Itô%27s_lemma) works backwards; we propose a function $Y=\phi\left(t,X(t)\right)$ and then construct the stochastic differential equation that governs $Y(t)$. 
If that stochastic differential equation is the same as the original equation, then we have constructed a solution. 

Suppose we want to construct a solution to the stochastic differential equation (SDE):

```{math}
dX\left(t\right) = \mu{dt}+\sigma{dW(t)}
```

where $\mu$ and $\sigma$ are constants, and $dW(t)$ is a one-dimensional Wiener Process. 
Let $Y\left(t\right) = X\left(t\right)$. Then, from Ito's Lemma we know that:

* The terms $a=\mu$ and $b=\sigma$ which are both constants
* The time derivative term $\partial{Y}/\partial{t} = 0$
* The state derivative term $\partial{Y}/\partial{X} = 1$
* The state derivative term $\partial^{2}{Y}/\partial{X}^{2} = 0$

which gives from Eqn. {eq}`eq-ito-lemma`:

```{math}
dY\left(t\right) = \mu{dt}+\sigma{dW(t)}
```

Integrating both sides from $t_{1}\rightarrow{t_{2}}$ gives:

```{math}
Y\left(t_{2}\right) - Y\left(t_{1}\right) = \int_{t_{1}}^{t_{2}}\mu{dt}+\int_{t_{1}}^{t_{2}}\sigma{dW(t)}
```

The first term on the right-hand side is easy to deal with:

```{math}
\int_{t_{1}}^{t_{2}}\mu{dt} = \mu\left(t_{2} - t_{1}\right)
```

However, the second term is the integral of a random process (which we don't know how to do!)
Thus, the best we can do now (substituting $X$ for $Y$ and pulling out constants) is:

```{math}
:label: ex-ordinary-brownian-motion-soln-almost
X\left(t_{2}\right) = X\left(t_{1}\right) + \mu\left(t_{2} - t_{1}\right) +\sigma\int_{t_{1}}^{t_{2}}{dW(t)}
```

Eqn. {eq}`ex-ordinary-brownian-motion-soln-almost` brings up an important question, how do we integrate a random process? 

### Ito Stochastic Integral
The integral on the right-hand side of Eqn. {eq}`ex-ordinary-brownian-motion-soln-almost` involves
integrating over a random process. This is an example of a stochastic integral, which fortunately 
can be evaluated as the limit of a [Riemann–Stieltjes sum](https://en.wikipedia.org/wiki/Riemann–Stieltjes_integral):

````{prf:definition} Ito Stochastic Integral
:label: riemann–stieltjes-integral

Let the random variable $S(\omega)$ be defined as:

```{math}
S(\omega) = \int_{t_{0}}^{t_{1}}g\left(t,\omega\right)dW\left(t\right)
```

where $dW(t)$ is a Wiener process. Futher, let $\left\{\pi_{n}\right\}$ denote a sequence of partitions of the interval $\left[t_{1},t_{2}\right]$.
Then the value for $S\left(\omega\right)$ can be computed as the limit of a Riemann–Stieltjes sum:

```{math}
S_{n}\left(\omega\right) = \lim_{n\rightarrow\infty}
\sum_{\left[t_{i-1},t_{i}\right]\in\pi_{n}}g\left(t_{i-1},\omega\right)\Bigl(W(t_{i}) - W(t_{i-1})\Bigr)
```

The parameter $n$ controls the width of the partitions on which the sum is evaluated; as $n$ becomes
large the width of each partition decreases. 
````

Now that we can evalue stochastic integrals ({prf:ref}`riemann–stieltjes-integral`), 
we can compute a value for the integral in Eqn. {eq}`ex-ordinary-brownian-motion-soln-almost`. 
Assume we have discretized time with some fixed step size $h$.  Finish me. Then:

```{math}
:label: ex-ordinary-brownian-motion-analytical-soln
\sigma\int_{t_{1}}^{t_{2}}{dW(t)} = \sigma\left[W\left(t_{2}\right) - W\left(t_{1}\right)\right]
```

which (using {prf:ref}`defn-wiener-process`) gives the solution:

```{math}
X\left(t_{2}\right) = X\left(t_{1}\right) + \mu\Delta{T} + \sigma{N\left(0,\Delta{T}\right)}
```

where $\Delta{T} = t_{2} - t_{1}$.
 
(content:references:geometric-brownian-motion)=
## Geometric Brownian Motion
Unfortunately, Eqn. {eq}`eq-SDE-BM` has a critical flaw; namely, its solution can admit negative values. 
Thus, it is not widely used as a model for a stock price (or the price of other risky assets) because asset prices are non-negative. Instead, we often model asset price using a [Geometric Brownian Motion (gbm) model](https://en.wikipedia.org/wiki/Geometric_Brownian_motion):

````{prf:definition} Geometric Brownian Motion

Suppose there exists constants $\mu$ and $\sigma>0$.
Then a random process $X(t)$ is said to follow a Geometric Brownian Motion (Wiener) process with drift $\mu$ and diffusion coefficient $\sigma^{2}$ if it is a solution to the Stochastic Differential Equation (SDE):

```{math}
:label: eq-SDE-GBM
\frac{dX\left(t\right)}{X(t)} = \mu{dt}+\sigma{dW(t)}
```
where $dW(t)$ is a one-dimensional Wiener Process.
````

The use of geometric Brownian motion as a financial model is primarily due to the work of Samuelson in the 1950s and 1960s {cite}`Merton2006`. However, today Geometric Brownian Motion is more often associated with the Black–Scholes options pricing model (which we'll describe later) {cite}`BlackScholes1973`.

Eqn. {eq}`eq-SDE-GBM` has several excellent properties.
Central among these properties is that it has an _analytical_ solution. 
Thus, we can estimate the price value $X(t)$ precisely as a function of time (no need to develop an approximate solution)!
However, to develop the analytical solution, we need to use {ref}`content:references:itos-calculus`.

````{prf:observation} Analytical and Numerical Solution Geometric Brownian Moition
:label: soln-gbm-anal-numerical-soln
The [Euler–Maruyama](https://en.wikipedia.org/wiki/Euler–Maruyama_method) solution of the
constant drift and variance geometric brownian motion equation is given by:

```{math}
X_{k+1} = X_{k}\left(1+\mu{h}+\sigma\sqrt{h}\times{Z\left(0,1\right)}\right)\qquad{k=1,2,\dots,N-1}
```

where $X_{\star}$ denotes the approximate solution at time step $\star$, 
$h$ denotes the time step size, $Z\left(0,1\right)$ denotes a standard normal random variable and
$\mu$ and $\sigma>0$ are constants.

````