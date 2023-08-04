# Data-Driven Portfolio Allocation
The central theme of modern portfolio theory is balancing risk and reward. Reward is measured as the [expected return](https://www.investopedia.com/terms/r/return.asp) of a portfolio of assets, while, the risk is calculated as the variance of the logarithmic or fraction return of the portfolio.

```{topic} Data Driven Portfolio Allocation Outline
Stuff goes here.
```

---

(content:references:markowitz)=
## Markowitz Portfolio Allocation
According to the Markowitz portfolio allocation theory, investors are rational and risk-averse {cite}`MPT1952`. Thus, when presented with two portfolios that offer the same expected return, a rational and risk-averse investor will choose the less risky portfolio, if an investor wants higher expected returns, they must accept more risk. However,  the balance between risk and reward varies from one investor to another (what may be an acceptable trade-off for you may not be the same for someone else).

```{prf:remark} Markowitz in Words
:label: remark-markowitz-in-words

Suppose we have a set of assets $\mathcal{A}$ composed of risky assets, e.g., equities and equity derivatives, and risk-free assets, e.g., treasury debt securities. The Markowitz portfolio allocation problem estimates the weight $\omega_{a}$ of asset $a$ for $\forall{a}\in\omega_{a}$ that minimizes the risk for a user-specified return.  

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

---

## Summary
Fill me in