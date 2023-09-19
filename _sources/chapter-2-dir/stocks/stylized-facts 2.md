---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Julia
  language: julia
  name: julia-1.9
---

(content:references:markets-exchanges-stylized-facts)=
# Equities, Markets, and Stylized Facts

```{topic} Outline
In this lecture, we'll introduce equity securities, discuss the different types of orders that can be used to buy or sell equity securities, introduce some components of market microstructure such as the order book and order matching, and finally explore the statistical properties of equity prices.

* {ref}`content:references:markets-exchanges` play a crucial role in contemporary economies as they enable the trade of goods, services, and financial instruments like stocks and bonds. A market is a platform where buyers and sellers convene to exchange commodities or services, while an exchange is a market that specializes in financial instruments and has specific trade regulations.

* {ref}`content:orders-order-book-matching`. Traders give instructions to buy or sell financial instruments at a specified price, known as orders. These orders are recorded in the order book, which shows all outstanding buy and sell orders for a specific financial instrument on the exchange. The exchange matches buy and sell orders based on price and other criteria through the process of order matching, which results in trades being executed. The order book provides transparency into market depth and liquidity.

* [Stylized facts are identifiable trends or recurring patterns](content:references:returns-stylized-facts) seen in investment returns and financial markets. One example is that stock price returns typically display minimal autocorrelation and a leptokurtic distribution, signifying a higher peak and fatter tails than a normal distribution. Familiarity with these patterns can aid investors in making well-informed choices and developing more successful investment strategies.

```

---

## Introduction
Equity securities, or just `equity` or `stock`, represent ownership in a company and entitle shareholders to assets and earnings. They are bought and sold on stock exchanges.

**Key Characteristics of Equity Securities:**

1. **Ownership Stake:** When an investor buys equity securities, they acquire a proportional ownership stake in the company based on the number of shares relative to the total outstanding shares.

2. **Dividends:** Shareholders may receive dividends, which are a portion of profits distributed periodically by the board of directors based on company performance.

3. **Capital Appreciation:** Equity securities offer the potential for capital appreciation, allowing shareholders to profit by selling their shares at a higher price than they initially paid.

4. **Voting Rights:** Shareholders of equity securities may vote on company decisions including board member elections and major corporate actions.

5. **Risk and Returns:** Investing in equity securities involves risk. If the company's performance deteriorates, the value of its shares can decrease, leading to potential financial losses for shareholders. On the other hand, successful companies can provide substantial returns to shareholders.

6. **Market Traded:** Equity securities are traded on stock exchanges, making them relatively _liquid_ compared to other investments. Investors can buy and sell these securities during trading hours (and sometimes after hours), enabling them to enter or exit their positions quickly.

**Types of Equity Securities:**

1. **Common Stock:** This is the most prevalent type of equity security. Common stockholders have voting rights and may receive dividends, although dividends are not guaranteed.

2. **Preferred Stock:** Preferred stockholders have a higher claim on company assets and dividends than common stockholders. They often receive dividends before common stockholders and may have certain privileges but usually have limited or no voting rights.

3. **Convertible Securities:** These are securities, often bonds or preferred stock, that can be converted into common stock at a predetermined price and within a specified timeframe.

Equity securities are essential for corporate financing and investment. They allow companies to raise capital from the public, while investors can participate in growth and profitability. However, It is important for investors to understand the risks and potential rewards of equity securities before investing.

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
Stylized facts are empirical statistical properties of the return time series {cite}`Cont-QuantFinance-2001`. A return refers to the increase or decrease in the price of an asset, e.g., shares of a stock over a specific time period period, e.g., minutes, days, weeks or even years ({prf:ref}`defn-log-return-1`):

````{prf:definition} Logarithmic return
:label: defn-log-return-1

Let the price of asset $i$ at time $j$ be given by $P_{ij}>0$. Then the logarithmic return 
on asset $i$ over time horizon $j\rightarrow{k}$ is defined as: 

```{math}
\bar{r}^{(i)}_{k,j} \equiv \log\left(\frac{P_{ik}}{P_{ij}}\right)
```

where $\bar{r}^{(i)}_{k,j}$ denotes the logarithmic return of asset $i$ over time horizon $j\rightarrow{k}$. The $\log\left(\star\right)$ term denotes the [natural log](https://en.wikipedia.org/wiki/Natural_logarithm). 

````

The logarithmic return can be computed using the `logR` function. The equity price data, passed into the function in the `data::DataFrame` argument, is assumed to an [ascending OHLC dataset](https://en.wikipedia.org/wiki/Open-high-low-close_chart). The `logR` function is defined in the following code block:


```{code-block} julia
:caption: The `logR` function
:linenos:


"""
    logR(data::DataFrame; r::Float64 = 0.045) -> Array{Float64,1}

Computes the log excess return for firm i from the 
Open High Low Close (OHLC) DataFrame.

See: https://dataframes.juliadata.org/stable/man/getting_started/
"""
function logR(data::DataFrame; r::Float64 = 0.045, key::Symbol=:close)::Array{Float64,1}

    # convert risk free rate to daily rate -
    r̄ = (1+r)^(1/365) - 1; # convert the annual risk free rate to daily value

    # initialize -
    number_trading_days = nrow(data);
    log_excess_return_array = Array{Float64,1}(undef, number_trading_days - 1)
    
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

Returns can also be described as the fractional change in price between two time periods ({prf:ref}`defn-percentage-return-1`):

````{prf:definition} Fractional return
:label: defn-percentage-return-1

Let the price of asset $i$ at any time $j$ be given by $P_{ij}>0$. Then the fractional return 
on asset $i$ over time horizon $j\rightarrow{k}$ is defined as: 

```{math}
r^{(i)}_{k,j} \equiv \frac{P_{ik} - P_{ij}}{P_{ij}}
```

where $r^{(i)}_{k,j}$ denotes the fractional return of asset $i$ over time horizon $j\rightarrow{k}$.
````

However, we will typically use the logarithmic return in this book. The logarithmic return is preferred because it is additive, i.e., the logarithmic return over a time period is the sum of the logarithmic returns over sub-periods. This is not true for the fractional return.

By examining returns and stylized facts, analysts and investors gain insights into market behavior, risk, and investment opportunities. While several stylized facts have been developed, let's consider the following important examples:

* [Absence of Autocorrelation](https://en.wikipedia.org/wiki/Autocorrelation):  Autocorrelation refers to the tendency of stock price returns to correlate with their past returns over time. This suggests some predictability in stock price returns, which traders and investors can exploit. A random walk will not be correlated with itself.
* [Volatility clustering](https://en.wikipedia.org/wiki/Volatility_clustering): Stock prices tend to be more volatile during specific periods and less volatile during others. This phenomenon is known as volatility clustering, suggesting that large price movements are more likely to be followed by significant moves in the same direction.
* [Heavy (also called fat) tails](https://en.wikipedia.org/wiki/Fat-tailed_distribution): Stock price returns often exhibit a distribution with fatter tails than would be expected under a normal distribution. This means that extreme price movements are more likely than would be predicted by a normal distribution.

Let's compute the stylized facts for the daily returns of [Wells Fargo & Company](https://en.wikipedia.org/wiki/Wells_Fargo) with ticker `WFC`. The daily logarithmic return time series for [Wells Fargo & Company](https://en.wikipedia.org/wiki/Wells_Fargo) is shown in {numref}`example-WFC-return-data-daily`:

```{figure} ./figs/Fig-WFC-Daily-Return-4yr.svg
---
height: 420px
name: example-WFC-return-data-daily
---
Daily logarithmic return of [Wells Fargo & Company](https://en.wikipedia.org/wiki/Wells_Fargo) computed from `2018-11-28` to `2022-11-28` using the `logR` function. Data was downloaded using the `aggregate` endpoint of [Polygon.io](https://polygon.io/docs/stocks/get_v2_aggs_ticker__stocksticker__range__multiplier___timespan___from___to).
```

To calculate Autocorrelation, Volatility clustering, and the return distribution, we utilize the [Statistics.jl](https://docs.julialang.org/en/v1/stdlib/Statistics/) and [Distributions.jl](https://github.com/JuliaStats/Distributions.jl) packages. For data visualization, we rely on the [Plots.jl](https://docs.juliaplots.org/stable/) and [StatsPlots.jl](https://github.com/JuliaPlots/StatsPlots.jl) packages.

### Autocorrelation
Autocorrelation is the correlation of a signal time series $X_{t}$ with a delayed copy of itself $X_{t+\tau}$ as the function of a delay parameter $\tau$:

```{math}
R_{XX}(\tau) = \mathbb{E}\left(X_{t+\tau}{X_{t}}\right)
```

where $\mathbb{E}(\star)$ denotes the expectation operator and $X_{t+\tau}$ is the time series delayed by $\tau$ time steps. In this case, we are interested in a particular signal vector, namely the logarithmic return time series $\bar{r}_{i,j\rightarrow{k}}$ computing using {prf:ref}`defn-log-return-1` and shown in {numref}`example-WFC-return-data-daily`.

```{code-block} julia
:caption: Script for computing the autocorrelation series
:linenos:

# Load the required packages -
using Statistics
using CSV
using DataFrames

# load the data -
data = CSV.read(path-to-csv-file, DataFrame);

# compute the return time series -
R = logR(data, key = :close);

# compute the autocorrelation -
L = length(R);
τ  = range(0,step=1,stop=(L-1));
AC = autocor(R, τ); # function provided by the Statistics package
```

The autocorrelation as a function of the lag parameter $\tau$ for `WFC` computed using the `autocorrelation script` can be visualized using the [Plots.jl](https://docs.juliaplots.org/stable/) package ({numref}`example-WFC-autocor-return-data-daily`):

```{figure} ./figs/Fig-WFC-Daily-Return-4yr-Autocorrelation.svg
---
height: 420px
name: example-WFC-autocor-return-data-daily
---
Autocorrelation as a function of lag $\tau$ (days) for logarithmic return of [Wells Fargo & Company](https://en.wikipedia.org/wiki/Wells_Fargo) computed from `2018-11-28` to `2022-11-28`. Data was downloaded using the `aggregate` endpoint of [Polygon.io](https://polygon.io/docs/stocks/get_v2_aggs_ticker__stocksticker__range__multiplier___timespan___from___to).
```


The autocorrelation of the `WFC` return displays a common [random walk pattern](https://en.wikipedia.org/wiki/Random_walk_hypothesis), where the correlation is negligible for all lags $\tau>0$. Hence, a future return is independent of the current return, making it impossible to predict future returns based on past returns. 

### Volatility clustering
Through analysis of various asset prices, Mandelbrot {cite}`Mandelbrot-1963, Mandelbrot-1967` discovered that significant changes in price are usually followed by other significant changes, regardless of whether they are positive or negative. Conversely, small changes are typically followed by small changes. 

```{figure} ./figs/Fig-WFC-Daily-Return-4yr-abs-Autocorrelation.svg
---
height: 420px
name: example-WFC-autocor-abs-return-data-daily
---
Autocorrelation as a function of lag $\tau$ (days) for the absolute value of logarithmic return of [Wells Fargo & Company](https://en.wikipedia.org/wiki/Wells_Fargo) computed from `2018-11-28` to `2022-11-28`. Data was downloaded using the `aggregate` endpoint of [Polygon.io](https://polygon.io/docs/stocks/get_v2_aggs_ticker__stocksticker__range__multiplier___timespan___from___to).
```

While we have shown that returns themselves are uncorrelated in time, the absolute value of returns $|\bar{r}_{i,j\rightarrow{k}}|$ or their squares $\bar{r}^{2}_{i,j\rightarrow{k}}$ demonstrate a positive and gradually decreasing absolute autocorrelation $\bar{R}_{XX}(\tau)$ as a function of the lag parameter $\tau$:

```{math}
\bar{R}_{XX}(\tau) = \mathbb{E}\left(|X_{t+\tau}||{X_{t}}|\right)
```


This phenomenon, commonly referred to as [volatility clustering](https://en.wikipedia.org/wiki/Volatility_clustering), is present in the `WFC` return series ({numref}`example-WFC-autocor-abs-return-data-daily`). Thus, large returns of `WFC` are more likely to be followed by large returns, and small returns followed by small returns, i.e., the volatility of the `WFC` return is clustered in the time series. You can see evidence of this in the `WFC` return data series shown in {numref}`example-WFC-return-data-daily`, as the the spikes in the return time series are clustered in time.

The existence of [volatility clustering](https://en.wikipedia.org/wiki/Volatility_clustering) has inspired a family of advanced mathematical models of financial time series, known as [stochastic volatility models](https://en.wikipedia.org/wiki/Stochastic_volatility). These models are based on the assumption that the volatility of the underlying asset is not constant, but varies over time.

```{code-block} julia
:caption: Script for computing the absolute autocorrelation series
:linenos:

# Load the required packages -
using Statistics
using CSV
using DataFrames

# load the data -
data = CSV.read(path-to-csv-file, DataFrame);

# compute the return time series
R = logR(data, key = :close);

# compute the autocorrelation -
L = length(R);
τ  = range(0,step=1,stop=(L-1));
AC = autocor(abs.(R), τ); # function provided by the Statistics package
```

### Return distribution
The daily return values for `WFC` show another typical pattern, namely a [fat- or hearvy-tailed distribution](https://en.wikipedia.org/wiki/Fat-tailed_distribution). The daily return values for `WFC` were calculated using the `logR` function. A [Normal](https://juliastats.org/Distributions.jl/stable/univariate/#Distributions.Normal) and [Laplace](https://juliastats.org/Distributions.jl/stable/univariate/#Distributions.Laplace) distribution was then fit to the return data using the [maximum likelihood estimation (MLE)](https://en.wikipedia.org/wiki/Maximum_likelihood_estimation#:~:text=In%20statistics%2C%20maximum%20likelihood%20estimation,observed%20data%20is%20most%20probable.) routine encoded in the [Distributions.jl](https://github.com/JuliaStats/Distributions.jl) package. 


```{figure} ./figs/Fig-WFC-Daily-Return-4yr-histogram.svg
---
height: 420px
name: example-WFC-return-histogram-data-daily
---
Return distribution for logarithmic daily return of [Wells Fargo & Company](https://en.wikipedia.org/wiki/Wells_Fargo) computed between `2018-11-28` to `2022-11-28`. Data was downloaded using the `aggregate` endpoint of [Polygon.io](https://polygon.io/docs/stocks/get_v2_aggs_ticker__stocksticker__range__multiplier___timespan___from___to).
```

The distribution of daily returns, visualized using the [StatsPlots.jl](https://github.com/JuliaPlots/StatsPlots.jl) package, has decreasing density around the mean and thicker tails compared to a [Normal](https://juliastats.org/Distributions.jl/stable/univariate/#Distributions.Normal) distribution ({numref}`example-WFC-return-histogram-data-daily`). Thus, the daily returns for `WFC` appear to not follow a [Normal](https://juliastats.org/Distributions.jl/stable/univariate/#Distributions.Normal) distribution. Instead, the returns appear to better described by a [Laplace](https://juliastats.org/Distributions.jl/stable/univariate/#Distributions.Laplace) distribution, which has thicker tails and less density around the mean. 

To determine if a dataset is normally distributed, there are several techniques that can be used. We consider three possible methods: [Q-Q plots](content:references:returns-stylized-facts-qq), the [Kolmogorov-Smirnov test](content:references:returns-stylized-facts-KS-test) and the [Anderson-Darling test](content:references:returns-stylized-facts-AD-test). Both the Kolmogorov-Smirnov and the Anderson-Darling tests are implemented in the [HypothesisTests.jl](https://github.com/JuliaStats/HypothesisTests.jl) package.


(content:references:returns-stylized-facts-qq)=
#### Q-Q plots
The quantile-quantile (Q-Q) plot compares two probability distributions by plotting their quantiles against each other. If two distributions are equal, their respective quantiles will lie on a 45$^{\circ}$ line. However, if the distributions are different, there will be a deviation from the 45$^{\circ}$ line.

In the logarithmic daily return series of `WFC`, the Q-Q plot shows that the return is not normally distributed. Instead, it closely follows a Laplace distribution ({numref}`example-WFC-return-QQ-daily-Normal-Laplace`). The data points deviate from the 45$^{\circ}$ line, particularly in the tails of the normal distribution (left panel). In contrast, the deviation from the 45$^{\circ}$ line is less pronounced for the Laplace distribution (right panel). 

```{figure} ./figs/Fig-WFC-Daily-Return-4yr-QQ-plot-Normal-Laplace.svg
---
height: 420px
name: example-WFC-return-QQ-daily-Normal-Laplace
---
Q-Q plot for logarithmic daily return of [Wells Fargo & Company](https://en.wikipedia.org/wiki/Wells_Fargo) computed between `2018-11-28` to `2022-11-28`. Data was downloaded using the `aggregate` endpoint of [Polygon.io](https://polygon.io/docs/stocks/get_v2_aggs_ticker__stocksticker__range__multiplier___timespan___from___to).
```

However, there is still some deviation particularly on the lower tail, suggesting that Laplace, while being better, is not a perfect description of the return distribution.

(content:references:returns-stylized-facts-KS-test)=
#### Kolmogorov-Smirnov test
The [Kolmogorov–Smirnov test (K–S test)](https://en.wikipedia.org/wiki/Kolmogorov–Smirnov_test) is a nonparametric test of the equality of continuous, one-dimensional probability distributions that can be used to compare a sample with a reference probability distribution (one-sample K–S test), or to compare two samples (two-sample K–S test). The Kolmogorov–Smirnov statistic quantifies a distance between the [empirical distribution function](https://en.wikipedia.org/wiki/Empirical_distribution_function) of the sample and the [cumulative distribution function (CDF) of the reference distribution](https://en.wikipedia.org/wiki/Cumulative_distribution_function), or between the empirical distribution functions of two samples.

* The null hypothesis of the K-S test is that the sample is drawn from the reference distribution (in the one-sample case) or that the samples are drawn from the same distribution (in the two-sample case). 
* The alternative hypothesis is that the sample is not drawn from the reference distribution (in the one-sample case) or that the samples are drawn from different distributions (in the two-sample case).

```{prf:observation} One-sample Kolmogorov-Smirnov test

A one-sample Kolmogorov-Smirnov test was performed to determine if the daily returns of `N = 458` tickers were Normally distributed using daily returns computed between `2018-01-03` to `2022-12-31` (a total of `1256` observations per ticker). 

Results for five example tickers are shown in the table below:

| id  | ticker | name                   | sector                 | Normal (pv)   | Laplace (pv) |
|-----|--------|------------------------|------------------------|----------|---------|
|  11 |    AMD | Advanced Micro Devices | Information Technology |  0.00878 |   0.178 |
| 241 |    IBM |                    IBM | Information Technology |  7.38e-9 |   0.507 |
| 487 |    WFC |            Wells Fargo |             Financials |  5.27e-7 |   0.438 |
| 221 |     GS |          Goldman Sachs |             Financials | 0.000712 |   0.364 |
| 437 |   TSLA |                  Tesla | Consumer Discretionary | 0.000258 |  0.0337 |

A p-value (pv) less than `0.05` means that the null hypothesis can be rejected at the `95%` confidence level. 

```


(content:references:returns-stylized-facts-AD-test)=
#### Anderson-Darling test
The [Anderson–Darling test](https://en.wikipedia.org/wiki/Anderson–Darling_test) is a statistical test of whether a given sample of data is drawn from a given probability distribution. The Anderson–Darling test assesses whether a sample comes from a specified distribution. It makes use of the fact that, when given a hypothesized underlying distribution and assuming the data does arise from this distribution, the [cumulative distribution function (CDF)](https://en.wikipedia.org/wiki/Cumulative_distribution_function) of the data can be assumed to follow a [uniform distribution](https://en.wikipedia.org/wiki/Continuous_uniform_distribution). 

* The null hypothesis of the Anderson–Darling test is that the sample is drawn from the reference distribution.
* The alternative hypothesis is that the sample is not drawn from the reference distribution.

```{prf:observation} One-sample Anderson-Darling test

A one-sample Anderson-Darling test was performed to determine if the daily returns of `N = 458` tickers were Normally distributed using daily returns computed between `2018-01-03` to `2022-12-31` (a total of `1256` observations per ticker). 

Results for five example tickers are shown in the table below:

| id  | ticker | name                   | sector                 | Normal (pv)   | Laplace (pv) |
|-----|--------|------------------------|------------------------|----------|---------|
|  11 |    AMD | Advanced Micro Devices | Information Technology | 0.000756 |   0.152 |
| 241 |    IBM |                    IBM | Information Technology |  4.78e-7 |   0.254 |
| 487 |    WFC |            Wells Fargo |             Financials |  4.78e-7 |   0.338 |
| 221 |     GS |          Goldman Sachs |             Financials |  5.25e-5 |   0.254 |
| 437 |   TSLA |                  Tesla | Consumer Discretionary |  8.34e-5 |   0.165 |

A p-value (pv) less than `0.05` means that the null hypothesis can be rejected at the `95%` confidence level.

```

---

## Summary
In this lecture, we introduced equity securities, discussed the different types of orders that can be used to buy or sell equity securities, introduced some components of market microstructure such as the order book and order matching, and finally explored the statistical properties of equity prices.

* {ref}`content:references:markets-exchanges` play a crucial role in contemporary economies as they enable the trade of goods, services, and financial instruments like stocks and bonds. A market is a platform where buyers and sellers convene to exchange commodities or services, while an exchange is a market that specializes in financial instruments and has specific trade regulations.

* {ref}`content:orders-order-book-matching`. Traders give instructions to buy or sell financial instruments at a specified price, known as orders. These orders are recorded in the order book, which shows all outstanding buy and sell orders for a specific financial instrument on the exchange. The exchange matches buy and sell orders based on price and other criteria through the process of order matching, which results in trades being executed. The order book provides transparency into market depth and liquidity.

* [Stylized facts are identifiable trends or recurring patterns](content:references:returns-stylized-facts)  seen in investment returns and financial markets. One such example is that stock price returns typically display minimal autocorrelation and a leptokurtic distribution, signifying a higher peak and fatter tails than a normal distribution. Familiarity with these patterns can aid investors in making well-informed choices and developing more successful investment strategies.