# Derivatives
There are two types of options contracts, a [call contract](https://www.investopedia.com/terms/c/calloption.asp) and a [put contract](https://www.investopedia.com/terms/p/putoption.asp), and two different styles of contracts that we'll consider American and European style contracts. A CALL contract gives the 
buyer the right but not the obligation to purchase 100 shares (per contract) of an underlying stock, `XYZ`, at a price per share called the strike price of $K$. On the other hand, a PUT contract gives the buyer the right but not the obligation to sell 100 shares (per contract) of an underlying stock, `XYZ`, at a strike price of $K$ per share. 

In European-style contracts, the transaction codified in CALL or PUT options can only occur at some fixed date in the future called the expiration date, which is agreed upon when the contract is purchased. However, American contract styles have a different policy; American contracts can be exercised (the buyer can initiate the transaction) at any time between when the contract was purchased and the expiration date.

## Cox-Ross-Rubinstein (CRR) binomial pricing model

The binomial options pricing model provides a generalizable numerical method for the valuation of American style call and put options contacts. The model uses a discrete-time lattice model of the varying price over time of the underlying financial instrument. The binomial model was first proposed by William Sharpe in the 1978 edition of Investments and formalized by Cox, Ross and Rubinstein {cite}`COX1979229`.

```{image} ./figs/CRR-BinomialModel.pdf
:alt: CRR-Schematic
:width: 480px
:align: center
```