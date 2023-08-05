# Model-Driven Portfolio Allocation
Fill me in.

```{topic} Model-Driven Portfolio Allocation Outline
Fill me in.
```

---

(content:references:single-index-models)=
## Single Index Models
The application of index models to construct risky portfolios was originally proposed by Treynor and Black {cite}`FB1973`. Single index models are asset pricing models which measure the risk and the return of a stock relative to a risk-free alternative investment, e.g., [government treasury bonds](./bonds.md). A single index model describes the return of a firm’s stock in terms of a firm-specific return and the overall market return. One of the simplest (yet still widely used) single index models was developed by Sharpe {cite}`SHARPE1963`.

### Derivation
The single-index model measures both the risk and the return of a stock, relative to a risk free alternative investment e.g., government treasury bounds. The single index model describes the return of the stock of firm $i$ in terms of a firm-specific return, and an overall market return:

```{math}
:label: eq-single-index-model
r_{i}\left(t\right) - r_{f} = \alpha_{i}+\beta_{i}\left(r_{m}\left(t\right)-r_{f}\right)+\epsilon_{i}
\left(t\right)\qquad{t=1,2,\dots,T}
```

The term $r_{i}\left(t\right)$ denotes the return of firm $i$, during time period $t$, 
$r_{f}$ denotes the risk-free rate i.e., the [interest rate of a riskless investment such as treasury bills](https://fred.stlouisfed.org/series/DTB3), while $r_{m}\left(t\right)$ denotes the return on a market portfolio e.g., an index such as the [S\&P500](https://en.wikipedia.org/wiki/S%26P_500) during time period $t$.  The term $\alpha_{i}$ denotes the firm-specific return, while $\beta_{i}$ denotes the proportion of the the firm's return associated with the overall market ({prf:ref}`defn-single-index-model-standard`): 

````{prf:definition} Single index model of Sharpe
:label: defn-single-index-model-standard

Let $R_{i}(t)\equiv\left(r_{i}\left(t\right) - r_{f}\right)$ and $R_{m}(t)\equiv\left(r_{m}\left(t\right)-r_{f}\right)$ denote the firm-specific and market excess returns (random variables) for period $t$. Further, let $\epsilon_{i}\left(t\right)$ denote a [stationary normally distributed random noise process](https://en.wikipedia.org/wiki/Normal_distribution) with mean zero and standard deviation $\sigma_{i}$. Then, the single index model of Sharpe is given by {cite}`SHARPE1963`:

```{math}
:label: eq-single-index-model-standard
R_{i}\left(t\right) = \alpha_{i}+\beta_{i}R_{m}\left(t\right)+\epsilon_{i}
\left(t\right)\qquad{t=1,2,\dots,T}
```

where $\alpha_{i}$ and $\beta_{i}$ are (unknown) model parameters: 

* The parameter $\alpha_{i}$ describes the firm specific return not explained by the market; thus, $\alpha_{i}$ is the idiosyncratic return of firm $i$.
* The parameter $\beta_{i}$ measures the relationship between the excess return of firm $i$ and the excess return of the market; a large $\beta_{i}$ suggests the market returns (or losses) are _amplified_ for firm $i$, while a small $\beta_{i}$ suggests the market returns (or losses) are _damped_ for firm $i$.
* The parameter $\beta_{i}$ can also be interpreted as a measure of the relative risk of investing in a firm $i$ relative to the overall market. 
````

To understand the various interpretations of $\beta_{i}$, we first must understand that both the firm specific $R_{i}$ and overall market excess returns $R_{m}$ are random variables. Thus, we can compute the expectation and variance of these variables and look at how these quantities depend upon $\beta_{i}$. 

Let's start by thinking about the reward interpretation of $\beta_{i}$:

````{prf:observation} Reward interpretation of $\beta_{i}$
:label: obs-beta-return-measure

Taking the expectation of the firm excess return $R_{i}$ gives:

```{math}
:label: eq-expected-R-sim
\mathbb{E}\left(R_{i}\right) = \alpha_{i}+\beta_{i}\mathbb{E}\left(R_{m}\right)
```

where $\mathbb{E}\left(\epsilon_{i}\left(t\right)\right) = 0$. 
Solving Eqn. {eq}`eq-expected-R-sim` for $\beta_{i}$ gives:

```{math}
:label: eqn-beta-return-ratio
\beta_{i} = \frac{\mathbb{E}\left(R_{i}\right) - \alpha_{i}}{\mathbb{E}\left(R_{m}\right)}
```
Thus, $\beta_{i}$ is a corrected ratio of expected (average) returns:

* $\beta_{i}>1$ expected return of firm $i$ is _greater_ than the expected market return
* $\beta_{i}\sim{1}$ firm $i$ performs _similar_ to the overall market on average
* $\beta_{i}<1$ expected excess return of firm $i$ is _less_ than the expected excess market return

````

However, $\beta_{i}$ has another interpretation, namely, the ratio of risks:

````{prf:observation} Risk interpretation of $\beta_{i}$
:label: obs-beta-risk-measure

The $\beta_{i}$ for asset $i$ can also be considered a measure of the risk of asset $i$ relative to the market. For example, we can show that:

```{math}
:label: eqn-beta-risk-ratio
\beta_{i} = \frac{\text{cov}(R_{i}, R_{m})}{\text{var}(R_{m})}
```

where $\text{cov}(R_{i}, R_{m})$ denotes the [covariance](https://en.wikipedia.org/wiki/Covariance) between the excess return of asset $i$ and the market, and $\text{var}(R_{m})$ denotes the variance of the market excess return. Thus, in the context of risk, $\beta_{i}$ has the interpretation:

* $\beta_{i}>1$ suggests firm $i$ has _greater risk_ than the overall market
* $\beta_{i}\sim{1}$ suggests that firm $i$ has the _same risk_ as the overall market on average
* $\beta_{i}<1$ suggests firm $i$ has _less risk_ compared to overall market 
````

Putting these two regimes together gives fundamental insight into the behavior of markets: __high returns come with high-risk__.

### Estimating Single Index Models from Data
Estimating single index models from data reduces to estimating values for the $(\alpha_{i},\beta_{i})$ parameters and developing a residual model $\epsilon_{i}(t)$. Let's decompose this problem into two phases:

* Phase 1: Estimate values for $(\alpha_{i},\beta_{i})$ using one of many possible approaches, and
* Phase 2: Estimate the $\epsilon_{i}(t)$ distribution by computing the residual between the data and the model with parameter values from phase 1.

#### Phase 1: Estimate $(\alpha_{i},\beta_{i})$.
Imagine that we have historical data for the excess return of `XYZ` and the market over some period of time; say we have $\mathcal{M}$ measurements for the excess returns. Then, the excess return for `XYZ` can be encoded as a $\mathcal{M}\times{1}$ column vector $\mathcal{y}$, while the excess market return can be encoded as an $\mathcal{M}\times{2}$ matrix $\mathbf{X}$, where the first column of $\mathbf{X}$ is all 1's while the second column holds the excess market return values. Then, the single index model is the overdetermined ($\mathcal{M}\gg{2}$) linear system:

```{math}
:label: eqn-linear-sys-sim
\mathbf{y} = \mathbf{X}\mathbf{\theta} + \mathbf{\epsilon}
```

where $\theta = (\alpha_{i},\beta_{i})^{T}$ is the $2\times{1}$ column vector of unknown parameters, $\mathbf{\epsilon}$ represents a vector of unexplained random errors. The task is to estimate the unknown $\theta$ vector, given $\mathbf{X}$ and $\mathbf{y}$.

To estimate the unknown parameter vector $\mathbf{\theta}$ we invert the data matrix $\mathbf{X}$. However, the inverse of an overdetermined matrix can not be computed directly. Instead, we solve the [normal equations](https://en.wikipedia.org/wiki/Ordinary_least_squares) which transforms the original overdetermined problem into a square system ({prf:ref}`defn-normal-eqn-ols`):

````{prf:definition} Normal solution overdetermined linear regression model
:label: defn-normal-eqn-ols

There exists dataset $\mathcal{D} = \left\{\mathbf{x}_{i},y_{i}\right\}_{i=1}^{n}$ where $\mathbf{x}_{i}$ is a p-dimensional vector of inputs (independent variables) and $y_{i}$ denotes a scalar response variable (dependent variable), and $n\gg{p}$.  Further, suppose we model the dataset $\mathcal{D}$ using the linear regression model:

```{math}
\mathbf{y} = \mathbf{X}\mathbf{\theta} + \mathbf{\epsilon}
```

where $\mathbf{\epsilon}$ represents a vector of unexplained random errors. Then, the value of the unknown parameter vector $\mathbf{\theta}$ that minimizes the sum of the squares loss function for an overdetermined system is given by:

```{math}
:label: eqn-loss-function-soln

\hat{\mathbf{\theta}} = \left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\mathbf{y} - \left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\mathbf{\epsilon}
```

The matrix $\mathbf{X}^{T}\mathbf{X}$ is called the normal matrix, while $\mathbf{X}^{T}\mathbf{y}$ is called the moment matrix. The existence of the normal solution $\hat{\mathbf{\theta}}$ requires that inverse $\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}$ exists.
````


{prf:ref}`example-dmi-single-index-model` explores the direct matrix inversion approach for computing the unknown parameter vector $\theta$:

````{prf:example} Direct matrix inversion to compute $\theta$
:label: example-dmi-single-index-model
:class: dropdown

Estimate the unknown single index model parameters $\theta = (\alpha,\beta)^{T}$ for [AMD](https://finance.yahoo.com/quote/AMD) using the daily log returns for the last 90 days. The [three-month T-bill interest rate](https://ycharts.com/indicators/3_month_t_bill) is r = 2.61\%. Finally, assume [SPY](https://finance.yahoo.com/quote/SPY) represents the market.

__Compute daily risk-free rate__: Because we are using daily price data to compute the excess return, we must convert the risk-free rate, reported in annual units, to daily units. Let $r_{f}$ denote the risk-free daily rate, then:

$$r_{f} = (1+r)^{(1/365)} - 1$$

The value for the daily risk-free rate of return was found to be $r_{f}$ = 7.06e-5.

__Estimate $\theta$__:
The daily log-return for [AMD](https://finance.yahoo.com/quote/AMD) and [SPY](https://finance.yahoo.com/quote/SPY) was computed using {prf:ref}`defn-log-return`; six-months of daily open high low close (OHLC) data was downloaded from [Polygon.io](https://polygon.io). 

The last 90-days of data were used to calculate the log return and to formulate the $Y$ vector and $X$ matrix. The matrix inverse $\left(X^{T}X\right)^{-1}$ was computed using the `inv` command from the `LinearAlgebra` package:

```{code-block} julia
Xᵀ = transpose(X);
θ̂ = inv((Xᵀ*X))*Xᵀ*Y
```

where θ̂ denotes the estimated model parameters; the estimated firm-specific return was $\hat{\alpha}$ = -0.000432, while $\hat{\beta}$ = 1.96. 

```{figure} ./figs/Fig-AMD-SIM-v-Data.pdf
---
height: 380px
name: fig-AMD-SIM-v-Data
---
Estimated performance of the single index model for [AMD](https://finance.yahoo.com/quote/AMD/) computed using direct matrix inversion. Green dots denote prediction data, while gray dots denote training data.
```

source: [live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [static HTML view](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-DirectMatrixInversion-SIM.jl.html)

````

#### Phase 2: Identification of the residual model
The residual model $\epsilon(t)$ describes the unmodeled random component of the return of `XYZ`; thus, it explains all the influences on the excess return that are _not_ associated with the firm or the overall market. Assume $\epsilon_{i}(t)\sim{N(0,\sigma_{\epsilon,i}^2)}$, i.e., the residual is [normally distributed](https://en.wikipedia.org/wiki/Normal_distribution) with a zero mean and a variance of $\sigma_{\epsilon,i}^2$. Define the residual (difference) between the model and the data as:

$$\Delta = \mathbf{y} - \hat{\mathbf{y}}$$

where $\hat{\mathbf{y}}$ denotes the _estimated_ excess return of firm $i$ (computed using the single index model), and $\mathbf{y}$ indicates the _actual_ excess return of firm $i$ as observed in the market. The values of $\Delta$ can be thought of as samples from the residual distribution $\epsilon_{i}(t)$, thus, we can use $\Delta$ to estimate $\sigma_{\epsilon,i}^2$. 

{prf:ref}`example-normal-residual-model` explores an approach to estimate the variance of the residuals.

````{prf:example} Identification of the Residual Model for [AMD](https://finance.yahoo.com/quote/AMD)
:label: example-normal-residual-model
:class: dropdown

Let's use the data and the estimated single index model parameters $\hat{\theta}$ for [AMD](https://finance.yahoo.com/quote/AMD) from {prf:ref}`example-dmi-single-index-model`. Given this data, let's estimate the variance of the unknown residual distribution, $\sigma_{\epsilon,i}^2$, using a maximum likelihood approach. 

We implemented the maximum likelihood strategy using routines implemented in the [Distributions.jl](https://github.com/JuliaStats/Distributions.jl) package.

Finish me this weekend. 

````

## Single Index Portfolios
The single index model can be used to construct portfolios of assets. In this section, we will explore the construction of a portfolio of assets using the single index model. 

### Portfolio Return using Single Index Models
Portfolio return shows the expected return of portfolio $\mathcal{P}$ in terms of the expected return of each of the assets in the portfolio. Thus, we must estimate the expected returns for each asset when solving the Markowitz allocation problem from data. However, a single index model can limit this work; instead of estimating the expected return for each asset from data, we only need to calculate the expected excess market return $\mathbb{E}(R_{m})$ and then use the single index model to predict the firm-specific expected excess returns $\mathbb{E}(R_{i})$: 

````{prf:observation} Single Index Model Portfolio Return
:label: obs-single-index-model-p-return
The single index model of Sharpe {cite}`SHARPE1963` describes the excess return of asset $i$ in terms of a firm specific contribution, and a contribution from the overall market. Substituting the expected excess return for asset $i$ into Eqn. {eq}`eqn-expected-p-rerturn` gives:

```{math}
:label: eqn-almost-sim-portfolio
\mathbb{E}(R_{\mathcal{P}}) = w^{T}\mathbb{E}(R) = \sum_{i\in\mathcal{P}}w_{i}\Bigl[\alpha_{i}+\beta_{i}\mathbb{E}(R_{m})\Bigr]
```

where the constant $\alpha_{i}$ is the estimated unexplained firm-specific return and $\mathbb{E}(R_{m})$ denotes the expected excess return of the market. Carrying through the multiplication in Eqn. {eq}`eqn-almost-sim-portfolio` gives:

```{math}
:label: eqn-expected-return-sim-portfolio
\mathbb{E}(r_{\mathcal{P}}) = w^{T}\mathbb{E}(r) = \alpha_{\mathcal{P}}+\beta_{\mathcal{P}}\mathbb{E}(R_{m})
```

where the constants $\alpha_{\mathcal{P}}$ and $\beta_{\mathcal{P}}$ are given by:

$$
\begin{eqnarray}
\alpha_{\mathcal{P}} & = & \sum_{i\in\mathcal{P}}w_{i}\alpha_{i}\\
\beta_{\mathcal{P}} & = & \sum_{i\in\mathcal{P}}w_{i}\beta_{i}
\end{eqnarray}
$$

Thus, the overall $\beta$ for the portfolio is a sum the individual firm-specific $\beta_{i}$'s weighted by $w_{i}$, the fraction of asset $i$ in the portfolio. Similarly, the unexplained excess return for the portfolio is the sum of the unexplained return for each firm $\alpha_{i}$, weighted by weighted by $w_{i}$.

````

### Portfolio Variance using Single Index Models
The single index portfolio approach provides a theoretically attractive model for the covariance matrix $\Sigma$. In particular, let's build upon {prf:ref}`defn-portfolio-variance`:

````{prf:observation} Single Index Model Portfolio Variance
:label: obs-single-index-model-covariance

To calculate the portfolio covariance matrix $\Sigma$, we must calculate $\text{cov}(R_{i}, R_{j})$, the covariance between the excess return of asset $i$ and $j$ in portfolio $\mathcal{P}$. Toward this, we take advantage of a property of the covariance between random variables $X$ and $Y$:

```{math}
:label: eqn-prop-cov
\text{cov}(X,Y) = \mathbb{E}(XY) - \mathbb{E}(X)\mathbb{E}(Y)
```

Let $X=R_{i}$ and $Y=R_{j}$ where the excess return of asset $\star$ is modeled using the single index model:

```{math}
R_{\star} = \alpha_{\star}+\beta_{\star}R_{m} + \epsilon_{\star}
```

where $\alpha_{\star}$ denotes the firm-specific return, $\beta_{\star}$ denotes the proportion of the firm's return associated with the overall market, and $\epsilon_{\star}$ is an error term; we have suppressed the time argument in the excess returns and the error. 

Substituting the single index model into Eqn. {eq}`eqn-prop-cov` and simplifing gives:


$$
\text{cov}(R_{i}, R_{j}) = \begin{cases}
\beta_{i}^{2}\sigma_{m}^{2}+\sigma_{\epsilon_{i}}^{2} & i = j \\
\beta_{i}\beta_{j}\sigma_{m}^2 & i \neq j
\end{cases}
$$


where $\sigma_{m}^2$ denotes the variance of the excess return of the market portfolio and $\sigma_{\epsilon_{i}}^{2}$ denotes the variance of the firm-specific error.

Thus, the covariance matrix $\Sigma$, when constructed using the single index model of Sharpe {cite}`SHARPE1963`, has a theoretically attractive structure that reduces to computing the variance of the market, the variance of the error, and the $\beta_{\star}$ values; $\beta_{\star}$ are often publicly tabulated (but are also relatively easy to calculate on our own). 

````

---

## Summary
Fill me in.