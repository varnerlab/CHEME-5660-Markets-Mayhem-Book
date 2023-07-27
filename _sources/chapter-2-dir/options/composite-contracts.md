(content:references:american-options-composite-contracts)=
# Composite Contract Payoff and Profit Diagrams
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
It is important to note that the future share price of `XYZ` is unknown when the investor opens the trade. Thus, the investor is making a direction assumption when trading a vertical spread about the movement of the share price.
```

### Put vertical spreads
There are two types of vertical spreads that can be made with put contracts, each with a different directional assumption. 
* The put bullish credit spread assumes that the share price of the underlying asset, in this case, `XYZ`, will increase by the time of expiration. 
* In contrast, the put bearish debit spread assumes that the share price of `XYZ` will decrease by the time of expiration. 

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
A `bull`` put credit spread is a composite contract that combines a short put and a long put, providing the investor with a credit upon opening the trade. This strategy has a directional bias (bullish) and a defined risk, with the short put strike price $K_{1}$ being lower than the current share price $S_{\circ}$ but higher than the long put strike price $K_{2}$ (i.e. $S_{\circ}>K_{1}>K_{2}$). The long put serves to limit potential losses, but it also restricts potential gains due to its cost ({numref}`fig-put-vertical-spread-credit`).


```{figure} ./figs//Fig-put-vertical-spread-credit.svg
---
height: 420px
name: fig-put-vertical-spread-credit
---
The payoff and profit for a bull put credit spread credit on `XYZ` with 56-DTE. Parameters: $K_{1}=60.0$ USD/share, $K_{2}=50.0$ USD/share, $S_{\circ}=64.69$ USD/share, $\mathcal{P}_{1}=1.39$ USD/share, $\mathcal{P}_{2}=0.23$ USD/share, $T=56$ days, and $r=0.04$.
```

#### Debit spreads
Fill me in.

(content:references:vertical-straddles-strangles)=
## Straddles and Strangles
A [straddle](https://www.investopedia.com/terms/s/straddle.asp) is a _neutral strategy_ constructed by simultaneously buying (or selling) a put and a call option on the same underlying asset `XYZ`, with the _same expiration_, and the _same strike price_. Depending upon the choice of the strike prices and whether an investor buys or sells both legs, a [straddle](https://www.investopedia.com/terms/s/straddle.asp) can be initiated as a credit or debit and can potentially have undefined profit or loss.

Unlike directional strategies such as [Vertical spreads](content:references:vertical-spreads), a [straddle](https://www.investopedia.com/terms/s/straddle.asp) is a _neutral_ position; an investor holding a [straddle](https://www.investopedia.com/terms/s/straddle.asp) profits if the share price of `XYZ` moves up, down or potentially zero depending upon the construction of the straddle.

A [strangle](https://www.investopedia.com/terms/s/strangle.asp) position is a _neutral strategy_ constructed by simultaneously buying and selling a put and a call option on the same underlying asset `XYZ`, with the same expiration but with _different_ strike prices. Depending upon the choice of the strike prices and whether an investor buys or sells both legs, a [strangle](https://www.investopedia.com/terms/s/strangle.asp) can be initiated as a credit or debit and can potentially have undefined profit or loss. 

Unlike directional strategies such as {ref}`content:references:option-contracts-vertical-spread`, a [strangle](https://www.investopedia.com/terms/s/strangle.asp) is a _neutral_ position; an investor holding a [strangle](https://www.investopedia.com/terms/s/strangle.asp) profits if the share price of `XYZ` moves between the strike prices of the strangle.



(content:references:vertical-butterflies-condors)=
## Butterflies and Condors
An [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) is a _neutral defined risk_ position constructed by _selling_ a put (1) and call (2) options on the underlying asset `XYZ`, while simultaneously _buying_ a put (3) and call (4) options on `XYZ`. All the legs of an [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) have the same underlying asset `XYZ`, and have the same expiration, but they have different strike prices where $K_{3}<K_{1}<K_{2}<K_{4}$. In particular, the two short options are sold with strikes on either side of the current share price $S_{o}$ of `XYZ`, with the short put strike price $K_{1}<S_{o}$ and the short call strike price $K_{2}>S_{o}$. Then, the long legs are purchased above and below the short strikes.  Thus, an [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) position has the character of a [strangle](https://www.investopedia.com/terms/s/strangle.asp) combined with a vertical spread. 

An investor holding an [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) profits if the share price of `XYZ` remains between the strike prices of the two short options (like a short strangle). However, unlike a [strangle](https://www.investopedia.com/terms/s/strangle.asp), an [iron condor](https://www.investopedia.com/terms/i/ironcondor.asp) is a defined risk strategy; the long options act to limit any possible losses, but they also restrict potential gains (because of their cost).

---

## Summary
Fill me in