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

The cost of a call contract $\mathcal{P}$ is a non-linear function of many variables including the current share price of the underlying asset $S$, the strike price of the contract, the number of days before contract expiration, and an unobservable quantity called the implied volatility.

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

The cost of a put contract leg $\mathcal{P}$ is a non-linear function of many variables including the current share price of the underlying asset $S$, the strike price of the contract, the number of days before contract expiration, and an unobservable quantity called the implied volatility. 

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

The overall profit $\hat{P}$ for a composite contract structure consiting of $\mathcal{C}$ indiviudal contracts, is the sum of the profits for each the individual contracts (legs) weighted by the number of contracts of type $i$:

$$\hat{P} = \sum_{i\in\mathcal{C}}\theta_{i}n_{i}P_{i}$$

where $\theta_{i}$ denotes the direction of contract $i$: if contract $i$ is short (sold), then $\theta_{i}=-1$, otherwise $\theta_{i}=1$. The quanitity $n_{i}$ denotes the copy number of contract $i$. 

(content:references:option-contracts-vertical-spread)=
#### Vertical spreads
[Vertical spreads](https://www.investopedia.com/terms/v/verticalspread.asp) are a _defined risk directional strategy_ constructed by simultaneously buying (long) and selling (short) the _same type of option_, with the same expiration date but with _different_ strike prices. Thus, [vertical spreads](https://www.investopedia.com/terms/v/verticalspread.asp) have two _legs_: a long leg (the option purchased by the investor) and a short leg (the option sold by the investor). [Vertical spreads](https://www.investopedia.com/terms/v/verticalspread.asp) are a defined risk, directional strategy, i.e., the investor believes the share price of the underlying asset `XYZ` will either increase or decrease, depending upon the type of vertical spread. [Vertical spreads](https://www.investopedia.com/terms/v/verticalspread.asp) are defined risk because the maximum possible gain (or loss) is known when the contract is sold; thus, an investor knows how much they can make or lose at expiration _before_ they enter the trade. However, the future share price of `XYZ` is unknown when the investor opens the trade. 

Two types of vertical spreads can be constructed from put contracts; each has a different directional assumption. A _put bullish credit spread_ assumes the underlying asset `XYZ` share price will increase between now and expiration. In contrast, a _put bearish debit spread_ assumes the underlying asset `XYZ` share price will decrease between now and expiration. When investors open a bullish credit spread, they receive a credit (the maximum profit) upfront. On the other hand, when opening a debit spread, the investor incurs a net debit to their account. The trade becomes profitable over time if the directional assumption is correct.

In general, the profit for a put vertical spread is a function of the strike prices, and the cost of each of the legs of the composite contract:


````{prf:definition} Profit Put Vertical Spread
:label: defn-PL-put-contract-vertical-spread

Consider a vertical spread constructed from put contracts on the underlying stock `XYZ`. Let $K_{j}$ denote the strike price of put contract $j$. The price of contract $j$ $\mathcal{P}_{j}$. Further, let $S$ denote the share price of `XYZ` at expiration. Finally, let contract 1 be the short leg ($\theta_{1} = -1$, $\theta_{2}=1$), and $n_{1} = n_{2} = 1$.

Then, the profit for a single Put Vertical spread $P$ at expiration is given by:

$$\hat{P} = -P_{1}+P_{2}$$

which after substitution of the profit functions for a put contract gives:

$$\hat{P} = \max\left(K_{2} - S,0\right) - \max\left(K_{1} - S,0\right) + \left(\mathcal{P}_{1} - \mathcal{P}_{2}\right)$$

The first term is the net payout of the two legs of the spread, while the second term is the net cost of the two contracts.

The maximum possible profit, loss and breakeven conditions are given by:
* The maximum possible profit of $\left(\mathcal{P}_{1} - \mathcal{P}_{2}\right)$ will occur when $S\geq{K_{1}}$.
* The maximum possible loss of $K_{2} - K_{1} + \left(\mathcal{P}_{1} - \mathcal{P}_{2}\right)$ will occur when $S\leq{K_{2}}$.
* The vertical put spread will breakeven, $\hat{P} = 0$, when $S =  K_{1}+\left(\mathcal{P}_{2} - \mathcal{P}_{1}\right)$.

````
{prf:ref}`defn-PL-put-contract-vertical-spread` has many exciting types of behavior; it is much more complex than it might first appear as the cost of each contract $\mathcal{P}_{j}$ is a non-linear function of many variables including the current share price of the underlying asset $S$, the strike price of the contract, the number of days the contract has before expiration, and the implied volatility.

````{prf:example} Vertical Put Spreads
:label: vertical-put-spread-expiration

Let the current share price of `XYZ` be $S_{o}$ USD/share, and let $S$ denote the share price of `XYZ` at expiration. Then:

* If $S_{o}>K_{1}>K_{2}$ and leg 1 is the short put leg, $\mathcal{P}_{1}>\mathcal{P}_{2}$. A vertical put spread constructed in this regime will be a _bullish credit spread_, i.e., the investor will receive a _credit_ when opening the trade, and expects the share price of `XYZ` to _increase_, $S>S_{o}$. The trade will reach maximum profit when $S\geq{K_{1}}$, maximum loss when $S\leq{K_{2}}$ and will break even at $S =  K_{1}+\left(\mathcal{P}_{2} - \mathcal{P}_{1}\right)$.

```{figure} ./figs/Fig-SPY-Profit-Put-Credit-Spread.pdf
---
height: 420px
name: fig-spy-profit-put-vertical-spread
---
Example profit and loss diagram at expiration for a [SPY](https://finance.yahoo.com/quote/SPY/) put vertical credit spread. Parameters: $K_{1}$ = \$315 USD/share (short strike), $K_{2}$ = \$310 USD/share (long strike), $\mathcal{P}_{1}$ = \$5.25 USD/share and $\mathcal{P}_{2}$ = \$4.31 USD/share.    
```

* If $S_{o}>K_{2}>K_{1}$ and leg 1 is the short put leg, $\mathcal{P}_{2}>\mathcal{P}_{1}$. A vertical put spread constructed in this regime will be a _bearish debit spread_, i.e., the investor will pay a _debit_ when opening the trade and expects the share price of `XYZ` to _decrease_ $S<S_{o}$. The trade will reach maximum profit when $S\leq{K_{1}}$, maximum loss when $S\geq{K_{2}}$ and will break even at $S =  K_{1}+\left(\mathcal{P}_{2} - \mathcal{P}_{1}\right)$.

```{figure} ./figs/Fig-AMD-Profit-Put-Debit-Spread.pdf
---
height: 420px
name: fig-amd-profit-put-vertical-spread
---
Example profit and loss diagram at expiration for a [AMD](https://finance.yahoo.com/quote/AMD/) put vertical debit spread. Parameters: $K_{1}$ = \$90 USD/share (short strike), $K_{2}$ = \$105 USD/share (long strike), $\mathcal{P}_{1}$ = \$4.70 USD/share and $\mathcal{P}_{2}$ = \$13.35 USD/share
```

source: [live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [static HTML](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-SPY-VericalSpread-Contract-Payoff.jl.html)

````

Although not shown here, [Vertical spreads](https://www.investopedia.com/terms/v/verticalspread.asp) can also be constructed using [call contracts](https://www.investopedia.com/terms/c/calloption.asp).

#### Straddles
A [straddle](https://www.investopedia.com/terms/s/straddle.asp) is a _neutral strategy_ constructed by simultaneously buying (or selling) a put and a call option on the same underlying asset `XYZ`, with the _same expiration_, and the _same strike price_. Depending upon the choice of the strike prices and whether an investor buys or sells both legs, a [straddle](https://www.investopedia.com/terms/s/straddle.asp) can be initiated as a credit or debit and can potentially have undefined profit or loss. Unlike directional strategies such as {ref}`content:references:option-contracts-vertical-spread`, a [straddle](https://www.investopedia.com/terms/s/straddle.asp) is a _neutral_ position; an investor holding a [straddle](https://www.investopedia.com/terms/s/straddle.asp) profits if the share price of `XYZ` moves up, down or potentially zero depending upon the construction of the straddle.

````{prf:definition} Profit of a Straddle
:label: defn-PL-put-contract-straddle

A [straddle](https://www.investopedia.com/terms/s/straddle.asp) is a _neutral strategy_ constructed by simultaneously buying (or selling) a put and a call option on the underlying asset `XYZ`, with the _same expiration_, and the _same strike price_. 

Let the current share price of `XYZ` be $S_{o}$ USD/share, and let $S$ denote the share price of `XYZ` at expiration. Further, let $K_{j}$ denote the strike price of contract $j$ (USD/share), where the price of contract $j$ is $\mathcal{P}_{j}$ (USD/share). Finally, let index $j=1$ denote the put contract, $j=2$ denote the call contract, and $K_{1}=K_{2}\equiv{K}$ (both legs have the same strike in a [straddle](https://www.investopedia.com/terms/s/straddle.asp)).

Then, the profit for a single straddle contract $\hat{P}$ at expiration is given by:

$$\hat{P} = \theta\cdot\left(P_{1}+P_{2}\right)$$

where $\theta_{1}=\theta_{2}\equiv\theta$ denotes a direction parameter: $\theta=-1$ if each leg is sold (short), $\theta=1$ otherwise. After substitution of the profit functions for a put and a call contract, 
the overall profit $\hat{P}$ is given by:

$$\hat{P} = \theta\cdot\Bigl[(K-S)^{+}+(S-K)^{+}-(\mathcal{P}_{1}+\mathcal{P}_{2})\Bigr]$$

where $(K-S)^{+}=\max(K-S,0)$ and $(S-K)^{+} = \max(S-K,0)$. Thus, the profit (or loss) of a straddle has three regimes given by:

$$
\hat{P} = \begin{cases}
  \theta\cdot\Bigl[(S-K)-\left(\mathcal{P}_{1}+\mathcal{P}_{2}\right)\Bigr]  & S>K \\
  -\theta\cdot\Bigl[\mathcal{P}_{1}+\mathcal{P}_{2}\Bigr] & S=K \\
    \theta\cdot\Bigl[(K-S)-\left(\mathcal{P}_{1}+\mathcal{P}_{2}\right)\Bigr] & S<K
\end{cases}
$$

Finally, a straddle has _two_ possible breakeven points denoted as $S^{+}$ and $S^{-}$:
* If $S>K$: a straddle will breakeven at $S^{+} = K + \left(\mathcal{P}_{1}+\mathcal{P}_{2}\right)$
* If $S<K$: a straddle will breakeven at $S^{-} = K - \left(\mathcal{P}_{1}+\mathcal{P}_{2}\right)$.

````

{prf:ref}`defn-PL-put-contract-straddle` gives the profit conditions for both long (buy both the call and the put legs) and short (sell both the call and put legs) straddles. Let's put some numbers into the profit conditions and analyze their behavior ({prf:ref}`straddle-profit-expiration`).


````{prf:example} Profit of a Straddle
:label: straddle-profit-expiration

A __short straddle__ is constructed by simultaneously _selling_ both a put and a call option with the same expiration, strike price, and underlying asset `XYZ` ({numref}`fig-amd-profit-short-straddle`). When opening a short straddle, an investor receives a _credit_, i.e., the proceeds from selling the call and put options. For a short straddle, $\theta=-1$ which gives the profit condtions:

$$\hat{P} = \begin{cases}
  -\Bigl[(S-K)-\left(\mathcal{P}_{1}+\mathcal{P}_{2}\right)\Bigr]  & S>K \\
  \Bigl[\mathcal{P}_{1}+\mathcal{P}_{2}\Bigr] & S=K \\
    -\Bigl[(K-S)-\left(\mathcal{P}_{1}+\mathcal{P}_{2}\right)\Bigr] & S<K
\end{cases}$$

A short straddle is profitable if the share price of the underlying asset of `XYZ` stays near the strike price of $K$. Thus, for a short straddle, the investor wants small price movements. At expiration:
* A short straddle experiences the maximum profit when $S=K$ 
* A short straddle can experience an _undefined loss_ when $S<S^{-}$ and $S>S^{+}$
* A short straddle benefits from limited movement of the share price of `XYZ` during the lifetime of the contract

```{figure} ./figs/Fig-AMD-Profit-Short-Straddle.pdf
---
height: 420px
name: fig-amd-profit-short-straddle
---
Example profit and loss diagram at expiration for an [AMD](https://finance.yahoo.com/quote/AMD/) short straddle. Parameters: $K$ = \$100 USD/share, $\mathcal{P}_{1}$ = \$9.95 USD/share and $\mathcal{P}_{2}$ = \$7.45 USD/share
```

A __long straddle__ is constructed by simultaneously _buying_ both a put and a call option with the same expiration, strike price, and underlying asset `XYZ` ({numref}`fig-amd-profit-long-straddle`). When opening a short strangle, an investor is charged a _debit_ to their account, i.e., the cost of purchasing the call and put options. For a long straddle, $\theta=1$ which gives the profit condtions:

$$\hat{P} = \begin{cases}
  (S-K)-\left(\mathcal{P}_{1}+\mathcal{P}_{2}\right) & S>K \\
  -\left(\mathcal{P}_{1}+\mathcal{P}_{2}\right) & S=K \\
  (K-S)-\left(\mathcal{P}_{1}+\mathcal{P}_{2}\right) & S<K
\end{cases}$$

As the share price of `XYZ` moves _away_ from the strike price of $K$, the long straddle becomes profitable. Thus, for a long straddle, the investor wants large price movements so that they can overcome the initial investment required to purchase the call and put options. At expiration:
* A long straddle experiences the maximum loss when $S=K$ 
* A long straddle can experience an _undefined profit_ when $S<S^{-}$ and $S>S^{+}$ 
* A long straddle benefits from large movements of the share price of `XYZ` during the lifetime of the contract

```{figure} ./figs/Fig-AMD-Profit-Long-Straddle.pdf
---
height: 420px
name: fig-amd-profit-long-straddle
---
Example profit and loss diagram at expiration for an [AMD](https://finance.yahoo.com/quote/AMD/) long straddle. 
Parameters: $K$ = \$100 USD/share, $\mathcal{P}_{1}$ = \$9.95 USD/share and $\mathcal{P}_{2}$ = \$7.45 USD/share
```

source: [live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [static HTML view](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-Straddle-Profit.jl.html) 

````

#### Strangles
A [strangle](https://www.investopedia.com/terms/s/strangle.asp) position is a _neutral strategy_ constructed by simultaneously buying and selling a put and a call option on the same underlying asset `XYZ`, with the same expiration but with _different_ strike prices. Depending upon the choice of the strike prices and whether an investor buys or sells both legs, a [strangle](https://www.investopedia.com/terms/s/strangle.asp) can be initiated as a credit or debit and can potentially have undefined profit or loss. Unlike directional strategies such as {ref}`content:references:option-contracts-vertical-spread`, a [strangle](https://www.investopedia.com/terms/s/strangle.asp) is a _neutral_ position; an investor holding a [strangle](https://www.investopedia.com/terms/s/strangle.asp) profits if the share price of `XYZ` moves between the strike prices of the strangle.

````{prf:definition} Profit of a Strangle
:label: defn-PL-put-contract-strangle

A [strangle](https://www.investopedia.com/terms/s/strangle.asp) position is a _neutral strategy_ constructed by simultaneously buying (or selling) a put and a call option on the same underlying asset `XYZ`, with the same expiration but with _different_ strike prices.

Let the current share price of `XYZ` be $S_{o}$ USD/share, and let $S$ denote the share price of `XYZ` at expiration. Further, let $K_{j}$ denote the strike price of contract $j$ (USD/share), where the price of contract $j$ is $\mathcal{P}_{j}$ (USD/share). Finally, let index $j=1$ denote the put contract, $j=2$ denote the call contract; for a [strangle](https://www.investopedia.com/terms/s/strangle.asp) $K_{1} < K_{2}$.

Then, the profit for a single strangle contract $\hat{P}$ at expiration is given by:

$$\hat{P} = \theta\cdot\left(P_{1}+P_{2}\right)$$

where $\theta_{1}=\theta_{2}\equiv\theta$ denotes a direction parameter: $\theta=-1$ if each leg is sold (short), $\theta=1$ otherwise. After substitution of the profit functions for a put and a call contract, 
the overall profit $\hat{P}$ is given by:

$$\hat{P} = \theta\cdot\Bigl[(K_{1}-S)^{+}+(S-K_{2})^{+}-(\mathcal{P}_{1}+\mathcal{P}_{2})\Bigr]$$

where $(K_{1}-S)^{+}=\max(K_{1}-S,0)$ and $(S-K_{2})^{+} = \max(S-K_{2},0)$. Thus, the profit (or loss) of a strangle has three regimes given by:

$$
\hat{P} = \begin{cases}
  \theta\cdot\Bigl[(S-K_{2})-\left(\mathcal{P}_{1}+\mathcal{P}_{2}\right)\Bigr]  & S>K_{2} \\
  -\theta\cdot\Bigl[\mathcal{P}_{1}+\mathcal{P}_{2}\Bigr] & K_{1}\leq{S}\leq{K_{2}} \\
  \theta\cdot\Bigl[(K_{1}-S)-\left(\mathcal{P}_{1}+\mathcal{P}_{2}\right)\Bigr] & S<{K_{1}}
\end{cases}
$$

A [strangle](https://www.investopedia.com/terms/s/strangle.asp) has two break-even points $S^{+}$ and $S^{-}$ where we know that $K_{2}<S^{+}$ and $S^{-}<K_{1}$. Thus, the low break-even point $S^{-}$ is given by:

$$S^{-} = K_{1} - \left(\mathcal{P}_{1}+\mathcal{P}_{2}\right)$$

while the high break-even point $S^{+}$ is given by:

$$S^{+} = K_{2} + \left(\mathcal{P}_{1}+\mathcal{P}_{2}\right)$$

````

{prf:ref}`defn-PL-put-contract-strangle` gives the profit conditions for both long (buy both the call and the put legs) and short (sell both the call and put legs) strangles. Let's put some numbers into the profit conditions and analyze their behavior ({prf:ref}`strangle-profit-expiration`).

````{prf:example} Profit of a Strangle
:label: strangle-profit-expiration

A __short strangle__ is constructed by simultaneously _selling_ both a put and a call option with the same underlying asset `XYZ` and the same expiration, but with different strike prices ({numref}`fig-amd-profit-short-strangle`). When opening a short strangle, an investor receives a _credit_, i.e., the proceeds from selling the call and put options. For a short strangle, $\theta=-1$ which gives the profit condtions:


```{figure} ./figs/Fig-AMD-Profit-Short-Strangle.pdf
---
height: 420px
name: fig-amd-profit-short-strangle
---
Example profit and loss diagram at expiration for an [AMD](https://finance.yahoo.com/quote/AMD/) short strangle. Parameters: $K_{1}$ = \$90 USD/share, $K_{2}$ = \$110 USD/share, $\mathcal{P}_{1}$ = \$4.05 USD/share and $\mathcal{P}_{2}$ = \$5.70 USD/share. $S_{o}$ = \$101.57 USD/share.
```

A __long strangle__ is constructed by simultaneously _buying_ both a put and a call option with the same underlying asset `XYZ` and the same expiration, but with different strike prices ({numref}`fig-amd-profit-long-strangle`). When opening a long strangle, the investor is charged a _debit_ to their account, i.e., the cost of purchasing the call and put options. For a long strangle, $\theta=1$ which gives the profit condtions::

```{figure} ./figs/Fig-AMD-Profit-Long-Strangle.pdf
---
height: 420px
name: fig-amd-profit-long-strangle
---
Example profit and loss diagram at expiration for an [AMD](https://finance.yahoo.com/quote/AMD/) long strangle. Parameters: $K_{1}$ = \$90 USD/share, $K_{2}$ = \$110 USD/share, $\mathcal{P}_{1}$ = \$4.05 USD/share and $\mathcal{P}_{2}$ = \$5.70 USD/share. $S_{o}$ = \$101.57 USD/share.
```
````

#### Iron Condor
An [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) is a _neutral defined risk_ position constructed by _selling_ a put (1) and call (2) options on the underlying asset `XYZ`, while simultaneously _buying_ a put (3) and call (4) options on `XYZ`. All the legs of an [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) have the same underlying asset `XYZ`, and have the same expiration, but they have different strike prices where $K_{3}<K_{1}<K_{2}<K_{4}$. In particular, the two short options are sold with strikes on either side of the current share price $S_{o}$ of `XYZ`, with the short put strike price $K_{1}<S_{o}$ and the short call strike price $K_{2}>S_{o}$. Then, the long legs are purchased above and below the short strikes.  Thus, an [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) position has the character of a [strangle](https://www.investopedia.com/terms/s/strangle.asp) combined with a vertical spread. 

An investor holding an [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) profits if the share price of `XYZ` remains between the strike prices of the two short options (like a short strangle). However, unlike a [strangle](https://www.investopedia.com/terms/s/strangle.asp), an [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) is a defined risk strategy; the long options act to limit any possible losses, but they also restrict potential gains (because of their cost).


````{prf:definition} Profit of an Iron Condor
:label: defn-PL-iron-condor

An [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) is a _neutral defined risk_ position constructed by _selling_ a put (1) and call (2) options on the underlying asset `XYZ`, while simultaneously _buying_ a put (3) and call (4) options on `XYZ`. All legs have the same underlying asset `XYZ`, the same expiration, but different strike prices.

Let the current share price of `XYZ` be $S_{o}$ USD/share, and let $S$ denote the share price of `XYZ` at expiration. Further, let $K_{j}$ denote the strike price of contract $j$ (USD/share), where the price of contract $j$ is $\mathcal{P}_{j}$ (USD/share). Finally, let index $j=1$ denote the short put contract, $j=2$ denote the short call contract,  $j=3$ denote the long put contract and  $j=4$ denote the long call contract; for an [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) $K_{3} < K_{1} <K_{2} < K_{3}$.

Then, the profit for a single iron condor contract $\hat{P}$ at expiration is given by:

$$\hat{P} = \theta_{1}P_{1} + \theta_{2}P_{2} + \theta_{3}P_{3} + \theta_{4}P_{4}$$

where $\theta_{1}=\theta_{2} = -1$ (short legs) and $\theta_{3}=\theta_{4} = 1$ (long legs). After substitution of the profit functions for put and call contracts, the overall profit $\hat{P}$ is given by:

$$\hat{P} = -(K_{1}-S)^{+} - (S-K_{2})^{+} + (K_{3} - S)^{+} + (S-K_{4})^{+} + \left(\mathcal{P}_{1} + \mathcal{P}_{2} - \mathcal{P}_{3}-\mathcal{P}_{4}\right)$$

where $(K_{\star}-S)^{+}=\max(K_{\star}-S,0)$ and $(S-K_{\star})^{+} = \max(S-K_{\star},0)$. The profit (or loss) of an iron condor has several important regimes given by:

$$
\hat{P} = \begin{cases}
  K_{2} - K_{4} + \Bigl(\mathcal{P}_{1} + \mathcal{P}_{2} - \mathcal{P}_{3}-\mathcal{P}_{4}\Bigr)  & S>K_{4} \\
  K_{2} - S + \Bigl(\mathcal{P}_{1} + \mathcal{P}_{2} - \mathcal{P}_{3}-\mathcal{P}_{4}\Bigr)  & K_{2}<S<K_{4} \\
  \Bigl(\mathcal{P}_{1} + \mathcal{P}_{2} - \mathcal{P}_{3}-\mathcal{P}_{4}\Bigr) & K_{1}\leq{S}\leq{K_{2}} \\
  S - K_{1} + \Bigl(\mathcal{P}_{1} + \mathcal{P}_{2} - \mathcal{P}_{3}-\mathcal{P}_{4}\Bigr) & K_{3}<S<K_{1} \\
  K_{3} - K_{1} + \Bigl(\mathcal{P}_{1} + \mathcal{P}_{2} - \mathcal{P}_{3}-\mathcal{P}_{4}\Bigr) & S<K_{3}
\end{cases}
$$

An [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) has two break-even points $S^{+}$ and $S^{-}$ where we know that $K_{2}<S^{+}<K_{4}$ and $K_{3}<S^{-}<K_{1}$. Thus, the low break-even point $S^{-}$ is given by:

$$S^{-} = K_{1} - \Bigl(\mathcal{P}_{1} + \mathcal{P}_{2} - \mathcal{P}_{3}-\mathcal{P}_{4}\Bigr)$$

while the high break-even point $S^{+}$ is given by:

$$S^{+} = K_{2} + \Bigl(\mathcal{P}_{1} + \mathcal{P}_{2} - \mathcal{P}_{3}-\mathcal{P}_{4}\Bigr)$$


````


{prf:ref}`defn-PL-iron-condor` gives the profit conditions for an [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp). Let's put some numbers into the profit conditions and analyze their behavior ({prf:ref}`iron-condor-expiration`).


````{prf:example} Profit of an Iron Condor
:label: iron-condor-expiration

An [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) is constructed by _selling_ a put (1) and call (2) options on the underlying asset `XYZ`, while simultaneously _buying_ a put (3) and call (4) options on `XYZ`. All legs have the same expiration, but different strike prices. 

In particular, the short legs of an [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) have strike prices near the share price of `XYZ`, while the two long legs are further out of the money (farther away from the current share price of `XYZ`). 

The profit (or loss) for an [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) on [MU](https://finance.yahoo.com/quote/MU/) is shown in {numref}`fig-mu-iron-condor`. The low break-even point $S^{-}$ = \$48.54 USD/share while the high break-even point $S^{+}$ = \$71.46 USD/share.

```{figure} ./figs/Fig-MU-Profit-IronCondor.pdf
---
height: 420px
name: fig-mu-iron-condor
---
Example profit and loss diagram at expiration for an [MU](https://finance.yahoo.com/quote/MU/) iron condor. Parameters: $K_{1}$ = \$50 USD/share, $K_{2}$ = \$70 USD/share, $K_{3}$ = \$45 USD/share, $K_{4}$ = \$75 USD/share, $\mathcal{P}_{1}$ = \$1.09 USD/share $\mathcal{P}_{2}$ = \$2.00 USD/share, $\mathcal{P}_{3}$ = \$0.60 USD/share and $\mathcal{P}_{4}$ = \$1.03 USD/share. $S_{o}$ = \$62.46 USD/share.
```

source: [live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [static HTML view](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-IronCondor-Profit.jl.html)
````

(content:references:option-probability-of-profit-algorithms)=
## Probability of profit at expiration
The Probability of Profit (POP) at expiration is the probability that your option position will make at least $0.01 at expiration. The probability of profit can be a helpful decision metric, e.g., investors engage in transactions with a _large_ POP and avoid low probability trades. However, the exact meaning of _large_ or _small_ depends upon the investor’s risk tolerance. 

### Monte-Carlo simulation
Using Monte-Carlo simulation, we can estimate the option position’s probability of Profit (POP) at expiration. 
First, we can develop a simulation of the price of the underlying asset `XYZ,` e.g., using a geometric Brownian motion model developed from historical data, and then use that model to project the underlying price into the future until expiration. Finally, we can compute the cumulative probability curve to determine the probability that a profit condition is satisfied.

To explore this idea, let's compute the probability of profit of a [short strangle](https://www.investopedia.com/terms/s/strangle.asp) position in [AMD](https://finance.yahoo.com/quote/AMD/) in {prf:ref}`pop-amd-strange-expiration`:


````{prf:example} Probability of Profit at Expiration for AMD Strangle
:label: pop-amd-strange-expiration

Let's compute the probability of profit at expiration for a short strangle for  [AMD](https://finance.yahoo.com/quote/AMD/) with the following data: short put strike $K_{1}$ = \$80.0 USD/share, short call srtike $K_{1}$ = \$120.0 USD/share, $\mathcal{P}_{1}$ = \$1.69 USD/share and $\mathcal{P}_{2}$ = \$2.97 USD/share. The current share price of [AMD](https://finance.yahoo.com/quote/AMD/) is $S_{o}$ = 102.53 USD/share.

* The first step is to _estimate_ the future close price of the underlying asset in this case [AMD](https://finance.yahoo.com/quote/AMD/) at expiration. The close price was _predicted_ by building a GBM model based on the previous 45-days of AMD close price data; close price data was downloaded from the [Polygon.io application programming interface (API)](https://polygon.io). The GBM analytical solution developed previously was used to generate N = 10,000 sample paths from which the cumulative probability was calculated ({numref}`fig-cumulative-d-AMD-10K`).

```{figure} ./figs/Fig-CumulativeDistribution-C-AMD-D-10-21-22-N10K.pdf
---
height: 380px
name: fig-cumulative-d-AMD-10K
---
Estimated [cumulative distribution curve](https://en.wikipedia.org/wiki/Cumulative_distribution_function) for the close price of [AMD](https://finance.yahoo.com/quote/AMD/) on 10/21/2022. 
```

* Next, we calculated the two break even points for an [AMD](https://finance.yahoo.com/quote/AMD/) short strangle with expiration on 10/21/2022. From {prf:ref}`defn-PL-put-contract-strangle` and the data for AMD we found: $S^{-}$ = \$75.34 USD/share and $S^{+}$ = \$124.66 USD/share.

* Finally, we used the [cumulative probability curve](https://en.wikipedia.org/wiki/Cumulative_distribution_function) shown in {numref}`fig-cumulative-d-AMD-10K`, estimated from Monte-Carlo simulation, to calculate the probability that [AMD](https://finance.yahoo.com/quote/AMD/) will close at various essential price points:

| Case   | Symbol |         Probability   
| :------------- | :-- | :-------------|
| AMD closes less than high break-even | $P(X<S^{+})$  | 0.80 |
| AMD closes less than low break-even | $P(X<S^{-})$  | 0.21 |
| AMD closes less than short call strike | $P(X<K_{2})$  | 0.76 |
| AMD closes less than short put strike  | $P(X<K_{1})$  | 0.27 |
| AMD closes between strikes (max profit) | $P(K_{1}<X\leq{K_{2}})$ | 0.49
| AMD closes between break-even points (profit) | $P(S^{-}<X\leq{S^{+}})$ | 0.59


source: [live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [static HTML view](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-POP-Short-AMD-Strangle.jl.html)
````

### Implied Volatility
The [implied volatility (IV)](https://www.investopedia.com/terms/i/iv.asp) is the market's forecast of the likely movement in the price of the underlying asset `XYZ`. Thus, it is a subjective belief of the traders buying and selling options contracts on `XYZ.` As we shall see, the IV is a critical factor in determining the price of an options contract. However, the IV can also be used as a tool to forecast the market’s belief of the price of the underlying asset `XYZ` into the future:

````{prf:definition} Implied Volatility
:label: defn-iv-std-model
Let the current share price of the underlying asset `XYZ` be given by $S_{o}$. 

Then, the [implied volatility (IV)](https://www.investopedia.com/terms/i/iv.asp) is the options markets estimate of the standard deviation of the share price of `XYZ` one year in the future. Thus, the IV is a forecast of the standard deviation of the price of `XYZ` (volatility), denoted as $\hat{\sigma}(\Delta{T})$, into the future:

```{math}
\hat{\sigma}(\Delta{T}) = S_{o}\cdot{IV}\cdot\sqrt{\beta\Delta{T}}
```

where $\Delta{T}$ denotes the number of days into the future for which we wish to estimate the share price of `XYZ,` and $\beta$ denotes a conversion factor; $\beta$ is the inverse of the number of trading days per year, typically 252 days.

````

Unfortunately, knowing a value for the standard deviation estimated from the [implied volatility (IV)](https://www.investopedia.com/terms/i/iv.asp) is only half of what we need to compute the probability of profit for an options position at expiration. In addition, we need a model of how the share price is distributed. 

A fundamental assumption in the mathematical finance community is that share prices are [Log-normally distributed](https://www.investopedia.com/articles/investing/102014/lognormal-and-normal-distribution.asp). Given the premise of [Log-normal distributed](https://www.investopedia.com/articles/investing/102014/lognormal-and-normal-distribution.asp) share prices of `XYZ` and the IV model of the volatility ({prf:ref}`defn-iv-std-model`) we postulate:

````{prf:conjecture} IV-Projected price distribution
:label: 

The share price of `XYZ` is [log-normal distributed](https://www.investopedia.com/articles/investing/102014/lognormal-and-normal-distribution.asp) distributed. Further, let $S_{o}$ denote the current share price of `XYZ`.

Then, the share price of `XYZ` $\Delta{T}$ days into the future, denoted by $S(\Delta{T})$, is a random variable governed by the probability density function (PDF):

```{math}
S(\Delta{T}) \sim \text{Lognormal}(S_{o},\hat{\sigma}(\Delta)^2)
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