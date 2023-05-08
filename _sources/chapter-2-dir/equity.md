# Equity Securities

Common stocks, also known as equity securities or equities, represent ownership shares in a corporation. Each share of common stock entitles its owner to one vote on any matters of corporate governance that are put to the vote at the corporation’s annual meeting and a share in the financial benefits of ownership. The corporation is controlled by a board of directors elected by the shareholders. The board meets a few times per year and selects the management team that runs the corporation daily. Managers have the authority to make most business decisions without the board’s specific approval. The board’s mandate is to oversee the management to ensure that it acts in the best interests of shareholders.

The two most important characteristics of common stock as an investment are its residual claim and limited liability features:

* Residual claim means that stockholders are the last in line of all those who have a claim on the assets and income of the corporation. In liquidating the firm’s assets, the shareholders have a claim to what is left after all other claimants, such as the tax authorities, employees, suppliers, bondholders, and other creditors, have been paid. For a firm not in liquidation, shareholders have a claim to the part of operating income left over after interest and taxes have been paid. Management can either pay this residual as cash dividends to shareholders or reinvest it in the business to increase the value of the shares. 

* Limited liability means the most shareholders can lose in the event of the corporation’s failure is their original investment. Unlike owners of unincorporated businesses, whose creditors can lay claim to the personal assets of the owner (house, car, furniture), corporate shareholders may, at worst, have worthless stock. They are not personally liable for the firm’s obligations.


---


## Markets and Exchanges 
Marketscare _places_ (perhaps physical locations such as a retail store or virtual sites on the internet) where parties exchange (trade) goods and services. In a physical market, buyers and sellers meet face-to-face, while there is no physical contact between buyers and sellers in a virtual market. Thus, a market is any _place_ where two or more parties engage in an economic transaction, i.e., the exchange of goods, services, information, currency, or any combination that passes from one party to another.

The various financial instruments we consider, e.g., shares of stock can be purchased (or sold) on an electronic exchange (typically), with processes and procedures influencing the efficiency and price of the assets being traded. Electronic exchanges in which investors buy (or sell) securities are examples of [continuous double auctions](https://en.wikipedia.org/wiki/Double_auction). 

A [continuous double auction](https://en.wikipedia.org/wiki/Double_auction) is a process where:
* potential buyers submit bids to a market institution; bids specify the quantity and price the buyer wishes to buy the good or service. 
* potential sellers submit asks to the same market institution; asks describe the amount and price of the good or service they want to sell. 

On a modern electronic exchange, bids and asks are arriving (or being canceled), and deals are being made between parties (a seller sells and a buyer buys) continuously. Thus, a [double auction](https://en.wikipedia.org/wiki/Double_auction) must have tools and strategies to track orders coming into the market and match buyers and sellers, as well as methods to keep market transactions flowing.

### Orders, the Order Book and Matching Systems
At the center of an electronic exchange are [orders](https://en.wikipedia.org/wiki/Order_(exchange)) and [order books](https://en.wikipedia.org/wiki/Order_book). An [order book](https://en.wikipedia.org/wiki/Order_book) holds a list of [orders](https://en.wikipedia.org/wiki/Order_(exchange)) for a particular security or financial instrument listed on the exchange; thus, it is a tick-by-tick record of the interest buyers and sellers have for a particular security or financial instrument on the exchange. 

Many types of [orders](https://en.wikipedia.org/wiki/Order_(exchange)) can be initiated by traders. However, let's consider only four basic classes of orders, a market order, a limit order, a stop order and a cancel order.

#### Market orders
A market order is a buy or sell order executed immediately, regardless of the current market prices. As long as willing sellers and buyers are present in the exchange, market orders are always executed (filled). Market orders are used when the certainty of execution is more important than the execution price. Thus, a market order is the simplest of the order types as it forgoes control over the execution price. A market order is filled at the best price available at execution. In fast-moving markets, the price paid or received may differ significantly from the price quoted when the order was entered. Further, a market order may be split across multiple participants on the other side of the transaction, resulting in different prices for some of the instruments involved in the trade.   

#### Limit orders
A limit order is an order to buy a financial instrument at no more than a specific price or sell a security at no less than a particular price. This gives the trader control over the price at which the trade is executed. However, unlike a market order which is guaranteed to be executed (filled), a limit order may never be executed if the price conditions are not met. Thus, limit orders are used when the trader wishes to control price rather than the certainty of being filled.

#### Stop orders
A stop order is an order to buy or sell a financial instrument once the price of that instrument reaches a specified price, the stop price. 

* A [buy-stop order](https://en.wikipedia.org/wiki/Order_(exchange)#Buy-stop_order) is entered at a stop price above the current market price. Traders use buy-stop orders to limit a loss or protect a profit on a stock they have sold short. 

* A [sell-stop order](https://en.wikipedia.org/wiki/Order_(exchange)#Sell-stop_order) is entered at a stop price below the current market price. Traders use sell-stop orders to limit a loss or protect a profit on a stock they already own. For either a [buy-stop order](https://en.wikipedia.org/wiki/Order_(exchange)#Buy-stop_order) or a [sell-stop order](https://en.wikipedia.org/wiki/Order_(exchange)#Sell-stop_order), when the stop price is reached, the stop order becomes a market order. Thus, a stop trade will be executed if the stop price is reached, but not necessarily at or near the stop price, particularly in a fast-moving market, or if there is insufficient liquidity available relative to the size of the order. 

* A [stop-limit order](https://en.wikipedia.org/wiki/Order_(exchange)#Stop-limit_order) is an order to buy or sell a stock that combines features of a stop order and a limit order. Once the stop price is reached, a stop-limit order becomes a limit order executed at a specified price (or better). As with all limit orders, a stop-limit order doesn't get filled if the security's price never reaches the specified limit price.

#### Cancel orders
Finally, a cancel order allows an investor to remove a current order from the exchange. If an order
has not already executed, it can be cancelled at any time. Moreover, if a limit order has not executed by the end of the trading day (or some specified time period) it is automatically cancelled. 

### Order Books and Matching Algorithms
An [order book](https://en.wikipedia.org/wiki/Order_book) holds a list of [orders](https://en.wikipedia.org/wiki/Order_(exchange)) for a particular security or financial instrument listed on the exchange. Order book data gives insight into the direction of price movement and the market sentiment of an asset. For example, if the number of sell orders is much larger than the number of buy orders, you expect a price decrease (negative sentiment). 

Order book data is available for viewing and electronically, for equity and derivative securities. For example, the [Chicago Board Options Exchange (CBOE)](https://www.cboe.com) has a free order-book viewer  ({numref}`example-cboe-order-book-data`).


```{figure} ./figs/Fig-CBOE-OrderBook-QQQ-9-8-22.png
---
height: 380px
name: example-cboe-order-book-data
---
Snapshot for the [QQQ](https://www.google.com/finance/quote/QQQ:NASDAQ?sa=X&ved=2ahUKEwjoqKOL0oX6AhUrkIkEHbrKBaMQ3ecFegQIFxAg) order book taken from the [Chicago Board Options Exchange (CBOE)](https://www.cboe.com). The ``top`` of the order book is shown on the left, while the last ten trades are shown on the right. The total volume (the number of share exchanged, bought or sold) and the number of orders accepted (number of matched orders) is also shown. __source__: [CBOE Book Viewer](https://www.cboe.com/us/equities/market_statistics/book_viewer/).
```

Financial data providers such as [Polygon.io](https://polygon.io) have [RESTful Application Programming Interface (APIs)](https://polygon.io/docs/stocks/getting-started) that enable programmatic access to market data of all sorts, including data about the buy and sell orders in the [order book](https://en.wikipedia.org/wiki/Order_book) for equities and derivatives, with a nanosecond resolution.

#### Bid/Ask Spread
Fill me in.

#### Order Matching
An [order matching system](https://en.wikipedia.org/wiki/Order_matching_system) matches buy and sell orders held in the [order books](https://www.investopedia.com/terms/o/order-book.asp) of an electronic exchange. [Order books](https://www.investopedia.com/terms/o/order-book.asp) are a data structure that organizes the orders that exchange can accept and allows matching to occur; [order books](https://www.investopedia.com/terms/o/order-book.asp) are essentially electronic lists of buy and sell orders for a specific security or financial instrument organized by price level. 

[Order matching algorithms](https://en.wikipedia.org/wiki/Order_matching_system) find matches between buyers and sellers by analyzing the data stored in the [order books](https://www.investopedia.com/terms/o/order-book.asp). The matching algorithms used on electronic exchanges are essential components that significantly impact efficiency, [liquidity](https://en.wikipedia.org/wiki/Market_liquidity) and prices of the instruments being traded in the market. There are a variety of algorithms for order matching. The Pro-Rata and Price/Time matching algorithms are the most common. 

(content:references:price-time-algo)=
##### Price/Time matching algorithm
The price-time algorithm, also known as the First-in-First-Out (FIFO) algorithm, is the most straightforward order book matching algorithm. In the price-time algorithm, the order matching priority is price and then time. For example, buy orders with higher prices are automatically prioritized over buy orders at lower prices.
However, buy orders arriving in the order book with the same maximum price are prioritized based on the bid time, where priority is given to the first buy order. 

````{prf:example} Price/Time mathching
For example, a buy order for 300 shares of a security at $50 per share is followed by another buy order of 100 shares of the same security at a similar price. 

According to the FIFO algorithm, the total 300 shares buy order will be matched to sell orders. There can be more than one sell order. After the 300 shares buy order is matched, the 100 shares buy order matching will start.
````

(content:references:pro-rata-algo)=
##### Pro-Rata matching algorithm
A system using the Pro-Rata algorithm also gives priority to the highest-priced buy order. However, buy orders with the same highest price are matched in proportion to each order size.

````{prf:example} Pro-Rata mathching
For example, buy orders of 300 shares and 100 shares of the same security are active in the system. At the same time, a compatible sell order of 300 shares becomes active. The sell order will not be able to fulfill both the buy orders.

The Pro-Rata algorithm will match 225 shares to the 300-share buy order and 75 shares to the 100-share buy order. Hence, both buy orders are partially filled. Here, the Pro-Rata algorithm fills 75% of both buy orders.
````

### Order Routing and Market Makers
In a classical face-to-face auction, the identity of the buyer and seller, or at least their representatives, is typically known. However, determining who the buyers and sellers are on an electronic exchange is impossible; you will (likely) never _know_ your counterparty. Instead, 
[Core](https://www.investopedia.com/terms/c/coreliquidityprovider.asp) and [supplemental liquidity providers](https://www.investopedia.com/terms/s/supplemental-liquidity-provider.asp), also called market makers, facilitate securities trading by providing a pool of shares, (which they own), so that buyers and sellers trade without having to locate and deal with each other individually. 

## Returns and Stylized Facts 
A return refers to the increase or decrease in the price of a stock over a specific period. Studying returns is crucial for understanding the performance of financial assets such as stocks, bonds, and commodities. 

Returns can be defined as the Logarithmic return ({prf:ref}`defn-log-return-1`):

````{prf:definition} Logarithmic return
:label: defn-log-return-1

Let the price of asset $i$ at any time $j$ be gievm by $P_{ij}>0$. Then the logarithmic return 
on asset $i$ over time horizon $j\rightarrow{k},j\neq{k}$ is defined as: 

```{math}
\bar{r}_{i,j\rightarrow{k}} \equiv \log\left(\frac{P_{ij}}{P_{ik}}\right)
```

where $\bar{r}_{i,j\rightarrow{k}}$ denotes the logarithmic return of asset $i$ over time horizon $j\rightarrow{k},i\neq{k}$. The $\log\left(\star\right)$ term denotes the [natural log](https://en.wikipedia.org/wiki/Natural_logarithm). 

````

or the fractional return ({prf:ref}`defn-percentage-return-1`):

````{prf:definition} Fractional return
:label: defn-percentage-return-1

Let the price of asset $i$ at any time $j$ be given by $P_{ij}>0$. Then the fractional return 
on asset $i$ over time horizon $j\rightarrow{k},j\neq{k}$ is defined as: 

```{math}
r_{i,j\rightarrow{k}} \equiv \frac{P_{ik} - P_{ij}}{P_{ij}}
```

where $r_{i,j\rightarrow{k}}$ denotes the fractional return of asset $i$ over time horizon $j\rightarrow{k},i\neq{k}$.

````

Stylized facts, on the other hand, are empirical observations about the return found to hold across different assets, e.g., stocks and time periods. They are essential for developing and testing economic and financial theories and models. By examining returns and stylized facts, analysts and investors can gain insights into market behavior, risk, and investment opportunities. Several stylized facts have been identified to characterize stock price returns:

* [Volatility clustering](https://en.wikipedia.org/wiki/Volatility_clustering): Stock prices tend to be more volatile during specific periods and less volatile during others. This phenomenon is known as volatility clustering, suggesting that large price movements are more likely to be followed by significant moves in the same direction.
* [Fat tails](https://en.wikipedia.org/wiki/Fat-tailed_distribution): Stock price returns often exhibit a distribution with fatter tails than would be expected under a normal distribution. This means that extreme price movements are more likely than would be predicted by a normal distribution.
* [Mean reversion](https://en.wikipedia.org/wiki/Mean_reversion_(finance)): Over the long run, stock prices tend to revert to their historical mean. This means that if a stock has experienced a period of high returns, it is likely to experience lower returns in the future, and vice versa.
* [Leverage effect](https://en.wikipedia.org/wiki/Leverage_(finance)): There is a negative relationship between stock returns and volatility. When stock prices fall, volatility tends to increase, exacerbating the decline in stock prices.
* [Autocorrelation](https://en.wikipedia.org/wiki/Autocorrelation):  Autocorrelation refers to the tendency of stock price returns to correlate with their past returns over time. This suggests some predictability in stock price returns, which can be exploited by traders and investors. However, autocorrelation is not universal and may not apply to all stocks or periods.
---

# Summary
Fill me in.