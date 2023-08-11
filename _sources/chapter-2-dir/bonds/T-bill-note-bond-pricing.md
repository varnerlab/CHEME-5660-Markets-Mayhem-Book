(content:references:bond-pricing-relationships)=
# Treasury Security Pricing Dynamics and Risks
U.S. Treasury debt is often taken to be a risk-free asset. However, the price of a bill, note, or bond can change over its term because of changes in interest rates. Moreover, the issuer of a bond could default on their repayment obligation. Thus, there is interest rate and credit risk associated with these instruments. 

```{topic} Outline
In this lecture, we discuss the pricing dynamics and risks of U.S. Treasury securities. We will first discuss the interest rate risk of zero-coupon treasury securities and coupon-bearing treasury securities. Then, we will discuss the credit risk of treasury securities.

* [Interest rate risk for zero-coupon treasury securities](content:references:zc-pricing-relationships-interest-rate-risk) is the risk that the price of zero-coupon treasury security will change due to changes in the market interest rate. 

* [Interest rate risk for coupon-bearing treasury securities](content:references:cb-pricing-relationships-interest-rate-risk) is the risk that the price of coupon-bearing treasury security will change due to changes in the market interest rate. In particular, we will discuss Malkiel’s bond-pricing guidelines, which govern the relationship between the price of coupon-bearing treasury security and the market interest rate under different market conditions and the security duration.

* [Credit risk for treasury securities](content:references:credit-risk-treasury-securities) is the risk that the U.S. government will default on its debt obligations. We will discuss the credit risk of treasury securities and how it is reflected in the price of these securities.
```

---

(content:references:zc-pricing-relationships-interest-rate-risk)=
## Zero-coupon Interest Rate Risk
The price of a zero-coupon treasury bill $V_{B}$ with a duration of `T` years is computed with respect to an effective market interest rate $\bar{r}$ on the day the bill is purchased. However, interest rates $\bar{r}$ vary with time and economic conditions ({numref}`fig-bill-daily-interest-rate`):


```{figure} ./figs/Fig-4-week-Daily-2022.svg
---
height: 420px
name: fig-bill-daily-interest-rate
---
Daily interest rate quotations for 2022 download from [Treasury.gov](https://home.treasury.gov/resource-center/data-chart-center/interest-rates/TextView?type=daily_treasury_bill_rates&field_tdr_date_value_month=202305). These rates are secondary market quotations on 4-week treasury bills, assuming a 360-day year,  computed at approximately 3:30 PM each business day by the [Federal Reserve Bank of New York](https://www.newyorkfed.org).
```

Thus, the market price of a treasury bill for the same par value and duration can change over its term because of changes in interest rates ({prf:ref}`example-zero-coupon-t-bill`):

````{prf:example} Pricing of a zero-coupon treasury bill
:class: dropdown
:label: example-zero-coupon-t-bill

Compute the fair price for a zero-coupon treasury bill with a par value of \$1,000, and a T = 26- and 52-week duration _assuming_ the effective market interest rate $\bar{r}$ is given by the 2022 values shown on {numref}`fig-bill-daily-interest-rate`.

__Solution__:
The fair price for a zero-coupon treasury bill $V_{B}$ is the future face (par) value $V_{P}$ of the bill discounted at $\bar{r}$ to the time of the purchase (current dollars):

$$V_{B} = \mathcal{D}^{-1}_{T,0}(\bar{r})\cdot{V_{P}}$$

where $\mathcal{D}_{T,0}$ is the discount factor for a zero-coupon treasury bill with a duration of `T` years. We can compute the price using the following [Julia](https://julialang.org/) code (which assumes continuous compounding):

```julia

# Assumptions:
# 1. The interest rate data is stored in the array r̄ (as a percentage). 
# 2. We have number_of_days days of interest rate data (from first to last day of the year).

# Define the compounding model -
𝒟(r̄,T) = exp(r̄*T);

# initialize variables
T₁ = (26/52);   # T = 0.5 yr or 26 weeks
T₂ = (52/52);   # T = 1 yr or 52 weeks
Vₚ = 1000.0;    # par value of the treasury bill

# main loop
price_array = Array{Float64,2}(undef, length(r̄), 2)
for i in 1:number_of_days
    rvalue = (1/100)*r̄[i];
    price_array[i,1] = (1/𝒟(rvalue,T₁))*Vₚ;
    price_array[i,2] = (1/𝒟(rvalue,T₂))*Vₚ;
end
```

Computing the price $V_{B}$ as a function of $\bar{r}$ gives ({numref}`fig-zcbill-price`):

```{figure} ./figs/Fig-Price-Zero-Coupon-Bill.svg
---
height: 400px
name: fig-zcbill-price
---
Price of a zero coupon treasury bills for terms of T = 26 weeks (light blue) and T = 52 weeks (dark blue) as a function of the historical market interest rate for 2022. The face value $V_{P}$ = 1000 USD for each T-bill. 
```
````

The example treasury bill pricing calculations shown in {prf:ref}`example-zero-coupon-t-bill` have some interesting properties:

* There is an _inverse_ relationship between the current price of a zero-coupon bill and the market interest rate $\bar{r}$; this must be true as the par value (which is in future dollars) is fixed. Thus, higher market interest rates imply lower initial T-bill prices. 

* The longer duration treasury bills are more sensitive to interest rate changes that shorter duration bills, i.e., the T = 52 week T-bill price is more sensitive to changes in $\bar{r}$ than the T = 26 week T-bill price. This is because the longer duration T-bill has a longer time to maturity, and thus, more time for the market interest rate to change.

(content:references:cb-pricing-relationships-interest-rate-risk)=
## Malkiel’s bond-pricing guidelines
Bond investors have two actions open to them: hold the bond until maturity (and collect the coupon payments along the way), or resell the bond (and potentially benefit from a change in the bond price). The latter is possible because after the bonds are issued, bondholders may buy or resell bonds in secondary bond markets. In these markets, bond prices fluctuate inversely with the market interest rate $\bar{r}$. Thus, interest rate fluctuations are the main source of risk to the bondholder if they are not holding the bound to maturity.

```{figure} ./figs/Fig-Sensitivity-Bond-Price-Interest-Rate.svg
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

(content:references:credit-risk-treasury-securities)=
## Credit Risk of Treasury Securities
Fill me in.

---

## Summary
Fill me in.