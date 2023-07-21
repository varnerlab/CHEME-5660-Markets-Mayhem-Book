(content:references:american-european-options-contracts)=
# American and European Call and Put Contracts

Derivatives are one of the three primary financial instrument categories: derivatives, equity (i.e., shares of stock), and debt (i.e., bonds and mortgages). Derivatives provide payoffs that depend on the value of other assets, such as commodities, bonds, stocks, or market indexes. Thus, the value of a derivative is based mainly on the price movements of an underlying asset, e.g., stocks, commodities, currencies, etc.

```{topic} Outline
In this lecture, we will focus exclusively on options, a type of derivative that use equity, i.e., shares of a stock or an exchange-traded fund, as their underlying asset. Options are structured agreements between a buyer and a seller that give the option buyer the right, but not the obligation, to execute the transaction described in the contract, i.e., to buy (or sell) an underlying asset in some predetermined way in a specified time frame. 

* [Call contracts](content:references:american-european-options-contracts-call) give the option buyer the right (but not the obligation) to buy an underlying asset, e.g., shares of stock at a predetermined price (called the strike price) within a specified time frame. The option buyer pays the option seller a premium for the right to buy the underlying asset.

* [Put contracts](content:references:american-european-options-contracts-put) give the option buyer the right (but not the obligation) to sell an underlying asset, e.g., shares of stock at a predetermined price (called the strike price) within a specified time frame. The option buyer pays the option seller a premium for the right to sell the underlying asset.

* [Put-Call parity](content:references:american-european-options-contracts-put-call-parity) is a relationship between the prices of a European call option and a European put option with the same strike price and expiration date. The put-call parity relationship is important because it allows us to price one option in terms of the other. 

```

---

(content:references:american-european-options-contracts-call)=
## Call contracts
A `call` option is a financial contract that gives the holder the right, but not the obligation, to sell a specified asset, such as stocks, commodities, or currencies, at a predetermined price within a specified time period. Let's consider stock as the underlying asset. A single standard `call` contract controls `100` shares of stock.

In the case of [American](https://www.investopedia.com/terms/a/americanoption.asp) style [call contracts](https://www.investopedia.com/terms/c/calloption.asp), the option buyer can exercise their right at any point between when the contract is purchased and the expiration date. On the other hand, buyers of [European](https://www.investopedia.com/terms/e/europeanoption.asp) style contracts can only exercise their right on the expiration date. 

The business case for buying (or selling) a `call` contract:
* __Buyer (long)__: From the buyer's perspective, call contracts allow an investor to benefit from the price movement of `XYZ` to the upside _without_ purchasing `XYZ`. Further, call options (again from the buyer's perspective) have _limited downside risk_, i.e., the maximum amount that the holder of the call option can lose is the premium paid for the option. Finally, call options are a mechanism to purchase shares of `XYZ` at the strike price of $K$ instead of the market price of $S$. 
* __Seller (short)__: From the seller's perspective, the main objective of selling a call contract is to collect the premium $\mathcal{P}$. Call contracts also allow the seller to benefit from the price movement of `XYZ` to the downside _without_ purchasing `XYZ`. However, for a seller, call options have _unlimted upside_ risk; thus, call options are often only sold by investors who already own the required number of shares of `XYZ` (known as a [covered call position](https://www.investopedia.com/terms/c/coveredcall.asp)). Finally, call options offer the seller the opportunity to sell shares of `XYZ` at the strike price of $K$ instead of the market price of $S$.


### Payoff, Profit, Premium and Breakeven
The payoff per share of a `call` contract at expiration `T` days in the future $V_{c}(K,S(T))$ is defined as:

$$V_{c}(K,S(T)) = \max\left(S(T) - K,~0.0\right)$$

where $K$ denotes the strike price and $S(T)$ represents the share price of the underlying asset `T` days in the future (at expiration). The right (but not the obligation) to buy shares at the strike `K` is not free. The contract `seller` charges the contract `buyer` a premium for each `call` contract $\mathcal{P}_{c}(\dots)$. From the perspective of the `buyer`, the profit per share for the `call` contract $P_{c}$ is the payoff of the contract minus the cost of the contract:

$$P_{c}(K,S(T)) = V_{c}(K,S(T)) -  \mathcal{P}_{c}(K,S(T))$$

Thus, from the buyer’s perspective, the share price must fall _above the strike price_ to make up the amount paid for the contract. This is called the breakeven price $\mathcal{B}_{c}(K, S(T))$:

$$\mathcal{B}_{c}(K,S(T)) = K + \mathcal{P}_{c}(K,S(T))$$

Finally, the premium (cost) for each `call` contract $\mathcal{P}_{c}(\dots)$ is defined by the expression:

$$\mathcal{P}_{c}(K,S(T))\geq\mathbb{E}\Bigl(\mathcal{D}^{-1}_{T,0}(\bar{r})\cdot{V_{c}}(K,S(T)\Bigr)$$

where $\mathcal{D}_{T,0}(\bar{r})$ denotes the discount rate between the time when the contract was purchased `0` and contract expiration `T` days in the future. Option contracts use risk-neutral pricing; thus, the discount rate $\bar{r}$ is typically taken as the interest rate on 10-year treasury notes. 

(content:references:american-european-options-contracts-put)=
## Put contracts
A `put` option is a financial contract that gives the holder the right, but not the obligation, to sell a specified asset, such as stocks, commodities, or currencies, at a predetermined price within a specified time period. Let's consider stock as the underlying asset. A single standard `put` contract controls `100` shares of stock.

In the case of [American](https://www.investopedia.com/terms/a/americanoption.asp) style [put contracts](https://www.investopedia.com/terms/p/putoption.asp), the option buyer can exercise their right at any point between when the contract is purchased and the expiration date. On the other hand, buyers of [European](https://www.investopedia.com/terms/e/europeanoption.asp) style contracts can only exercise their right on the expiration date. 

The business case for buying (or selling) `put` contracts:
* __Buyer (long)__: From the buyer's perspective, `put` contracts allow an investor to benefit from the price movement of `XYZ` to the downside _without_ purchasing `XYZ`. Further, `put` options (again from the buyer's perspective) have _limited downside risk_, i.e., the maximum amount that the holder of the `put` option can lose is the premium paid for the option. Finally, `put` contracts are a mechanism to sell shares of `XYZ` at the strike price of $K$ instead of the market price of $S$. 
* __Seller (short)__: From the seller's perspective, the motivation for selling a `put` contract is to collect the premium $\mathcal{P}$. Put contracts also allow the seller to benefit from the price movement of `XYZ` to the upside _without_ purchasing `XYZ`. However, for a seller, `put` options have _unlimted downside_ risk; thus, `put` options are often only sold by investors who have set aside the required capital to purchase the required number of shares of `XYZ` (known as a [cash secured put position](https://www.fidelity.com/learning-center/investment-products/options/know-about-cash-covered-puts)). Finally, `put` options offer the seller the opportunity to buy shares of `XYZ` at the strike price of $K-\mathcal{P}$ instead of the market price of $S$.

### Payoff, Profit, Premium and Breakeven
The payoff per share of a `put` contract at expiration `T` days in the future $V_{p}(K,S(T))$ is defined as:

$$V_{p}(K,S(T)) = \max\left(K - S(T),~0.0\right)$$

where $K$ denotes the strike price and $S(T)$ represents the share price of the underlying asset `T` days in the future (at expiration). The right (but not the obligation) to sell shares at the strike `K` is not free. The contract `seller` charges the contract `buyer` a premium for each `put` contract $\mathcal{P}_{p}(\dots)$. From the perspective of the `buyer`, the profit per share for the `put` contract $P_{p}$ is the payoff of the contract minus the cost of the contract:

$$P_{p}(K,S(T)) = {V}_{p}(K,S(T)) -  \mathcal{P}_{p}(K,S(T))$$

Thus, from the buyer’s perspective, the share price must fall _below the strike price_ to make up the amount paid for the contract. This is called the breakeven price $\mathcal{B}_{p}(K, S(T))$:

$$\mathcal{B}_{p}(K,S(T)) = K - \mathcal{P}(K,S(T))$$

Finally, the premium (cost) for each `put` contract $\mathcal{P}_{p}(\dots)$ is defined by the expression:

$$\mathcal{P}_{p}(K,S(T))\geq\mathbb{E}\Bigl(\mathcal{D}^{-1}_{T,0}(\bar{r})\cdot{V_{p}}(K,S(T)\Bigr)$$

where $\mathcal{D}_{T,0}(\bar{r})$ denotes the discount rate between the time when the contract was purchased `0` and contract expiration `T` days in the future. Option contracts use risk-neutral pricing; thus, the discount rate $\bar{r}$ is typically taken as the interest rate on 10-year treasury notes. 

(content:references:american-european-options-contracts-put-call-parity)=
## Put-Call Parity
Fill me in.

---

## Summary
In this lecture, we will focused exclusively on options, a type of derivative that use equity, i.e., shares of a stock or an exchange-traded fund, as their underlying asset. 

* [Call contracts](content:references:american-european-options-contracts-call) give the option buyer the right (but not the obligation) to buy an underlying asset, e.g., shares of stock at a predetermined price (called the strike price) within a specified time frame. The option buyer pays the option seller a premium for the right to buy the underlying asset.

* [Put contracts](content:references:american-european-options-contracts-put) give the option buyer the right (but not the obligation) to sell an underlying asset, e.g., shares of stock at a predetermined price (called the strike price) within a specified time frame. The option buyer pays the option seller a premium for the right to sell the underlying asset.

* [Put-Call parity](content:references:american-european-options-contracts-put-call-parity) is a relationship between the prices of a European call option and a European put option with the same strike price and expiration date. The put-call parity relationship is important because it allows us to price one option in terms of the other. 