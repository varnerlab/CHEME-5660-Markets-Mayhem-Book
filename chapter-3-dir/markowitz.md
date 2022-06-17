# Modern Portfolio Theory

## Introduction
Modern portfolio theory (MPT) is a practical method for selecting a collection of assets, e.g., stocks or bonds, to maximize the overall reward of the investor within an acceptable level of risk to the investor. Harry Markowitz, who developed the mathematical foundation of MPT {cite}`MPT1952`, was later awarded a [Nobel Prize for his work in 1990](https://www.nobelprize.org/prizes/economic-sciences/1990/markowitz/facts/). 

The central theme of Markowitz is the balance between risk and reward, where the reward is measured as the [expected return](https://www.investopedia.com/terms/r/return.asp) of a basket of assets (called a portfolio). In contrast, the risk of a portfolio is calculated as the standard deviation (or sometimes the variance) of the logarithmic return, otherwise known as [volatility](https://en.wikipedia.org/wiki/Volatility_(finance)), of the portfolio. 

The ideas of this chapter closely follow Part II (chapters 5 - 8) of Bodie, Kane, and Marcus {cite}`Bodie:2011ug`. In particular, in this chapter:

* We introduce {ref}`content:references:markowitz` for a general portfolio of risk-free and risky assets
* We introduce {ref}`content:references:markowitz-solution` and 
* We we explore the question  {ref}`content:references:markowitz-solution-test`
---

(content:references:markowitz)=
## Markowitz Portfolio Allocation
Markowitz portfolio allocation assumes that investors are risk-averse and rational. 
Thus, if an investor chooses between two portfolios that offer _the same expected return_, a rational risk-averse investor will choose the less risky portfolio. Further, a rational risk-averse investor will incur increased risk only if compensated for this risk by a higher expected return, the so-called high-risk, high-reward paradigm. On the other hand, an investor who wants higher expected returns must accept more risk; there is no free lunch. However, the acceptable trade-off between risk and reward will differ for each investor; what you may find as an acceptable risk versus reward is not the same for everyone. Thus, a rational risk-averse investor will not invest in a portfolio if a second portfolio exists with a more favorable risk-expected return profile. 

### Portfolio risk and reward
To make these ideas more concrete, let's develop expressions for computing the risk and reward of a 
portfolio. Denote the set of assets in a potential portfolio as $\mathcal{P}$; where $\vert\mathcal{P}\vert$ denotes the size (the number of assets) of the portfolio. Then, the expected return (reward) of the portfolio is defined as ({prf:ref}`defn-portfolio-return`):

````{prf:definition} Expected Portfolio Return
:label: defn-portfolio-return

Denote the return of asset $i$ in portfolio $\mathcal{P}$ on some time basis $\mathcal{B}$ as $r_{i}$. Then, the expected return of portfolio $\mathcal{P}$ denoted by 
$\mathbb{E}\left(r_{\mathcal{P}}\right)$ is:

```{math}
\mathbb{E}\left(r_{\mathcal{P}}\right) = \sum_{i\in\mathcal{P}}\omega_{i}\mathbb{E}\left(r_{i}\right)
```

where $w_{i}$ denotes the fraction of asset $i$ in the portfolio $\mathcal{P}$, and 
$\mathbb{E}\left(r_{i}\right)$ denotes the expected return of asset $i$ on time basis $\mathcal{B}$.

````


(content:references:markowitz-solution)=
## Solution approaches for Markowitz Portfolio Allocation

(content:references:markowitz-solution-test)=
## Does Markowitz Portfolio Allocation work?


## Summary

