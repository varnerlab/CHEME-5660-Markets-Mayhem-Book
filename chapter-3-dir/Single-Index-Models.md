# Index Models

## Introduction

(content:references:return)=
## Return
The return of an asset is a measure of the difference in the price of that asset between two time periods. 
Return can be calculated in many ways; two common approaches are the percentage or fractional return and the
logarithmic return. 

(content:references:fractional-return)=
### Fractional return

````{prf:definition} Fractional return
:label: defn-percentage-return

Let the price of asset $i$ at any time $j$ be given by $P_{ij}>0$. Then the fractional return 
on asset $i$ over time horizon $j\rightarrow{k},j\neq{k}$ is defined as: 

```{math}
r_{i,j\rightarrow{k}} \equiv \frac{P_{ik} - P_{ij}}{P_{ij}}
```

where $r_{i,j\rightarrow{k}}$ denotes the fractional return of asset $i$ over time horizon $j\rightarrow{k},i\neq{k}$.

````

Consider the daily return on stock `XYZ` computed using the close price and the fractional return measure.
Let $P_{ij}$ denote the close price today, and $P_{ij-1}$ denote the close price for the previous trading day.
Then, the fractional daily return is given by:

```{math}
:label: eq-example-daily-close-price

r_{i,j-1\rightarrow{j}} = \frac{P_{ij} - P_{i,j-1}}{P_{i,j-1}}
```

However, Eqn. {eq}`eq-example-daily-close-price` can be rearranged to give an expression similar to 
Eqn. {eq}`eq-cash-flow-1-period`:

```{math}
P_{ij} = \left(1+r_{i,j-1\rightarrow{j}}\right)P_{i,j-1}
```

Thus, the fractional daily return (or a fractional return computed between any two different dates) is a type of discount rate that quantifies how the value of an asset changes, in the case of the share price of ticker `XYZ`, because of market forces. 
Becuase $P_{i,\star}$ is a random variable, the return is also a random variable. 

(content:references:log-return)=
### Logarithmic return

````{prf:definition} Logarithmic return
:label: defn-log-return

Let the price of asset $i$ at any time $j$ be gievm by $P_{ij}>0$. Then the logarithmic return 
on asset $i$ over time horizon $j\rightarrow{k},j\neq{k}$ is defined as: 

```{math}
\bar{r}_{i,j\rightarrow{k}} \equiv \log\left(\frac{P_{ij}}{P_{ik}}\right)
```

where $\bar{r}_{i,j\rightarrow{k}}$ denotes the logarithmic return of asset $i$ over time horizon $j\rightarrow{k},i\neq{k}$. The $\log\left(\star\right)$ term denotes the [natural log](https://en.wikipedia.org/wiki/Natural_logarithm). 

````

Consider the daily return on stock `XYZ` computed using the close price and the fractional return measure.
Let $P_{ij}$ denote the close price today, and $P_{ij-1}$ denote the close price for the previous trading day.
Then, the fractional daily return is given by:

```{math}
:label: eq-example-daily-close-price-log

\bar{r}_{i,j-1\rightarrow{j}} = \log\left(\frac{P_{ij}}{P_{i,j-1}}\right)
```

However, Eqn. {eq}`eq-example-daily-close-price-log` can be rearranged to give an expression similar to 
Eqn. {eq}`eq-cont-exchange-tvm`:

```{math}
P_{ij} = \exp\left(\bar{r}_{i,j-1\rightarrow{j}}\right)P_{i,j-1}
```

Thus, the logarithmic daily return (or a logarithmic return computed between any two different dates) is a continuous discount rate that quantifies how the value of an asset, e.g., the share price of ticker `XYZ`, changes because of market forces. Becuase $P_{i,\star}$ is a random variable, the return is also a random variable. 

### Single Index Return Models
The {ref}`content:references:fractional-return` or {ref}`content:references:log-return` can be computed
from historical data. However, what if we do not have access to price data for `XYZ` or we want to
_predict_ the return of `XYZ`, for example, in an automated trading system? 
In these cases, we need a model. One of the simplest (yet still widely used) models is the single index
model (SIM) developed by Sharpe {cite}`SHARPE1963`. 

The single-index model (SIM) is an asset pricing model which measures both the risk and the return of a stock, relative to a risk free alternative investment e.g., government treasury bounds. The single index model describes the return of the stock of firm $i$ in terms of a firm-specific return, and the overall market return:

```{math}
:label: eq-single-index-model
r_{i}\left(t\right) - r_{f} = \alpha_{i}+\beta_{i}\left(r_{m}\left(t\right)-r_{f}\right)+\epsilon_{i}
\left(t\right)\qquad{t=1,2,\dots,T}
```

The term $r_{i}\left(t\right)$ denotes the return of firm $i$, during time period $t$, 
$r_{f}$ denotes the risk-free rate i.e., the [interest rate of a riskless investment such as treasury bills](https://fred.stlouisfed.org/series/DTB3), while $r_{m}\left(t\right)$ denotes the return on a market portfolio e.g., an index such as the [S\&P500](https://en.wikipedia.org/wiki/S%26P_500) during time period $t$.  The term $\alpha_{i}$ denotes the firm-specific return, while $\beta_{i}$ denotes the proportion of the the firm's return associated with the overall market. 

The term $R_{i}(t)\equiv\left(r_{i}\left(t\right) - r_{f}\right)$ describes the excess return of specific firm $i$, while $R_{m}(t)\equiv\left(r_{m}\left(t\right)-r_{f}\right)$ describes the excess return of the market portfolio. Replacing the excess returns in Eqn. {eq}`eq-single-index-model` gives the single index model in standard form:

````{prf:definition} Single index model
:label: defn-single-index-model-standard

Let $R_{i}(t)$ and $R_{m}(t)$ denote the firm specific and market excess returns (random variables) 
for time period $t$.
Further, let $\epsilon_{i}\left(t\right)$ denote a [stationary normally distributed random noise process](https://en.wikipedia.org/wiki/Normal_distribution) with mean zero and standard deviation $\sigma_{i}$. Then, the standard single index model of Sharpe is given by {cite}`SHARPE1963`:

```{math}
:label: eq-single-index-model-standard
R_{i}\left(t\right) = \alpha_{i}+\beta_{i}R_{m}\left(t\right)+\epsilon_{i}
\left(t\right)\qquad{t=1,2,\dots,T}
```

where $\alpha_{i}$ and $\beta_{i}$ are constant model paramaters. 
````

The $\alpha_{i}$ parameter in Eqn {eq}`eq-single-index-model-standard` describes the firm specific 
return that is not explained by the market; thus, $\alpha_{i}$ is the 
idiosyncratic return of firm $i$.

The $\beta_{i}$ parameter in Eqn {eq}`eq-single-index-model-standard` has several interpretations. 
First, $\beta_{i}$ measures how the excess return of firm $i$ is related to the overall excess return of the market; a large $\beta_{i}$ suggests the market returns (or losses) are _amplified_ for firm $i$, while
a small $\beta_{i}$ suggests the market returns (or losses) are _damped_ for firm $i$.
On the other hand, $\beta_{i}$ can also be interpreted as a measure of the relative risk of investing in firm $i$. 

To understand the various interpretations of $\beta_{i}$, we first must understand that both the firm specific $R_{i}$ and overall market excess returns $R_{m}$ are random variables. Thus, we can compute the expectation and variance of these variables and look at how these quantities depend upon $\beta_{i}$:

````{prf:observation} Risk and Reward intepretations of $\beta_{i}$
:label: obs-beta-risk-measure

Taking the expectation of the firm excess return $R_{i}$ gives:

```{math}
:label: eq-expected-R-sim
\mathbb{E}\left(R_{i}\right) = \alpha_{i}+\beta_{i}\mathbb{E}\left(R_{m}\right)
```

where $\mathbb{E}\left(\epsilon_{i}\left(t\right)\right) = 0$. 
Solving Eqn. {eq}`eq-expected-R-sim` for $\beta_{i}$ gives:

```{math}
\beta_{i} = \frac{\mathbb{E}\left(R_{i}\right) - \alpha_{i}}{\mathbb{E}\left(R_{m}\right)}
```
Thus, $\beta_{i}$ is a corrected ratio of expected (average) returns:

* $\beta_{i}>1$ expected excess return of firm $i$ is _greater_ than the expected excess market return
* $\beta_{i}\sim{1}$ firm $i$ performs _similar_ to the overall market on average
* $\beta_{i}<1$ expected excess return of firm $i$ is _less_ than the expected excess market return

On the other hand, the variance of $R_{i}$:

```{math}
\text{Var}\left(R_{i}\right) = \mathbb{E}\left(R_{i}^{2}\right) - \mathbb{E}\left(R_{i}\right)^{2}
```
is given by:

```{math}
:label: eq-var-beta
\sigma_{i}^2 = \beta_{i}^{2}\sigma_{m}^{2}+\sigma_{\epsilon}^{2}
```

where $\text{Var}\left(\star\right) = \sigma_{\star}^{2}$. 
Rearranging Eqn. {eq}`eq-var-beta` gives another expression for $\beta_{i}$ in terms of the corrected variance (risk) of firm $i$

```{math}
\beta_{i}^{2} = \frac{\sigma_{i}^2 - \sigma_{\epsilon}^{2}}{\sigma_{m}^{2}}
```

In the context of risk, $\beta_{i}$ has the interpretation:

* $\beta_{i}>1$ suggests firm $i$ has _greater risk_ than the overall market
* $\beta_{i}\sim{1}$ suggests that firm $i$ has the _same risk_ as the overall market on average
* $\beta_{i}<1$ suggests firm $i$ has _less risk_ compared to overall market

Putting these two regimes together gives fundamental insight into the behavior of markets: __high returns come with high-risk__. 

````

### Expected Excess Returns from Data
Suppose we had a data set $\mathcal{P}$ that contained the daily close
price for a share of stock of firm $i$ for the last $T$ days, e.g., $1\rightarrow{T}$. 
Let the ticker symbol for firm $i$ be given by `XYZ`.
Then, from the definition of expectation, we know the expected excess return for `XYZ` is given by:

```{math}
:label: eq-defn-expected-return
\mathbb{E}\left(R_{i}\right) = \sum_{t}p(t)R_{i,t}
```

where the probability terms are subject to $\sum_{t}p(t) = 1$. The probability terms in Eqn. {eq}`eq-defn-expected-return` have several interpretations. First, they could represent the output
of some (unknown) market process governing the returns. Another actionable interpretation is to think of them as weighting
factors. Suppose the recent trend in `XYZ` prices is significantly different from long-term historical price trends, e.g., `XYZ` has recently experienced a sustained period of decline. You could weigh the recent data more highly
to calculate an expected return (or volatility) that is more representative of current trends. Of course, the opposite could also be true; you could also empathize older versus newer data. 

Many weighting schemes could be used; any approach that obeys the axioms of probability will work! However, let's borrow a strategy from chemical physics, namely, we'll assume $p(t)$ follows the [Boltzmann distribution](https://en.wikipedia.org/wiki/Boltzmann_distribution).

````{prf:definition} Boltzmann weighted excess returns
:label: defn-bwer

The expected excess return for firm $i$ is given by:

```{math}
\mathbb{E}\left(R_{i}\right) = \sum_{t}p(t)R_{i,t}
```

where $R_{i,t}$ denotes the excess return in time period $t$ for firm $i$. 
Further, let the probability factors $p(t)$ follow a [Boltzmann distribution](https://en.wikipedia.org/wiki/Boltzmann_distribution):

```{math}
p(t) = \frac{1}{Z}\exp(-\lambda\epsilon_{t})
```

where the partition function $Z$ is given by $Z = \sum_{t}\exp(-\lambda\epsilon_{t})$, $\lambda\geq{0}$ is an adjustable parameter, and $\epsilon_{t}>0$ is the pseudo energy of the market at time $t$.  Then, the Boltzmann weighted expected excess return $\mathbb{E}_{B}\left(R_{i}\right)$ is given by: 

```{math}
\mathbb{E}_{B}\left(R_{i}\right) = \frac{1}{Z}\sum_{t}\exp\left(-\lambda\epsilon_{t}\right){R}_{i,t}
```
````

Depending upon how we choose $\lambda$ and the pseudo energies in {prf:ref}`defn-bwer`, we can recover 
equally weighted, past or present exponentially weighted expectations.

```{prf:algorithm} Boltzmann Weighted Expected Return 
:label: algo-expected-boltzmann-return

**Inputs** Ticker `XYZ` price dataset $\bar{\mathcal{P}}$ for time period $1\rightarrow T$, 
annualized risk free rate $r_{f}$, time-window $\mathcal{L}$, $\lambda$, and $\epsilon_{t}>0$ values

**Outputs** Boltzmann weighted expected return $\mathbb{E}_{B}\left(R\right)$, 
the unweighted excess return vector $R$, and the probability array $p$

**Initialize**
1. sort dataset $\mathcal{P}\leftarrow\bar{\mathcal{P}}$ from newest to oldest prices.
1. initialize $R~\leftarrow$ Array($\mathcal{L}$,1)
1. initialize $W~\leftarrow$ Array($\mathcal{L}$,1)
1. initialize $\mathcal{R}~\leftarrow$ Array($\mathcal{L}$,1)

**Main**
1. for t $\in$ 1:$\mathcal{L}$

    1. compute excess return $R[t]\leftarrow \log\left(P[t]/P[t+1]\right) - r_{f}$
    1. compute weight factor $W[t]\leftarrow \exp\left(-\lambda\times\epsilon[t]\right)$
    1. compute weighted return factor $\mathcal{R}[t] \leftarrow R[t]\times~W[t]$

**Process**
1. compute normalization constant $Z\leftarrow \sum~W$
1. compute expectation $\mathbb{E}_{B}\left(R\right)\leftarrow(1/Z)\times\sum\mathcal{R}$
1. compute probability $p\leftarrow(1/Z)\times~W$  

**Return**
1. expected return $\mathbb{E}_{B}\left(R\right)$, excess return vector $R$, and probability array $p$
```


(content:references:risk-volatility)=
## Volatility
Now that we have defined different types of returns, and the rewards of a portfolio, let's define the risk. One measure of risk is volatility, e.g., the standard deviation of the {ref}`content:references:log-return`:

````{prf:definition} Volatility
:label: defn-volatility

Let the price of asset $i$ at time $j$ be denoted by $P_{ij}>0$. Then the _volatility_ of asset $i$ is
the standard deviation of the logarithmic returns calculated between time periods 
$j\rightarrow{j+1}$.

````
We can estimate the volatility of `XYZ` directly from historical price data; calculating volatility from data
gives the _historic volatility_, a backward-looking measure of the risk. An unbiased 
estimate of the variance (which is the square of the _historic volatility_) is given by:

```{math}
\sigma_{n}^2 = \frac{1}{m-1}\sum_{i=1}^{m}\left(\bar{r}_{n-i}-\hat{\mu}_{r}\right)^2\qquad{n>{m+1}}
```
where $\bar{r}_{n-i}$ denotes logarithmic return computed for time $n-i-1\rightarrow{n-i}$ and
$\hat{\mu}_{r}$ denotes the average logarithmic return, computed using the $m$ most recent values of
the return:

```{math}
\hat{\mu}_{r} = \frac{1}{m}\sum_{i=1}^{m}\bar{r}_{n-i}
```

The choice of $(n,m)$ is up to you and the application you are interested in. A sketch of an algorithm that can be used to calculate the _historic volatility_ is given in {prf:ref}`algo-unbiased-historic-volatility`:

```{prf:algorithm} Unbiased estimate of the return variance
:label: algo-unbiased-historic-volatility

**Inputs** Ticker `XYZ` price dataset $\bar{\mathcal{P}}$ for time period $1\rightarrow T$, parameters $(n,m)$ where $n>m+1$ and $\texttt{avg}$ a function that computes the average of a vector.

**Outputs** An unbiased estimate of the return variance $\sigma_{n}^{2}$

**Initialize**
1. sort dataset $\mathcal{P}\leftarrow\bar{\mathcal{P}}$ from newest to oldest prices.
1. initialize $\bar{R}~\leftarrow$ Array($m$,1)
1. initialize $\mu_{r}$ = 0
1. initialize $\text{tmp}$ = 0

**Compute $\bar{R}$**
1. for i $\in~1:m$
  
    1. compute $\bar{r}_{n-i}\leftarrow\log\left(\frac{P_{n-i}}{P_{n-i-1}}\right)$
    1. store $\bar{R}[i]\leftarrow{\bar{r}_{n-i}}$

**Compute $\mu_{r}$**
1. compute $\mu_{r}\leftarrow\texttt{avg}\left(\bar{R}\right)$

**Compute $\sigma_{n}^{2}$**
1. for i $\in~1:m$

    1. compute $\text{tmp}~\leftarrow~\text{tmp}~+ \left( \bar{R}[i] - \mu_{r} \right)^2$

1. compute $\sigma_{n}^{2}\leftarrow\frac{1}{m-1}\cdot\text{tmp}$

**Return**
1. return $\sigma_{n}^{2}$
```

### Example
* [Computation of the unbiased historical volatility using {prf:ref}`algo-unbiased-historic-volatility`](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-UnbiasedVolatility-Estimation.jl.html)

## Summary