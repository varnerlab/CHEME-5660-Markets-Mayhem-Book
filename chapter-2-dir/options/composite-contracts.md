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
Fill me in.

(content:references:vertical-spreads)=
## Vertical Spreads
[Vertical spreads](https://www.investopedia.com/terms/v/verticalspread.asp) are a _defined risk directional strategy_ constructed by simultaneously buying (long) and selling (short) the _same type of option_, with the same expiration date but with _different_ strike prices. Thus, [vertical spreads](https://www.investopedia.com/terms/v/verticalspread.asp) have two _legs_: a long leg (the option purchased by the investor) and a short leg (the option sold by the investor). [Vertical spreads](https://www.investopedia.com/terms/v/verticalspread.asp) are a defined risk, directional strategy, i.e., the investor believes the share price of the underlying asset `XYZ` will either increase or decrease, depending upon the type of vertical spread. [Vertical spreads](https://www.investopedia.com/terms/v/verticalspread.asp) are defined risk because the maximum possible gain (or loss) is known when the contract is sold; thus, an investor knows how much they can make or lose at expiration _before_ they enter the trade. However, the future share price of `XYZ` is unknown when the investor opens the trade. 

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