# Option Contract Price Dynamics and Sensitivities
The price of options contracts depends upon many market factors, e.g., the cost of the underlying asset when the option is purchased, the implied volatility of the underlying asset, the time to expiration, and the risk-free rate. 

```{topic} Option Contract Price Dynamics
In this lecture, we explore how market factors affect the price of an option contract. We also introduce the concept of option contract sensitivities, which are used to quantify the impact of these factors on the price of an option contract.
```

---

(content:references:european-contract-price)=
## European Contract Prices
Buyers of [European call and put](https://www.investopedia.com/terms/e/europeanoption.asp) contracts can only exercise their right at expiration. Thus, the premium for a European call or put contract is equal to the discounted expected payoff of the contract at expiration:

```{math}
:label: eqn-european-contract-price
\mathcal{P}_{\star}(K,S(0)) = \mathbb{E}\Bigl(\mathcal{D}^{-1}_{T,0}(\bar{r})\cdot{V_{\star}}(K,S(T))\Bigr)
```

where $\mathcal{D}_{T,0}(\bar{r})$ denotes the discount factor between the time when the contract was purchased `0` and contract expiration `T` days in the future. Option contracts use risk-neutral pricing. Thus, the discount rate $\bar{r}$ is taken as the interest rate on 10-year treasury notes. Finally, $V_{\star}(K,S(T))$ denotes the payoff per share of contract $\star$ at expiration `T` days in the future.


(content:references:american-contract-price)=
## American Contract Prices
In the case of [American style call and put contracts](https://www.investopedia.com/terms/a/americanoption.asp), the option buyer can exercise their right at any point between when the contract is purchased and the expiration date. Thus, the contract seller may demand a premium that is greater than the European contract because of the possibility of early exercise (inequality case):

```{math}
:label: eqn-american-contract-price
\mathcal{P}_{\star}(K,S(0)) \geq \mathbb{E}\Bigl(\mathcal{D}^{-1}_{T,0}(\bar{r})\cdot{V_{\star}}(K,S(T))\Bigr)
```

where $\mathcal{D}_{T,0}(\bar{r})$ denotes the discount factor between the time when the contract was purchased `0` and contract expiration `T` days in the future. Option contracts use risk-neutral pricing. Thus, the discount rate $\bar{r}$ is taken as the interest rate on 10-year treasury notes. Finally, $V_{\star}(K,S(T))$ denotes the payoff per share of contract $\star$ at expiration `T` days in the future.


(content:references:greeks-calculations)=
## The Greeks
[The Greeks](https://www.investopedia.com/trading/using-the-greeks-to-understand-options/) provide a way to measure an option’s price sensitivity to quantifiable market factors. Thus, they are sensitivity coefficients that measure how the price changes when an underlying market factor changes. 

Suppose the price of an American call option is described by the function $C(...)$. The price of the call contract $C(...)$ is a function of the set of market variables that influence the option contract price, e.g., the share price of the underlying asset $S$, the risk-free rate of return $\mu$, the price volatility of the underlying asset $\sigma$, the duration of the option contract $T$, etc.

---

## Summary
Fill me in