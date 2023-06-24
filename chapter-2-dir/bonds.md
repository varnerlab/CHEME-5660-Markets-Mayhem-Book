# Fixed Income Securities
Fixed-income debt securities are contracts between a borrower and a lender that regulate the repayment of a debt. An archetypal category of fixed-income debt security: [United States Treasury Securities](https://www.investor.gov/introduction-investing/investing-basics/glossary/treasury-securities), are issued by the U.S. Department of the Treasury to represent debt obligations. 

<!-- Fixed-income securities are financial instruments with predefined cashflows at selected dates over the lifetime of the instrument. While there are several types of fixed-income securities, we'll focus on an archetypal category: [United States Treasury Debt Securities](https://www.investor.gov/introduction-investing/investing-basics/glossary/treasury-securities). Treasury debt securities, e.g., [Treasury bills, notes, and bonds](https://www.treasurydirect.gov/indiv/products/prod_tbonds_glance.htm), are debt obligations issued by the United States Department of the Treasury to holder of the security. U.S. Treasury debt securities are a mechanism used by the United States government to borrow money, from bondholders, with a fixed set of repayment terms. Treasury debt securities are viewed as one of the safest possible investments, e.g., defacto risk-free, because Treasury debt securities are backed by the full faith and credit of the United States government. [The U.S. government has never defaulted on its debt obligations (at least in recent memory)](https://thehill.com/opinion/finance/575722-the-us-has-never-defaulted-on-its-debt-except-the-four-times-it-did/).   -->


```{topic} Outline

In this lecture, we introduce US government debt securities, their risks and pricing, and the term structure of interest rates: 

* {ref}`content:references:treasury-bonds` are fixed-income securities issued by the US government to fund its operations and meet financial obligations. Treasury bills have a short-term maturity of less than a year, while Treasury notes and bonds have longer maturities ranging from two to thirty years. These securities are regarded as some of the safest investment options globally, backed by the US government’s full faith and credit.

* {ref}`content:references:bond-pricing-relationships` are utilized to determine the equitable value of a bond, considering its maturity, coupon rate, and current market interest rates. As per Malkiel’s guidelines, the bond’s price will fluctuate inversely with changes in interest rates. Long-term bonds will be more affected than short-term bonds. 

* {ref}`content:references:term-structure-of-interest-rates` describes the correlation between fixed-income security interest rates and their maturity period. This concept represents the market’s outlook on future interest rates. The shape of the term structure - whether it’s upward-sloping, flat, or inverted - offers valuable insights into the economy’s present and potential future state. 

```
<!-- 
These securities are deemed to be secure investments as they carry no risk and are backed by the full faith and credit of the U.S. government, which has never failed to meet its debt obligations. -->

---

(content:references:treasury-bonds)=
## Treasury Bills, Notes and Bonds
In the case of United States treasury debt instruments, the borrower is the U.S. government, where a bond is issued (i.e., sold) to a lender in exchange for cash ({numref}`fig-bill-notes-bonds-schematic`).

```{figure} ./figs/Fig-Govt-Debt-Schematic.pdf
---
height: 340px
name: fig-bill-notes-bonds-schematic
---
Schematic of United States Treasury debt instruments. The treasury borrows money from bondholders by selling treasury bills, notes, and bonds. Each debt instrument has a particular repayment plan, e.g., a specified duration and payment schedule.   
```

Through this agreement, the U.S. Treasury is obligated to make specified payments to the bondholder on specific dates throughout the instrument's lifetime. While there are several types of U.S. government debt securities, they share several similarities:

* U.S. Treasury debt securities have fixed term lengths, signifying that the duration of the contract between the borrower and the lender is predetermined.
* U.S. Treasury debt securities have a par value, which is the face value of the instrument, a price (which may differ from the par value), and an interest rate paid to the lender.
* U.S. Treasury debt securities have interest payments historically referred to as coupons. They pay the lender a fixed amount of cash on a predetermined schedule throughout the debt instrument's term.
* Interest income from U.S. Treasury debt securities is exempt from state and local income taxes but subject to federal income taxes.
* You can lend money to the U.S. government by purchasing U.S Treasury debt directly from the [United States Treasury via TreasuryDirect](https://www.treasurydirect.gov/indiv/products/prod_tbonds_glance.htm) or through a bank or broker.


### Treasury Bills
Treasury bills, or T-bills, which are [auctioned off regularly](https://www.treasurydirect.gov/auctions/upcoming/), are treasury debt instruments with short-term maturity periods $T$ = 4, 8, 13, 26, and 52 weeks and zero coupon payments ({numref}`fig-bill-payout-schematic`):

```{figure} ./figs/Fig-Zero-Coupon-Schematic.pdf
---
height: 320px
name: fig-bill-payout-schematic
---
Schematic of a zero-coupon United States Treasury bill. The bill holder purchases the bill for $V_{B}$ (current dollars). At the term of the bill, the treasury pays the bondholder the face (par) value of the bill $V_{P}$.   
```

T-bills are zero-coupon fixed-income investments, i.e., they are no coupon payments during their term. Instead, treasury bills are priced so that the bill holder receives the face (par) value at the end of the term ({prf:ref}`defn-zero-coupon-bond-pricing`): 

````{prf:definition} Zero Coupon bill pricing
:label: defn-zero-coupon-bond-pricing

A zero-coupon treasury bill has a T-year term with an annual market (constant) interest rate of $\bar{r}$ specified at the time of purchase. The fair price of the T-bill is the future face (par) value discounted to today by the market interest rate $\bar{r}$:

```{math}
:label: eqn-zero-coupon-bill-bond
V_{B} = \mathcal{D}^{-1}_{T,0}\cdot{V_{P}}
```

The quantity $V_{B}$ denotes the current price of the bill, $V_{P}$ represents the future face (par) value of the bill, and $\mathcal{D}_{T,0}$ denotes the discount factor governing the period $0\rightarrow{T}$, i.e., from when the zero coupon treasury security was auctioned (current) to maturation (future). The discount factor model can be either discrete or continuous.
````

The price of a treasury bill $V_{B}$ is computed with respect to a market interest rate $\bar{r}$ on the day the bill is purchased. Further, the fair price of a treasury bill has a net present value equal to zero. However, interest rates $\bar{r}$ vary with time and economic conditions ({numref}`fig-bill-daily-interest-rate`):


```{figure} ./figs/Fig-4-week-Daily-2022.pdf
---
height: 420px
name: fig-bill-daily-interest-rate
---
Daily interest rate quotations for 2022 download from [Treasury.gov](https://home.treasury.gov/resource-center/data-chart-center/interest-rates/TextView?type=daily_treasury_bill_rates&field_tdr_date_value_month=202305). These rates are secondary market quotations on 4-week treasury bills, assuming a 360-day year,  computed at approximately 3:30 PM each business day by the [Federal Reserve Bank of New York](https://www.newyorkfed.org).
```


Thus, the market price of a treasury bill for the same par value and duration can change over its term because of changes in interest rates ({prf:ref}`example-zero-coupon-t-bill`):

````{prf:example} Pricing of a Treasury Bill
:class: dropdown
:label: example-zero-coupon-t-bill

Compute the fair price for a zero-coupon treasury bill with a par value of \$1,000 and T = 26-week and T = 52-week duration as a function of annualized market interest rate $\bar{r}$. 

The fair price for a zero-coupon treasury bill, denoted by $V_{B}$, is the future face (par) value $V_{P}$ of the bill discounted at $\bar{r}$ to the time of the purchase (current dollars):

$$V_{B} = \mathcal{D}^{-1}_{T,0}\cdot{V_{P}}$$

Solving this expression as a function of $\bar{r}$ for different values of the T-bill term $T$ gives the results shown in {numref}`fig-zcbill-price`:

```{figure} ./figs/Fig-Price-Zero-Coupon-Bill.pdf
---
height: 400px
name: fig-zcbill-price
---
Price of a zero coupon treasury bill for a term of 0.5 (dark blue) and one year (light blue) as a function of the market interest rate. Face value $V_{P}$ = 1000 USD.
```

The treasury bill pricing calculations have some interesting properties:

* There is an _inverse_ relationship between the current price of a zero-coupon bill and the market interest rate $\bar{r}$; this must be true as the par value (which is in future dollars) is fixed. Thus, higher market interest rates imply lower initial T-bill prices. 

* The relationship between $V_{B}$ and $\bar{r}$ is _not_ linear (dashed versus solid lines); even though it may appear to be the case from the parameters used in the example, the relationship between price and interest rate is convex

* Finally, the longer duration treasury bills are more sensitive to interest rate changes; the T = 1-year slope is larger than the T = 0.5-year case.

````

### Treasury Notes and Bonds
Treasury notes, also known as T-notes, are debt instruments that offer a fixed interest rate every six months until they reach maturity. They are available in 2, 3, 5, 7, and 10-year terms. The price of a T-note can be more or less than its par value, but when it matures, the lender receives the full par value. T-notes are coupon debt instruments, meaning that the lender gets regular interest payments that correspond to a coupon rate throughout the T-note’s life ({numref}`fig-bond-payout-schematic`):

```{figure} ./figs/Fig-Bond-Asset-Timeline-Schematic.pdf
---
height: 320px
name: fig-bond-payout-schematic
---
Schematic of the lifetime of a Treasury Bond with semiannual coupon payments. The bond is purchased now and the bondholder receives semi-annual coupon payments until the maturity of the bond T-years into the future. At maturity, the bondholder receives a final coupon payment plus the face value of the bond.    
```

Treasury bonds, like T-notes, are debt instruments that pay a fixed rate of interest every six months. However, treasury bonds are long-term U.S. Treasury debt instruments with terms of 20 or 30 years. When a bond reaches maturity, the bondholder receives the bond’s face value. Bonds can be held until maturity or sold before maturity. 

#### Pricing of U.S. Treasury Notes and Bonds
A bond’s coupon payments, and the eventual repayment of the face value, occurs many years in the future. Thus, the price an investor is willing to pay for a claim to those payments depends on the future value of the dollars that will be received versus the present value of the face value of the bond ({prf:ref}`defn-fixed-r-bond-pricing`):

````{prf:definition} Fixed Coupon Rate Bond Pricing
:label: defn-fixed-r-bond-pricing

Assuming a bond term of T-years with semiannual coupon payments per year (represented by $\lambda = 2$), there will be N = $\lambda{T}$ coupon payments over the bond term. The annual coupon rate is $\bar{c}$%, while the annual market interest rate is denoted by $\bar{r}$%. The fair price for the bond $V_{B}$ is the present value of coupon payments $C$ added to the discounted face value of the bond $V_{P}$:

```{math}
V_{B} = \mathcal{D}^{-1}_{N,0}V_{P}+\sum_{j=1}^{N}\mathcal{D}_{j,0}^{-1}C
```

The discount factor for time period $0\rightarrow{I}$, denoted as $\mathcal{D}_{i,0}$, can be either a discrete or continuous compounding model. The coupon payment is determined at the time of bond is purchased, where $C=\left(\bar{c}/\lambda\right)\cdot{V_{P}}$. The market interest rate is assumed to be constant over the course of the bond and is represented as $I=\bar{r}/\lambda$. 
````

Let's do an example illustrating bond pricing ({prf:ref}`example-treaury-bond-price`).

````{prf:example} Pricing T = 30 year Treasury Bond
:class: dropdown
:label: example-treaury-bond-price

Compute the price of a bond with a T = 30-year term and a par value of $V_{P}$ = \$1000 for different combinations of the interest rate $\bar{r}$ and coupon rate $\bar{c}$ of the bond. In particular, 
1. The interest rate $\bar{r}$ equals to the coupon rate $\bar{c}$; let $\bar{c}=8\%$ and $\bar{r}=8\%$
1. The interest rate $\bar{r}$ is larger than the coupon rate $\bar{c}$; let $\bar{c}=8\%$ and $\bar{r}=10\%$
1. The interest rate $\bar{r}$ is smaller than the coupon rate $\bar{c}$; let $\bar{c}=8\%$ and $\bar{r}=6\%$

The bond price is given by {prf:ref}`defn-fixed-r-bond-pricing`. A 30-year term gives 60 semi-annual coupon payments. Substituting the values for $\bar{r}$, $\bar{c}$ and the number of payments into the pricing equation gives:

| Case | $\bar{r}$ (\%) | $\bar{c}$ (\%) | $V_{P}$ (USD) | $V_{B}$ (USD) |
| :----: | :---------: | :---------: | :-------: | :-------: |
| 1    | 8       | 8       | 1000    | 1000    |
| 2    | 10      | 8       | 1000    | 810.71  |
| 3    | 6       | 8       | 1000    | 1276.76 |

__source__: [Live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [a static HTML view](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-Price-TreasuryBond.jl.html).
````


#### Yield to Maturity of U.S. Treasury Notes and Bonds
To determine the rate of return of a bond, we use a metric called the yield to maturity (YTM). The yield to maturity considers the current income generated by coupon payments and the potential price increase or decrease over the bond term ({prf:ref}`defn-yield-to-maturity`): 

````{prf:definition} Yield to Maturity 
:label: defn-yield-to-maturity

The yield to maturity (YTM) is defined as the market interest rate that makes the present value of a bond’s payments equal to its price, $V_{B}$.

Let the term of a bond be T-years with $\lambda$ coupon payments per year; $N = \lambda{T}$ coupon payments over the bond duration. The yield to maturity (YTM) is defined as the market interest rate that makes the present value of a bond’s payments equal to its price, $V_{B}$:

```{math}
V_{B} - \frac{V_{P}}{\left(1+i\right)^{N}}-\sum_{j=1}^{N}\frac{C}{\left(1+i\right)^{j}} = 0
```

where $C=\left(\bar{c}/\lambda\right)\cdot{V_{P}}$ denotes the value of the coupon payment which is set at the time the bond is purchased, and $i=\bar{r}/\lambda$ denotes the market interest rate (spot rate), which can fluctuate over time.

````

##### Example
* Let's do an example illustrating the Yield to Maturity (YTM) calculation ({prf:ref}`defn-yield-to-maturity`). Sources: [Live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [a static HTML view](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-YieldToMaturity-TreasuryBond.jl.html).


(content:references:bond-pricing-relationships)=
## Malkiel’s bond-pricing guidelines
Bond investors have two actions open to them: hold the bond until maturity (and collect the coupon payments along the way), or resell the bond (and potentially benefit from a change in the bond price). The latter is possible because after the bonds are issued, bondholders may buy or resell bonds in secondary bond markets. In these markets, bond prices fluctuate inversely with the market interest rate $\bar{r}$. Thus, interest rate fluctuations are the main source of risk to the bondholder if they are not holding the bound to maturity.

```{figure} ./figs/Fig-Sensitivity-Bond-Price-Interest-Rate.pdf
---
height: 420px
name: fig-bond-price-sensitivity
---
Sensitivity of bond price to changes in the market interest rate.   
```


The relationship between the price of a bond, and the yeild (i.e., the market interest rate $\bar{r}$) was previously studied by Malkiel {cite}`Malkiel1962`. The so-called Malkiel’s bond-pricing rules are demonstrated by the simulations shown in ({numref}`fig-bond-price-sensitivity`):

1. The price of a U.S. Treasury Bond _increases_ as the market interest rate $\bar{r}$ _decreases_; thus, there is an _inverse_ relationship between the bond yield to maturity (i.e., the market rate $\bar{r}$) and the price of the bond $V_{B}$. 
1. Changes in price as a function of changes in the interest rate are not symmetric;
an increase in a bond’s interest rate $\bar{r}$ results in a _smaller price change_ than a decrease in $\bar{r}$ of equal magnitude. For example, consider Case II in ({numref}`fig-bond-price-sensitivity`); a 50% decrease in $\bar{r}$ increases the price of this bond by approximately 75%, while a 50% increase in $\bar{r}$ decreases the bond price approximately 30%.
1. Prices of long-term bonds are more sensitive to interest rate changes than short-term bonds. For example, consider Case I and Case II in ({numref}`fig-bond-price-sensitivity`); Case I (short-term bond) is _less sensitive_ to the same magnitude change in $\bar{r}$ compared with Case II (long-term bond).
1. Interest rate risk is inversely related to a bond’s coupon rate. Prices of low coupon-rate bonds are more sensitive to changes in interest rates than prices of high-rate coupon bonds. For example, compare Case II and III in ({numref}`fig-bond-price-sensitivity`); case III (the low coupon-rate bond) is significanly more sensitive to decreases in interest rate compared with case II (the high coupon-rate bond). A similar, albeit less pronounced, trend is visible for increased
interest rate.

(content:references:term-structure-of-interest-rates)=
## Term structure of interest rates
In discrete compounding models, the interest rate denoted by $\bar{r}$ is assumed to be constant throughout the life of the treasury security. This gives us the discrete discount factor in the form:

$$\mathcal{D}_{T,0} = (1+\bar{r})^{T}$$ 

However, in reality, interest rates fluctuate, giving us insight into larger macroeconomic conditions and affecting the price movement of different assets. To account for this variation, we can consider _short rates_, i.e., the interest rates between the periods $j\rightarrow{j+1}$, denoted by $r_{j+1,j}$. The discount factor in terms of the _short rates_ is expressed as: 

$$\mathcal{D}_{T,0} = \left[\prod_{j=0}^{t-1}\left(1+r_{j+1,j}\right)\right]$$ 

Of course, these two discount factor expressions must be equal, giving the mathching condition:

```{math}
:label: eqn-discount-factor-matching
(1+\bar{r})^{T} = \left[\prod_{j=0}^{t-1}\left(1+r_{j+1,j}\right)\right]
```

Solving Eqn. {eq}`eqn-discount-factor-matching` gives the market interest rate $\bar{r}$ in terms of the _short rates_:

```{math}
:label: eqn-rbar-in-terms-of-short rates
\bar{r} = \left(\left[\prod_{j=0}^{t-1}\left(1+r_{j+1,j}\right)\right]\right)^{1/T} - 1
```

---
 
## Summary
In this lecture, we introduced fixed-income debt securities. Fixed-income debt securities are contracts between a borrower and a lender that regulate the repayment of a debt. Here we focused on an archetypal category of fixed-income debt security: [United States Treasury Securities](https://www.investor.gov/introduction-investing/investing-basics/glossary/treasury-securities). 

In particular, we discussed:

* {ref}`content:references:treasury-bonds` are fixed-income securities issued by the US government to fund its operations and meet financial obligations. Treasury bills have a short-term maturity of less than a year, while Treasury notes and bonds have longer maturities ranging from two to thirty years. These securities are regarded as some of the safest investment options globally, backed by the US government’s full faith and credit.

* {ref}`content:references:bond-pricing-relationships` are utilized to determine the equitable value of a bond, considering its maturity, coupon rate, and current market interest rates. As per Malkiel’s guidelines, the bond’s price will fluctuate inversely with changes in interest rates. Long-term bonds will be more affected than short-term bonds. 

* {ref}`content:references:term-structure-of-interest-rates` describes the correlation between fixed-income security interest rates and their maturity period. This concept represents the market’s outlook on future interest rates. The shape of the term structure - whether it’s upward-sloping, flat, or inverted - offers valuable insights into the economy’s present and potential future state. 