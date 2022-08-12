# Modern Portfolio Theory

## Introduction
Modern portfolio theory (MPT) is a method for selecting a collection of assets, e.g., stocks or bonds, to maximize the overall reward of the investor within an acceptable level of risk to the investor. Harry Markowitz, who developed the mathematical foundation of MPT {cite}`MPT1952`, was later awarded a [Nobel Prize for his work in 1990](https://www.nobelprize.org/prizes/economic-sciences/1990/markowitz/facts/). 

The central theme of MPT is the balance between risk and reward, where the reward is measured as the [expected return](https://www.investopedia.com/terms/r/return.asp) of a basket of assets (called a portfolio). In contrast, the risk is calculated as the variance of the logarithmic return of the portfolio. Thus, the objective of MPT is to balance the composition of the portfolio such that an investor obtains a desired expected return while minimizing the variance (risk). For a detailed discussion of MPT, see Part II (chapters 5 - 8) of Bodie, Kane, and Marcus {cite}`Bodie:2011ug`.

In this chapter:

* We introduce {ref}`content:references:markowitz` for a portfolio of risky and risk-free assets
* We introduce {ref}`content:references:markowitz-solution` and 
* We we explore the question  {ref}`content:references:markowitz-solution-test`
---

(content:references:markowitz)=
## Markowitz Portfolio Allocation
Markowitz portfolio allocation assumes that investors are risk-averse and rational. 
Thus, if an investor chooses between two portfolios that offer _the same expected return_, a rational risk-averse investor will choose the less risky portfolio. Further, a rational risk-averse investor will incur increased risk only if compensated for this risk by a higher expected return, the so-called high-risk, high-reward paradigm. On the other hand, an investor who wants higher expected returns must accept more risk. However, the acceptable trade-off between risk and reward will differ for each investor; what you may find as an acceptable risk versus reward is not the same for everyone. Thus, a rational risk-averse investor will not invest in a portfolio if a second portfolio exists with a more favorable risk-expected return profile. 

### Portfolio Risk and Reward
To make these ideas more concrete, let's develop expressions for the risk and reward of a 
portfolio. Denote the set of assets in a portfolio as $\mathcal{P}$; where $\vert\mathcal{P}\vert$ denotes the number of assets in the portfolio set. Then, the expected return (reward) of the portfolio $\mathcal{P}$ is defined as ({prf:ref}`defn-portfolio-return`):

````{prf:definition} Expected Portfolio Return
:label: defn-portfolio-return

Denote the return of asset $i$ in portfolio $\mathcal{P}$ on some time basis $\mathcal{B}$ as $r_{i}$. Then, the expected return of portfolio $\mathcal{P}$ denoted by 
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

#### Asset correlation in a portfolio  
An exciting feature of the variance of the portfolio return ({prf:ref}`defn-portfolio-variance`) is the dependence on the [correlation](https://en.wikipedia.org/wiki/Correlation) denoted by $\rho_{ij}$ between assets $i$ and $j$. To see why this is exciting, let's consider a portfolio $\mathcal{P}$ consisting of two risky assets; $\vert\mathcal{P}\vert$ = 2. Then, the variance of the portfolio returns $\sigma_{\mathcal{P}}^{2}$ is given by:

```{math}
\sigma_{\mathcal{P}}^2 = w_{1}^{2}\sigma_{1}^{2}+w_{2}^{2}\sigma_{2}^{2}+2w_{1}w_{2}\sigma_{1}
\sigma_{2}\rho_{12}
```
where $w_{\star}$ is the fraction of asset $\star$ in the portfolio, and 
$\sigma_{\star}$ denotes the standard deviation of the return of asset $\star$. 
Thus, we can influence the overall portfolio variance by choosing the assets 
based upon their correlation.

````{prf:observation} The role of correlation in $\mathcal{P}$
* __Positive correlation__: For two assets that are positively correlated $p_{12}>{0}$, 
the variance of the return of the portfolio $\sigma_{\mathcal{P}}^{2}$ is _greater_ than to the variance of the assets alone (assuming $w_{\star}\geq{0}$).
* __Zero (or small) correlation__: For two assets that are either perfectly uncorrelated $p_{12} = 0$ (or have small correlation $p_{12}\ll{1}$), 
the variance of the return of the portfolio $\sigma_{\mathcal{P}}^{2}$ is _similar to_ the variance of the assets alone (assuming $w_{\star}\geq{0}$).
* __Negative correlation__: For two assets that are negatively correlated $p_{12}<0$, the variance of the return of the portfolio $\sigma_{\mathcal{P}}^{2}$ is _less_ than to the variance of the assets alone (assuming $w_{\star}\geq{0}$).
````

Further, the correlation does not appear in the expected portfolio return ({prf:ref}`defn-portfolio-return`); thus, by carefully selecting assets with low correlation, the overall risk of a portfolio can be reduced without impacting the return (all else being equal). 

#### Examples
* Example: Computation of the variance of a portofilio for different asset combinations

(content:references:markowitz-solution)=
## Solution Markowitz Portfolio Allocation 

The objective of Markowitz portfolio allocation problem is to estimate the weights $w=\left(w_{1},w_{2},\dots\right)^{T}$ of the assets in portfolio $\mathcal{P}$  such that overall variance of the portfolio is minimized, for a specified return, subject to some constraints on $w$. 

### Risky assets only
The Markowitz allocation problem for a portfolio $\mathcal{P}$ composed of __only__ risky assets is the [quadratic program](https://en.wikipedia.org/wiki/Quadratic_programming):

```{math}
\min_{w} \sigma^{2}_{\mathcal{P}}\left(w\right)
```

subject to the constraints:

$$
\begin{eqnarray}
\mathbb{E}(r_{\mathcal{P}})&\geq&{R^{*}}\\
1^{T}w &=& 1\\
w_{i}&\geq&{0}\qquad{\forall{i}\in\mathcal{P}}
\end{eqnarray}
$$

where $w$ denotes the vector of weights of the assets in portfolio $\mathcal{P}$, $\sigma^{2}_{\mathcal{P}}\left(w\right)$ represents the portfolio variance; the portfolio variance can re-written as $\sigma^{2}_{\mathcal{P}}\left(w\right) = w^{T}\Sigma{w}$  where $\Sigma$ is the [covariance matrix](https://en.wikipedia.org/wiki/Covariance_matrix). The quantity $\mathbb{E}(r_{\mathcal{P}})$ denotes the expected return (or excess return) of the portfolio $\mathcal{P}$; the expected return (or excess return) can be re-writtem as $w^{T}\mathbb{E}(r)$ where $\mathbb{E}(r)$ denotes the vector of expected returns (or excess returns) for each asset in the portfolio. 
The quantity $R^{*}$ denotes the minimal required return for $\mathcal{P}$ and $1^{T}$ denotes a vector of ones (full allocation constraint). The last constraint $w_{i}\geq{0}~\forall{i}\in\mathcal{P}$ says that no short selling (borrowing shares) is allowed; if short selling is allowed, then this constraint can be removed.

A couple of issues:
* While the problem above is written in terms of absolute return $r_{\star}$, we can also write the portfolio allocation problem using excess returns; the excess return is $R_{\star} = r_{\star} - r_{f}$, where $r_{f}$ denotes the risk free rate of return.
* The challenge to solving the Markowitz problem is estimating the expected assets in the portfolio and the covariance matrix $\Sigma$. These quantities can be calculated from data if available or from models of the return and variance of the assets in the portfolio. Let's consider both approaches. 

(content:references:markowitz-solution-data)=
### Data-driven risky portfolios
Fill me in.

(content:references:markowitz-solution-sim)=
### Single-index model portfolios
The application of index models to construct risky portfolios was originally proposed by Treynor and Black {cite}`FB1973`. 

[Single index models (SIMs)](./Single-Index-Models.md) are asset pricing models which measure the risk and the return of a stock relative to a risk-free alternative investment, e.g., [government treasury bonds](./bonds.md). A single index model describes the return of a firm’s stock in terms of a firm-specific return and the overall market return. One of the simplest (yet still widely used) single index models was developed by Sharpe {cite}`SHARPE1963`; see {prf:ref}`defn-single-index-model-standard`.

#### Portfolio Return using Single Index Models
{prf:ref}`defn-portfolio-return` shows the expected return of portfolio $\mathcal{P}$ in terms of the expected return of each of the assets in the portfolio. Thus, we must estimate the expected returns for each asset when solving the Markowitz allocation problem from data (as shown in {ref}`content:references:markowitz-solution-data`). However, a single index model can limit this work; instead of estimating the expected return for each asset from data, we only need to calculate the expected excess market return $\mathbb{E}(R_{m})$ and then use the single index model to predict the firm-specific expected excess returns $\mathbb{E}(R_{i})$: 

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

#### Portfolio Variance using Single Index Models
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

