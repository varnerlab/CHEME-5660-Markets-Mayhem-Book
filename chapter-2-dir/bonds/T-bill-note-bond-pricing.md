# The Pricing of Treasury Bills, Notes and Bonds

---
```{topic} Learning Objectives
Fill me in.
```
---

## Introduction
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

---

## Summary
Fill me in.