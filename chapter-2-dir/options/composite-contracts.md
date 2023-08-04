(content:references:american-options-composite-contracts)=
# Composite Contract Profit Diagrams
Call and put contracts can be combined to develop composite contract structures with interesting payoff and profit properties. Initially let's focus on contracts that have the same underlying asset and the same expiration date.

```{topic} Outline
In this lecture we analyze the payoff and profit diagrams of composite option contracts at expiration. In particular, we start by introducing the general case of composite contracts, then focus on composite contracts that have a directional bias, and conclude with contracts that are neutral to the direction of the underlying asset.

* [General composite contracts](content:references:general-composite-contracts) are constructed by combining two or more option contracts to generate a new composite contract with some desired payoff and profit properties. For now, we limit our analysis to contracts that have the same underlying asset and the same expiration date. 
* [Vertical spreads](content:references:vertical-spreads) are composite contracts that have a directional bias. They are constructed by combining a single long and and single short option contract with the same expiration date but different strike prices.
* [Straddles and Strangles](content:references:vertical-straddles-strangles) are composite contracts that are neutral to the direction of the underlying asset. They are constructed by combining two long or two short options contracts with the same expiration date and strike price.
* [Butterflies and Condors](content:references:vertical-butterflies-condors) are composite contracts that are neutral to the direction of the underlying asset. They are constructed by combining two short and two long option contracts with the same expiration date but different strike prices.

```

---

(content:references:general-composite-contracts)=
## General composite contracts
Call and put contracts can be combined to develop composite contract structures with interesting payoff diagrams. Let's limit our focus to contracts that have the same underlying asset and the same expiration date ({prf:ref}`defn-composite-contract-profit`):

````{prf:definition} Composite contract payoff and profit
:label: defn-composite-contract-profit

Let a composite option contract be composed of the set of $d$ legs (individual contracts) $\mathcal{C}$ where each leg $i\in\mathcal{C}$ is written with respect to the same underlying stock `XYZ` and has the same expiration date. Then, the overall payoff of the composite contract $\hat{V}(S(T),K_{1},\dots,K_{d})$ is given by:

```{math}
:label: eqn-overall-payoff-composite-contract
\hat{V}(S(T),K_{1},\dots,K_{d}) = \sum_{i\in\mathcal{C}}\theta_{i}n_{i}V_{i}(S(T),K_{i})
```

where $K_{i}$ denotes the strike price of contract $i\in\mathcal{C}$. The overall profit of the composite contract $\hat{P}$ is given by:

```{math}
:label: eqn-overall-profit-composite-contract
\hat{P}(S(T),K_{1},\dots,K_{d}) = \sum_{i\in\mathcal{C}}\theta_{i}n_{i}P_{i}(S(T),K_{i})
```

where $\theta_{i}$ denotes the direction of contract $i$: if contract $i$ is short (sold), then $\theta_{i}=-1$, otherwise $\theta_{i}=1$, the quantity $n_{i}$ denotes the copy number of contract $i$, ${V}_{i}(S(T),K_{i})$ denotes the payoff of contract $i$, and $P_{i}(S(T),K_{i})$ denotes the profit of contract $i$.

````

For those interested in more advanced cases, e.g., combining contracts with different expiration dates, check out [calendar spreads](https://www.investopedia.com/terms/c/calendarspread.asp), or [diagonal spreads](https://www.investopedia.com/terms/d/diagonalspread.asp) which combine different experation dates and strike prices.

### Implementation
We compute the payoff and profit of a composite contract by summing the payoff and profit of each leg of the contract. 

```{code-block} julia
:caption: Function to compute the Profit of a composite contract
:linenos:

function profit(contracts::Array{T,1}, 
    S::Array{Float64,1})::Array{Float64,2} where T <: AbstractContractModel

    # initialize - 
    number_of_underlying_prices = length(S);
    number_of_contracts = length(contracts);
    profit_array = Array{Float64,2}(undef, number_of_underlying_prices, number_of_contracts+2);

    # main loop -
    for i ∈ 1:number_of_underlying_prices

        # get the underlying price -
        Sᵢ = S[i];

        # compute the payoff -
        profit_array[i,1] = Sᵢ;

        # loop over the contracts -
        for j ∈ 1:number_of_contracts

            # get the contract, and data associated with it -
            contract = contracts[j];
            sense = contract.sense |> Float64;
            copy = contract.copy |> Float64;
            premium = contract.premium;

            # compute the payoff -
            profit_array[i,j+1] = (copy*sense)*(_payoff(contract, Sᵢ) - premium)
        end
    end

    # compute the sum -
    for i ∈ 1:number_of_underlying_prices
        profit_array[i,end] = sum(profit_array[i,2:end-1]);
    end

    # return -
    return profit_array;    
end
```


(content:references:vertical-spreads)=
## Vertical Spreads
[Vertical spreads](https://www.fidelity.com/bin-public/060_www_fidelity_com/documents/learning-center/Deck_Vertical-spreads.pdf), a defined risk directional strategy, involve buying and selling the same type of option with different strike prices and the same expiration date. This creates two legs, a long leg (the option purchased by the investor) and a short leg (the option sold by the investor). The investor can use the strategy to take a position on whether the share price of the underlying stock, such as `XYZ`, will increase or decrease. 

Vertical spreads are defined risk because the maximum possible gain or loss is known when the contract is sold, meaning investors know how much they can make or lose before entering the trade. 

```{note}
It is important to note that the future share price of `XYZ` is unknown when the investor opens the trade. Thus, the investor is making a directional assumption when trading a vertical spread about the future movement of the share price.
```

### Put vertical spreads
There are two types of vertical spreads that can be made with put contracts, each with a different directional assumption. 
* The`bull` put credit spread assumes that the share price of the underlying asset, in this case, `XYZ`, will increase by the time of expiration. 
* In contrast, the `bear` put debit spread assumes that the share price of `XYZ` will decrease by the time of expiration. 

When investors choose the bullish credit spread, they receive a credit upfront, which is the maximum profit. However, when they choose the debit spread, they incur a net debit to their account. The trade can become profitable over time if the directional assumption is correct.

Generally, the profit for a put vertical spread depends on the strike prices and the cost of each leg of the composite contract ({prf:ref}`defn-PL-put-contract-vertical-spread`):


````{prf:definition} Profit Put Vertical spread
:label: defn-PL-put-contract-vertical-spread

Let contract $j$ have a strike price of $K_{j}$ and premium $\mathcal{P}_{j}$. The share price at expiration is given by $S(T)$. Finally, let contract 1 be the short leg $\theta_{1} = -1$ and contract 2 be the long leg $\theta_{2} = 1$. Then, the profit for a single Put vertical spread $P_{12}$ at expiration is given by:

$$\hat{P} = -P_{1}+P_{2}$$

which, after substitution of the profit functions for a put contract, gives:

$$
\hat{P}(S(T),K_{1},K_{2}, \mathcal{P}_{1}, \mathcal{P}_{2}) = \max\left(K_{2} - S(T),0\right) - \max\left(K_{1} - S(T),0\right) + \left(\mathcal{P}_{1} - \mathcal{P}_{2}\right)$$

The first term is the net payout of the two legs of the spread, while the second term is the net cost of the two contracts. The maximum possible profit, loss, and breakeven conditions are given by:

* The maximum possible profit of $\left(\mathcal{P}_{1} - \mathcal{P}_{2}\right)$ will occur when $S\geq{K_{1}}$.
* The maximum possible loss of $K_{2} - K_{1} + \left(\mathcal{P}_{1} - \mathcal{P}_{2}\right)$ will occur when $S\leq{K_{2}}$.
* The vertical put spread will breakeven when $S =  K_{1}+\left(\mathcal{P}_{2} - \mathcal{P}_{1}\right)$.

````

{prf:ref}`defn-PL-put-contract-vertical-spread` has many exciting behaviors. It is much more complex than it might first appear as the cost of each contract $\mathcal{P}_{j}$ is a non-linear function of many variables including the current share price of the underlying asset $S$, the strike price of the contract, the number of days the contract has before expiration, and the implied volatility.

#### Credit spreads
A `bull` put credit spread is a composite contract that combines a short put and a long put, providing the investor with a credit upon opening the trade. This strategy has a directional bias (bullish) and a defined risk, with the short put strike price $K_{1}$ being lower than the current share price $S_{\circ}$ but higher than the long put strike price $K_{2}$ (i.e. $S_{\circ}>K_{1}>K_{2}$). The long put serves to limit potential losses, but it also restricts potential gains due to its cost ({numref}`fig-put-vertical-spread-credit`).


```{figure} ./figs/Fig-put-vertical-spread-credit-bull.svg
---
height: 420px
name: fig-put-vertical-spread-credit
---
The payoff and profit for a bull put credit spread on `XYZ` with 56-DTE. Parameters: $K_{1}=60.0$ USD/share, $K_{2}=50.0$ USD/share, $S_{\circ}=64.69$ USD/share, $\mathcal{P}_{1}=1.39$ USD/share, $\mathcal{P}_{2}=0.23$ USD/share, $T=56$ days, and $r=0.04$.
```

A `bear` put debit spread is a composite contract that combines a short put and a long put, providing the investor with a debit upon opening the trade. This strategy has a directional bias (bearish) and a defined risk, with the short put strike price $K_{1}$ being higher than the current share price $S_{\circ}$ but lower than the long put strike price $K_{2}$ (i.e. $S_{\circ}<K_{1}<K_{2}$). The long put serves to limit potential losses, but it also restricts potential gains due to its cost ({numref}`fig-put-vertical-spread-debit`).

```{figure} ./figs/Fig-put-vertical-spread-debit-bear.svg
---
height: 420px
name: fig-put-vertical-spread-debit
---
The payoff and profit for a bear put debit spread on `XYZ` with 56-DTE. Parameters: $K_{1}=65.0$ USD/share, $K_{2}=75.0$ USD/share, $S_{\circ}=64.69$ USD/share, $\mathcal{P}_{1}=3.30$ USD/share, $\mathcal{P}_{2}=10.70$ USD/share, $T=56$ days, and $r=0.04$.
```

(content:references:vertical-straddles-strangles)=
## Straddles and Strangles

[Straddles](https://www.investopedia.com/terms/s/straddle.asp) and [Strangles](https://www.investopedia.com/terms/s/strangle.asp) are neutral trades, i.e., they do not make a directional assumption. Thus, an investor can benefit in these trades if the share price of the underyling asset increases, decreases or potentially (depending upon how the trade was initialized) not move at all. The primary difference between a [straddle](https://www.investopedia.com/terms/s/straddle.asp) and a [strangle](https://www.investopedia.com/terms/s/strangle.asp) is that the strike prices of the contracts are different in a [strangle](https://www.investopedia.com/terms/s/strangle.asp) while they are the same in a [straddle](https://www.investopedia.com/terms/s/straddle.asp).

### Straddles
A [straddle](https://www.investopedia.com/terms/s/straddle.asp) is a _neutral strategy_ constructed by simultaneously buying (or selling) a `put` and a `call` option on the same underlying asset `XYZ`, with the _same expiration_, and the _same strike price_ ({prf:ref}`defn-PL-straddle`):

```{prf:definition} Profit and loss of a straddle
:label: defn-PL-straddle

Let $K_{j}$ denote the strike price of contract $j$ (USD/share), and let $\mathcal{P}_{j}$ denote the price of contract $j$ (USD/share). Finally, let index $j=1$ denote the `put` contract, $j=2$ denote the `call` contract; for a straddle $K_{1} = K_{2}\equiv{K}$ (both legs have the same strike). The profit for a single straddle contract $\hat{P}$ at expiration is given by:

$$\hat{P} = \theta\cdot\left(P_{1}+P_{2}\right)$$

where $\theta_{1}=\theta_{2}\equiv\theta$ denotes a direction parameter: $\theta=-1$ if each leg is sold (short), $\theta=1$ otherwise. After substitution of the profit functions for a `put` and a `call` contract, the overall profit $\hat{P}$ is given by:

$$\hat{P} = \theta\cdot\Bigl[(K-S)^{+}+(S-K)^{+}-(\mathcal{P}_{1}+\mathcal{P}_{2})\Bigr]$$

where $V_{p} = (K-S)^{+}=\max(K-S,0)$ is the payoff function for the `put` contract, and $V_{c} = (S-K)^{+} = \max(S-K,0)$ is the payoff function for the `call` contract. The profit (or loss) of a straddle has three regimes given by:

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

```

Investors can initiate a straddle either for a credit or a debit, depending on whether they buy or sell both legs. This strategy has the potential for unlimited profit or loss. A [long straddle](content:references:vertical-straddles-long) is initiated for a debit and has unlimited profit potential but limited loss potential. On the other hand, a [short straddle](content:references:vertical-straddles-short) is initiated for a credit and has limited profit potential but unlimited loss potential.

(content:references:vertical-straddles-long)=
#### Long straddle
For a long straddle, we purchase (are long) both the `put` and the `call` contracts in the straddle, thus $\theta = 1$. Let's contruct the profit diagram for a long straddle for `AMD` with the parameters:

* Underlying: `AMD` has `S(0) = 117.50 USD/share`, the average implied volatility for `AMD` options with `DTE = 31 days` is `IV = 51.75%`.
* Leg 1: The strike price for the `long put` leg is given by $K_{1}$ = 120 USD/share with `DTE = 31 days`. The premium for this contract is $\mathcal{P}_{1}$ = 7.85 USD/share.
* Leg 2: The strike price for the `long call` leg is given by $K_{2}$ = 120 USD/share with `DTE = 31 days`. The premium for this contract is $\mathcal{P}_{2}$ = 6.30 USD/share.

```{figure} ./figs/Fig-AMD-long-straddle-DTE-31d.svg
---
height: 420px
name: fig-long-amd-straddle
---
Profit for a long straddle on `AMD` with `DTE = 31 days` until expiration. The strike price for both legs is $K = 120$ USD/share. The premium for the `put` leg is $\mathcal{P}_{1} = 7.85$ USD/share and the premium for the `call` leg is $\mathcal{P}_{2} = 6.30$ USD/share. 
```


(content:references:vertical-straddles-short)=
#### Short straddle
For a short straddle, we sell (are short) both the `put` and the `call` contracts in the straddle, thus $\theta = 1$. Let's contruct the profit diagram for a long straddle with the parameters:

* Underlying: `AMD` has `S(0) = 117.50 USD/share`, the average implied volatility for `AMD` options with `DTE = 31 days` is `IV = 51.75%`.
* Leg 1: The strike price for the `short put` leg is given by $K_{1}$ = 120 USD/share with `DTE = 31 days`. The premium for this contract is $\mathcal{P}_{1}$ = 7.85 USD/share.
* Leg 2: The strike price for the `short call` leg is given by $K_{2}$ = 120 USD/share with `DTE = 31 days`. The premium for this contract is $\mathcal{P}_{2}$ = 6.30 USD/share.

```{figure} ./figs/Fig-AMD-short-straddle-DTE-31d.svg
---
height: 420px
name: fig-short-amd-straddle
---
Profit for a short straddle on `AMD` with `DTE = 31 days` until expiration. The strike price for both legs is $K = 120 USD/share$. The premium for the `put` leg is $\mathcal{P}_{1} = 7.85$ USD/share, and the premium for the `call` leg is $\mathcal{P}_{2} = 6.30$ USD/share. 
```

### Strangles
A [strangle](https://www.investopedia.com/terms/s/strangle.asp) position is a _neutral strategy_ constructed by simultaneously buying and selling a put and a call option on the same underlying asset `XYZ`, with the _same expiration_ but with _different strike prices_ ({prf:ref}`defn-PL-strangle`):

```{prf:definition} Profit and loss of a strangle
:label: defn-PL-strangle
Let $K_{j}$ denote the strike price of contract $j$ (USD/share), and let $\mathcal{P}_{j}$ denote the price of contract $j$ (USD/share). Finally, let index $j=1$ denote the `put` contract, $j=2$ denote the `call` contract; for a strangle $K_{1}<K_{2}$. The profit for a single strangle contract $\hat{P}$ at expiration is given by:

$$\hat{P} = \theta\cdot\left(P_{1}+P_{2}\right)$$

where $\theta_{1}=\theta_{2}\equiv\theta$ denotes a direction parameter: $\theta=-1$ if each leg is sold (short), $\theta=1$ otherwise. After substitution of the profit functions for a `put` and a `call` contract, the overall profit $\hat{P}$ is given by:

$$\hat{P} = \theta\cdot\Bigl[(K_{1}-S)^{+}+(S-K_{2})^{+}-(\mathcal{P}_{1}+\mathcal{P}_{2})\Bigr]$$

where $V_{p} = (K_{1}-S)^{+}=\max(K_{1}-S,0)$ is the `payoff` for the `put` contract, and $V_{c} = (S-K_{2})^{+} = \max(S-K_{2},0)$ is the `payoff` for the `call` contract. The profit (or loss) of a strangle has three regimes given by:

$$
\hat{P} = \begin{cases}
  \theta\cdot\Bigl[(S-K_{2})-\left(\mathcal{P}_{1}+\mathcal{P}_{2}\right)\Bigr]  & S>K_{2} \\
  -\theta\cdot\Bigl[\mathcal{P}_{1}+\mathcal{P}_{2}\Bigr] & K_{1}\leq{S}\leq{K_{2}} \\
  \theta\cdot\Bigl[(K_{1}-S)-\left(\mathcal{P}_{1}+\mathcal{P}_{2}\right)\Bigr] & S<{K_{1}}
\end{cases}
$$

A [strangle](https://www.investopedia.com/terms/s/strangle.asp) has two break-even points $S^{+}$ and $S^{-}$ where $K_{2}<S^{+}$ and $S^{-}<K_{1}$. The low break-even point $S^{-}$ is given by:

$$S^{-} = K_{1} - \left(\mathcal{P}_{1}+\mathcal{P}_{2}\right)$$

while the high break-even point $S^{+}$ is given by:

$$S^{+} = K_{2} + \left(\mathcal{P}_{1}+\mathcal{P}_{2}\right)$$
```


Depending upon the choice of the strike prices and whether an investor buys or sells both legs, a [strangle](https://www.investopedia.com/terms/s/strangle.asp) can be initiated as a credit or debit and can potentially have undefined profit or loss.

#### Long strangle
For a long strangle, we purchase (are long) both the `put` and the `call` contracts in the straddle, thus $\theta = 1$. Opening this trade results in a `debit`, where the investor profits when the trade is closed. Let's contruct the profit diagram for a long straddle with the parameters:

* Underlying: `AMD` has `S(0) = 117.50 USD/share`, the average implied volatility for `AMD` options with `DTE = 31 days` is `IV = 51.75%`.
* Leg 1: The strike price for the `short put` leg is given by $K_{1}$ = 105 USD/share with `DTE = 31 days`. The premium for this contract is $\mathcal{P}_{1}$ = 1.95 USD/share. 
* Leg 2: The strike price for the `short call` leg is given by $K_{2}$ = 135 USD/share with `DTE = 31 days`. The premium for this contract is $\mathcal{P}_{2}$ = 2.20 USD/share.

```{figure} ./figs/Fig-AMD-long-strangle-DTE-31d.svg
---
height: 420px
name: fig-long-amd-strangle
---
Profit for a long strangle on `AMD` with `DTE = 31 days` until expiration. The strike price for the `put` leg $K_{1} = 105$ USD/share, while the strike price for the `call` leg $K_{2} = 135$ USD/share. The premium for the `put` leg is $\mathcal{P}_{1} = 1.95$ USD/share, and the premium for the `call` leg is $\mathcal{P}_{2} = 2.20$ USD/share. 
```

#### Short strangle
For a short strangle, we sell (are short) both the `put` and the `call` contracts in the straddle, thus $\theta = 1$. Let's contruct the profit diagram for a long straddle with the parameters:

* Underlying: `AMD` has `S(0) = 117.50 USD/share`, the average implied volatility for `AMD` options with `DTE = 31 days` is `IV = 51.75%`.
* Leg 1: The strike price for the `short put` leg is given by $K_{1}$ = 105 USD/share with `DTE = 31 days`. The premium for this contract is $\mathcal{P}_{1}$ = 1.95 USD/share. 
* Leg 2: The strike price for the `short call` leg is given by $K_{2}$ = 135 USD/share with `DTE = 31 days`. The premium for this contract is $\mathcal{P}_{2}$ = 2.20 USD/share.

```{figure} ./figs/Fig-AMD-short-strangle-DTE-31d.svg
---
height: 420px
name: fig-short-amd-strangle
---
Profit for a short strangle on `AMD` with `DTE = 31 days` until expiration. The strike price for the `put` leg $K_{1} = 105$ USD/share, while the strike price for the `call` leg $K_{2} = 135$ USD/share. The premium for the `put` leg is $\mathcal{P}_{1} = 1.95$ USD/share, and the premium for the `call` leg is $\mathcal{P}_{2} = 2.20$ USD/share. 
```


(content:references:vertical-butterflies-condors)=
## Butterflies and Condors
An [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) is a _neutral defined risk_ position constructed by _selling_ a put (1) and call (2) options on the underlying asset `XYZ`, while simultaneously _buying_ a put (3) and call (4) options on `XYZ`. All the legs of an [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) have the same underlying asset `XYZ`, and have the same expiration, but they have different strike prices where $K_{3}<K_{1}<K_{2}<K_{4}$. In particular, the two short options are sold with strikes on either side of the current share price $S_{o}$ of `XYZ`, with the short put strike price $K_{1}<S_{o}$ and the short call strike price $K_{2}>S_{o}$. Then, the long legs are purchased above and below the short strikes.  Thus, an [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) position has the character of a [strangle](https://www.investopedia.com/terms/s/strangle.asp) combined with a vertical spread. 

An investor holding an [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) profits if the share price of `XYZ` remains between the strike prices of the two short options (like a short strangle). However, unlike a [strangle](https://www.investopedia.com/terms/s/strangle.asp), an [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) is a defined risk strategy; the long options act to limit any possible losses, but they also restrict potential gains (because of their cost).

---

## Summary
Fill me in