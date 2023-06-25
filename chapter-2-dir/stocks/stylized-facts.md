# Markets and Stylized Facts

---

```{topic} Outline
In this lecture, we'll introduce equity securities, discuss the different types of orders that can be used to buy or sell equity securities and explore the statistical properties of equity security data.

In this lecture, we'll introduce equity securities, discuss the different types of orders that can be used to buy or sell equity securities, introduce some components of market microstructure such as the order book and order matching, and finally explore the statistical properties of equity prices.

* {ref}`content:references:markets-exchanges` play a crucial role in contemporary economies as they enable the trade of goods, services, and financial instruments like stocks and bonds. A market is a platform where buyers and sellers convene to exchange commodities or services, while an exchange is a market that specializes in financial instruments and has specific trade regulations.

* {ref}`content:orders-order-book-matching`. Traders give instructions to buy or sell financial instruments at a specified price, known as orders. These orders are recorded in the order book, which shows all outstanding buy and sell orders for a specific financial instrument on the exchange. The exchange matches buy and sell orders based on price and other criteria through the process of order matching, which results in trades being executed. The order book provides transparency into market depth and liquidity.

* {ref}`content:references:returns-stylized-facts`. Investment returns are a vital indicator of an investment’s value change over time. Returns play a crucial role in evaluating investment performance. Stylized facts are recognizable patterns or empirical regularities observed in financial markets and investment returns. For instance, stock returns tend to be positively correlated with economic growth. Familiarity with these patterns can assist investors in making informed decisions and creating more effective investment strategies.

```

---

(content:references:markets-exchanges)=
## Markets
Markets are physical or virtual locations where parties exchange goods and services. In a physical market, buyers and sellers interact face-to-face, while a virtual market does not require physical contact. Any place where two or more parties engage in an economic transaction, such as the exchange of goods, services, information, or currency, is considered a market.

Financial instruments, like shares of stock, can be purchased or sold on electronic exchanges. Potential buyers submit `bids` specifying the quantity and price they wish to purchase the good or service, and potential sellers submit `asks` describing the amount and price at which they want to sell. These `bids` and `asks` are continuously arriving or being canceled, and deals are being made between parties continuously. Therefore, a double auction must have strategies and tools to track orders and match buyers and sellers and methods to keep market transactions flowing smoothly.

(content:orders-order-book-matching)=
## Orders, Order Books and Order Matching
At the center of an electronic exchange are [orders](https://en.wikipedia.org/wiki/Order_(exchange)) and [order books](https://en.wikipedia.org/wiki/Order_book). An [order book](https://en.wikipedia.org/wiki/Order_book) holds a list of [orders](https://en.wikipedia.org/wiki/Order_(exchange)) for a particular security or financial instrument listed on the exchange; thus, it is a tick-by-tick record of the interest buyers and sellers have for a particular security or financial instrument on the exchange. 

Many types of [orders](https://en.wikipedia.org/wiki/Order_(exchange)) can be initiated by traders. However, let's consider only four basic classes of orders, a market order, a limit order, a stop order and a cancel order.

* __Market order__: A market order is a buy or sell order executed immediately, regardless of the current market prices. As long as willing sellers and buyers are present in the exchange, market orders are always executed (filled). Market orders are used when the certainty of execution is more important than the execution price. Thus, a market order is the simplest of the order types as it forgoes control over the execution price. A market order is filled at the best price available at execution. In fast-moving markets, the price paid or received may differ significantly from the price quoted when the order was entered. Further, a market order may be split across multiple participants on the other side of the transaction, resulting in different prices for some of the instruments involved in the trade.   

* __Limit order__: A limit order is an order to buy a financial instrument at no more than a specific price or sell a security at no less than a particular price. This gives the trader control over the price at which the trade is executed. However, unlike a market order which is guaranteed to be executed (filled), a limit order may never be executed if the price conditions are not met. Thus, limit orders are used when the trader wishes to control price rather than the certainty of being filled.

* __Stop order__: A stop order is an order to buy or sell a financial instrument once the price of that instrument reaches a specified price, the stop price:

    * A [buy-stop order](https://en.wikipedia.org/wiki/Order_(exchange)#Buy-stop_order) is entered at a stop price above the current market price. Traders use buy-stop orders to limit a loss or protect a profit on a stock they have sold short. 
    * A [sell-stop order](https://en.wikipedia.org/wiki/Order_(exchange)#Sell-stop_order) is entered at a stop price below the current market price. Traders use sell-stop orders to limit a loss or protect a profit on a stock they already own. For either a [buy-stop order](https://en.wikipedia.org/wiki/Order_(exchange)#Buy-stop_order) or a [sell-stop order](https://en.wikipedia.org/wiki/Order_(exchange)#Sell-stop_order), when the stop price is reached, the stop order becomes a market order. Thus, a stop trade will be executed if the stop price is reached, but not necessarily at or near the stop price, particularly in a fast-moving market, or if there is insufficient liquidity available relative to the size of the order. 
    * A [stop-limit order](https://en.wikipedia.org/wiki/Order_(exchange)#Stop-limit_order) is an order to buy or sell a stock that combines features of a stop order and a limit order. Once the stop price is reached, a stop-limit order becomes a limit order executed at a specified price (or better). As with all limit orders, a stop-limit order doesn't get filled if the security's price never reaches the specified limit price.

* __Cancel order__: A cancel order allows an investor to remove a current order from the exchange. If an order
has not already executed, it can be cancelled at any time. Moreover, if a limit order has not executed by the end of the trading day (or some specified time period) it is automatically cancelled. 

(content:references:returns-stylized-facts)=
## Returns and Stylized Facts 
A return refers to the increase or decrease in the price of an asset, e.g., shares of a stock over a specific time period period, e.g., minutes, days, weeks or even years. Studying returns is crucial for understanding the performance of financial assets such as stocks, bonds, and commodities ({prf:ref}`defn-log-return-1`):

````{prf:definition} Logarithmic return
:label: defn-log-return-1

Let the price of asset $i$ at time $j$ be gievm by $P_{ij}>0$. Then the logarithmic return 
on asset $i$ over time horizon $j\rightarrow{k},j\neq{k}$ is defined as: 

```{math}
\bar{r}_{i,j\rightarrow{k}} \equiv \log\left(\frac{P_{ij}}{P_{ik}}\right)
```

where $\bar{r}_{i,j\rightarrow{k}}$ denotes the logarithmic return of asset $i$ over time horizon $j\rightarrow{k},i\neq{k}$. The $\log\left(\star\right)$ term denotes the [natural log](https://en.wikipedia.org/wiki/Natural_logarithm). 

````

Returns can also be described as the fractional change in price ({prf:ref}`defn-percentage-return-1`):

````{prf:definition} Fractional return
:label: defn-percentage-return-1

Let the price of asset $i$ at any time $j$ be given by $P_{ij}>0$. Then the fractional return 
on asset $i$ over time horizon $j\rightarrow{k},j\neq{k}$ is defined as: 

```{math}
r_{i,j\rightarrow{k}} \equiv \frac{P_{ik} - P_{ij}}{P_{ij}}
```

where $r_{i,j\rightarrow{k}}$ denotes the fractional return of asset $i$ over time horizon $j\rightarrow{k},i\neq{k}$.

````

Data on stock prices are sourced from platforms like [Polygon.io](https://polygon.io), where datasets are compiled with aggregated Open High Low Close (OHLC) values. The Open price is the share price at the beginning of a specific time frame, while the Close price indicates the share price at the end of that time frame. The High and Low prices indicate the highest and lowest values for that time period, respectively. In addition, these datasets usually include information on the number of shares traded, the number of transactions, and the volume-weighted average price (vwap).

Consider the time-series for the daily rerturn of the share price of [Advanced Micro Devices](https://en.wikipedia.org/wiki/AMD) computed over a four year window ({prf:ref}`example-amd-daily-returns`):

````{prf:example} Daily logarithmic AMD returns
:label: example-amd-daily-returns
:class: dropdown

The daily logarithmic return time series for [Advanced Micro Devices](https://en.wikipedia.org/wiki/AMD) with ticker `AMD` is shown in {numref}`example-AMD-return-data-daily`:

```{figure} ./figs/Fig-AMD-Daily-Return-4yr.pdf
---
height: 380px
name: example-AMD-return-data-daily
---
Daily logarithmic return of [Advanced Micro Devices](https://en.wikipedia.org/wiki/AMD) computed from `2018-11-28` to `2022-11-28`. data was downloaded using the `aggregate` endpoint from [Polygon.io](https://polygon.io).
```

The logarithmic return was computed using the `logR` function:

```julia
"""
    logR(data::DataFrame; r::Float64 = 0.045) -> Array{Float64,1}

Computes the log excess return for firm i from the 
Open High Low Close (OHLC) DataFrame.

See: https://dataframes.juliadata.org/stable/man/getting_started/
"""
function logR(data::DataFrame; 
    r::Float64 = 0.045, key::Symbol=:close)::Array{Float64,1}

    # initialize -
    number_trading_days = nrow(data);
    log_excess_return_array = Array{Float64,1}(undef, number_trading_days - 1)
    r̄ = (1+r)^(1/365) - 1; # convert the annual risk free rate to daily value
    
    # main loop - compute the excess returns, store them in an array
    for i ∈ 2:number_trading_days
        
        # grab yesterday's and today's close price
        P₁ = data[i-1, key]; # yesterday
        P₂ = data[i, key];   # today

        # compute the excess return -
        log_excess_return_array[i-1] = log(P₂/P₁) - r̄
    end

    # return -
    return log_excess_return_array;
end
```
````

---

## Summary
In this lecture, we introduced equity securities, discussed the different types of orders that can be used to buy or sell equity securities, introduced some components of market microstructure such as the order book and order matching, and finally explored the statistical properties of equity prices.

* {ref}`content:references:markets-exchanges` play a crucial role in contemporary economies as they enable the trade of goods, services, and financial instruments like stocks and bonds. A market is a platform where buyers and sellers convene to exchange commodities or services, while an exchange is a market that specializes in financial instruments and has specific trade regulations.

* {ref}`content:orders-order-book-matching`. Traders give instructions to buy or sell financial instruments at a specified price, known as orders. These orders are recorded in the order book, which shows all outstanding buy and sell orders for a specific financial instrument on the exchange. The exchange matches buy and sell orders based on price and other criteria through the process of order matching, which results in trades being executed. The order book provides transparency into market depth and liquidity.

* {ref}`content:references:returns-stylized-facts`. Investment returns are a vital indicator of an investment’s value change over time. Returns play a crucial role in evaluating investment performance. Stylized facts are recognizable patterns or empirical regularities observed in financial markets and investment returns. For instance, stock returns tend to be positively correlated with economic growth. Familiarity with these patterns can assist investors in making informed decisions and creating more effective investment strategies.