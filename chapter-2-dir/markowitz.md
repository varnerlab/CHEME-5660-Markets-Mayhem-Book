# Modern Portfolio Theory
Modern portfolio theory (MPT) is a practical method for selecting collection of assets e.g., stocks or bonds in order to maximize the overal reward of the investor within an acceptable level of risk to the investor. Harry Markowitz, who developed the mathematical foundation of MPT {cite}`MPT1952`, was later awarded a [Nobel Prize for his work in 1990](https://www.nobelprize.org/prizes/economic-sciences/1990/markowitz/facts/). The central theme of Markowitz is to balance risk and reward, where reward is measured as the [return](https://www.investopedia.com/terms/r/return.asp) of a basket of assets, while risk is measured as the standard deviation of the logrithmic return, otherwise known as [volatility](https://en.wikipedia.org/wiki/Volatility_(finance)). 

## Returns

### Single Index Return Models
The single-index model (SIM), developed by William Sharpe, is an asset pricing model which measures both the risk and the return of a stock {cite}`SHARPE1963`. The single index model describes the return of the stock of firm $i$ in terms of a firm-specific return, and the overall market return:

```{math}
:label: eq-single-index-model
r_{i}\left(t\right) - r_{f} = \alpha_{i}+\beta_{i}\left(r_{m}\left(t\right)-r_{f}\right)+\epsilon_{i}
\left(t\right)\qquad{t=1,2,\dots,T}
```

The term $r_{i}\left(t\right)$ denotes the return of firm $i$, during time period $t$, 
$r_{f}$ denotes the risk-free rate i.e., the interest rate on a riskless investment such as treasury bills, while $r_{m}\left(t\right)$ denotes the return on a market portfolio e.g., an index such as the [S\&P500](https://en.wikipedia.org/wiki/S%26P_500) during time period $t$.  The term $\alpha_{i}$ denotes the firm-specific return, while $\beta_{i}$ denotes the proportion of the the firm's return associated with the overall market. Finally, $\epsilon_{i}\left(t\right)\sim\mathcal{N}\left(0,\sigma_{i}^{2}\right)$ is the unexplained (random) return of stock $i$, which is assumed to be normally distributed with mean zero and standard deviation $\sigma_{i}$. The term $R_{i}(t)\equiv\left(r_{i}\left(t\right) - r_{f}\right)$ describes the excess return of specific firm $i$, while $R_{m}(t)\equiv\left(r_{m}\left(t\right)-r_{f}\right)$ describes the excess return of the market portfolio. Replacing the excess returns gives the single index model in standard
form:

```{math}
:label: eq-single-index-model-standard
R_{i}\left(t\right) = \alpha_{i}+\beta_{i}R_{m}\left(t\right)+\epsilon_{i}
\left(t\right)\qquad{t=1,2,\dots,T}
```

In Eqn {eq}`eq-single-index-model-standard`, the quantity $\beta_{i}$ has several interpretations. 
First, $\beta_{i}$ measures how the excess return of firm $i$ moves with the overall excess return of the market. Thus, $\beta_{i}$ can be thought of as a proportionality constant, a large $\beta_{i}$ suggests large swings in the return of firm $i$ relative to the overall market return. 

On the other hand, $\beta_{i}$ can also be interpreted as a measure of risk. To understand the risk interpretation of $\beta_{i}$, we first must understand that both the firm specific $R_{i}$ and overall market excess returns $R_{m}$ are random variables. Thus, we can compute the expectation and variance of these variables and look at how these quantities depend upon $\beta_{i}$:

````{prf:observation} Risk intepretation of $\beta_{i}$
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

* $\beta_{i}>1$ suggests the expected excess return of firm $i$ is _greater_ than the expected excess market return
* $\beta_{i}\sim{1}$ suggests that firm $i$ performs _similar_ to the overall market on average
* $\beta_{i}<1$ suggests the expected excess return of firm $i$ is _less_ than the expected excess market return

On the other hand, the variance of $R_{i}$:

```{math}
\text{Var}\left(R_{i}\right) = \mathbb{E}\left(R_{i}^{2}\right) - \mathbb{E}\left(R_{i}\right)^{2}
```
is given by:

```{math}
\sigma_{i}^2 = \beta_{i}\sigma_{m}^{2}+\sigma_{\epsilon}^{2}
```

where $\text{Var}\left(\star\right) = \sigma_{\star}^{2}$. 

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

