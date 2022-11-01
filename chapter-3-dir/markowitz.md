# Equity, Debt and Modern Portfolio Theory

## Introduction
Modern portfolio theory (MPT) is a method for selecting a collection of assets, e.g., stocks or bonds, to maximize the overall reward of the investor within an acceptable level of risk to the investor. Harry Markowitz, who developed the mathematical foundation of MPT {cite}`MPT1952`, was later awarded a [Nobel Prize for his work in 1990](https://www.nobelprize.org/prizes/economic-sciences/1990/markowitz/facts/). 

The central theme of MPT is the balance between risk and reward, where the reward is measured as the [expected return](https://www.investopedia.com/terms/r/return.asp) of a basket of assets (called a portfolio). In contrast, the risk is calculated as the variance of the logarithmic return of the portfolio. Thus, the objective of MPT is to balance the composition of the portfolio such that an investor obtains a desired expected return while minimizing the variance (risk). For a detailed discussion of MPT, see Part II (chapters 5 - 8) of Bodie, Kane, and Marcus {cite}`Bodie:2011ug`.

In this chapter, we will:

* Introduce {ref}`content:references:markowitz` for a portfolio of risky and risk-free assets
* Introduce {ref}`content:references:markowitz-solution` and 
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



### Risky assets only
In the risky asset only case, the asset set $\mathcal{A}$ is composed only of shares of common stock. 

#### Stocks
Common stocks, also known as equity securities or equities, represent ownership shares in a corporation. Each share of common stock entitles its owner to one vote on any matters of corporate governance that are put to the vote at the corporation’s annual meeting and a share in the financial benefits of ownership. The corporation is controlled by a board of directors elected by the shareholders. The board meets a few times per year and selects the management team that runs the corporation daily. Managers have the authority to make most business decisions without the board’s specific approval. The board’s mandate is to oversee the management to ensure that it acts in the best interests of shareholders.

The two most important characteristics of common stock as an investment are its residual claim and limited liability features:

 * Residual claim means that stockholders are the last in line of all those who have a claim on the assets and income of the corporation. In liquidating the firm’s assets, the shareholders have a claim to what is left after all other claimants, such as the tax authorities, employees, suppliers, bondholders, and other creditors, have been paid. For a firm not in liquidation, shareholders have a claim to the part of operating income left over after interest and taxes have been paid. Management can either pay this residual as cash dividends to shareholders or reinvest it in the business to increase the value of the shares. 

 * Limited liability means the most shareholders can lose in the event of the corporation’s failure is their original investment. Unlike owners of unincorporated businesses, whose creditors can lay claim to the personal assets of the owner (house, car, furniture), corporate shareholders may, at worst, have worthless stock. They are not personally liable for the firm’s obligations.

#### Markowitz allocation for risk assets only
 The Markowitz allocation problem for a portfolio of risky assets is defined in {prf:ref}`defn-markowitz-risky-assets-only`.

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
* While the problem above is written in terms of absolute return $r_{\star}$, we can also write the portfolio allocation problem using excess returns; the excess return is $R_{\star} = r_{\star} - r_{f}$, where $r_{f}$ denotes the risk free rate of return.
* The challenge to solving the Markowitz problem is estimating the expected return of assets in the portfolio and the covariance matrix $\Sigma$. These quantities can be calculated from data if available or from models of the return and variance of the assets in the portfolio. Let's consider both approaches. 

The return of an asset is a measure of the price difference of that asset between two time periods. 
Return can be calculated in many ways; two common approaches are the percentage or fractional return and the logarithmic return. 


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
1^{T}w &=& 1\\
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

A couple of thoughts:
* While the problem above is written in terms of absolute return $r_{\star}$, we can also write the portfolio allocation problem using excess returns; the excess return is $R_{\star} = r_{\star} - r_{f}$, where $r_{f}$ denotes the risk free rate of return.
* The challenge to solving the Markowitz problem is estimating the expected return of assets in the portfolio and the covariance matrix $\Sigma$. These quantities can be calculated from data if available or from models of the return and variance of the assets in the portfolio. Let's consider both approaches. 

The return of an asset is a measure of the price difference of that asset between two time periods. 
Return can be calculated in many ways; two common approaches are the percentage or fractional return and the logarithmic return. 

(content:references:markowitz-solution)=
## Data-Driven Markowitz Allocation 
The objective of Markowitz portfolio allocation problem is to estimate the weights $w=\left(w_{1},w_{2},\dots\right)^{T}$ of the assets in portfolio $\mathcal{P}$  such that overall variance of the portfolio is minimized, for a specified return, subject to some constraints on $w$. 

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

### Expected Excess Returns from data
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

### Single Index Models
The application of index models to construct risky portfolios was originally proposed by Treynor and Black {cite}`FB1973`. Single index models are asset pricing models which measure the risk and the return of a stock relative to a risk-free alternative investment, e.g., [government treasury bonds](./bonds.md). A single index model describes the return of a firm’s stock in terms of a firm-specific return and the overall market return. One of the simplest (yet still widely used) single index models was developed by Sharpe {cite}`SHARPE1963`.

The single-index model developed by developed Sharpe {cite}`SHARPE1963` is an asset pricing model which measures both the risk and the return of a stock, relative to a risk free alternative investment e.g., government treasury bounds. The single index model describes the return of the stock of firm $i$ in terms of a firm-specific return, and an overall market return:

```{math}
:label: eq-single-index-model
r_{i}\left(t\right) - r_{f} = \alpha_{i}+\beta_{i}\left(r_{m}\left(t\right)-r_{f}\right)+\epsilon_{i}
\left(t\right)\qquad{t=1,2,\dots,T}
```

The term $r_{i}\left(t\right)$ denotes the return of firm $i$, during time period $t$, 
$r_{f}$ denotes the risk-free rate i.e., the [interest rate of a riskless investment such as treasury bills](https://fred.stlouisfed.org/series/DTB3), while $r_{m}\left(t\right)$ denotes the return on a market portfolio e.g., an index such as the [S\&P500](https://en.wikipedia.org/wiki/S%26P_500) during time period $t$.  The term $\alpha_{i}$ denotes the firm-specific return, while $\beta_{i}$ denotes the proportion of the the firm's return associated with the overall market. 

The term $R_{i}(t)\equiv\left(r_{i}\left(t\right) - r_{f}\right)$ describes the excess return of specific firm $i$, while $R_{m}(t)\equiv\left(r_{m}\left(t\right)-r_{f}\right)$ describes the excess return of the market portfolio. Replacing the excess returns in Eqn. {eq}`eq-single-index-model` gives the single index model in standard form:

````{prf:definition} Single index model of Sharpe
:label: defn-single-index-model-standard

Let $R_{i}(t)$ and $R_{m}(t)$ denote the firm specific and market excess returns (random variables) 
for time period $t$. Further, let $\epsilon_{i}\left(t\right)$ denote a [stationary normally distributed random noise process](https://en.wikipedia.org/wiki/Normal_distribution) with mean zero and standard deviation $\sigma_{i}$. 

Then, the single index model of Sharpe is given by {cite}`SHARPE1963`:

```{math}
:label: eq-single-index-model-standard
R_{i}\left(t\right) = \alpha_{i}+\beta_{i}R_{m}\left(t\right)+\epsilon_{i}
\left(t\right)\qquad{t=1,2,\dots,T}
```

where $\alpha_{i}$ and $\beta_{i}$ are (unknown) model paramaters: 

* The parameter $\alpha_{i}$ describes the firm specific return not explained by the market; thus, $\alpha_{i}$ is the idiosyncratic return of firm $i$.
* The parameter $\beta_{i}$ measures the relationship between the excess return of firm $i$ and the excess return of the market; a large $\beta_{i}$ suggests the market returns (or losses) are _amplified_ for firm $i$, while a small $\beta_{i}$ suggests the market returns (or losses) are _damped_ for firm $i$.
* The parameter $\beta_{i}$ can also be interpreted as a measure of the relative risk of investing in firm $i$ relative to the overall market. 
````

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

* $\beta_{i}>1$ expected return of firm $i$ is _greater_ than the expected market return
* $\beta_{i}\sim{1}$ firm $i$ performs _similar_ to the overall market on average
* $\beta_{i}<1$ expected excess return of firm $i$ is _less_ than the expected excess market return

The $\beta_{i}$ for asset $i$ can also be thought of as a measure of risk of asset $i$ relative to the market. For example, we can show that:

```{math}
\beta_{i} = \frac{\text{cov}(R_{i}, R_{m})}{\text{var}(R_{m})}
```

where $\text{cov}(R_{i}, R_{m})$ denotes the [covariance](https://en.wikipedia.org/wiki/Covariance) between the excess return of asset $i$ and the market, and $\text{var}(R_{m})$ denotes the variance of the market excess return. Thus, in the context of risk, $\beta_{i}$ has the interpretation:

* $\beta_{i}>1$ suggests firm $i$ has _greater risk_ than the overall market
* $\beta_{i}\sim{1}$ suggests that firm $i$ has the _same risk_ as the overall market on average
* $\beta_{i}<1$ suggests firm $i$ has _less risk_ compared to overall market

Putting these two regimes together gives fundamental insight into the behavior of markets: __high returns come with high-risk__. 
````

#### Estimating Single Index Models from Data
Estimating single index models from data reduces to estimating values for the $(\alpha_{i},\beta_{i})$ parameters and developing a residual model $\epsilon_{i}(t)$. Let's decompose this problem into two phases:

* Phase 1: Estimate values for $(\alpha_{i},\beta_{i})$ using one of many possible approaches, and
* Phase 2: Estimate the $\epsilon_{i}(t)$ distribution by computing the residual between the data and the model with parameter values from phase 1.

##### Phase 1: Estimate $(\alpha_{i},\beta_{i})$.
Imagine that we have historical data for the excess return of `XYZ` and the market over some period of time; say we have $\mathcal{M}$ measurements for the excess returns. Then, the excess return for `XYZ` can be encoded as a $\mathcal{M}\times{1}$ column vector $Y$, while the excess market return can be encoded as an $\mathcal{M}\times{2}$ matrix $X$, where the first column of $X$ is all 1's while the second column holds the excess market return values. Then, the single index model (in the absence of the residual) is the overdetermined ($\mathcal{M}\gg{2}$) linear system:

```{math}
:label: eqn-linear-sys-sim
Y = X\theta
```

where $\theta = (\alpha_{i},\beta_{i})^{T}$ is the $2\times{1}$ column vector of unknown parameters. The task is to estimate the unknown $\theta$ vector, given $X$ and $Y$.

###### Direct Matrix Inversion
One method to estimate the unknown parameter vector $\theta$ is to directly invert the data matrix $X$. In particular, if we multiply both sides of Eqn. {eq}`eqn-linear-sys-sim` by the transpose of the data matrix:

```{math}
:label: eqn-linear-sys-sim-1
X^{T}Y = X^{T}X\theta
```

we get a square matrix $X^{T}X$ that can be inverted to solve for the unknown parameter vector $\theta$:

```{math}
:label: eqn-linear-sys-sim-2
\hat{\theta} = \left(X^{T}X\right)^{-1}X^{T}Y
```

when we have assumed $\det(X^{T}X)\neq{0}$. {prf:ref}`example-dmi-single-index-model` explores the direct matrix inversion approach for computing the unknown parameter vector $\theta$:

````{prf:example} Direct matrix inversion to compute $\theta$
:label: example-dmi-single-index-model

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

##### Phase 2: Identification of the residual model
Now that we have estimated $\hat{\theta}$, we can compute the residual model. The residual model $\epsilon_{i}(t)$ describes the unmodeled random component of the return of `XYZ`; thus, it explains all the influences on the excess return that are _not_ associated with the firm or the overall market. 

Let's assume $\epsilon_{i}(t)\sim{N(0,\sigma_{\epsilon,i}^2)}$, i.e., the residual is [normally distributed](https://en.wikipedia.org/wiki/Normal_distribution) with a zero mean and a variance of $\sigma_{\epsilon,i}^2$; we'll estimate the variance from data. In particular, define the residual (difference) between the model and the data as:

$$\Delta = Y - \hat{Y}$$

where $\hat{Y}$ denotes the _estimated_ excess return of firm $i$ (computed using the single index model), and $Y$ indicates the _actual_ excess return of firm $i$ as observed in the market. Then, for each data point, e.g., close price value in our dataset, we'll have a value for $\Delta$, the difference between the predicted and actual excess return; the values of $\Delta$ can be thought of as samples from the residual distribution $\epsilon_{i}(t)$. Thus, we can use $\Delta$ to estimate $\sigma_{\epsilon,i}^2$. {prf:ref}`example-normal-residual-model` explores an approach to estimate the variance of the residuals.

````{prf:example} Identification of the Residual Model for [AMD](https://finance.yahoo.com/quote/AMD)
:label: example-normal-residual-model

Let's use the data and the estimated single index model parameters $\hat{\theta}$ for [AMD](https://finance.yahoo.com/quote/AMD) from {prf:ref}`example-dmi-single-index-model`. Given this data, let's estimate the variance of the unknown residual distribution, $\sigma_{\epsilon,i}^2$, using a maximum likelihood approach. 

We implemented the maximum likelihood strategy using routines implemented in the [Distributions.jl](https://github.com/JuliaStats/Distributions.jl) package.



````



(content:references:buy-and-hold-strategy)=
## Buy and Hold Strategy
We have tools to measure the risk and reward of stocks, now, let's begin the discussion of investment strategies. The [buy and hold strategy](https://www.investopedia.com/terms/b/buyandhold.asp) is arguably the most straightforward approach for investing in stocks (or ETFs). In this approach, an investor buys shares of `XYZ` on a regular basis and then holds these shares indefinitely, regardless of the short-term price fluctuations in `XYZ.` 

The [buy and hold strategy](https://www.investopedia.com/terms/b/buyandhold.asp) is a passive investment approach. No consideration is given to unrealized gains (or losses), and no adjustments are made to the fund other than adding new shares. However, while this approach may appear naive, it can be surprisingly successful. 

The keys to the success of the [buy and hold strategy](https://www.investopedia.com/terms/b/buyandhold.asp) are:

* The expected return of the market, when viewed over a long time horizon, is positive; thus, stocks (or ETFs) with $\beta>0$ will (on average) be expected to appreciate. 
* Further, because the investor is periodically adding new shares of `XYZ` to their overall portfolio, the average share price of `XYZ` held by the investor can reflect short-term price fluctuations. 

Let's explore these two points with an example:   

````{prf:example} Buy and hold strategy for [SPY](https://finance.yahoo.com/quote/SPY/) 
:label: example-average-cost

Suppose we purchased \$1.00's worth of [SPY](https://finance.yahoo.com/quote/SPY/) shares at the close of every trading day over a five year period. 

````

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


(content:references:markowitz-solution-test)=
## Does Markowitz Portfolio Allocation work?
Fill me in.

---

## Summary
Fill me in.

