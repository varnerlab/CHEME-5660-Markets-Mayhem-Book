# Modern Portfolio Theory (MPT) 
Modern portfolio theory (MPT) is a practical method for selecting investments in order to maximize their overall returns within an acceptable level of risk. Harry Markowitz, who developed the mathematical foundation of MPT {cite}`MPT1952`, was later awarded a Nobel Prize for his work. 

## Estimating Returns

### Single Index Return Models
The single-index model (SIM), developed by William Sharpe, is an asset pricing model which measures both the risk and the return of a stock {cite}`SHARPE1963`. The single index model describes the return of stock $i$ in terms of a firm-specific return, and an overall market return component:

```{math}
:label: eq-single-index-model
r_{i}\left(t\right) - r_{f} = \alpha_{i}+\beta_{i}\left(r_{m}\left(t\right)-r_{f}\right)+\epsilon_{i}
\left(t\right)\qquad{t=1,2,\dots,T}
```

where $r_{i}\left(t\right)$ denotes the return of stock $i$, during time period $t$, 
$r_{f}$ denote the risk-free rate i.e., typically the interest rate on treasury bills, while $r_{m}\left(t\right)$ is the return of the market portfolio e.g., an index such as the [S\&P500](https://en.wikipedia.org/wiki/S%26P_500) during time period $t$. 
The term $\alpha_{i}$ denotes the firm-specific return, while $\beta_{i}$ denotes the proportion of the the stock's return associated with the overall market. Finally, $\epsilon_{i}\left(t\right)\sim\mathcal{N}\left(0,\sigma_{i}^{2}\right)$ is 
the unexplained (random) return of stock $i$, which is assumed to be normally distributed with mean zero and standard deviation $\sigma_{i}$.


## Estimating Volatility
Fill me in. 

## The Markowitz Portfolio Allocation Problem
Fill me in.

