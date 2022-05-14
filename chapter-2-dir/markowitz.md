---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Julia
  language: julia
  name: julia-1.7
---

# Modern Portfolio Theory
Modern portfolio theory (MPT) is a practical method for selecting a collection of assets, e.g., stocks or bonds, to maximize the overall reward of the investor within an acceptable level of risk to the investor. Harry Markowitz, who developed the mathematical foundation of MPT {cite}`MPT1952`, was later awarded a [Nobel Prize for his work in 1990](https://www.nobelprize.org/prizes/economic-sciences/1990/markowitz/facts/). 

The central theme of Markowitz is the balance between risk and reward, where the reward is measured as the [return](https://www.investopedia.com/terms/r/return.asp) of a basket of assets. In contrast, the risk is calculated as the standard deviation (or sometimes the variance) of the logarithmic return, otherwise known as [volatility](https://en.wikipedia.org/wiki/Volatility_(finance)). 

In this chapter:
* We introduce the idea of reward as a {ref}`content:references:return` on the price of an asset
* We introduce the idea of risk as the {ref}`content:references:risk-volatility` of the return
* We introduce the {ref}`content:references:markowitz`

---

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

Thus, the logarithmic daily return (or a logarithmic return computed between any two different dates) is a continuous discount rate that quantifies how the value of an asset, e.g., the share price of ticker `XYZ`, changes because of market forces. 
Becuase $P_{i,\star}$ is a random variable, the return is also a random variable. 

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
Now that we have defined different types of returns, and the rewards of a portfolio, let's define
risk. This risk of an asset or a collection of assets can be quantified by asset price volatility.
The volatility of an asset price e.g., the share price of firm $i$ with ticker symbol `XYZ` is 
defined as the standard deviation of the {ref}`content:references:log-return`:

````{prf:definition} Volatility
:label: defn-volatility

Let the price of asset $i$ at time $j$ be denoted by $P_{ij}>0$. Then the _volatility_ of asset $i$ is
the standard devivation $\sigma_{i}$ of the logarithmic returns calculated between time periods 
$j\rightarrow{j+1}$.

````

We can compute the volatility of the share price of `XYZ` from historic data; computing the volatility from data
gives the _historic volatility_ which is a backward looking measure of the price volatility.
{prf:ref}`algo-volatility-unweighted` describes an approach to calculate the _unweighted_ volatility (along with the return) from a 
historic price dataset $\bar{\mathcal{P}}$; an _unweighted_ volatility (return) assumes all price values in dataset $\bar{\mathcal{P}}$
are equally important.  

```{prf:algorithm} Unweighted Historic Return and Volatility for Firm $i$ 
:label: algo-volatility-unweighted 

**Inputs** Ticker `XYZ` price dataset $\bar{\mathcal{P}}$ for time period $1\rightarrow T$

**Output** unweighted rerturn and volatility for ticker `XYZ`

1. sort dataset $\mathcal{P}\leftarrow\bar{\mathcal{P}}$ from newest to oldest prices.
1. initialize $\bar{r}~\leftarrow$ Array($\dim\left(T\right)$ - 1)
1. initialize $\sigma~\leftarrow$ Array($\dim\left(T\right)$ - 1)
1. for j $\in$ 2:$\dim\left(T\right)$
    
    1. $P_{1},P_{0} \leftarrow \mathcal{P}\left[j-1\right],\mathcal{P}\left[j\right]$
    2. $\bar{r}\left[j-1\right]\leftarrow\log\left(P_{1}/P_{0}\right)$

1.
1. compute mean return $\mu\leftarrow\left({\dim{T} - 1}\right)^{-1}\times\displaystyle{\sum_{k=1}^{\dim(T) - 1}\bar{r}\left[k\right]}$
1. compute $\sigma^{2} \leftarrow \left({\dim{T} - 2}\right)^{-1}\times\displaystyle{\sum_{k=1}^{\dim(T) - 1}\left(\bar{r}\left[k\right]-\mu\right)^2}$
1. $\sigma\leftarrow\sqrt{\sigma^{2}}$
1. rerurn ($\bar{r},\sigma$)
```

### Weighted Volatility
The weighted volatility for time point $n$ is computed over a window of length $m$, using data from the previous $n-1\rightarrow{n-m}$ time points:  

```{math}
:label: eqn-wghted-vol
\sigma^{2}_{n} = \sum_{i=1}^{m}\alpha_{i}\left(\bar{r}_{n-i} - \mu\right)^2
```

where $\alpha_{i}>0~\forall{i}$ denotes the weight of the ith element in the window of length $m$ such that:

```{math}
\sum_{i=1}^{m}\alpha_{i} = 1
```

Thus, while Eqn. {eq}`eqn-wghted-vol` is still a backward-looking calculation (over the previous $m$ time points), the relative  importance of each time point is controlled by the selection of the weights $\alpha_{i}$. One common approach is the [exponentially weighted moving average](https://en.wikipedia.org/wiki/Moving_average), where the weight of 
each older data value decreases exponentially but never reaches zero. An easy implementation of the 
[exponentially weighted moving average](https://en.wikipedia.org/wiki/Moving_average) is to assume 
$\alpha_{i+1} = \lambda\alpha_{i}$ where $0<\lambda\leq{1}$, which gives a recursion of the form:

```{math}
:label: eqn-wghted-vol-exma
\sigma^{2}_{n} = \lambda\sigma_{n-1}^{2} + (1-\lambda)\left(\bar{r}_{n-1} - \mu\right)^2
```

{prf:ref}`algo-volatility-exp-weighted` implements the [exponentially weighted moving average](https://en.wikipedia.org/wiki/Moving_average) approach, emphasizing recent over past data. {prf:ref}`algo-volatility-exp-weighted` was inspired by the [exponentially weighted moving average](https://en.wikipedia.org/wiki/Moving_average) discussion in Hull {cite}`HULL2009`

```{prf:algorithm} Exponentially Weighted Moving Average Return and Volatility for Firm $i$ 
:label: algo-volatility-exp-weighted

**Inputs** Ticker `XYZ` dataset $\bar{\mathcal{P}}$ for time period $1\rightarrow T$, starting index $n$, 
window length $m$, and weight parameter $\lambda$.

**Output** exponentially weighted return and volatility for ticker `XYZ`

1. sort dataset $\mathcal{P}\leftarrow\bar{\mathcal{P}}$ from newest to oldest prices.
1. initialize $\bar{r}~\leftarrow$ Array(m)

```

---

(content:references:markowitz)=
## Markowitz Portfolio Allocation Problem
Fill me in.

