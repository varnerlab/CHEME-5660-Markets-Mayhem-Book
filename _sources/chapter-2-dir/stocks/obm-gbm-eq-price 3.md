(content:brownian-models-equity-share-price-simple)=
# Brownian Motion Models of Equity Pricing

```{topic} Outline
Today’s lecture will introduce the first continuous-time tool of equity pricing - Brownian motion models. Our focus for today will be on ordinary Brownian motion, the simplest model, and geometric Brownian motion, arguably the most commonly used model.  

* [Brownian motion models](content:brownian-models-introduction) are continuous-time models used to describe the evolution of an asset price, i.e., share price. We'll discuss the properties of Brownian motion models and how to use them to price assets.

* [Ordinary Brownian motion models](content:brownian-models-ordinary) are the simplest Brownian motion models for share prices. We'll discuss how to use them to price assets and the basic of monte carlo price simulations.

* [Geometric Brownian motion models](content:brownian-models-geometric) are arguably the most commonly used Brownian motion model for the share price. We'll discuss how to use them to price assets and how to estimate model parameters from historical data. 

* [Testing the geometric Brownian motion model](content:gbm-models-testing) is an important step in the model building process. We'll discuss how to test the geometric Brownian motion model using real-world parameters and historic data.
```

(content:brownian-models-introduction)=
## Introduction to Brownian motion models
One of the most important models in quantitative finance is Brownian motion. It was named after the [Scottish botanist Robert Brown](https://en.wikipedia.org/wiki/Robert_Brown_(botanist,_born_1773)). Essentially, it’s a continuous-time random walk that represents the price of a financial asset, which evolves over time in a random way. The two main characteristics of Brownian motion are independence and stationarity. 

* Independence means that the future behavior of a process is not influenced by its past, i.e., a process has no memory.
* Stationarity means that the statistical properties of a process remain constant over time. 

Brownian models are incredibly useful in many areas of quantitative finance, such as option pricing, risk management, and portfolio optimization.


(content:brownian-models-ordinary)=
## Ordinary Brownian motion models
Ordinary Brownian Motion (OBM) is a continuous-time stochastic process in which the random variable $S(t)$, e.g., the share price at time $t$ of a firm with ticker `XYZ`, is described by a deterministic drift term corrupted by a [Wiener noise process](https://en.wikipedia.org/wiki/Wiener_process):

```{math}
:label: eq-SDE-BM
dS = {\mu}dt + \sigma{dW}
```

The constant $\mu$ denotes a drift parameter, $\sigma$ indicates a volatility parameter and $dW$ represents the output of a [Wiener process](https://en.wikipedia.org/wiki/Wiener_process).  However, while Louis Bachelier used a similar model to describe stock prices in his pioneering thesis work in 1900 {cite:p}`Bachelier:2006vl`, ordinary Brownian motion is not commonly used as a model for stock prices or other risky assets. The primary reason is that the share price can take on negative values, which is unrealistic. 

Despite the negativity issue, ordinary Brownian motion models are useful for understanding the properties of more realistic models, such as [geometric Brownian motion models which we consider next](content:brownian-models-geometric), understanding the properties of stochastic processes in general, and developing numerical methods for solving stochastic differential equations.

### Analytical solution
Using [Ito's lemma](https://en.wikipedia.org/wiki/Itô%27s_lemma), we can formulate an analytical solution to the OBM equation which describes the evolution of the share price $S(t)$ over time $t$:

```{math}
:label: eq-SDE-BM-solution
S(t) = S_{\circ} + \mu\left(t-t_{\circ}\right)+\left(\sigma\sqrt{t - t_{\circ}}\right)\cdot{Z_{t}(0,1)}
```

where $S_{\circ}$ denotes the share price at the initial time $t_{\circ}$, and $Z_{t}(0,1)$ denotes a [standard normal random variable](https://en.wikipedia.org/wiki/Normal_distribution#Standard_normal_distribution) at time $t$. The analytical solution allows us to directly compute the expected value and variance of the share price at time $t$. The expected share price is given by:

$$\mathbb{E}\left(S_{t}\right) = S_{o} + \mu\cdot\Delta{t}$$

where $\Delta{t} = t-t_{o}$. On the other hand, the variance of the share price $\text{Var}(S_{t})$ at time $t$ is given by:

$$\text{Var}\left(S_{t}\right) = \sigma^{2}{\Delta{t}}$$

The derivation of the analytical solution, the expectation and the variance of the share price are [provided in the Appendix](../../appendix/ito.md).

### Monte Carlo simulation
Monte Carlo simulation is a powerful tool for simulating stochastic systems, e.g., share prices, where analytical expressions for the solution, expectation, and variance are unavailable. Monte Carlo simulation is based on generating a large number of random sample paths, e.g., possible trajectories of the share price $S(t)$, and then computing the expected value and variance of the share price from the population of sample paths ({numref}`fig-obm-samples`)

```{figure} ./figs/Fig-Samples-OBM.svg
---
height: 420px
name: fig-obm-samples
---
Simulation of Brownian motion for share price $S(t)$ with N = 100 and 1000 sample paths (blue lines). The analytical expected value is shown as a black dashed line, and the analytical variance is shown as shaded regions for `z = 1.0, 1.96, 2.576`. Sample path expectation and variance are shown as black lines. Parameters: $S_{\circ} = 100$, $\mu = 2.0$, $\sigma = 20$, and `T = 42` days.
```

As the number of sample path increases, the estimated expected value and variance converge to the analytical values ({numref}`fig-obm-samples`, left versus right panels). However, this opens up the question of how many sample paths are required to obtain a good estimate of the expected value and variance, i.e., what is a good stopping criterion? 

Bicher et al., recently reviewed the stopping criteria for Monte Carlo simulation {cite}`Bicher2022ReviewOM`.


<!-- the literature on the convergence of Monte Carlo simulation for stochastic differential equations {cite:p}`Bichsel:2013vz`. They found that the convergence rate of Monte Carlo simulation for stochastic differential equations is $O(N^{-1/2})$, where $N$ is the number of sample paths. This means that the variance of the Monte Carlo estimate of the expected value and variance decreases as $N^{-1/2}$, i.e., the variance decreases as the square root of the number of sample paths. -->

### Discretization
However, if we don't have an analytical solution for the share price (which for advanced models is typically the case), how can we simulate it? The answer is to use a discretization technique such the [Euler-Maruyama (EM) method](https://en.wikipedia.org/wiki/Euler%E2%80%93Maruyama_method), which is a numerical method for approximating the solution of stochastic differential equations. For the general scalar stochastic differential equation with a Wiener noise process:

$$dX = a(X,t)dt + b(X,t)dW$$

The EM method gives the discrete approximate solution at time-step $k\rightarrow{k+1}$:

```{math}
:label: eq-EM-method-general-case
X_{k+1} = X_{k} + a(X_{k}, t_{k})h + \left(b(X_{k},t_{k})\sqrt{h}\right)\cdot{Z_{k}}\left(0,1\right)
```

where the step size $h=t_{k+1} - t_{k}$ and $Z_{k}(0,1)$ denotes a standard normal random variable at time-step $k$.  While the EM method is straightforward to implement, it has a poor overall accuracy with error on order $\sqrt{h}$. Thus, small step sizes are required to get accurate solutions.


<!-- As a result, we will focus on the geometric Brownian motion model, which is a more realistic model of share price evolution.


there is a significant issue with this type of stochastic model for share prices. The problem lies in the potential for negative share prices, which is unrealistic.

Finally, let's compute the expectation and variance of the share price simulation. We could estimate these values from the population of sample paths. However, for the Geometric Brownian Motion (GBM) analytical expressions are available for both the expected value and the variance of the share price. 

Despite the negative share price issue, Eqn. {eq}`eq-SDE-BM` is the simplest Brownian model of equity share price.  -->


(content:brownian-models-geometric)=
## Geometric Brownian motion models
A more popular model for asset prices is the geometric Brownian motion (GBM) model. The GBM model is a stochastic differential equation that describes the evolution of the share price $S(t)$ as random walk with drift and volatility:

```{math}
:label: eq-SDE-GBM
\frac{dS\left(t\right)}{S(t)} = \mu{dt}+\sigma{dW(t)}
```

Here, $S(t)$ denotes the share price, the constant $\mu$ denotes a drift parameter, $\sigma>0$ indicates a volatility parameter and $dW$ represents the output of a [Wiener noise process](https://en.wikipedia.org/wiki/Wiener_process). 

Geometric Brownian motion is primarily used as a financial model due to the work of Samuelson in the 1950s and 1960s {cite}`Merton2006`. However, today GBM is more commonly associated with the Black–Scholes options pricing model, which we will describe later {cite}`BlackScholes1973`.

### Analytical solution
We can calculate the share price value $S(t)$ as a function of time without the need for an approximate solution by developing an analytical solution to Eqn. {eq}`eq-SDE-GBM`. The analytical solution to the geometric Brownian motion stochastic differential equation with constant drift $\mu$ and volatility $\sigma>0$ is given by:

```{math}
:label: eq-SDE-GBM-analytical-solution
S(t) = S_{\circ}\cdot\exp\Biggl[\left(\mu-\frac{\sigma^{2}}{2}\right)\left(t - t_{\circ}\right) + (\sigma\sqrt{t-t_{\circ}})\cdot{Z(0,1)}\Biggr]
```

where $S_{\circ}$ is the initial share price of the asset at $t_{\circ}$, the initial time, and $Z(0,1)$ is a standard normal random variable. Finally, we can use the analytical solution in Eqn. {eq}`eq-SDE-GBM-analytical-solution` to develop analytical expressions for the expectation and variance of the share price. The expected share price is given by:

```{math}
:label: eq-SDE-GBM-expected-value
\mathbb{E}\left(S_{t}\right) = S_{o}\cdot\exp\left(\mu\cdot\Delta{t}\right)
```

where $\Delta{t} = t-t_{o}$ and $S_{o}$ denotes the share price at $t=t_{o}$. On the other hand, the variance of the share price $\text{Var}(S_{t})$ at time $t$ is given by:

```{math}
:label: eq-SDE-GBM-variance
\text{Var}\left(S_{t}\right) = S_{\circ}^{2}e^{2\mu\cdot\Delta{t}}\left[e^{\sigma^{2}{\Delta{t}}} - 1\right]
```

The derivation of the analytical solution, the expectation and the variance of the share price are [provided in the Appendix](../../appendix/ito.md).

### Estimating the $\mu$ parameter
Suppose there was no stochastic noise in the system, i.e., the volatility parameter $\sigma=0$ in Eqn. {eq}`eq-SDE-GBM-analytical-solution`. In this case, the GBM solution becomes deterministic:

```{math}
:label: eq-SDE-GBM-deterministic-solution
S(t) = S_{\circ}\cdot\exp\bigl(\mu\cdot\Delta{t}\bigr)
```

where $\Delta{t} = t-t_{o}$ and $S_{o}$ denotes the share price at $t=t_{o}$. Rearranging the `ln` of the deterministic solution gives the linear expression:

```{math}
:label: eqn-SDE-GBM-deterministic-solution-ln
\ln{S(t)} = \ln{S_{\circ}} + \mu\left(t-t_{\circ}\right)+\epsilon(t)
```

where $\epsilon(t)$ is an error term, i.e., the component of the share price that is not explained by this linear deterministic model. We construct a [least-squares estimate](https://en.wikipedia.org/wiki/Least_squares) of $\hat{\mu}$ by solving the [normal equations](./background/CS3220-L10-Bindel.pdf), and then estimating the parameters of the error term $\epsilon(t)$ by calculating the [residuals](https://en.wikipedia.org/wiki/Errors_and_residuals_in_statistics).

#### Solving the normal equations
Let $\mathbf{A}$ denote a $\mathcal{S}\times{2}$ matrix, where each row corresponds to a time value. The first column of $\mathbf{A}$ is all 1's while the second column holds the $(t_{k}-t_{\circ})$ values. Further, let $\mathbf{Y}$ denote the `ln` of the price values of `firm_id` (in the same order as the $\mathbf{A}$ matrix). Then, the y-intercept and slope (drift parameter) can be estimated by solving the `overdetermined` system of equations:

$$\mathbf{A}\mathbf{\theta} + \mathbf{\epsilon} = \mathbf{Y}$$

where $\mathbf{\theta}$ denotes the vector of unknown parameters. This system can be solved as:

$$\mathbf{\theta} = (\mathbf{A}^{T}\mathbf{A})^{-1}\mathbf{A}^{T}\mathbf{Y} - (\mathbf{A}^{T}\mathbf{A})^{-1}\mathbf{A}^{T}\mathbf{\epsilon}$$

where $\mathbf{A}^{T}$ denotes the transpose of the matrix $\mathbf{A}$, and $(\mathbf{A}^{T}\mathbf{A})^{-1}$ denotes the inverse of the square matrix product $\mathbf{A}^{T}\mathbf{A}$. Finally, we can estimate the error term $\mathbf{\epsilon}$ by calculating the residuals:

$$\mathbf{\epsilon} = \mathbf{Y} - \mathbf{A}\mathbf{\theta}$$

and fitting a normal distribution to the resisduals to compute the uncertainty in the estimate of the mean of the drift parameter $\hat{\mu}$.

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

We implemented this method to estimate the drift parameter $\mu$ and the error model $\epsilon(t)$ for two example tickers, namely `WFC` and `AMD` using daily training data ({numref}`fig-drift-simulation-WFC-AMD`).

```{figure} ./figs/Fig-drift-simulation-WFC-AMD.svg
---
height: 480px
name: fig-drift-simulation-WFC-AMD
---
The `ln` of share price of `AMD` (left) and `WFC` (right) versus time using a deterministic geometric Brownian motion model. The dashed line denotes the mean simulation, the shaded regions show the 99.9% confidence interval of the mean (inner shaded region) and individual simulations (outer shaded region). Daily training data between `2018-11-28` to `2022-11-28` was downloaded using the `aggregate` endpoint of [Polygon.io](https://polygon.io/docs/stocks/get_v2_aggs_ticker__stocksticker__range__multiplier___timespan___from___to).
```

### Estimating the $\sigma$ parameter
There are multiple methods to calculate the volatility parameter $\sigma$. Generally, these approaches can be classified into two categories - historical volatility estimates based on the distribution of the return data and future volatility estimates based on the [Implied Volatility (IV)](https://en.wikipedia.org/wiki/Implied_volatility) of [put and call options contracts](https://en.wikipedia.org/wiki/Option_(finance)). For now, let's focus on computing the volatility $\sigma$ from historical data and talk about options later.

The historic volatility is estimated by analyzing the distribution of returns using much the same approach we took when looking at the stylized facts. To do this, let's assume a share price model of the form:

$$
S_{j} = S_{j-1}\cdot\exp\left(\mu_{j,j-1}\cdot\Delta{t}\right)
$$

where $S_{j-1}$ and $S_{j}$ denote the share price at time $j-1$ and $j$, $\mu_{j,j-1}$ denotes the _growth rate_ (units: 1/time) and $\Delta{t}$ (units: time) denotes the time step for time period $(j-1)\rightarrow{j}$. Solving for the growth rate parameter $\mu_{j,j-1}$ gives the expression:

```{math}
:label: eqn-growth-rate-sigma-estimate
\mu_{j,j-1} = \left(\frac{1}{\Delta{t}}\right)\cdot\ln\left(\frac{S_{j}}{S_{j-1}}\right)
```

The time frame between two historical prices $S_{j-1}$ and $S_{j}$, varies depending on the frequency of the data (daily, weekly, monthly, etc.). For instance, if the data is daily, then the time difference $\Delta{t} =  1/252$, which is the fraction of a trading year that occurs in a single day. Similarly, if the data is weekly, then $\Delta{t} = 1/52$, and if it is monthly, then $\Delta{t} = 1/12$. 

````{note}
The product of the growth rate and the timestep equals the logaritmic return defined in {prf:ref}`defn-log-return-1` over the time period $\Delta{t}$:

```{math}
:label: eqn-log-return-growt-rate
\mu_{j,j-1}\cdot\Delta{t} = \ln\left(\frac{S_{j}}{S_{j-1}}\right) = \bar{r}^{(i)}_{j,j-1}
```

Thus, we can use the growth rate parameter $\mu_{j,j-1}$ to estimate the log return $\bar{r}^{(i)}_{j,j-1}$ for firm $i$ over the time period $(j-1)\rightarrow{j}$.
````

#### Implementation
To compute the historical volatility parameter, $\hat{\sigma}$, we calculated the variance of the returns of the historical training data set. In particular, we fit the historical return data to a [Normal distribution](https://juliastats.org/Distributions.jl/stable/univariate/#Distributions.Normal) using [maximum likelihood estimation](https://juliastats.org/Distributions.jl/stable/fit/#Distributions.fit_mle-Tuple{Any,%20Any,%20Any}) we then estimated the historical annualized volatility as $\sqrt{252}\cdot\hat{\sigma}$, where $\hat{\sigma}$ is the standard deviation of the return distribution. Example values for a few typical firms in the S&P 500 index are shown in {prf:ref}`obs-gbm-model-parameter-estimates`.

```{prf:observation} Real-world estimates of the drift and volatility parameters
:label: obs-gbm-model-parameter-estimates

Estimated annualized drift and volatility parameters for five sample firms in the S&P 500 index. The $\hat{\mu}$ and $\hat{\sigma}$ columns denote the estimated drift and volatility parameters, respectively.

| id  | ticker | name                   | sector                 | $\hat{\mu}$        | $\hat{\sigma}$    |
|-----|--------|------------------------|------------------------|----------|--------|
|  11 |    AMD | Advanced Micro Devices | Information Technology |   0.4605 | 0.4688 |
| 241 |    IBM |                    IBM | Information Technology | -0.01817 | 0.2414 |
| 487 |    WFC |            Wells Fargo |             Financials | -0.05003 |  0.322 |
| 221 |     GS |          Goldman Sachs |             Financials |   0.1274 | 0.2841 |
| 437 |   TSLA |                  Tesla | Consumer Discretionary |   0.7519 |   0.57 |


Daily logarithmic return values from `2018-11-28` to `2022-11-28` were computed from data downloaded using the `aggregate` endpoint of [Polygon.io](https://polygon.io/docs/stocks/get_v2_aggs_ticker__stocksticker__range__multiplier___timespan___from___to). The `fit_mle(...)` function from the [Distributions.jl package](https://juliastats.org/Distributions.jl/stable/) was used to fit the data to a Normal distribution.

```

Now that we have estimates of the drift and volatility parameters, we can simulate the share price of a firm using the geometric Brownian motion model and the [`sample(...)` function defined below](contest:geometric-brownian-motion-sample-function):

(contest:geometric-brownian-motion-sample-function)=
```{code-block} julia
:caption: Simulating the share price of a firm using the geometric Brownian motion model.
:linenos:

"""
    MyGeometricBrownianMotionEquityModel <: AbstractAssetModel

Mutable composite type holding the drift and volatility parameters 
for a geometric Brownian motion model.
"""
mutable struct MyGeometricBrownianMotionEquityModel <: AbstractAssetModel

    # data -
    μ::Float64;     # drift parameter
    σ::Float64;     # volatility parameter

    # constructor -
    MyGeometricBrownianMotionEquityModel() = new()
end


""" 
    sample(model::MyGeometricBrownianMotionEquityModel, data::NamedTuple) -> Array{Float64,2}
"""
function sample(model::MyGeometricBrownianMotionEquityModel, data::NamedTuple; 
    number_of_paths::Int64 = 100)::Array{Float64,2}

    # get information from data tuple 
    T₁ = data[:T₁]; # start time
    T₂ = data[:T₂]; # stop time
    Δt = data[:Δt]; # time step
    Sₒ = data[:Sₒ]; # initial price

    # get information from model -
    μ = model.μ; # drift parameter
    σ = model.σ; # volatility parameter

	# initialize -
	time_array = range(T₁, stop=T₂, step=Δt) |> collect
    number_of_time_steps = length(time_array)
    X = zeros(number_of_time_steps, number_of_paths + 1) # extra column for time -

    # put the time in the first col -
    for t ∈ 1:number_of_time_steps
        X[t,1] = time_array[t]
    end

	# replace first-row w/Sₒ (we always start at Sₒ) -
	for p ∈ 1:number_of_paths
		X[1, p+1] = Sₒ
	end

	# build a noise array of Z(0,1)
	d = Normal(0,1)
	ZM = rand(d,number_of_time_steps, number_of_paths);

	# main simulation loop -
	for p ∈ 1:number_of_paths
		for t ∈ 1:number_of_time_steps-1
			X[t+1,p+1] = X[t,p+1]*exp((μ - σ^2/2)*Δt + σ*(sqrt(Δt))*ZM[t,p])
		end
	end

	# return -
	return X
end
```

Let's simulate, [using the `sample(...)` function](contest:geometric-brownian-motion-sample-function), the volume-weighted averaged share price of two example firms `IBM` and `GS` for a random `T = 66` day time interval ({numref}`fig-gbm-simulation-IBM-GS`).

```{figure} ./figs/Fig-GBM-IBM-GS-T66.svg
---
height: 480px
name: fig-gbm-simulation-IBM-GS
---
Geometric Brownian motion simulation of the daily volume weighted average price (vwap) of `IBM` (left) and `GS` (right) for a random `T = 66` day period (in-sample). The solid lines denote the analytical confidence intervals, while the shaded regions denote the 68%, 95% and 99% confidence estimates of the vwap recovered by sampling (N = 100). Daily training data between `2018-11-28` to `2022-11-28` was downloaded using the `aggregate` endpoint of [Polygon.io](https://polygon.io/docs/stocks/get_v2_aggs_ticker__stocksticker__range__multiplier___timespan___from___to).
```

The geometric Brownian motion model captured the general trend of the share price for both firms, but it failed to capture the large spikes in the share price. This is because the geometric Brownian motion model assumes that the growth rate (drift term) and volatility are constant over time, which is may not be true for real-world share prices. 

Thus, while these two example firms and time periods were consistent with the observed price, choosing a different firm or time interval may result in a very different simulation. This leaves us with two questions to answer: first, can a geomertric Brownian motion model accurately predict stylized facts, i.e., the statistical properties, of return data and second, how likely is it that the geometric Brownian motion model will accurately predict the share price of a firm?

(content:gbm-models-testing)=
## Testing geometric Brownian motion

(content:gbm-models-testing-stylized-facts)=
### Stylized facts
The stylized facts of return data are the statistical properties of the data. These properties include the distribution of logarithmic returns, the autocorrelation of logarithmic returns, and the volatility clustering of the logarithmic returns. 

#### Autocorrelation of logarithmic returns
Fill me in.

#### Volatility clustering of logarithmic returns
Fill me in.

#### Distribution of logarithmic returns
The logarithmic return under the assumption that the share price follows a geometric Brownian motion model is given by:

```{math}
:label: eqn-log-return-gbm-return

\bar{r}_{j,j-1} = \left(\mu - \frac{\sigma^{2}}{2}\right)h + \left(\sigma\cdot\sqrt{h}\right)\cdot{Z}_{j,j-1}(0.1)
```

where $h$ is the time step, $\mu$ is the drift parameter, $\sigma$ is the volatility parameter, and ${Z}_{j,j-1}(0,1)$ is a random variable drawn from a standard normal distribution (mean zero and variance one) for the time period $(j-1)\rightarrow{j}$. From the definition of the standard normal distribution and Eqn. {eq}`eqn-log-return-gbm-return` , we can see that the logarithmic return $\bar{r}_{j,j-1}$ for a process described by geometric Brownian motion is normally distributed:

```{math}
:label: eqn-log-return-gbm-distribution
\bar{r}_{j,j-1} \sim \mathcal{N}\left(\left(\mu - \frac{\sigma^{2}}{2}\right)h, ~\sigma^{2}h\right)
```

with mean $\left(\mu - \frac{\sigma^{2}}{2}\right)h$ and variance $\sigma^{2}h$. 

Thus, a geometric Brownian motion model predicts the distribution returns only in cases where the logarithmic returns are normally distributed, which is not always true as we have seen [in our previous discussion of stylized facts](content:references:returns-stylized-facts). Let's visualize a few observed return distributions compared with the distributiuon predicted by Eqn. {eq}`eqn-log-return-gbm-distribution`. 




(content:gbm-models-testing-price-prediction)=
### Share price prediction
A limitation of geometric Brownian motion would seem to be the assumption of constant drift and volatility parameters. However, we have not quantified the `goodness` of the model. In other words, how likely is it that the geometric Brownian motion model will accurately predict the future share price of a firm?

Let's determine the likelihood of making accurate predictions using a geometric Brownian motion model. To do this, we'll randomly divide the future time into continuous segments of `T` days, denoted as $\mathcal{I}_{k}\in\mathcal{I}$. At the beginning of each segment $\mathcal{I}_{k}$, we'll initialize a geometric Brownian motion model and compare the actual price of a firm ($S_{j}$) at time $j$ with the simulated price during each time segment. 

* If the simulated price falls between the lower bound $L_{j}$ and upper bound $U_{j}$ for all $j\in\mathcal{I}_{k}$, we consider the simulation to be a `success`. The lower and upper bounds can be specified, but we'll set them to $\mu\pm{z}\cdot\sigma$, where $\mu$ is the expected value, $\sigma$ is the standard deviation of the simulation, and $z$ is the number of standard deviations from the mean (e.g., the z-score). 
* However, if the actual price violates the upper or lower bound at any point, the simulation is deemed a `failure`.

We'll repeat this process $\forall{\mathcal{I}_{k}}\in\mathcal{I}$ and calculate the fraction of `successful` simulations. This percentage is the likelihood of making bounded predictions using the geometric Brownian motion model ({prf:ref}`obs-gbm-prediction-likelihood`):

```{prf:observation} Geometric Brownian motion prediction likelhood
:label: obs-gbm-prediction-likelihood

Fraction of `successful` simulations for five exaample firms using geometric Brownian motion to predict the share price of a firm over a random `T = 21` day time periods (in sample). The fraction was calculated using `N = 500` trials.

| id  | ticker | name                   | $\pm$ 1.0$\cdot\sigma$   | $\pm$ 1.96$\cdot\sigma$   |  $\pm$ 2.576$\cdot\sigma$  |
|-----|--------|------------------------|:-------:|:-------:|:-------:|
|  11 |    AMD | Advanced Micro Devices | 0.168 | 0.688 | 0.862 |
| 241 |    IBM |                    IBM | 0.282 | 0.732 | 0.882 |
| 487 |    WFC |            Wells Fargo | 0.358 |  0.78 | 0.886 |
| 221 |     GS |          Goldman Sachs | 0.174 | 0.782 | 0.904 |
| 437 |   TSLA |                  Tesla | 0.224 | 0.676 |  0.87 |

As the z-score increases, the likelihood of making bounded predictions using the geometric Brownian motion model increases. However, the likelihood of making bounded predictions is lower than the theoretical values of 68%, 95% and 99% for all firms. 

```

---

## Summary
Today we introduced the first continuous-time tool of equity pricing - Brownian motion models. We focused on ordinary Brownian motion model, which is the simplest model, and geometric Brownian motion model, arguably the most commonly used model.  

* [Brownian motion models](content:brownian-models-introduction) are continuous-time models used to describe the evolution of an asset price, i.e., share price. We'll discuss the properties of Brownian motion models and how to use them to price assets.

* [Ordinary Brownian motion models](content:brownian-models-ordinary) are the simplest Brownian motion models for share prices. We'll discuss how to use them to price assets and the basic of monte carlo price simulations.

* [Geometric Brownian motion models](content:brownian-models-geometric) are arguably the most commonly used Brownian motion model for the share price. We'll discuss how to use them to price assets and how to estimate model parameters from historical data. 

* [Testing the geometric Brownian motion model](content:gbm-models-testing) is an important step in the model building process. We'll discuss how to test the geometric Brownian motion model using real-world parameters and historic data.