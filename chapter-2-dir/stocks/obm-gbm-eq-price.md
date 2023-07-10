# Brownian Motion Models of Equity Pricing

```{topic} Outline
Today’s lecture will introduce the first continuous-time tool of equity pricing - Brownian motion models. Our focus for today will be on the ordinary Brownian motion model, which is the simplest model. We will also consider the geometric Brownian motion model, arguably the most commonly used model.  

* [Introduction to Brownian motion models](content:brownian-models-introduction). Brownian motion models are continuous-time models that are used to describe the evolution of an asset price. We'll discuss the properties of Brownian motion models and how to use them to price assets.

* [Ordinary Brownian motion models](content:brownian-models-ordinary). Ordinary Brownian motion models are the simplest Brownian motion models. We'll discuss how to use them to price assets and how to test the model using real-world versus risk-neutral parameters.

* [Geometric Brownian motion models](content:brownian-models-geometric). Geometric Brownian motion models are the most commonly used Brownian motion models. We'll discuss how to use them to price assets and how to test the model using real-world versus risk-neutral parameters.

```

(content:brownian-models-introduction)=
## Introduction to Brownian motion models
Fill me in.


(content:brownian-models-ordinary)=
## Ordinary Brownian motion models
Ordinary Brownian motion is a general class of models that simulate random fluctuations around a constant deterministic drift term. Suppose there exists constants $\mu$ and $\sigma>0$. Then a random process $X(t)$ is said to follow an oridinary Brownian motion (Wiener) process with drift $\mu$ and diffusion coefficient $\sigma$ if $X(t)$ is a solution to the Stochastic Differential Equation (SDE):

```{math}
:label: eq-SDE-BM
dX\left(t\right) = \mu{dt}+\sigma\cdot{dW(t)}
```

where $dX(t)$ is the infinitesimal change in $X(t)$, $dt$ is the infinitesimal change in time, and $dW(t)$ is a one-dimensional Wiener Process. Eqn. {eq}`eq-SDE-BM` is the simplest Brownian model of equity share price. For example, Louis Bachelier used a similar model to describe stock prices in his pioneering thesis work in 1900 {cite:p}`Bachelier:2006vl`.  

### Analytical and numerical solution
When simulating stock prices using Brownian motion, it’s common to calculate the noise terms and state terms at specific times $0 < t_{1}  < \dots < t_{n}$. However, since the equation Eqn. {eq}`eq-SDE-BM` and the underlying Wiener noise process are continuous, we need to develop a discretization method that approximates the solution of the equation at discrete-time points. The [Euler–Maruyama method](https://en.wikipedia.org/wiki/Euler–Maruyama_method) is the simplest (and least accurate) procedure and involves the use of independent standard normal random variables $Z_{1},\dots, Z_{n}$. For an ordinary Brownian motion where $t_{o} = 0$ and $W(0) = 0$, the [Euler–Maruyama method](https://en.wikipedia.org/wiki/Euler–Maruyama_method) method approximates the solution to equation {eq}`eq-SDE-BM` using a recurrence relationship:

```{math}
:label: eq-SDE-BM-Euler
X_{i+1} = X_{i}+\mu\left(t_{i+1} - t_{i}\right)+\left(\sigma\sqrt{t_{i+1} - t_{i}}\right)\cdot{Z_{i+1}}\qquad{i=0,1,\dots,n-1}
```

where $X_{i+1}$ denotes the state variable evaluated at time index $i+1$. In Eqn. {eq}`eq-SDE-BM-Euler`, both $\mu$ and $\sigma$ are assumed to be constants, and:

$$W_{i+1} = W_{i} + \left(\sqrt{t_{i+1} - t_{i}}\right)\cdot{Z_{i+1}}\qquad{i=0,1,\dots,n-1}$$

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

### Estimating the drift and volatility parameters
Fill me in.

(content:brownian-models-geometric)=
## Geometric Brownian motion models
Unfortunately, Equation {eq}`eq-SDE-BM` has a significant flaw: its solution can have negative values. As a result, it is not commonly used as a model for stock prices or other risky assets, since their prices are always non-negative. Instead, a more popular model for asset prices is the geometric Brownian motion (GBM) model. This model assumes the existence of constants $\mu$ and $\sigma>0$, and a random process $X(t)$ which is described by the solution of the Stochastic Differential Equation (SDE):

```{math}
:label: eq-SDE-GBM
\frac{dX\left(t\right)}{X(t)} = \mu{dt}+\sigma{dW(t)}
```

Here, $dW(t)$ is a one-dimensional Wiener process. Geometric Brownian motion is primarily used as a financial model due to the work of Samuelson in the 1950s and 1960s {cite}`Merton2006`. However, today GBM is more commonly associated with the Black–Scholes options pricing model, which we will describe later {cite}`BlackScholes1973`.

### Analytical and numerical solution
Geometric Brownian motion has several excellent theoretical properties, most notably that it has an analytical solution that will not produce negative values. Therefore, we can calculate the price value $X(t)$ precisely as a function of time without the need for an approximate solution. The analytical solution to the geometric Brownian motion stochastic differential equation with constant drift and volatility is given by:

```{math}
:label: eq-SDE-GBM-analytical-solution
X(t) = X_{\circ}\cdot\exp\Biggl[\left(\mu-\frac{\sigma^{2}}{2}\right)\left(t - t_{\circ}\right) + (\sigma\sqrt{t-t_{\circ}})\cdot{Z(0,1)}\Biggr]
```

where $X_{\circ}$ is the initial price of the asset, $t_{\circ}$ is the initial time, and $Z(0,1)$ is a standard normal random variable. Meanwhile, the approximate Euler–Maruyama solution is given by:

```{math}
:label: eq-SDE-GBM-EM-solution
X_{k+1} = X_{k}\cdot\left[1+\mu{h}+\left(\sigma\sqrt{h}\right)\cdot{Z\left(0,1\right)}\right]\qquad{k=1,2,\dots,N-1}
```

Here, $X_{\star}$ represents the approximate solution at time step $\star$, $h = t_{k+1} - t_{k}$ represents the time step size, $Z\left(0,1\right)$ denotes a standard normal random variable, and $\mu$ and $\sigma>0$ are constants.

### Estimating the $\mu$ parameter
Suppose there was no stochastic noise in the system, i.e., the volatility parameter $\sigma=0$. In this case, the GBM solution becomes deterministic:

$$X(t) = X_{\circ}\exp\bigl[{\mu}\left(t-t_{\circ}\right)\bigr]$$

Rearranging the `ln` of the deterministic solution gives the linear expression:

$$\ln{S(t)} = \ln{S_{\circ}} + \mu\left(t-t_{\circ}\right)+\epsilon(t)$$

where $\epsilon(t)$ is an error term, i.e., the component of the share price that is not explained by this linear deterministic model. We construct a [least-squares estimate](https://en.wikipedia.org/wiki/Least_squares) of $\hat{\mu}$ by solving the [normal equations](./background/CS3220-L10-Bindel.pdf), and then estimating the parameters of the error term $\epsilon(t)$ by calculating the [residuals](https://en.wikipedia.org/wiki/Errors_and_residuals_in_statistics).

#### Solving the normal equations
Let $\mathbf{A}$ denote a $\mathcal{S}\times{2}$ matrix, where each row corresponds to a time value. The first column of $\mathbf{A}$ is all 1's while the second column holds the $(t_{k}-t_{\circ})$ values. Further, let $\mathbf{Y}$ denote the `ln` of the price values of `firm_id` (in the same order as the $\mathbf{A}$ matrix). Then, the y-intercept and slope (drift parameter) can be estimated by solving the `overdetermined` system of equations:

$$\mathbf{A}\mathbf{\theta} + \mathbf{\epsilon} = \mathbf{Y}$$

where $\mathbf{\theta}$ denotes the vector of unknown parameters. This system can be solved as:

$$\mathbf{\theta} = (\mathbf{A}^{T}\mathbf{A})^{-1}\mathbf{A}^{T}\mathbf{Y} - (\mathbf{A}^{T}\mathbf{A})^{-1}\mathbf{A}^{T}\mathbf{\epsilon}$$

where $\mathbf{A}^{T}$ denotes the transpose of the matrix $\mathbf{A}$, and $(\mathbf{A}^{T}\mathbf{A})^{-1}$ denotes the inverse of the square matrix product $\mathbf{A}^{T}\mathbf{A}$. Finally, we can estimate the error term $\mathbf{\epsilon}$ by calculating the residuals:

$$\mathbf{\epsilon} = \mathbf{Y} - \mathbf{A}\mathbf{\theta}$$

and fitting a normal distribution to compute the uncertainty in the estimate of the drift parameter $\hat{\mu}$.

#### Implementation
Let’s say we have a historical training dataset that shows the [volume-weighted average price over time](https://en.wikipedia.org/wiki/Volume-weighted_average_price#:~:text=In%20finance%2C%20volume%2Dweighted%20average,transactions%20during%20a%20trading%20session.). We store this data for all the firms of interest in the `dataset` variable. We can estimate the drift parameter $\mu$ for a specific stock within the `dataset`, identified by `firm_id`,  using the following method:

```{code-block} julia
:caption: Mean drift parameter estimate in a geometric Brownian motion model.
:linenos:

# load typical required packages -
using DataFrames, CSV, LinearAlgebra, Statistics, Distributions

# get the firm specific data from the dataset -
firm_data = dataset[firm_id];
number_of_trading_days = nrow(firm_data);

# define the range of the time values (use all for now) -
all_range = range(1,stop=number_of_trading_days,step=1) |> collect
T_all = all_range*Δt .- Δt

# Setup the normal equations -
A = [ones(number_of_trading_days) T_all];
Y = log.(firm_data[!,:volume_weighted_average_price]);

# Solve the normal equations -
θ = inv(transpose(A)*A)*transpose(A)*Y;

# get estimated μ and b (intercept) values -
b̂ = exp(θ[1]);
μ̂ = θ[2];

# compute the residuals -
residuals = Y - A*θ;

# fit a normal distribution to the residuals -
ϵ = mle_fit(Normal, residuals);
```


### Estimating the $\sigma$ parameter
There are multiple methods to calculate the volatility parameter $\sigma$. Generally, these approaches can be classified into two categories - historical volatility estimates based on return data and future volatility estimates based on the [Implied Volatility (IV)](https://en.wikipedia.org/wiki/Implied_volatility) of [put and call options contracts](https://en.wikipedia.org/wiki/Option_(finance)). For now, let's focus on computing the volatility $\sigma$ from historical data and talk about options later.

The historic volatility is estimated by analyzing the distribution of returns. To do this, let's assume a share price model of the form:

$$
S_{j} = \exp\left(\mu_{j,j-1}\Delta{t}\right)\cdot{S_{j-1}}
$$

where $\mu_{j,j-1}$ denotes the _growth rate_ (units: 1/time) and $\Delta{t}$ (units: time) denotes the time step during the time period $(j-1)\rightarrow{j}$. Solving for the return parameter $\mu_{j,j-1}$ gives the expression:

$$
\mu_{j,j-1} = \left(\frac{1}{\Delta{t}}\right)\cdot\ln\left(\frac{S_{j}}{S_{j-1}}\right)
$$

We use daily data; thus, the natural time frame between $S_{j-1}$ and $S_{j}$ is a single day. However, subsequently, it will be easier to use an annualized value for the $\mu$ parameter; thus, we let $\Delta{t} = 1/365$, or $\Delta{t} = 1/252$, i.e., the fraction of a calendar or trading year that occurs in a single day (specified above). 

We can then approximate the historical volatility parameter $\sigma$ from the variance of the returns computed from the historical data set. In particular, we fit the return data to a `Normal` distribution using [maximum likelihood estimation](https://en.wikipedia.org/wiki/Maximum_likelihood_estimation), and then compute an estimate of the historical volatility as $\hat{\sigma} = \sqrt{\text{Var}(\mu\cdot\Delta{t})}$. 

---

## Summary
Fill me in.