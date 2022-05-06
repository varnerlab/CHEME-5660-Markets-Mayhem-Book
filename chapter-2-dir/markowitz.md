# Modern Portfolio Theory
Modern portfolio theory (MPT) is a practical method for selecting collection of assets e.g., stocks or bonds in order to maximize the overal reward of the investor within an acceptable level of risk to the investor. Harry Markowitz, who developed the mathematical foundation of MPT {cite}`MPT1952`, was later awarded a [Nobel Prize for his work in 1990](https://www.nobelprize.org/prizes/economic-sciences/1990/markowitz/facts/). 

The central theme of Markowitz is the balance risk and reward, where reward is measured as the [return](https://www.investopedia.com/terms/r/return.asp) of a basket of assets, while risk is measured as the standard deviation (or sometimes the variance) of the logrithmic return, otherwise known as [volatility](https://en.wikipedia.org/wiki/Volatility_(finance)). 

## Returns
The return of an asset is a measure of the difference in the price of that asset between two time periods. 
Return can be calculated in many ways; two common approaches are the percentage or fractional return and the
logarithmic return. 

(content:references:fractional-return)=
### Fractional return

````{prf:definition} Fractional return
:label: defn-percentage-return

Let the price of asset $i$ at any time $j$ be denoted by $P_{ij}>0$. Then the fractional return 
on asset $i$ over time horizon $j\rightarrow{k},i\neq{k}$ is defined as: 

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

(content:references:log-return)=
### Logarithmic return

````{prf:definition} Logarithmic return
:label: defn-log-return

Let the price of asset $i$ at any time $j$ be denoted by $P_{ij}>0$. Then the logarithmic return 
on asset $i$ over time horizon $j\rightarrow{k},i\neq{k}$ is defined as: 

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

Let $R_{i}(t)$ and $R_{m}(t)$ denote the firm specific and market excess returns (random) for time period $t$.
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



<!-- as a ratio of risks, i.e., the risk of firm $i$ normalized by the overall market risk. Thus, values of $\beta_{i}$ fall into the ranges:



* $\beta_{i}>1$: Firm $i$ is riskier than the overall market
* $\beta_{i}\sim{1}$: Firm $i$ has approximately the same risk as the overall market
* $\beta_{i}<{1}$: Firm $i$ has less risk than the overall market
* $\beta_{i}\sim{0}$: Firm $i$ is risk-free or firm $i$ is completely uncorrelated with the overall market
* $\beta_{i}<{0}$: Firm $i$ is anti-correlated with the overall market -->




## Volatility


## The Markowitz Portfolio Allocation Problem
Fill me in.

