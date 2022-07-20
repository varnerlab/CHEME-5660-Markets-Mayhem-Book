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
* Discuss the {ref}`content:references:option-probability-of-profit-algorithms`
* Discuss several {ref}`content:references:option-pricing-algorithms`

---

(content:references:option-contracts)=
## Option Contracts

```{figure} ./figs/Fig-Options-Grid.pdf
---
height: 280px
name: fig-options-contract-grid
---
The rights and responsibilities of the buyer and seller of [American](https://www.investopedia.com/terms/a/americanoption.asp)
style put and call option contracts.  
```

The types, rights, and responsibilities of options contracts are shown in ({numref}`fig-options-contract-grid`).
There are two types of contracts, a [call contract](https://www.investopedia.com/terms/c/calloption.asp) and a [put contract](https://www.investopedia.com/terms/p/putoption.asp), and many different styles of contracts. However, we'll consider only [American](https://www.investopedia.com/terms/a/americanoption.asp) and [European](https://www.investopedia.com/terms/e/europeanoption.asp) style contracts.  Option contract buyers (long positions), regardless of the type of contract, pay a premium to have the right (but not the obligation) to perform an action (buy or sell shares of `XYZ`); [American](https://www.investopedia.com/terms/a/americanoption.asp) style contract buyers can act at any time between when the contract was purchased and expiration, while [European](https://www.investopedia.com/terms/e/europeanoption.asp) style buyers can only act at expiration.  On the other hand, the option seller (short position), in exchange for the premium paid by the buyer, _must_ buy or sell shares of `XYZ` in response to the choice of the contract buyer. 

Like bonds, investors can profit from holding contracts until expiration or by trading the contracts in the options market. Thus, options contracts can be reviewed from two perspectives, at expiration or as stand-alone tradable instruments. 

Let's begin the discussion of options contracts by exploring their behavior at expiration.      

### Call contracts
A [call contract](https://www.investopedia.com/terms/c/calloption.asp) gives the option contract buyer the right, but not the obligation, to purchase 100 shares of `XYZ` (per contract) from the seller at a particular price per share (called the strike price $K$) at some point in the future (called the expiration date). In the case of [American](https://www.investopedia.com/terms/a/americanoption.asp) style [call contracts](https://www.investopedia.com/terms/c/calloption.asp), the option buyer can exercise their right at any point between when the contract was purchased and the expiration date. On the other hand, buyers of [European](https://www.investopedia.com/terms/e/europeanoption.asp) style contracts can only exercise their right on the expiration date. The right to purchase shares of `XYZ` at $K$ USD/share is not free; the option buyer pays a premium per contract to the option seller for this right. 

The profit at expiration that a call contract buyer experiences depends upon the difference between the share price of `XYZ` and the strike price $K$ of the contract (contract payoff) and how much the call contract costs:

````{prf:definition} Call Contract Payoff and Profit
:label: defn-PL-call-contract

An investor purchases a call contract for the underlying stock `XYZ` for $\mathcal{P}$ USD/contract, where the contract controls 100 shares of `XYZ`. 

Let the strike price of the call contract be $K$ USD/share, and the share price of `XYZ` at expiration be $S$ USD/share. Then, at expiration, the call contract has the payoff $V_{c}$ USD/share:

```{math}
V_{c} = \max\left(S-K,0\right)
```

and a profit (loss) for the buyer of:

```{math}
P_{c} = V_{c} -  \mathcal{P}
```

where $P_{c}$ denotes the profit (or loss) per contract per share of `XYZ`. The contract seller experiences a profit (or loss) of $\bar{P}_{c}$ where

```{math}
P_{c}+\bar{P}_{c} = 0
```

````

#### Payoff, Profit and Loss for Call contracts
The payoff (and profit/loss) diagram for a call contract at expiration for Advanced Micro Devices with ticker [AMD](https://www.google.com/search?client=safari&rls=en&sxsrf=ALiCzsbTZ3IEA10C9Rgs6Lb7YLN8LAILVQ:1657882036543&q=NASDAQ:+AMD&stick=H4sIAAAAAAAAAONgecRoyi3w8sc9YSmdSWtOXmNU4-IKzsgvd80rySypFJLgYoOy-KR4uLj0c_UNzKuy4ytzeRaxcvs5Brs4BlopOPq6AACfr0n4SAAAAA&sa=X&ved=2ahUKEwjV_ffu2_r4AhUxJUQIHcXZAPkQsRV6BAhVEAM&biw=1594&bih=921&dpr=2) is shown in 
{prf:ref}`call-contract-expiration`. The _buyer_ of the [AMD](https://www.google.com/search?client=safari&rls=en&sxsrf=ALiCzsbTZ3IEA10C9Rgs6Lb7YLN8LAILVQ:1657882036543&q=NASDAQ:+AMD&stick=H4sIAAAAAAAAAONgecRoyi3w8sc9YSmdSWtOXmNU4-IKzsgvd80rySypFJLgYoOy-KR4uLj0c_UNzKuy4ytzeRaxcvs5Brs4BlopOPq6AACfr0n4SAAAAA&sa=X&ved=2ahUKEwjV_ffu2_r4AhUxJUQIHcXZAPkQsRV6BAhVEAM&biw=1594&bih=921&dpr=2) call contract experiences (at expiration): 

* Loss $S<K+\mathcal{P}$: the share price is _less than_ the strike price plus the premium paid per share for the contract. 
* Breakeven $S=K+\mathcal{P}$: the share price _equals_ the strike price plus the premium paid per share for the contract. 
* Profit $S>K+\mathcal{P}$: the share price is _greater than_ the strike price plus the premium paid per share for the contract. 

````{prf:example} AMD Call Contract
:label: call-contract-expiration

We are interested in buying a call contract for Advanced Micro Devices with ticker [AMD](https://www.google.com/search?client=safari&rls=en&sxsrf=ALiCzsbTZ3IEA10C9Rgs6Lb7YLN8LAILVQ:1657882036543&q=NASDAQ:+AMD&stick=H4sIAAAAAAAAAONgecRoyi3w8sc9YSmdSWtOXmNU4-IKzsgvd80rySypFJLgYoOy-KR4uLj0c_UNzKuy4ytzeRaxcvs5Brs4BlopOPq6AACfr0n4SAAAAA&sa=X&ved=2ahUKEwjV_ffu2_r4AhUxJUQIHcXZAPkQsRV6BAhVEAM&biw=1594&bih=921&dpr=2). The current share price of `AMD` is \$78.94 per share (around 3:30 PM ITH time on Th 7/14), and we belive the shares will close higher before contract expiration.

Compute the payoff and profit/loss diagram at expiration for a July 15 `AMD` call contract with a strike $K$ = 80.0 USD/share. The market price for the July 15 `AMD` call contract is $\mathcal{P}$ = 0.36 USD/share.


```{figure} ./figs/Fig-AMD-Call-Jul15-1DTE.pdf
---
height: 420px
name: fig-call-contract-payout-schematic
---
Payoff and profit diagrams for an AMD call option.  Solid lines denote the payout (profit) from the perspective of the contract buyer. Dashed lines denote the payout (profit) from the perspective of the contract seller
```

source: [live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [static HTML](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-CallPutContract-Payoff.jl.html)

````

The business case for buying (or selling) a call contract:
* __Buyer (long)__: From the buyer's perspective, call contracts allow an investor to benefit from the price movement of `XYZ` to the upside _without_ purchasing `XYZ`. Further, call options (again from the buyer's perspective) have _limited downside risk_, i.e., the maximum amount that the holder of the call option can lose is the premium paid for the option. Finally, call options are a mechanism to purchase shares of `XYZ` at the strike price of $K$ instead of the market price of $S$. 
* __Seller (short)__: From the seller's perspective, the main objective of selling a call contract is to collect the premium $\mathcal{P}$. Call contracts also allow the seller to benefit from the price movement of `XYZ` to the downside _without_ purchasing `XYZ`. However, for a seller, call options have _unlimted upside_ risk; thus, call options are often only sold by investors who already own the required number of shares of `XYZ` (known as a [covered call position](https://www.investopedia.com/terms/c/coveredcall.asp)). Finally, call options offer the seller the opportunity to sell shares of `XYZ` at the strike price of $K$ instead of the market price of $S$.

### Put contracts
A [put contract](https://www.investopedia.com/terms/p/putoption.asp) gives the option contract buyer the right, but not the obligation, to sell 100 shares of `XYZ` (per contract) to the option seller at the strike price $K$, either by or on the expiration date. In the case of [American](https://www.investopedia.com/terms/a/americanoption.asp) style [put contracts](https://www.investopedia.com/terms/p/putoption.asp), the option buyer can exercise their right at any point between when the contract is purchased and the expiration date. On the other hand, buyers of [European](https://www.investopedia.com/terms/e/europeanoption.asp) style contracts can only exercise their right on the expiration date. The right to sell shares of `XYZ` at $K$ USD/share is not free; the option buyer pays a premium per contract to the option seller for this right. 

The profit that a put contract buyer experiences, denoted by $V_{p}$, depends upon the difference between the share price of `XYZ` and the strike price $K$ of the contract:

````{prf:definition} Put Contract Payoff and Profit
:label: defn-PL-put-contract

An investor purchases a put contract for the underlying stock `XYZ` for $\mathcal{P}$ USD/contract, where the contract controls 100 shares of `XYZ`. 

Let the strike price of the put contract be $K$ USD/share, and the share price of `XYZ` be $S$ USD/share. Then, at expiration, the put contract has the payoff $V_{p}$ USD/share:

```{math}
V_{p} = \max\left(K - S,0\right)
```

and a profit (loss) for the buyer of:

```{math}
P_{p} = V_{p} -  \mathcal{P}
```

where $P_{p}$ denotes the profit (or loss) per contract per share of `XYZ`. 
The contract seller experiences a profit (or loss) of $\bar{P}_{p}$ where

```{math}
P_{p}+\bar{P}_{p} = 0
```

````

#### Payoff, Profit and Loss for Put contracts
The payoff (and profit/loss) diagram for a put contract at expiration for Advanced Micro Devices with ticker [AMD](https://www.google.com/search?client=safari&rls=en&sxsrf=ALiCzsbTZ3IEA10C9Rgs6Lb7YLN8LAILVQ:1657882036543&q=NASDAQ:+AMD&stick=H4sIAAAAAAAAAONgecRoyi3w8sc9YSmdSWtOXmNU4-IKzsgvd80rySypFJLgYoOy-KR4uLj0c_UNzKuy4ytzeRaxcvs5Brs4BlopOPq6AACfr0n4SAAAAA&sa=X&ved=2ahUKEwjV_ffu2_r4AhUxJUQIHcXZAPkQsRV6BAhVEAM&biw=1594&bih=921&dpr=2) is shown in 
{prf:ref}`put-contract-expiration`. The _buyer_ of the [AMD](https://www.google.com/search?client=safari&rls=en&sxsrf=ALiCzsbTZ3IEA10C9Rgs6Lb7YLN8LAILVQ:1657882036543&q=NASDAQ:+AMD&stick=H4sIAAAAAAAAAONgecRoyi3w8sc9YSmdSWtOXmNU4-IKzsgvd80rySypFJLgYoOy-KR4uLj0c_UNzKuy4ytzeRaxcvs5Brs4BlopOPq6AACfr0n4SAAAAA&sa=X&ved=2ahUKEwjV_ffu2_r4AhUxJUQIHcXZAPkQsRV6BAhVEAM&biw=1594&bih=921&dpr=2) put contract experiences (at expiration): 

* Loss $S>K+\mathcal{P}$: the share price is _greater than_ the strike price plus the premium paid per share for the contract. 
* Breakeven $S=K+\mathcal{P}$: the share price _equals_ the strike price plus the premium paid per share for the contract. 
* Profit $S<K+\mathcal{P}$: the share price is _less than_ the strike price plus the premium paid per share for the contract. 

````{prf:example} AMD Put Contract 1 DTE
:label: put-contract-expiration

We are interested in buying a call contract for Advanced Micro Devices with ticker [AMD](https://www.google.com/search?client=safari&rls=en&sxsrf=ALiCzsbTZ3IEA10C9Rgs6Lb7YLN8LAILVQ:1657882036543&q=NASDAQ:+AMD&stick=H4sIAAAAAAAAAONgecRoyi3w8sc9YSmdSWtOXmNU4-IKzsgvd80rySypFJLgYoOy-KR4uLj0c_UNzKuy4ytzeRaxcvs5Brs4BlopOPq6AACfr0n4SAAAAA&sa=X&ved=2ahUKEwjV_ffu2_r4AhUxJUQIHcXZAPkQsRV6BAhVEAM&biw=1594&bih=921&dpr=2). The current share price of `AMD` is \$78.94 per share (around 3:30 PM ITH time on Th 7/14), and we belive the shares will close lower before contract expiration.

Compute the payoff and profit/loss diagram at expiration for a July 15 `AMD` put contract with a strike $K$ = 77.0 USD/share. The market price for the July 15 `AMD` put contract is $\mathcal{P}$ = 0.50 USD/share.


```{figure} ./figs/Fig-AMD-Put-Jul15-1DTE.pdf
---
height: 420px
name: fig-put-contract-payout-schematic
---
Payoff and profit diagrams for an AMD put option. Solid lines denote the payout (profit) from the perspective of the contract buyer. Dashed lines denote the payout (profit) from the perspective of the contract seller.
```

source: [live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [static HTML](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-CallPutContract-Payoff.jl.html)

````

The business case for buying (or selling) put contracts:
* __Buyer (long)__: From the buyer's perspective, put contracts allow an investor to benefit from the price movement of `XYZ` to the downside _without_ purchasing `XYZ`. Further, put options (again from the buyer's perspective) have _limited downside risk_, i.e., the maximum amount that the holder of the put option can lose is the premium paid for the option. Finally, put options are a mechanism to sell shares of `XYZ` at the strike price of $K$ instead of the market price of $S$. 
* __Seller (short)__: From the seller's perspective, the main objective of selling a put contract is to collect the premium $\mathcal{P}$. Put contracts also allow the seller to benefit from the price movement of `XYZ` to the upside _without_ purchasing `XYZ`. However, for a seller, put options have _unlimted downside_ risk; thus, put options are often only sold by investors who have set aside the required capital to purchase
the required number of shares of `XYZ` (known as a [cash secured put position](https://www.fidelity.com/learning-center/investment-products/options/know-about-cash-covered-puts)). Finally, put options offer the seller the opportunity to buy shares of `XYZ` at the strike price of $K-\mathcal{P}$ instead of the market price of $S$.


### Composite contracts
Call and put contracts can be combined to develop composite contract structures with interesting payoff diagrams. In this section, we'll limit our focus to contracts that have the same underlying asset and the same expiration date. However, for those interested in more advanced cases, e.g., combining contracts with different expiration dates, check out [calendar spreads](https://www.investopedia.com/terms/c/calendarspread.asp). 

#### Vertical spreads
[Vertical spreads](https://www.investopedia.com/terms/v/verticalspread.asp) are a _directional strategy_ constructed by simultaneously buying (long) and selling (short) the _same type of option_, with the same expiration date but with different strike prices. Thus, [vertical spreads](https://www.investopedia.com/terms/v/verticalspread.asp) have two _legs_: a long leg (the option purchased by the investor) and a short leg (the option sold by the investor). 

[Vertical spreads](https://www.investopedia.com/terms/v/verticalspread.asp) are a defined risk, directional strategy, i.e., the investor believes the underlying asset `XYZ` share price will either increase or decrease (depending upon the vertical spread). [Vertical spreads](https://www.investopedia.com/terms/v/verticalspread.asp) are defined risk because the maximum possible gain and loss are known when the contract is sold; thus, an investor knows how much they can make or lose at expiration. 

````{prf:example} Vertical spreads
:label: vertical-spread-expiration
Fill me in with some stuff.
````


#### Straddles
A [strangle](https://www.investopedia.com/terms/s/straddle.asp) position is a _neutral strategy_ constructed by simultaneaously buying and selling a put and a call optionm, with the same expiration, and the same strike prices. 


````{prf:example} Straddle
:label: straddle-expiration
Fill me in with some stuff.
````

#### Strangles
A [strangle](https://www.investopedia.com/terms/s/strangle.asp) position is a _neutral strategy_ contructed by simultaneously buying and selling a put and a call option, with the same experiation, but with different strike pricess.


````{prf:example} Strangle
:label: strangle-expiration
Fill me in with some stuff.
````

#### Iron condor
An [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) position is constructed by selling a put and a call options, and simulataneously buying a call and put options, where all legs have different strike prices. 


````{prf:example} Iron condor
:label: iron-condor-expiration
Fill me in with some stuff.
````

(content:references:option-probability-of-profit-algorithms)=
## Probability of profit at expiration
The Probability of Profit (POP) at expiration is the probability that your option position will make at least $0.01 at expiration. 
The probability of profit can be a useful deccison metric, e.g., investors engange in transactions that have a _large_ POP and avoid low probability trades. However, the exact meaning of _large_ or _small_ depnds upon the risk tolerance of the investor. 

We can estimate the Probability of Profit (POP) at expiration using monte-carlo simulation. For example, we can develop a 
geometric brownian motion model of the underlying price dynamics (based on historical data), and then use that model to project the underlying price into the future. 

````{prf:example} Probability of Profit at Expiration
:label: pop-at-expiration


```{figure} ./figs/Fig-AMD-GBM-Sim-N200-IS36-OS10.pdf
---
height: 420px
name: fig-gbm-sim-AMD
---
Payoff and profit diagrams for an AMD put option. Solid lines denote the payout (profit) from the perspective of the contract buyer. Dashed lines denote the payout (profit) from the perspective of the contract seller.
```

````

(content:references:option-pricing-algorithms)=
## Options Pricing Algorithms

### Black-Scholes-Merton (BSM)
The Black-Scholes-Merton (BSM) model is a partial differential equation widely used to price [European](https://www.investopedia.com/terms/e/europeanoption.asp) style options contracts; thus, the BSM model does not condsider the possibility of early excercise that is possible with [American](https://www.investopedia.com/terms/a/americanoption.asp) option contracts. In 1997, Scholes and Merton were awarded the [Nobel Memorial Prize in Economic Sciences](https://www.nobelprize.org/prizes/economic-sciences/1997/press-release/) for their work in finding "a new method to determine the value of derivatives." Black had passed away two years earlier; thus could not share in the prize.

#### Assumptions of the BSM model
The Black-Scholes model makes several assumptions when pricing [European](https://www.investopedia.com/terms/e/europeanoption.asp) style options contracts:

* No dividends are paid by the underlying asset `XYZ` during the life of the option contract.
* Markets are random (i.e., market movements cannot be predicted).
* There are no transaction costs when buying (or selling) an option contract.
* The risk-free rate and volatility of the underlying stock `XYZ` are known and constant.
* The returns of the underlying stock `XYZ` are normally distributed.
* No early excercise of the option contract is possible


### Binomial pricing model
Fill me in.

### Monte-carlo pricing model
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