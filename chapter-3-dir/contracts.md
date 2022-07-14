# Derivative Securities

## Introduction
Derivatives are one of the three primary financial instrument categories: derivatives, equity (i.e., shares of stock), and debt (i.e., bonds and mortgages). Derivatives provide payoffs that depend on the value of other assets, such as commodities, bonds, stocks, or market indexes. Thus, the value of a derivative is based mainly on the price movements of an underlying asset, e.g., stocks, commodities, currencies, etc. In this lecture, we will focus exclusively on options, a type of derivative product that uses stock as its underlying asset. Like bonds, options are contractural agreements between buyers and sellers to conduct a particular transaction at some later date. Options, derivatives that use equity, i.e., shares of a stock or an exchange-traded fund, as their underlying asset, are structured agreements between a buyer and a seller that give the option buyer the right, but not the obligation, to execute the transaction described in the contract, i.e., to buy (or sell) an underlying asset in some predetermined way in a specified time frame. 

Investors can use options to [hedge](https://www.investopedia.com/terms/h/hedge.asp) against future asset price movements or for speculation. For example, a trader can buy an option instead of shares of an underlying stock to generate profits from the underlying stock's price movements, typically at a lower cost than the corresponding block of shares. Options contracts are traded on exchanges throughout the world; the [The Chicago Board Options Exchange](https://www.cboe.com) is the largest options exchange in the United States, responsible for approximately 33\% of the daily options trading volume in the United States (27 million contracts are traded each day in the United States). Worldwide, in 2021, there were about 33 billion options contracts traded annually.

Options are attractive because they offer [leverage](https://www.merrilledge.com/investment-products/options/options-trading-leverage-risk), i.e., an option contract can control a unit of asset, e.g., 100 shares of a stock, at a cost that is typically _less_ than the market value of that asset. This allows option buyers to pay a relatively small premium for market exposure in relation to the value of the underlying asset. An option buyer can see significant gains from comparatively small percentage moves in the price of the underlying asset. However, leverage also has a considerable downside. For example, if the underlying asset price does not rise or fall as anticipated during the lifetime of the option contract, leverage magnifies the investment's percentage loss.





<!-- However, unlike bonds which is a codified lending agreement, the contract that underlies an option decribes the purchase or sale of shares of stock.  -->

<!-- There are two types of options contracts, a [call contract](https://www.investopedia.com/terms/c/calloption.asp) and a [put contract](https://www.investopedia.com/terms/p/putoption.asp), and two different styles of contracts that we'll consider American and European style contracts. A CALL contract gives the 
buyer the right but not the obligation to purchase 100 shares (per contract) of an underlying stock, `XYZ`, at a price per share called the strike price of $K$. On the other hand, a PUT contract gives the buyer the right but not the obligation to sell 100 shares (per contract) of an underlying stock, `XYZ`, at a strike price of $K$ per share. 

In European-style contracts, the transaction codified in CALL or PUT options can only occur at some fixed date in the future called the expiration date, which is agreed upon when the contract is purchased. However, American contract styles have a different policy; American contracts can be exercised (the buyer can initiate the transaction) at any time between when the contract was purchased and the expiration date. -->

In this lecture, we will:
* Discuss the two types, and two styles of {ref}`content:references:option-contracts`
* Discuss several {ref}`content:references:option-pricing-algorithms`

---

(content:references:option-contracts)=
## Option Contracts

```{figure} ./figs/Fig-Options-Grid.pdf
---
height: 280px
name: fig-options-contract-grid
---
The rights and responsibilities of the buyer and seller of put and call option contracts.  
```

There are two types of options contracts, a [call contract](https://www.investopedia.com/terms/c/calloption.asp) and a [put contract](https://www.investopedia.com/terms/p/putoption.asp), and many different styles of options contracts. However, we'll consider only two styles, [American](https://www.investopedia.com/terms/a/americanoption.asp) and [European](https://www.investopedia.com/terms/e/europeanoption.asp) style options contracts. The roles and responsibilities of each contract type, and the respectrive role of the buyer and seller, are shown in ({numref}`fig-options-contract-grid`).

### Call contracts
A [call contract](https://www.investopedia.com/terms/c/calloption.asp) gives the option contract buyer the right, but not the obligation, to purchase 100 shares of `XYZ` (per contract) from the seller at a particular price per share (called the strike price $K$) at some point in the future (called the expiration date). In the case of [American](https://www.investopedia.com/terms/a/americanoption.asp) style [call contracts](https://www.investopedia.com/terms/c/calloption.asp), the option buyer can exercise their right at any point between when the contract was purchased and the expiration date. On the other hand, buyers of [European](https://www.investopedia.com/terms/e/europeanoption.asp) style contracts can only exercise their right on the expiration date. The right to purchase shares of `XYZ` at $K$ USD/share is not free; the option buyer pays a premium per contract to the option seller for this right. 

The profit that a call contract buyer experiences, denoted by $V$, depends upon the difference between the share price of `XYZ` and the strike price $K$ of the contract:

````{prf:definition} Call Contract Payoff for Contract Holder
:label: defn-PL-call-contract

An investor purchases a call contract for the underlying stock `XYZ` for $\mathcal{P}$ USD/contract, where the contract controls 100 shares of `XYZ`. 

Let the strike price of the call contract be $K$ USD/share, and the share price of `XYZ` be $S$ USD/share. Then, at expiration, the call contract has the payoff:

```{math}
V_{c} = \max\left(S-K,0\right)
```

and a profit (loss) of:

```{math}
P_{c} = V_{c} -  \mathcal{P}
```

where $P_{c}$ denotes the profit (or loss) per contract per share of `XYZ`.

````

### Put contracts
A [put contract](https://www.investopedia.com/terms/p/putoption.asp) gives the option contract buyer the right, but not the obligation, to sell 100 shares of `XYZ` (per contract) to the option seller at the strike price $K$, either by or on the expiration date. In the case of [American](https://www.investopedia.com/terms/a/americanoption.asp) style [put contracts](https://www.investopedia.com/terms/p/putoption.asp), the option buyer can exercise their right at any point between when the contract is purchased and the expiration date. On the other hand, buyers of [European](https://www.investopedia.com/terms/e/europeanoption.asp) style contracts can only exercise their right on the expiration date. The right to sell shares of `XYZ` at $K$ USD/share is not free; the option buyer pays a premium per contract to the option seller for this right. 

The profit that a put contract buyer experiences, denoted by $V_{p}$, depends upon the difference between the share price of `XYZ` and the strike price $K$ of the contract:

````{prf:definition} Fractional return
:label: defn-PL-put-contract

One put contract was purchased for the underlying stock `XYZ` for $\mathcal{P}$ USD/contract. Let the strike price of the put contract be $K$ USD/share, and the share price of `XYZ` be $S$ USD/share. Then, at expiration, the put contract has
value $V_{p}$:

```{math}
V_{p} = \max\left(K - S,0\right) - \mathcal{P}
```

````


(content:references:option-pricing-algorithms)=
## Options Pricing Algorithms
Fill me in.

---

## Summary
Fill me in here.

<!-- ## Cox-Ross-Rubinstein (CRR) binomial pricing model

The binomial options pricing model provides a generalizable numerical method for the valuation of American style call and put options contacts. The model uses a discrete-time lattice model of the varying price over time of the underlying financial instrument. The binomial model was first proposed by William Sharpe in the 1978 edition of Investments and formalized by Cox, Ross and Rubinstein {cite}`COX1979229`.

```{image} ./figs/CRR-BinomialModel.pdf
:alt: CRR-Schematic
:width: 480px
:align: center
``` -->