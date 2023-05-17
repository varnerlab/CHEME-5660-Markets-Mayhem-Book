# Interest, Cash Flows and Future Value

<!-- The development of processes or products does not occur inside a mythical universe that is free 
from market forces. Instead, processes and products must be, at a minimum, financially neutral to be viable. Processes and products that are not financially viable, while perhaps being technically innovative or otherwise advantageous, will not survive in the marketplace without external support e.g., local, state or federal government subsities.  -->

```{topic} Outline

In this lecture, we introduce three basic financial concepts: simple and compound interest, abstract assets, and the net present value. 

* {ref}`content:references:interest-models`: Simple interest refers to the interest calculated solely on the initial principal amount, while compound interest takes into account both the principal and the accumulated interest. 

* {ref}`content:references:abstract-asset-defn` generate value and cash flows for the holder. Cash flows, on the other hand, are the inflows and outflows of money from a business or investment, and are a key factor in determining the value of abstract assets. Finally, interest is the cost of borrowing money, and understanding how interest rates impact cash flows and the value of abstract assets is essential for financial decision making.

* {ref}`content:references:npv-defn` is a financial concept used to determine the current value of future cash flows. It takes into account the time value of money, recognizing that a dollar today is worth more than a dollar in the future due to the potential for investment and earning interest. NPV is a useful tool for evaluating investment opportunities and determining whether they are financially viable.

```

---

(content:references:interest-models)=
## Simple and Compound Interest
The distinction between simple and compound interest is crucial in the world of finance and investing. These concepts significantly impact investment growth and borrowing costs, making them fundamental aspects to consider when making financial decisions. 

Simple interest is paid only on the initial principle. For example, if amount $A(0)$ is invested in an account at $t=0$ which pays a simple interest rate of $r$ per period, then after $n$ periods the amount $A(n)$ is given by:

```{math}
:label: eqn-simple-interest
A(n) = A(0)\cdot\left(1+rn\right)
```

Compound interest considers both the principal and the interest accumulated over time. For example, if amount $A(0)$ is invested in an account at $t=0$ which pays a compound interest rate $r$ per period, then after $n$ periods the amount $A(n)$ is given by:

```{math}
:label: eqn-compound-interest
A(n) = A(0)\cdot\left(1+r\right)^n
```

````{prf:example} Simple versus compound interest
:label: example-simple-vs-compound-interest
:class: dropdown

Compute the balance of an investment account $A(n)$ that pays $r = 0.05$ per period after $n$ periods using a simple and compound interest rate model for an initial investment of $A(0) = 100.0$ USD.

```{figure} ./figs/Fig-Simple-Compound-Interest.pdf
---
height: 360px
name: fig-simple-compound-interest
---
Simple versus compound interest for n-periods for an interest rate of $r = 0.05$ per-period. Compound interest outperforms simple interest as the number of periods becomes large.
```
````

Interest rates are typically quoted on an annual basis, and can be compounded at different rates, e.g., annually, quarterly, etc. Putting these ideas together gives a useful definition of compound interest ({prf:ref}`defn-compound-interest`):

````{prf:definition} Continuous compounding
:label: defn-compound-interest

Let there be n-compounding periods per year and an annualized interest rate of r-percent.  Then an initial investment $A(0)$ will be worth:

```{math}
:label: eqn-compound-interest-model-discrete
A(m) = A(0)\cdot\left(1+r/n\right)^{mn}
```

after $m$-years. As the number of compounding periods $n\rightarrow\infty$, the investment $A(m)$ approaches the continuous compounding case:

```{math}
:label: eqn-compound-interest-model-cont
\lim_{n\rightarrow\infty}A(m) = A(0)\cdot\exp\left(rm\right)
```

````


(content:references:abstract-asset-defn)=
## Abstract Assets

An _abstract asset_ is a sequence of current and future cash flows 
demarcated in some currency, for example, Euros, Dollars, Yuan, or cryptocurrencies such as Bitcoin ({numref}`cash-flow-abstract-asset-fig`).

```{figure} ./figs/Fig-Asset-CashFlowDiagram.pdf
---
height: 240px
name: cash-flow-abstract-asset-fig
---
Abstract asset diagram. During each time period $t=0,2,\dots,T$ an asset has cash flow(s) $\dot{c}_{t}$. The value of the asset is some function $\mathcal{V}$ of these cash flows; the function $\mathcal{V}$ is the called the valuation operator.  
```

The value of an abstract asset is determined using a valuation operator $\mathcal{V}$ applied to the current and future cash flows:


```{math}
:label: eq-asset-cash-flows
\mathcal{V}\left(Asset_{t}\right) = \mathcal{V}\left(\dot{c}_{0},\dot{c}_{1},\dots,\dot{c}_{T}\right)
```
where $\dot{c}_{t}$ denotes the cash flow in time period $t = 0,\dots,T$.
The most common (and intuitive) valuation operator $\mathcal{V}$ is the sum of net cash flows in each time period, i.e., we compute the net cash in each period (cash inflow - cash outflow in period $i$) and then sum these net cash flows over all $T$ periods.


### Time value of money
There is a fundamental challenge to the summation valuation intuition, the time value of money ({prf:ref}`remark-tvof-money`): 

```{prf:remark} Time value of Money
:label: remark-tvof-money
The value of money is _not_ conserved over time. One dollar today is not worth the same as one dollar tomorrow. The change in the value of money over time is called the _time value of money_.  
```

The time value of money is an [empirical observation that has been seen over hundreds of years](https://en.wikipedia.org/wiki/Time_value_of_money#History). But why is this the case? The short answer: money given to us today has a greater [Utility](https://en.wikipedia.org/wiki/Utility) than the same amount tomorrow; because we have an extra day to invest that money ({prf:ref}`obs-time-value-of-money`): 

````{prf:observation} Why does that value of money chnage over time?
:label: obs-time-value-of-money

There exists a _risk-free_ investment guaranteed to return $i>0$ per period. If we invested $P$ dollars today in this risk-free investment, at the end of the investment period, we are _guaranteed_ to get $F$ dollars back (because the investment is risk-free):

```{math}
F = (1+i)\cdot{P}
```

If given a choice between $P$ dollars today, or $P$ dollars one investment period in the future, a rational investor would _always_ choose to take the $P$ dollars now. 

__Why?__ 

* By taking $P$ dollars today, you could invest those $P$ dollars risk-free and get $F = (1+i)\cdot{P}$ back, where $F>P$. Thus, the only case where it makes sense to take the future money is if $i\leq{0}$, i.e., $F\leq{P}$; which is forbidden by the condition $i>0$. 

* This hypothetical scenario assumes that a _risk-free_ investment exists that always returns $i>0$. Does such an investment exist? [Unfortunately, the _risk-free_ investment is only a theoretical concept](https://www.investopedia.com/terms/r/risk-freerate.asp). However, the _risk-free rate of return_ $i$ is often approximated by the [yield on 10-year US Treasury bonds](https://www.bloomberg.com/markets/rates-bonds/government-bonds/us) or some other US Treasury debt security. 

````

<!-- Unfortunately, our intuitive valuation operator (net cash flows) does not consider (yet) the time of value of money. Let's develop some tools to address this issue.  -->

### Exchange rate model
A useful mental model for the time value of money is to think of money from different time periods 
as being in different currencies (e.g., dollars versus euros) that must be exchanged. Thus, to compare money or cash flows from different time periods we formulate the equivalent of an exchange rate.

#### Discrete one-period conversion
Suppose we wanted to convert the value of a cash flow from one time period in the future 
into today's dollars (or vice-versa, we want to compute the value of a future cash flow to a current value). To do this, we use a one-period discrete conversion ({prf:ref}`defn-one-perod-discrete-conversion`):

````{prf:definition} One Period Discrete Conversion
:label: defn-one-perod-discrete-conversion
For any one-period ($t\rightarrow{t+1}$),  the present value of cash flow, denoted as $\dot{c}_{t}$, and the future value of cash-flow, denoted by $\dot{c}_{t+1}$, there exists a one time-step discrete conversion:

```{math}
:label: eq-cash-flow-1-period
\dot{c}_{t+1} = \left(1+r_{t+1,t}\right)\cdot{\dot{c}_{t}}
```
where $r_{t+1,t}>{0}$ is the _discount rate_ between periods $t$ and $t+1$. The term $(1+r_{t+1,t})$, which denotes the hypothetical exchange rate between time period $t\rightarrow{t+1}$, is called the _discrete discount factor_. The _discrete discount factor_ is always greater than one, thus $\dot{c}_{t+1}>\dot{c}_{t}$ for any $t$. 
````

Let's do an example to illustrate one-period conversions ({prf:ref}`example-one-period-discrete-conversion`):

````{prf:example} One period conversion
:label: example-one-period-discrete-conversion
:class: dropdown

Prof. Varner offers to buy you a coffee tommorrow (one time period in the future) for $\dot{c}_{2} = \$ 3.35$. How much is the future coffee worth today if $r_{21}=10\%$? Let's put some numbers into Eqn. {eq}`eq-cash-flow-1-period` to answer this question.  Rearraninging Eqn. {eq}`eq-cash-flow-1-period` for $\dot{c}_{1}$ gives:

```{math}
\dot{c}_{1} = \frac{\dot{c}_{2}}{1+r_{21}}
```

Subsutituing $r_{21}=10\%$ and $\dot{c}_{2}=\$ 3.35$ says the current value of your future coffee is: $\dot{c}_{1} = \$ 3.05$.
````

#### Discrete multiple-period conversion
Suppose, instead of a single period, we are interested in an asset that will be active over multiple periods, e.g., a multi-year project or some other transaction that occurs over many years. In this case, we develop a multi-year conversion that is easily constructed by sequentially applying many one-period calculations.

To see this idea, let's start with period zero to period one:
```{math}
\dot{c}_{1} = \left(1+r_{10}\right)\cdot\dot{c}_{0}
```
Then, period one to period two is given by:

```{math}
\dot{c}_{2} = \left(1+r_{21}\right)\cdot\dot{c}_{1}
```

but we can substiture $\dot{c}_{1}$ into the expression above to give:

```{math}
\dot{c}_{2} = \Bigl[\left(1+r_{21}\right)\left(1+r_{10}\right)\Bigr]\cdot\dot{c}_{0}
```

If we do this computation between 2 and 3, and then 3 to 4, etc, we develop a relationship between the current value of cash flow ($t=0$) and the future ($t>1$) value of cash flows ({prf:ref}`defn-multi-perod-discrete-conversion`):

````{prf:definition} Multiple period discrete conversion
:label: defn-multi-perod-discrete-conversion

Let $\dot{c}_{0}$ denote the cash-flow in period 0 (current value), and $\dot{c}_{t}$ the cash-flow in period $t>0$ (future value). Further, let $r_{j+1,j}$ denote the rate of return between discrete time period $j$ and $j+1$. Then: 

```{math}
:label: eq-cash-flow-multiple-period
\dot{c}_{t} = \left[\prod_{j=0}^{t-1}\left(1+r_{j+1,j}\right)\right]\cdot\dot{c}_{0}\qquad{t=1,2,\dots,T}
```
````

The product term (the $\prod\star$ in the brackets) in Eqn. {eq}`eq-cash-flow-multiple-period` is called the _multi-period discount factor_ and given the symbol $\mathcal{D}$. Thus, Eqn. {eq}`eq-cash-flow-multiple-period` can be written in a more compact form as:

```{math}
\dot{c}_{t} = \mathcal{D}_{t,0}\cdot\dot{c}_{0}\qquad{t=1,2,\dots,T}
```

In the particular case where the rates of return $r_{\star}$ are equal in each period (let's call this value $\bar{r}$), the _multi-period discount factor_ becomes:

```{math}
:label: eqn-discrete-discount-factor-constant-r
\mathcal{D}_{t,0} = (1+\bar{r})^{t}\qquad{t=1,2,\dots,T}
```

Let's do an example of multi-period discounting ({prf:ref}`ex-future-value-discrete`):

````{prf:example} Multiple period discount
:label: ex-future-value-discrete
:class: dropdown

Compute the present value of \$1 collected $T$ time units into the future for a constant discount rate of 2\%, 4\%, and 6\% per time period.

The value of money today is the present value, whereas the value of money $T$ time periods in is the future  value. The quantity $\dot{c}_{0}$ is the present value, while $\dot{c}_{i},i=1,2,\dots,T$ denotes future value. 

To compute the present value of \$1 collected $T$ time units into the future, we solve Eqn. {eq}`eq-cash-flow-multiple-period` for $\dot{c}_{0}$ in terms of the future value $\dot{c}_{i},i=1,\dots,T$ and the discount factor $\mathcal{D}$:

```{math}
\dot{c}_{0} = \mathcal{D}_{i,0}^{-1}\cdot\dot{c}_{i}\qquad{i=0,1,\dots,T}
```

where $\mathcal{D}_{i,0}^{-1}$ is given by:

```{math}
\mathcal{D}_{i,0}^{-1} = \frac{1}{(1+\bar{r})^{i}}\qquad{i=0,1,\dots,T}
```

We assumed a constant discount rate $r$ between now (i = 0) and $i = T$ time units into the future. Given that we are looking at the present value of \$1, we can set $\dot{c}_{i} = 1$ USD:


```{math}
\dot{c}_{0} = \frac{\dot{c}_{i}}{(1+\bar{r})^{i}}\qquad{i=0,1,\dots,T}
```

```{figure} ./figs/Fig-PresentValue-FuturePayment.pdf
---
height: 380px
name: fig-presentvalue-futurepayment
---
Present value (PV) of \$1 USD collected T periods in the future. 
```

__source__: [live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [static HTML](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-PresentValue.jl.html)

````

#### Continuous discounting
When formulating Eqn. {eq}`eq-cash-flow-1-period` we used a finite discrete-time difference, e.g., days, weeks, or maybe even years to compute the discount factor. However, suppose the time difference between $t\rightarrow{t+1}$ were infinitesimally small, i.e., the time difference was continuous. In this case, we have [continuous compounding](https://www.investopedia.com/terms/c/continuouscompounding.asp) where the discount factor $\mathcal{D}$ is defined as:

```{math}
\mathcal{D}(r,t) = \exp\left(rt\right)
```

A continuous discount factor gives a future value expression of the form:

```{math}
:label: eq-cont-exchange-tvm
CF(t) = \exp\left(rt\right)CF(t_{o})
```

where $r$ denotes the _instantaneous_ discount rate, $t$ denotes the current time, $t_{o}$ denotes the initial time.  

````{prf:observation} Discrete and continuous discount factor
:label: continuous-compounding

There is a relationship between the discrete and continuous discount factors; the discrete discount factor is the linear portion of the continuous discount factor. We can see this by looking at the series representation of the `exp` function:

```{math}
\exp\left(x\right) = \sum_{k=0}^{\infty} \frac{x^{k}}{k!} = 1+x+\frac{x^{2}}{2}+\frac{x^{3}}{6}+\dots
```

The first two terms are the discrete discount factor. Thus, for _small_ values of $rt$ the discrete and continuous discount factors will be similar.  

````

Let's do a continuous discount factor example. 

````{prf:example} What is \$1 collected today worth T years from now? 
:label: ex-future-value-continuous

Let's consider the opposite case from the previous example. Suppose we are given \$1 dollar today. What is the future value of \$1 in T years from now? Assume a 2.0\%, 4.0\% and 6.0\% instantaneous annualized discount factor. 

In this example, $CF(t_{o}) = 1$, the value of $r$ = 2\%, 4\% and 6\% and the time $t$ will be in years. Plugging these into [Julia](https://julialang.org) and plotting using the [Plots.jl](https://github.com/JuliaPlots/Plots.jl) package gives:

```{figure} ./figs/Fig-FutureValue-1-dollar.pdf
---
height: 380px
name: fig-futurevalue-1-dollar
---
Future value (FV) of \$1 USD (today) T-years in the future using a continuous discont factor. 
```

__source__: [live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [static HTML](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-CDF.jl.html)
````

(content:references:npv-defn)=
## Net Present Value (NPV)
```{figure} ./figs/Fig-FinanicalNode-Schematic.pdf
---
height: 220px
name: cash-financial-node-flow-fig
---
Node cash-flow balance diagram. During time $t=k$ monety flows enter (revenues) and exit (expenses) the time-node.  
```

Now that we have tools to account for the time value of money, we can return to the question of how to value an asset. The most intuitive aproach is to compute the net cash flow at every node. Imagine at node $t=k$ we have $\mathcal{S}^{t=k}$ cash streams, denoted as $\dot{C}_{s}$, entering (or exiting) the asset node. Then, the net cash would at node $t=k$ is given by:

```{math}
CF_{k} = \sum_{s\in\mathcal{S}^{t=k}}\nu_{s}\dot{C}_{s}
```

where $\nu_{s}$ denotes a direction parameter; $\nu_{s}=+1$ if stream $s$ enters node $t=k$, $\nu_{s}=-1$ if stream $s$ exists node $t=k$. Finally, to value an asset, we could imagine adding up all the current and future cash flows, converted to some shared basis, e.g., current dollars. This sum is called the [Net Present Value (NPV)](https://en.wikipedia.org/wiki/Net_present_value); NPV is a widespread method for asset valuation. As well shall see, NPV is also a widely used tool for financial decision-making.   

````{prf:definition} Discrete Net Present Value
:label: net-present-value-defn

The discrete Net Present Value (NPV) is the sum of the discrete current and future cash flows, corrected to current dollars:

```{math}
\text{NPV} = \sum_{t=1}^{T}{\mathcal{D}_{t,1}^{-1}}\cdot{CF_{t}}
```

where $CF_{t}$ denotes the cash flow in time period $t$, and $\mathcal{D}_{t,1}$ denotes the discrete multistep discount factor between the current time period, and time period $t$. However, we know that $r_{1,1} = 0$ because there is no possibility of an instantaneous return; thus, $\mathcal{D}_{t,1} = 1$. Therefore NPV can be re-written as:

```{math}
\text{NPV} = CF_{1} + \sum_{t=2}^{T}{\mathcal{D}_{t,1}^{-1}}\cdot{CF_{t}}
```

where the value of each cash flow at time $\star$, denoted by $CF_{\star}$, is the net cash flow:

```{math}
CF_{\star} = \sum_{s\in\mathcal{S}^{t=\star}}\nu_{s}\dot{C}_{s}
```
````

(content:references:npv-decision-tool)=
### NPV as a Decision Tool
The net present value is a widely used tool for financial decision-making. However, to understand the basis of the approach, we must first answer a technical question: What discount rate should we use? 

The discount rates $r_{t+1,t}$, i.e., the rates of return between time periods $t\rightarrow{t+1}$ appearing in the discount factors, have an exciting interpretation within the context of net present value calculations. These rates can be _specified_ by the decision maker as the minimum acceptable rate of return that some hypothetical _alternative_ investment could earn. 

We can set up the following criteria to decide between a possible asset or project and a hypothetical alternative investment:

* $\text{NPV}<0$: A negative NPV indicates the proposed project will generate less income than the alternative investment, e.g., a zero-coupon bond at the same discount rate and time-to-maturity as the project.

* $\text{NPV}=0$: A zero NPV indicates the proposed project will generate the same income as the alternative investment, e.g., a zero-coupon bond at the same discount rate and time-to-maturity as the project.

* $\text{NPV}>0$: A positive NPV indicates the proposed project will generate more income than a hypothetical alternative investment, e.g., a zero-coupon bond at the same discount rate and time-to-maturity as the project.

Let's do a net present value example:

````{prf:example} Install an upgraded lighting system?
:label: example-net-present-value-discrete

Should we install a new computer-controlled lighting system (or not)? Johnson Controls offers to install a new computer-controlled lighting system that will reduce electric bills by 90,000 USD each of the next three years. Is this a good investment if the system costs 230,000 USD fully installed?

The discount rate is constant over the lifetime of the project, but unkown; thus, $\bar{r}$ is a parameter in the problem.

```{figure} ./figs/Fig-JControls-NPV.pdf
---
height: 380px
name: example-jcontrols-npv-fig
---
Net Present Value (NPV) as a function of the discount rate $\bar{r}$ for the proposed Johnson Controls lighting upgrade. The alternative investment is a perfectly priced zero-coupon bond with the same $\bar{r}$ and time-to-maturity as the lighting project. 
```

The installation of the computer-controlled lighting system from Johnson Controls had a positive net present value (NPV) for discount rates less than 8.5%. However, the alternative investment would be the preferred choice beyond this discount rate.

__source__: The Johnson Controls example was modified from [MIT 15.401](https://ocw.mit.edu/courses/sloan-school-of-management/15-401-finance-theory-i-fall-2008/). Donwload [the live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [a static html version](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-NetPresentValue.jl.html).

````

### The Internal Rate of Return (IRR)
The NPV decision rule above relies on computing the sum of discounted future cash flows. However, in these calculations, what discount rate should we use? This is not an easy question; the correct discount rate varies between applications and industries.  Thus, let's think of the discount rate as a variable. 

* If the net present value of an investment or project is positive, the project earns more than a zero-coupon bond with a yield equal to the discount rate used to discount future cash flows. 
* If the net present value of a project is negative, the project earns less than a zero-coupon bond with a yield equal to the discount rate used to discount future cash flows. 
* If the net present value of a project or investment is precisely $0, the project earns the same as a zero-coupon bond with a yield equal to the discount rate used to discount future cash flows.

The special discount rate where the net present value is zero is called the Internal Rate of Return (IRR):

````{prf:definition} Internal Rate of Return
:label: defn-internal-rate-of-return

Assume the discount rate is constant between time periods, denote this rate as $\bar{r}$. Then, the internal rate of rerturn (IRR) is the discount rate that satifies the following condition:

```{math}
\sum_{t=1}^{T}{\mathcal{D}_{t,1}^{-1}}\cdot{CF_{t}} = 0
```

Discount rates greater than the IRR favor the alternative investment.

````

Thus, IRR can thought of as a decision boundary of sorts; the IRR is the discount rate where the project manager or investor is indifferent to the project. 

---

## Summary
In this lecture:

* We introduced the definition of a {ref}`content:references:abstract-asset-defn`. An asset is a sequence of current and future cash flows demarcated in some currency. Assets can be tangible things like cars or houses, but they can also be projects or ideas.  
* We introduced the {ref}`content:references:npv-defn`, a tool to calculate the valuation of an asset. The net present value is the sum of net cash flows discounted to the current period. 
* Used {ref}`content:references:npv-decision-tool` to evaluate the _relative_ attractiveness of assets and projects. Assets with a positive net present value have a larger return than hypothetical alternative investments. On the other hand, investments with a negative net present value will have a smaller return than a  hypothetical alternative investment.

## Additional Resources
* [IEOR E4706: Foundations of Financial Engineering, Columbia University](https://martin-haugh.github.io/teaching/foundations-fe/)
