(content:references:treasury-bonds)=
# Treasury Bills, Notes and Bonds

```{topic} Outline
After introducing the structure and properties of U.S. Treasury securities, in this lecture we'll discuss the following topics:

* [Simple and Compound Interest](content:references:interest-models) are two methods of calculating interest. Simple interest is calculated on the principal amount of a loan only. Compound interest is calculated on the principal amount and also on the accumulated interest of previous periods, and can thus be regarded as `interest on interest.`

* [U.S. Treasury Bills](content:references:US-T-Bills) are short-term debt securities with a maturity of less than one year. On the other hand,[Treasury Notes and Bonds](content:references:US-T-Notes-Bonds) are long-term debt securities with a maturity of two to thirty years. Bills, Notes and Bonds are structured contracts between the U.S. government and bondholders that specify the repayment terms of the loan, e.g., the duration of the loan and the payment schedule.

* [The Yield to Maturity (YTM)](content:references:US-YTM-Defn) is a measure of the _return of a bond investment_. Yield to maturity is the discount rate that equates the present value of a bond's cashflows to its price.  The YTM is the internal rate of return (IRR) of an investment in a bond if the investor holds the bond until maturity and if all payments are made as scheduled.
```

---

## Introduction
United States Treasury debt securities are structured loan agreements between a borrower, i.e., the U.S. government, and a lender (you) that allows the government to fund its operations and obligations ({numref}`fig-bill-notes-bonds-schematic`).

```{figure} ./figs/Fig-Govt-Debt-Schematic.svg
---
height: 340px
name: fig-bill-notes-bonds-schematic
---
Schematic of United States Treasury debt instrument. The treasury borrows money from bondholders by selling treasury bills, notes, and bonds. Each debt instrument has a particular repayment plan, e.g., a specified duration and payment schedule.   
```

The bondholder and the U.S. Treasury have a marketable agreement, which can be resold. This agreement mandates the Treasury to make payments to the bondholder on specific dates throughout the instrument’s lifetime. Although there are various types of U.S. government debt securities, they all share a few common characteristics:

* U.S. Treasury debt securities have a predetermined term length, indicating that the duratio The YTM is the internal rate of return (IRR) of an investment in a bond if the investor holds the bond until maturity and if all payments are made as scheduled.n of the contract between the borrower and lender is fixed.
* U.S. Treasury debt securities have a par value, representing the instrument's face value, a price (which may differ from the par value), and an interest rate paid to the lender.
* Some U.S. Treasury debt securities have interest payments commonly called coupons. These payments give the lender fixed cashflows on a predetermined schedule throughout the debt instrument's term.
* Income from interest on U.S. Treasury debt securities is free of state and local income taxes but subject to federal income taxes.
* You can purchase U.S. Treasury debt directly from the [United States Treasury via TreasuryDirect](https://www.treasurydirect.gov/indiv/products/prod_tbonds_glance.htm) or through a bank or broker to lend money to the U.S. government.

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


(content:references:US-T-Bills)=
## U.S. Treasury Bills
[United States Treasury Bills](https://treasurydirect.gov/marketable-securities/treasury-bills/), or T-bills are Treasury debt instruments with short-term maturity periods `T = 4, 8, 13, 26, and 52 weeks` and zero coupon payments ({numref}`fig-bill-payout-schematic`):

```{figure} ./figs/Fig-Zero-Coupon-Schematic.svg
---
height: 320px
name: fig-bill-payout-schematic
---
Schematic of a zero-coupon United States Treasury bill. The bill holder purchases the bill for $V_{B}$ (current). At the term of the bill, the Treasury pays the bondholder the face (par) value of the bill $V_{P}$ (future).   
```

T-bills, which are [auctioned off regularly](https://www.treasurydirect.gov/auctions/upcoming/), are zero-coupon fixed-income investments, i.e., they have no coupon payments during their term. Instead, T-bills are priced at a discount to thier face (par) value ({prf:ref}`defn-zero-coupon-bond-pricing`): 

````{prf:definition} Zero Coupon T-bill pricing
:label: defn-zero-coupon-bond-pricing

A zero-coupon Treasury bill with a face (par) value of $V_{P}$ (future) has a `T-year` term and an _annualized_ effective market rate of interest of $\bar{r}$. The _fair price_, denoted by $V_{B}$, is the face (par) value discounted to back to today at an effective market interest rate $\bar{r}$:

```{math}
:label: eqn-zero-coupon-bill-bond
V_{B}(\bar{r}) = \mathcal{D}^{-1}_{T,0}(\bar{r})\cdot{V_{P}}
```

The quantity $\mathcal{D}_{T,0}(\bar{r})$ denotes the discount factor governing the period between the auction at `t = 0` and the term of the bill in `t = T years`. 
````

(content:references:US-T-Notes-Bonds)=
## U.S. Treasury Notes and Bonds
[T-notes, or United States Treasury Notes](https://treasurydirect.gov/marketable-securities/treasury-notes/), are debt instruments that provide a stable interest rate every six months until maturity. These notes are offered in terms of `T = 2, 3, 5, 7, and 10 years` and can be bought for more or less than their face (par) value. Upon maturity, the lender receives the entire par value. T-notes are considered coupon debt instruments, which means that the lender receives periodic interest payments based on a coupon rate during the T-note’s lifespan ({numref}`fig-bond-payout-schematic`):

```{figure} ./figs/Fig-Bond-Asset-Timeline-Schematic.svg
---
height: 320px
name: fig-bond-payout-schematic
---
Schematic of the lifetime of a Treasury Bond with semiannual coupon payments. The bond is purchased now and the bondholder receives semi-annual coupon payments until the maturity of the bond T-years into the future. At maturity, the bondholder receives a final coupon payment plus the face value of the bond.    
```

Similar to T-notes, [United States Treasury Bonds](https://treasurydirect.gov/marketable-securities/treasury-bonds/) are a type of debt instrument that provides a fixed interest rate every six months. These bonds are considered long-term, with terms of either 20 or 30 years. Upon maturity of the bond, the holder receives its face value. Bonds can be held until maturity or sold before maturity. 

### Pricing
The price an investor is willing to pay for a claim to the future coupon payments of a Treasury note or bond depends on the future value that will be received versus the discounted face value of the bond ({prf:ref}`defn-fixed-r-bond-pricing`):

````{prf:definition} Fixed Coupon Rate Bond Pricing
:label: defn-fixed-r-bond-pricing

A note or bond has a term of `T-years` and $\lambda$ coupon payments per year. The _fair price_ of the note or bond is the present value of the sum of the future coupon payments $C$ and the discounted face value $V_{P}$:

```{math}
:label: eqn-fixed-r-bond-price-w-coupon
V_{B}(T,\bar{r}) = \mathcal{D}^{-1}_{N,0}(\bar{r})\cdot{V_{P}}+C\cdot\sum_{j=1}^{\lambda{T}}\mathcal{D}_{j,0}^{-1}(\bar{r})
```

The term $\mathcal{D}_{i,0}(\bar{r})$ denotes the discount factor for the period $0\rightarrow{i}$, which can be either a discrete or continuous compounding model. The coupon payment is given by $C=\left(\bar{c}/\lambda\right)\cdot{V_{P}}$, and the interest rate $\bar{r}$ are set at auction. 
````

Let’s use historical auction data from 1975-1979 and the [VLQuantitativeFinancePackage.jl](https://github.com/varnerlab/VLQuantitativeFinancePackage.jl.git) package to compute the historical 30-year treasury bond prices ({prf:ref}`example-treaury-bond-price`).

````{prf:example} Pricing 30-year treasury bonds
:class: dropdown
:label: example-treaury-bond-price

Compute 30-year treasury bond prices from historical auctions held between 1977 and 1979, assuming discrete compounding. 

__Historical data__: The dataset for this example was reproduced from the [Treasury Notes & Bonds Historical Information page on Treasury.gov](https://treasurydirect.gov/auctions/announcements-data-results/announcement-results-press-releases/previous-announcements-and-results/treasury-notes-bonds-historical-information/). The data consists of 30-year treasury bond information (coupon rate, market interest rate, and price) for bonds issued between 1977 and 1979.

__Strategy__

1. First, let's load the historical data set using a `loaddatafile` function, which returns the bond data as a [DataFrame](https://dataframes.juliadata.org/stable/) with the key fields:
    * The `:CouponRate` field holds the data for the coupon interest rate (annualized rate as a percentage)
    * The `:AverageYield` field holds the market rate of interest for the treasury bond (annualized rate as a percentage)
    * The `:AveragePrice` field holds the price data for the 30-year treasury bond
1. Next, we'll compute the treasury bond price for each bond in the data set by iterating through the data set using a `for` loop using the shortcut syntax for creating bond, and compounding models.
1. Last, we'll store the actual and computed prices in a table and calculate the percentage error of the estimate.

```julia

# Assumptions:
# 1. The path_to_data_file is specified
# 2. The short-cut syntax for bond and compounding models is specfied elsewhere
# 3. The loaddatafile function is defined elsewhere

# load external packages
using VLQuantitativeFinancePackage

# load the data set, create a compounding model, and set bond parameters
dataset = loaddatafile(path_to_data_file);
discrete_compounding = DiscreteCompoundingModel();
T,λ,Vₚ = 30.0, 2, 100.0 # years, payments per year, par value
number_of_records = nrow(dataset);

# create an array of bond models, one for each record in the data set
bonds = Array{MyUSTreasuryCouponSecurityModel,1}(undef,number_of_records);
for i ∈ 1:number_of_records
    
    # get the data from the data frame for this record 
    c = dataset[i,:CouponRate]*(1/100); # convert from percentage to decimal
    r̄ = dataset[i,:AverageYield]*(1/100); # convert from percentage to decimal
    
    # build the model, and compute the price using the short-cut syntax
    model = build(MyUSTreasuryCouponSecurityModel, (
            par = Vₚ, T = T, rate = r̄, coupon = c, λ = λ
        )) |> discrete_compounding;
    
    # store the updated model (with computed price)
    bonds[i] = model;
end
```

__Results__: The calculated $\hat{V}_{B}$ and actual $V_{B}$ prices for 30-year treasury bond are shown in the table below. The prices are reported as the percentage of the par value. The actual and computed prices are very close, with the maximum percentage error $\epsilon\ll{0.01}$%.


| date    | c      | r̄     | Vᵦ     | V̂ᵦ     | ϵ   |
|:---------:|:--------:|:-------:|:--------:|:--------:|:-----:|
|  5/8/75 |   8.25 |   8.3 |  99.45 |  99.45 | 0.0 |
|  2/4/77 |  7.625 |  7.63 | 99.941 | 99.941 | 0.0 |
| 11/2/77 |  7.875 |  7.94 | 99.261 | 99.261 | 0.0 |
|  8/3/78 |  8.375 |  8.43 | 99.402 | 99.402 | 0.0 |
| 11/3/78 |   8.75 |  8.86 | 98.851 | 98.851 | 0.0 |
|  5/2/79 |  9.125 |  9.23 | 98.938 | 98.938 | 0.0 |
| 11/1/79 | 10.375 | 10.44 | 99.407 | 99.407 | 0.0 |

The implementation of {prf:ref}`example-treaury-bond-price` in the [VLQuantitativeFinancePackage.jl](https://github.com/varnerlab/VLQuantitativeFinancePackage.jl.git) package gives results consistent with the historical data.

````



(content:references:US-YTM-Defn)=
## Yield to Maturity (YTM)
The Yield to Maturity (YTM) of a treasury note or bond is the [internal rate of return (IRR)](https://en.wikipedia.org/wiki/Internal_rate_of_return) associated with buying and holding the security until its maturity date ({prf:ref}`defn-yield-to-maturity`):

````{prf:definition} Yield to Maturity 
:label: defn-yield-to-maturity

The yield to maturity (YTM) is defined as the effective market interest rate that makes the present value of a bond’s coupon payments and discounted par value equal to its price $V_{B}$:

```{math}
V_{B}(T^{\prime},y) - \mathcal{D}^{-1}_{T,0}(y)\cdot{V_{P}} - C\cdot\sum_{j=1}^{\lambda{T}^{\prime}}\mathcal{D}_{j,0}^{-1}(y) = 0
```

The term $\mathcal{D}_{i,0}(y)$ denotes the discount factor for the period $0\rightarrow{i}$, which can be either a discrete or continuous compounding model, $T^{\prime}$ denotes duration remaining on the note or bond, the coupon payment value is given by $C=\left(\bar{c}/\lambda\right)\cdot{V_{P}}$, and $y$ denotes the yield to maturity of the note or bond.
````

The YTM and the effective market interest rate are the same when the note or bond is initially auctioned in the primary market. However, treasury securities are marketable securities, i.e., they can be resold on a [secondary treasury market](https://www.investopedia.com/articles/bonds/08/treasuries-fed.asp#:~:text=For%20many%20people%2C%20TreasuryDirect%20is,convenience%20and%20liquidity%20than%20TreasuryDirect), even after some coupon payments have been paid out. In such cases, the YTM does not equal the initial market interest rate at auction.

Let's do a yield to maturity calculation for a 5-year treasury note ({prf:ref}`example-ytm-5-year-t-note`):

````{prf:example} Yield to Maturity for 5-Year T-Note
:class: dropdown
:label: example-ytm-5-year-t-note

You purchased a 5-year treasury note with a face value of $V_{P}$ = 100 USD at auction for $V_{B}$ = 96.82 USD. The note has an annual coupon rate of 6%, with semi-annual coupon payments. 

1. Compute the effective annual interest rate $\bar{r}$ at the time of the auction.
1. After holding the note for $T^{\prime}$ years, you sell it on the secondary market for the purchase price. Compute the yield to maturity at the time of the sale on the secondary market.

__Solution__: The yeild to maturity and the annual effective interest rate $\bar{r}$ are equal at the time of auction. Thus, we can compute the effective annual interest rate $\bar{r}$ using {prf:ref}`defn-yield-to-maturity`.

```julia
# load external packages
using VLQuantitativeFinancePackage

# 1. Calculate the YTM for the 5y note at auction
Vₚ, Vᵦ, T, c, λ = 100.0, 96.82, 5.0, 0.06, 2
compounding = DiscreteCompoundingModel();

# build the debt model, we don't know the rate, but we know the price -
model = build(MyUSTreasuryCouponSecurityModel, (
    par = Vₚ, T = T, λ = λ, coupon = c
));
model.price = Vᵦ

# compute the rate by doing a YTM calculation -
estimated_rate = YTM(model, compounding) |> x->round(x,digits=4);
```

This calculation gives an effective annual interest rate of `r̄  = 6.76%`. Now, let's compute the yield to maturity at the time of the sale on the secondary market. Let the number of years the note is held before it is sold on the secondary market be `ΔT = 0.0,1.0,2.0,3.0, and 4.0 years`.

__Strategy__:

1. First we set up a holding time array `ΔT`, set the note parameters and then initialize some storage for the  yield to maturity values. 
1. Next, we process each element in the `ΔT` array using a `for` loop. For each pass through the loop:
    * We compute the remaining time on the note (store this value in the $\hat{T}$ variable), set the price, and then compute the yield to maturity by calling the `YTM(...)` function
1. Finally, we store the yield to maturity value in the `YTM_value_array` array.


```julia
# load external packages
using VLQuantitativeFinancePackage

# 2. Calculate the YTM for the 5y note at auction
Vₚ, Vᵦ, T, c, λ = 100.0, 96.82, 5.0, 0.06, 2;
ΔT = [0.0,1.0,2.0,3.0,4.0];
YTM_value_array = Array{Float64,1}(undef, length(ΔT));
counter = 0;
for T′ ∈ ΔT 
    
    # update the counter -
    global counter += 1
    
    # how much time is left on the security?
    T̂ = T - T′
    
    # build a bond model, we don't know the rate, but we know the price. 
    ytm_model = build(MyUSTreasuryCouponSecurityModel, (
        par = Vₚ, T = T̂, λ = λ, coupon = c
    ));
    ytm_model.price = Vᵦ
    
    # We compute the yeild and store in the YTM_value_array
    YTM_value_array[counter] = YTM(ytm_model, compounding)
end
```

__Results__: The table below shows the yield to maturity at the time of sale of the note on the secondary market. 

| ΔT (y) | R (y)   | Vₚ (USD)   | Vᵦ (USD)   | c    | YTM (%)   |
|-----|-----|-------|-------|------|--------|
| 0.0 | 5.0 | 100.0 | 96.82 | 0.06 | 6.7601 |
| 1.0 | 4.0 | 100.0 | 96.82 | 0.06 | 6.9238 |
| 2.0 | 3.0 | 100.0 | 96.82 | 0.06 | 7.1974 |
| 3.0 | 2.0 | 100.0 | 96.82 | 0.06 | 7.7469 |
| 4.0 | 1.0 | 100.0 | 96.82 | 0.06 | 9.4061 |

* When the time to maturity decreases and the price remains fixed, the yield to maturity for a treasury note increases. 
* This is logical since the note always pays its face value at maturity. Therefore, if the new owner acquires the note at the same price as the initial buyer, they will receive the face value (as well as the remaining coupon payments) over a shorter period.

````


---

## Summary
In this lecture we introduced Treasury, Bills, Notes, and Bonds, and we discussed the relationship between the coupon rate, the interest rate, and the price of the security. We also introduced the Yield to Maturity (YTM) and the relationship between the YTM and the market interest rate.

* [U.S. Treasury Bills](content:references:US-T-Bills) are short-term debt securities with a maturity of less than one year. [Treasury Notes and Bonds](content:references:US-T-Notes-Bonds) are long-term debt securities with a maturity of two to thirty years.

* [The Yield to Maturity (YTM)](content:references:US-YTM-Defn) is a measure of the _return_ of a bond investment. Yield to maturity is the discount rate that equates the present value of a bond's cashflows to its price.