# Data-Driven Portfolio Theory

Modern portfolio theory (MPT), a method for selecting a portfolio of assets, e.g., a collection of stocks or bonds, maximizes the overall reward an investor recieves, gievn an acceptable level of risk. In particular, we'll explore Markowitz portfolio optimization; Harry Markowitz, who developed the mathematical foundation of MPT {cite}`MPT1952`, was later awarded a [Nobel Prize for his work in 1990](https://www.nobelprize.org/prizes/economic-sciences/1990/markowitz/facts/). 

The central theme of modern portfolio theory is balancing risk and reward. Reward is measured as the [expected return](https://www.investopedia.com/terms/r/return.asp) of a portfolio of assets, while, the risk is calculated as the variance of the logarithmic or fraction return of the portfolio. Thus, the objective of modern portfolio theory is to balance the composition of the portfolio such that an investor obtains a desired expected return while minimizing the variance (risk). 

For a more detailed discussion of MPT, see Part II (chapters 5 - 8) of Bodie, Kane, and Marcus {cite}`Bodie:2011ug`.

In this chapter, we will:

* Introduce {ref}`content:references:markowitz` for a portfolio of risky and risk-free assets
* Introduce {ref}`content:references:markowitz-solution` and {ref}`content:references:markowitz-solution-sim`
* Explore the question {ref}`content:references:markowitz-solution-test`
---

(content:references:markowitz)=
## Markowitz Portfolio Allocation
Markowitz portfolio allocation assumes that investors are risk-averse and rational. 
Thus, if an investor chooses between two portfolios that offer _the same expected return_, a rational risk-averse investor will choose the less risky portfolio. Further, a rational risk-averse investor will incur increased risk only if compensated for this risk by a higher expected return, the so-called high-risk, high-reward paradigm. On the other hand, an investor who wants higher expected returns must accept more risk. However, the acceptable trade-off between risk and reward will differ for each investor; what you may find as an acceptable risk versus reward is not the same for everyone. Thus, a rational risk-averse investor will not invest in a portfolio if a second portfolio exists with a more favorable risk-expected return profile. 

```{prf:remark} Markowitz in Words
:label: remark-markowitz-in-words

Suppose we have a set of assets $\mathcal{A}$ composed of risky, e.g., equities and equity derivatives, and risk-free assets, e.g., treasury debt securities. The Markowitz portfolio allocation problem estimates the weight $\omega_{a}$ of asset $a$ for $\forall{a}\in\omega_{a}$ that minimizes the risk for a user-specified return.  

```

To make these ideas more concrete, let's develop expressions for the risk and reward of a 
portfolio. Denote the set of assets in a portfolio as $\mathcal{P}$; where $\vert\mathcal{P}\vert$ denotes the number of assets in the portfolio set. Then, the expected return (reward) of the portfolio $\mathcal{P}$ is defined as ({prf:ref}`defn-portfolio-return`):

````{prf:definition} Expected Portfolio Return
:label: defn-portfolio-return

Suppose we have a set of assets represented as $\mathcal{A}$. We can arrange these assets into a portfolio $\mathcal{P}$. Denote the return of asset $i$ in portfolio $\mathcal{P}$ on some time basis $\mathcal{B}$ as $r_{i}$. 

Then, the expected return of portfolio $\mathcal{P}$ denoted by 
$\mathbb{E}\left(r_{\mathcal{P}}\right)$ is:

```{math}
:label: eqn-expected-p-rerturn
\mathbb{E}\left(r_{\mathcal{P}}\right) = \sum_{i\in\mathcal{P}}\omega_{i}\mathbb{E}\left(r_{i}\right)
```

where $w_{i}$ denotes the fraction of asset $i$ in the portfolio $\mathcal{P}$, and 
$\mathbb{E}\left(r_{i}\right)$ denotes the expected return of asset $i$ on time basis $\mathcal{B}$.

````

while the variance (risk) of the portfolio is defined as ({prf:ref}`defn-portfolio-variance`):

````{prf:definition} Portfolio Variance
:label: defn-portfolio-variance

Denote the return of asset $i$ in portfolio $\mathcal{P}$ for some time basis $\mathcal{B}$ 
as $r_{i}$. Then, the variance of a portfolio $\mathcal{P}$ is given by:

```{math}
:label: eqn-p-var-general
\sigma_{\mathcal{P}}^2 = 
\sum_{i\in\mathcal{P}}\sum_{j\in\mathcal{P}}w_{i}w_{j}
\text{cov}\left(r_{i},r_{j}\right)
```

where $w_{\star}$ denotes the fraction of asset $\star$ in the portfolio $\mathcal{P}$, and 
$\text{cov}\left(r_{i},r_{j}\right)$ denotes the covariance between the return on assets $i$ and $j$.
The $\text{cov}\left(r_{i},r_{j}\right)$, which quantifies the relationship between assets $i$ and $j$, is given by:

```{math}
\text{cov}\left(r_{i},r_{j}\right) = \sigma_{i}\sigma_{j}\rho_{ij}
```

where $\sigma_{\star}$ denote the standard deviation of the return of asset $\star$, and 
$\rho_{ij}$ denotes the correlation between assets $i$ and $j$.

````

Now that we know how to compute a portfolio’s risk and expected reward let’s think about what we can control as a financial engineer. Of course, we cannot control the return or volatility of asset $i$; the market drives those. However, we can control which assets we include in the portfolio and the relative amount of each of these assets. Thus, how we choose which assets to include and their associated weights give insight into the type of investor we are. If we are a Markowitz investor, we minimize the risk required to obtain a specified reward. 

````{prf:observation} The role of correlation in $\mathcal{P}$
An exciting feature of the variance of the portfolio return ({prf:ref}`defn-portfolio-variance`) is the dependence on the [correlation](https://en.wikipedia.org/wiki/Correlation) denoted by $\rho_{ij}$ between assets $i$ and $j$. To see why this is exciting, let's consider a portfolio $\mathcal{P}$ consisting of two risky assets; $\vert\mathcal{P}\vert$ = 2. Then, the variance of the portfolio returns $\sigma_{\mathcal{P}}^{2}$ is given by:

```{math}
\sigma_{\mathcal{P}}^2 = w_{1}^{2}\sigma_{1}^{2}+w_{2}^{2}\sigma_{2}^{2}+2w_{1}w_{2}\sigma_{1}
\sigma_{2}\rho_{12}
```
where $w_{\star}$ is the fraction of asset $\star$ in the portfolio, and 
$\sigma_{\star}$ denotes the standard deviation of the return of asset $\star$. 
Thus, we can influence the overall portfolio variance by choosing the assets 
based upon their correlation.

* __Positive correlation__: For two assets that are positively correlated $p_{12}>{0}$, 
the variance of the return of the portfolio $\sigma_{\mathcal{P}}^{2}$ is _greater_ than to the variance of the assets alone (assuming $w_{\star}\geq{0}$).
* __Zero (or small) correlation__: For two assets that are either perfectly uncorrelated $p_{12} = 0$ (or have small correlation $p_{12}\ll{1}$), 
the variance of the return of the portfolio $\sigma_{\mathcal{P}}^{2}$ is _similar to_ the variance of the assets alone (assuming $w_{\star}\geq{0}$).
* __Negative correlation__: For two assets that are negatively correlated $p_{12}<0$, the variance of the return of the portfolio $\sigma_{\mathcal{P}}^{2}$ is _less_ than to the variance of the assets alone (assuming $w_{\star}\geq{0}$).
````

Further, the correlation does not appear in the expected portfolio return ({prf:ref}`defn-portfolio-return`); thus, by carefully selecting assets with low correlation, the overall risk of a portfolio can be reduced without impacting the return (all else being equal). 

### Markowitz allocation for risk assets only
In the risky asset only case, the asset set $\mathcal{A}$ is composed only of shares of common stock. The Markowitz allocation problem for a portfolio of risky assets is defined in {prf:ref}`defn-markowitz-risky-assets-only`.

````{prf:definition} Risky Markowitz Portfolio
:label: defn-markowitz-risky-assets-only

The Markowitz allocation problem for a portfolio $\mathcal{P}$ composed of __only__ risky assets is the [quadratic program](https://en.wikipedia.org/wiki/Quadratic_programming):

$$\min_{w} \sigma^{2}_{\mathcal{P}}\left(w\right)$$

subject to the constraints:

$$
\begin{eqnarray}
\mathbb{E}(r_{\mathcal{P}})&\geq&{R^{*}}\\
1^{T}w &=& 1\\
w_{i}&\geq&{0}\qquad{\forall{i}\in\mathcal{P}}
\end{eqnarray}
$$

where $w$ denotes the vector of weights of the assets in portfolio $\mathcal{P}$, $\sigma^{2}_{\mathcal{P}}\left(w\right)$ represents the portfolio variance; the portfolio variance can re-written as $\sigma^{2}_{\mathcal{P}}\left(w\right) = w^{T}\Sigma{w}$  where $\Sigma$ is the [covariance matrix](https://en.wikipedia.org/wiki/Covariance_matrix). The quantity $\mathbb{E}(r_{\mathcal{P}})$ denotes the expected return (or excess return) of the portfolio $\mathcal{P}$; the expected return (or excess return) can be re-written as $w^{T}\mathbb{E}(r)$ where $\mathbb{E}(r)$ denotes the vector of expected returns (or excess returns) for each asset in the portfolio. 

The quantity $R^{*}$ denotes the minimal required return for $\mathcal{P}$, and $1^{T}$ represents a vector of ones (total allocation constraint). The last constraint $w_{i}\geq{0}~\forall{i}\in\mathcal{P}$ says that no short selling (borrowing shares) is allowed; if short selling is allowed, then this constraint can be removed.
````

A schematic of the solution of risky Markowitz problem defined in {prf:ref}`defn-markowitz-risky-assets-only` is given in {numref}`fig-markowitz-only-risk`.

 ```{figure} ./figs/Fig-Markowitz-Only-Risky.pdf
---
height: 440px
name: fig-markowitz-only-risk
---
Schematic of the solution to the Markowitz allocation problem for a collection of risky assets.
```

A couple of thoughts:
* While the problem above is written in terms of absolute return $r_{\star}$, we can also write the portfolio allocation problem using excess returns; the excess return is $R_{\star} = r_{\star} - r_{f}$, where $r_{f}$ denotes the risk-free rate of return.
* The challenge to solving the Markowitz problem is estimating the expected return of assets in the portfolio and the covariance matrix $\Sigma$. These quantities can be calculated from available data or from models of the return and variance of the assets in the portfolio. We'll consider both approaches.
* Which portfolio along the efficient frontier in {numref}`fig-markowitz-only-risk` is up to the risk-reward tolerance of the investor; some investors are willing to take the additional risk because they expect to be rewarded with an increased return, others are not. 
* The minimum variance portfolio represents the maximum reward given the minimum risk. 



### Portfolios of risky and risk-free assets
Suppose that our asset set $\mathcal{A}$ now contains both risky assets, i.e., shares of stock and a risk-free asset, e.g., [debt securities](./bonds.md). Thus, we have a guaranteed return associated with the risk-free asset, while the return associated with the risky assets is governed by the risk measure. 

````{prf:definition} Risky and Risk-free Markowitz
:label: defn-risky-risk-free-markowitz

The Markowitz allocation problem for a portfolio $\mathcal{P}$ composed of both risky and risk-free assets is the [quadratic program](https://en.wikipedia.org/wiki/Quadratic_programming):

```{math}
\min_{w} \sigma^{2}_{\mathcal{P}}\left(w\right)
```

subject to the constraints:

$$
\begin{eqnarray}
\left(1-\sum_{i\in\mathcal{P}}\omega_{i}\right)r_{f}+\mathbb{E}(r_{\mathcal{P}})&\geq&{R^{*}}\\
w_{i}&\geq&{0}\qquad{\forall{i}\in\mathcal{P}}
\end{eqnarray}
$$

where $w$ denotes the vector of weights of the assets in portfolio $\mathcal{P}$, $\sigma^{2}_{\mathcal{P}}\left(w\right)$ represents the portfolio variance; the portfolio variance can re-written as $\sigma^{2}_{\mathcal{P}}\left(w\right) = w^{T}\Sigma{w}$  where $\Sigma$ is the [covariance matrix](https://en.wikipedia.org/wiki/Covariance_matrix). The quantity $\mathbb{E}(r_{\mathcal{P}})$ denotes the expected return (or excess return) of the portfolio $\mathcal{P}$; the expected return (or excess return) can be re-written as $w^{T}\mathbb{E}(r)$ where $\mathbb{E}(r)$ denotes the vector of expected returns (or excess returns) for each asset in the portfolio. 

The quantity $R^{*}$ denotes the minimal required return for $\mathcal{P}$, and $1^{T}$ represents a vector of ones (total allocation constraint). The last constraint $w_{i}\geq{0}~\forall{i}\in\mathcal{P}$ says that no short selling (borrowing shares) is allowed; if short selling is allowed, then this constraint can be removed.
````

A schematic of the solution of risky and risk-free Markowitz problem defined in {prf:ref}`defn-risky-risk-free-markowitz` is given in {numref}`fig-markowitz-risky-and-risky-free`.

 ```{figure} ./figs/Fig-Markowitz-Risk-Free-Asset.pdf
---
height: 440px
name: fig-markowitz-risky-and-risky-free
---
Schematic of the solution to the Markowitz allocation problem for a combination of risky and a risk-free asset.
```

A couple of thoughts on {numref}`fig-markowitz-risky-and-risky-free`:
* While the problem above is written in terms of absolute return $r_{\star}$, we can also write the portfolio allocation problem using excess returns; the excess return is $R_{\star} = r_{\star} - r_{f}$, where $r_{f}$ denotes the risk-free rate of return.
* The challenge to solving the Markowitz problem is estimating the expected return of assets in the portfolio and the covariance matrix $\Sigma$. These quantities can be calculated from available data or from models of the return and variance of the assets in the portfolio. We'll consider both approaches.
* The tangency point in {numref}`fig-markowitz-risky-and-risky-free` is the optimal portfolio of risky assets.


(content:references:markowitz-solution)=
## Data-Driven Markowitz Allocation 
The objective of Markowitz portfolio allocation problem is to estimate the weights $w=\left(w_{1},w_{2},\dots\right)^{T}$ of the assets in portfolio $\mathcal{P}$  such that overall variance of the portfolio is minimized, for a specified return, subject to some constraints on $w$. 

The return of an asset is a measure of the price difference of that asset between two time periods. 
Return can be calculated in many ways; two common approaches are the percentage or fractional return and the logarithmic return. 

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

Consider the daily return on stock `XYZ` computed using the close price and the fractional return measure. Let $P_{ij}$ denote the close price today, and $P_{ij-1}$ denote the close price for the previous trading day. Then, the fractional daily return is given by:

```{math}
:label: eq-example-daily-close-price

r_{i,j-1\rightarrow{j}} = \frac{P_{ij} - P_{i,j-1}}{P_{i,j-1}}
```
````

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

Consider the daily return on stock `XYZ` computed using the close price and the fractional return measure. Let $P_{ij}$ denote the close price today, and $P_{ij-1}$ denote the close price for the previous trading day. Then, the fractional daily return is given by:

```{math}
:label: eq-example-daily-close-price-log

\bar{r}_{i,j-1\rightarrow{j}} = \log\left(\frac{P_{ij}}{P_{i,j-1}}\right)
```
````

However, Eqn. {eq}`eq-example-daily-close-price-log` can be rearranged to give an expression similar to 
Eqn. {eq}`eq-cont-exchange-tvm`:

```{math}
P_{ij} = \exp\left(\bar{r}_{i,j-1\rightarrow{j}}\right)P_{i,j-1}
```

Thus, the logarithmic daily return (or a logarithmic return computed between any two different dates) is a continuous discount rate that quantifies how the value of an asset, e.g., the share price of ticker `XYZ`, changes because of market forces. Becuase $P_{i,\star}$ is a random variable, the return is also a random variable. 

### Expected excess returns from data
Suppose we had a data set $\mathcal{P}$ that contained the daily close price firm $i$ for the last $T$ days, e.g., $1\rightarrow{T}$. 
Let the ticker symbol for firm $i$ be given by `XYZ`.
Then, from the definition of expectation, we know the expected excess return for `XYZ` is given by:

```{math}
:label: eq-defn-expected-return
\mathbb{E}\left(R_{i}\right) = \sum_{t}p(t)R_{i,t}
```

where the probability $\sum_{t}p(t) = 1$. The probability terms in Eqn. {eq}`eq-defn-expected-return` have several interpretations. First, they could represent the output of some (unknown) market process governing the returns. Another actionable interpretation is to think of them as weighting factors. 

Suppose the recent trend in `XYZ` prices is significantly different from long-term historical price trends, e.g., `XYZ` has recently experienced a sustained period of decline. You could weigh the recent data more highly to calculate an expected return (or volatility) that is more representative of current trends. Of course, the opposite could also be true; you could also empathize older versus newer data. 

Many weighting schemes could be used; any approach that obeys the axioms of probability will work! However, let's borrow a strategy from chemical physics, namely, we'll assume $p(t)$ follows the [Boltzmann distribution](https://en.wikipedia.org/wiki/Boltzmann_distribution).

````{prf:definition} Boltzmann weighted excess returns
:label: defn-bwer

Let the excess return values for firm $i$ at the time intervals $t=1,2,\dots,T$ be represented by $R_{i,t}$; the expected excess return for a firm $i$ is represented by:

```{math}
\mathbb{E}\left(R_{i}\right) = \sum_{t=1}^{T}p(t)R_{i,t}
```

where $R_{i,t}$ denotes the excess return in time period $t$ for firm $i$. 
Further, let the probability factors $p(t)$ follow a [Boltzmann distribution](https://en.wikipedia.org/wiki/Boltzmann_distribution):

```{math}
p(t) = \frac{1}{Z}\exp(-\lambda\epsilon_{t})
```

where the partition function $Z$ is defined as:

```{math}
:label: eqn-partition-factor-bw
Z = \sum_{t=1}^{T}\exp(-\lambda\epsilon_{t})
```

The adjustable parameter $\lambda\geq{0}$ controls the rate of decay, while $\epsilon_{t}>0$ is a pseudo energy of the market at time $t$; although more interesting functions may be possible to model the energy of a market, let $\epsilon_{t} = t$.

Then, the Boltzmann weighted expected excess return for $\epsilon_{t} = t$ is given by: 

```{math}
:label: eqn-boltzmann-weight-expectation
\mathbb{E}_{B}\left(R_{i}\right) = \frac{1}{Z}\sum_{t=1}^{T}\exp\left(-\lambda{t}\right){R}_{i,t}
```

````

Depending upon how we choose $\lambda$ and the pseudo energies in {prf:ref}`defn-bwer`, we can recover 
equally weighted, past or present exponentially weighted expectations.

```{prf:algorithm} Boltzmann Weighted Expected Return 
:class: dropdown
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

    1. compute excess return $R[t]\leftarrow \log\left(P[t]/P[t-1]\right) - r_{f}$
    1. compute weight factor $W[t]\leftarrow \exp\left(-\lambda\times\epsilon[t]\right)$
    1. compute weighted return factor $\mathcal{R}[t] \leftarrow R[t]\times~W[t]$

**Process**
1. compute normalization constant $Z\leftarrow \sum~W$
1. compute expectation $\mathbb{E}_{B}\left(R\right)\leftarrow(1/Z)\times\sum\mathcal{R}$
1. compute probability $p\leftarrow(1/Z)\times~W$  

**Return**
1. expected return $\mathbb{E}_{B}\left(R\right)$, unweighted excess return vector $R$,  weighted excess return vector $\mathcal{R}$, and probability array $p$
```

#### Example
* Markowitz portfolio allocation using Boltzmann weighted excess returns. [Live notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or a [static HTML view](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/jupyter-notebooks/html/Example-SIM-Boltzmann-Markowitz-Allocation.html). 

(content:references:risk-volatility)=
### Volatility and the Covariance Matrix
Now that we have defined different types of returns, the rewards of a portfolio, let's define the risk. One measure of risk is volatility, e.g., the standard deviation of the {ref}`content:references:log-return`:

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

(content:references:markowitz-solution-sim)=
## Model-Driven Markowitz Allocation


(content:references:markowitz-solution-test)=
## Does Markowitz Portfolio Allocation work?

Let's try to get a sense of whether Markowitz portfolios work in practice. 

(content:references:buy-and-hold-strategy)=
### Buy and Hold Strategy
We have tools to measure the risk and reward of stocks, now, let's begin the discussion of investment strategies. The [buy and hold strategy](https://www.investopedia.com/terms/b/buyandhold.asp) is arguably the most straightforward approach for investing in stocks (or ETFs). In this approach, an investor buys shares of `XYZ` on a regular basis and then holds these shares indefinitely, regardless of the short-term price fluctuations in `XYZ.` 

The [buy and hold strategy](https://www.investopedia.com/terms/b/buyandhold.asp) is a passive investment approach. No consideration is given to unrealized gains (or losses), and no adjustments are made to the fund other than adding new shares. However, while this approach may appear naive, it can be surprisingly successful. 

The keys to the success of the [buy and hold strategy](https://www.investopedia.com/terms/b/buyandhold.asp) are:

* The expected return of the market, when viewed over a long time horizon, is positive; thus, stocks (or ETFs) with $\beta>0$ will (on average) be expected to appreciate. 
* Further, because the investor is periodically adding new shares of `XYZ` to their overall portfolio, the average share price of `XYZ` held by the investor can reflect short-term price fluctuations. 

Let's explore these two points with an example:   

````{prf:example} Buy and hold strategy for [SPY](https://finance.yahoo.com/quote/SPY/) 
:label: example-average-cost

Suppose we purchased \$1.00's worth of [SPY](https://finance.yahoo.com/quote/SPY/) shares at the close of every trading day over a five year period. 

Finish me. 

````



---

## Summary
In this section, we introduced Modern portfolio theory (MPT), a method for selecting a portfolio of assets, e.g., a collection of stocks or bonds, that maximize the overall reward an investor recieves, gievn an acceptable level of risk. In particular, we explored Markowitz portfolio optimization; Harry Markowitz, who developed the mathematical foundation of MPT {cite}`MPT1952`, was later awarded a [Nobel Prize for his work in 1990](https://www.nobelprize.org/prizes/economic-sciences/1990/markowitz/facts/). 

The central theme of modern portfolio theory is balancing risk and reward. Reward is measured as the [expected return](https://www.investopedia.com/terms/r/return.asp) of a portfolio of assets, while, the risk is calculated as the variance of the logarithmic or fraction return of the portfolio. Thus, the objective of modern portfolio theory is to balance the composition of the portfolio such that an investor obtains a desired expected return while minimizing the variance (risk). 

In this chapter, we:

* Introduced {ref}`content:references:markowitz` for a portfolio of risky and risk-free assets
* Introduced {ref}`content:references:markowitz-solution` and {ref}`content:references:markowitz-solution-sim`
* Explored the question {ref}`content:references:markowitz-solution-test`
