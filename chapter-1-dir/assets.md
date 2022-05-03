# Assets are Current and Future Cash Flows

The development of processes or products does not occur inside a mythical universe that is free 
from market forces. Instead, processes and products must be, at a minimum, financially neutral to be viable.
Processes and products that are not financially viable, while perhaps being technically 
innovative or otherwise advantageous, will not survive in the marketplace without external support. 

## Assets
From a business perspective, an _asset_ is a sequence of present and future cash flows 
demarcated in some currency, for example, Euros, Dollars, Yuan, or cryptocurrencies such as Bitcoin.
The value of an asset can be determined using a valuation operator $\mathcal{V}$ applied to these cash flows:

```{math}
:label: eq-asset-cash-flows
\mathcal{V}\left(Asset_{t}\right) = \mathcal{V}\left(CF_{t},CF_{t+1},\dots,CF_{t+T}\right)
```
where $CF_{t}$ denotes the cash flow in time period $t$ up to $T$ time periods in the future.
The most common (and intuitive) valuation operator $\mathcal{V}$ is the sum of net cash flows in each period, i.e., we compute the net cash in each period (cash inflow - cash outflow in period $i$) and then sum 
these net cash flows over all $T$ periods. 
However, there is a critical and fundamental challenge to this intuition: 
the value of money is _not_ conserved over time. A dollar today is not worth a dollar tomorrow.

## Time value of money
The value of money is not constant over time. One dollar in Year T is worth less than one dollar in Year 0 (today). 
The change in the value of money is called the time value of money. 
A useful mental model for the time value of money is to think of money from different time periods 
as being in different currencies (e.g., $\$$ and $\def\euro{\unicode{x20AC}} \euro$) that must be exchanged. 
Thus, to compare money or cash flows from different time periods we formulate the equivalent of an exchange rate.
For example, suppose we wanted to compute the value of a cash flow one time period in the future in today's dollars.
In this case we could write a relationship of the form:

```{math}
:label: eq-cash-flow-1-period
CF_{2} = \left(1+r_{21}\right)CF_{1}
```
where $CF_{1}$ denotes the value of the cash flow today, and $CF_{2}$ denotes the value of the cash flow one time period in the future. 
The term $r_{21}$ denotes the hypothetical exchange rate between time period 1 and 2 
(where $r_{ii}=0$, and $r_{ij}>0$ for $i\neq{j}$). 
If we do this computation between time period 2 and 3, and then 3 and 4, etc we can develop an expression
that describes the relationship between the value of cash flow today (time period 1) and $i$ time periods into the future:

```{math}
:label: eq-cash-flow-multiple-period
CF_{i} = CF_{1}\left[\prod_{j=1}^{i-1}\left(1+r_{j+1,j}\right)\right]\qquad{i=2,3,\dots,T}
```

The product term (the $\prod\star$ in the brackets) is called the discount factor and given the symbol $d_{i1}$.
Eqn. {eq}`eq-cash-flow-multiple-period` can be written in a more compact form as:

```{math}
	CF_{i} = d_{i1}CF_{1}\qquad{i=2,3,\dots,T}
```

In the special case when the exchange factors $r_{ij}$ are equal in each period (let's call this $r$, or the overall discount rate), then the overall discount factor is given by:

```{math}
	d_{i1} = (1+r)^{i-1}\qquad{i=2,3,\dots,T}
```
