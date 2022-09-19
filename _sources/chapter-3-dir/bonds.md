# Fixed Income Debt Securities

## Introduction
Fixed-income securities are financial instruments with predefined cashflows at selected dates over the lifetime of the instrument. While there are several types of fixed-income securities, we'll focus on an archetypal category: [United States Treasury Debt Securities](https://www.investor.gov/introduction-investing/investing-basics/glossary/treasury-securities). Treasury debt securities, e.g., [Treasury bills, notes, and bonds](https://www.treasurydirect.gov/indiv/products/prod_tbonds_glance.htm), are debt obligations issued by the United States Department of the Treasury to holder of the security. U.S. Treasury debt securities are a mechanism used by the United States government to borrow money, from bondholders, with a fixed set of repayment terms. 

Treasury debt securities are viewed as one of the safest possible investments, e.g., defacto risk-free, because Treasury debt securities are backed by the full faith and credit of the United States government. [The U.S. government has never defaulted on its debt obligations (at least in recent memory)](https://thehill.com/opinion/finance/575722-the-us-has-never-defaulted-on-its-debt-except-the-four-times-it-did/).  

In this lecture, we will discuss:

* The definition and valuation of {ref}`content:references:treasury-bonds`
* Introduce {ref}`content:references:bond-pricing-relationships`


---

```{figure} ./figs/Fig-Govt-Debt-Schematic.pdf
---
height: 340px
name: fig-bill-notes-bonds-schematic
---
Schematic of United States Treasury debt instruments. The treasury borrows money from bondholders by selling treasury bills, notes, and bonds. Each debt instrument has a particular repayment plan, e.g., a specified duration and payment schedule.   
```

(content:references:treasury-bonds)=
## Treasury Bills, Notes and Bonds
A fixed-income debt security is a contract between a borrower and a lender. In the context of this lecture, we'll focus on U.S. Treasury Bills, Notes, and Bonds, examples of government debt securities. For United States treasury debt instruments, the borrower is the U.S. government; the government issues (i.e., sells) a bond to a lender (you) for some cash. This arrangement obligates the U.S. Treasury to make specified payments to the bondholder (you) on specified dates over the lifetime of the instrument ({numref}`fig-bill-notes-bonds-schematic`).

There are many types of U.S. government debt securities. However, the various debt instruments share several similarities:

* U.S. Treasury debt securities have specified term lengths, meaning the duration of the borrowing contract between the borrower and the lender is fixed. 
* U.S. Treasury debt securities have a par value, i.e., the face value of the instrument, a price (which may not be the same as the par value), and an interest rate paid to the lender.
* U.S. Treasury debt securities have interest payments (historically called coupons) which pay the lender a specified amount of cash on a fixed schedule over the term of the debt instrument. 
* Interest income from U.S. Treasury debt securities is exempt from state and local income taxes but subject to federal income taxes.
* You can buy U.S Treasury debt (meaning lend money to the U.S. government) directly from the [United States Treasury via TreasuryDirect](https://www.treasurydirect.gov/indiv/products/prod_tbonds_glance.htm) or through a bank or broker.



```{figure} ./figs/Fig-Zero-Coupon-Schematic.pdf
---
height: 360px
name: fig-bill-payout-schematic
---
Schematic of a zero-coupon United States Treasury Bill (T-bill). The bondholder purchases the T-bill for $V_{B}$ USD (current). At the term of the T-bill, the treasury pays the bondholder the face (par) value of the T-bill.    
```

### Treasury Bills
Treasury bills (also called T-bills) are short-term debt instruments sold in terms ranging from a few days to 52 weeks ({numref}`fig-bill-payout-schematic`). Treasury bills are issued for terms of 4, 8, 13, 26, and 52 weeks; 4-week, 8-week, 13-week, 26-week, and 52-week T-bills are auctioned on a regular schedule. 

#### Pricing of U.S. Treasury Bills
T-bills are an example of a zero-coupon fixed-income instrument; thus, T-bills do not make coupon payments during the bill term. Instead, T-bills are priced, so the bondholder receives the par value at the bond’s duration. T-bills are typically sold at a discount from the par amount; rarely are they sold at a price equal to the par amount:

````{prf:definition} Zero Coupon Rate Bond Pricing
:label: defn-zero-coupon-bond-pricing

Let a zero-coupon treasury bill (T-bill) have a T-year term with an annual market interest rate of $\bar{r}$. Then, the _fair price_ for a zero-coupon treasury bill is the future face (par) value of the bill discounted to today by the market interest rate $\bar{r}$:

```{math}
:label: eqn-zero-coupon-bill-bond
V_{B} = \frac{V_{P}}{\left(1+\bar{r}\right)^{T}}
```

where $V_{B}$ denotes the price of the treasury bill, and $V_{P}$ represents the face (par) value of the treasury bill. 
````

The price of the bill $V_{B}$ is computed with respect to a particular value of the market interest rate $\bar{r}$ on the day the T-bill is purchased. However, the market interest rate $\bar{r}$ may vary over the T-bill term; hence, the market price of the T-bill can change over its term. Let's do an example illustrating the pricing of a zero-coupon treasury bill ({prf:ref}`defn-zero-coupon-bond-pricing`).


````{prf:example} Pricing of a Treasury Bill
:label: example-zero-coupon-t-bill

Compute the fair price for a zero-coupon treasury bill with a par value of \$1,000 and T = 26-week and T = 52-week duration as a function of annualized market interest rate $\bar{r}$. 

The fair price for a zero-coupon treasury bill, denoted by $V_{B}$, is the future par value $V_{P}$ of the bill discounted to the time of the purchase:

$$V_{B} = \frac{V_{P}}{\left(1+\bar{r}\right)^{T}}$$

Solving this expression as a function of $\bar{r}$ for different values of the bill term parameter $T$ gives the results shown in {numref}`fig-zcbill-price`:

```{figure} ./figs/Fig-Price-Zero-Coupon-Bill.pdf
---
height: 400px
name: fig-zcbill-price
---
Price of a zero coupon treasury bill for a term of 0.5 (dark blue) and 1 year (light blue) as a function of the market interest rate. Face value $V_{P}$ = 1000 USD.
```

__source__: [Live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [a static HTML view](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-Price-ZeroCoupon-TreasuryBill.jl.html).
````


The treasury bill pricing calculations shown in {prf:ref}`example-zero-coupon-t-bill` have some interesting properties:

* There is an _inverse_ relationship between the current price of a zero-coupon bill and the market interest rate $\bar{r}$; this must be true as the par value (which is in future dollars) is fixed. Thus, higher market interest rates imply lower initial T-bill prices. 

* The relationship between $V_{B}$ and $\bar{r}$ is _not_ linear (dashed versus solid lines); even though it may appear to be the case from the parameters used in the example, the relationship between price and interest rate is convex

* Finally, the longer duration treasury bills are more sensitive to interest rate changes; the T = 1-year slope is larger than the T = 0.5-year case.

Thus, the duration and the risk-free interest rate are critical to the pricing of the treasury bill. However, what is the risk-free market interest rate?

````{prf:remark} What is the Risk-free Market Interest Rate?
:label: remark-market-interest-rate

The present value calculation for a treasury bond depends upon the discount rate, which we assume is the risk-free market interest rate, denoted by $\bar{r}$. However, what is the risk free market interest rate for a bond?

 The risk-free market interest rate is the sum of (at least) two terms: the real risk-free rate of return $\bar{r}^{\circ}_{f}$ and a premium paid above the real rate to compensate for expected inflation $\bar{r}_{I}$: 

```{math}
\bar{r} = \bar{r}^{\circ}_{f}+\bar{r}_{I}+\dots
```

where $\bar{r}^{\circ}_{f}$ denotes the real risk-free rate and $r_{I}$ denotes a premium above the real-risk free rate, which accounts for inflation risk; the $\bar{\star}$ notation represents the assumption of a constant rate over the bond term. In addition to inflation risk, there can (potentially) be additional terms to compensate the bond buyer for other expected risks. 
````

### Treasury Notes and Bonds
Treasury notes, sometimes called T-notes, are a medium-term debt instrument that earns a fixed rate of interest every six months until maturity. T-notes are issued in terms of 2, 3, 5, 7, and 10 years. The price of a T-note can be greater than, less than, or equal to the T-note's par value. However, at maturity, the par value of the T-note is paid to the owner of the T-note (lender). 

T-notes are an example of a non-zero coupon debt instrument; thus, the lender receives periodic interest payments, called coupon payments which are proportional to the coupon rate, over the lifetime of the T-note.

```{figure} ./figs/Fig-Bond-Asset-Timeline-Schematic.pdf
---
height: 320px
name: fig-bond-payout-schematic
---
Schematic of the lifetime of a Treasury Bond with semiannual coupon payments. The bond is purchased now (t=0). The bondholder receives semi-annual coupon payments until the maturity of the bond T years in the future. At maturity (t = T), the bondholder receives a final coupon payment plus the face value of the bond.   
```

Similar to T-notes, treasury bonds are also a coupon debt instrument. However, treasury bonds are long-term U.S Treasury debt instruments. Treasury bonds pay a fixed rate of interest (the coupon rate) every six months until the bond's maturity ({numref}`fig-bond-payout-schematic`). The U.S. Treasury issues bonds with terms of 20 or 30 years. When a bond matures, the bondholder receives the face value of the bond. Bonds can be held until maturity or sold before maturity. 

When a U.S. Treasury bond matures, the U.S government repays the debt by paying the bond's par (or face) value. The bond's coupon rate determines the interest payment: the annual payment is the coupon rate times the bond's par value. The coupon rate, maturity date, and par value of the bond are part of the contract between the issuer, the U.S. government, and the bondholder (you).

#### Pricing of U.S. Treasury Bonds
A bond’s coupon payments, and the eventual repayment of the face value, occurs many years in the future. Thus, the price an investor is willing to pay for a claim to those payments depends on the future value of the dollars that will be received versus the present value of the face value of the bond. 

````{prf:definition} Fixed Coupon Rate Bond Pricing
:label: defn-fixed-r-bond-pricing

Let the term of a bond be T-years with semi-annual coupon payments (N = 2T coupon payments over the term of the bond), with an annual coupon rate of $\bar{c}$, and an annual market interest rate of $\bar{r}$. 

Then, the _fair price_ for the bond, denoted by $V_{B}$, is the present value of coupon payments $C$ plus the discounted par value $V_{P}$ of the bond:

```{math}
V_{B} = \frac{V_{P}}{\left(1+i\right)^{N}}+\sum_{j=1}^{N}\frac{C}{\left(1+i\right)^{j}}
```

where $i=\bar{r}/2$ is set by the market at the time when the bond is purchased, and $C=\left(\bar{c}/2\right)\cdot{V_{P}}$. If $\bar{c}=\bar{r}$, the fair price equals the par value i.e., $V_{B} = V_{P}$.
````

Let's do an example illustrating bond pricing ({prf:ref}`defn-fixed-r-bond-pricing`).

````{prf:example} Pricing T = 30 year Treasury Bond
:label: example-treaury-bond-price

Compute the price of a bond with a T = 30-year term and a par value of $V_{P}$ = \$1000 for different combinations of the interest rate $\bar{r}$ and coupon rate $\bar{c}$ of the bond. In particular, 
1. The interest rate $\bar{r}$ equals to the coupon rate $\bar{c}$; let $\bar{c}=8\%$ and $\bar{r}=8\%$
1. The interest rate $\bar{r}$ is larger than the coupon rate $\bar{c}$; let $\bar{c}=8\%$ and $\bar{r}=10\%$
1. The interest rate $\bar{r}$ is smaller than the coupon rate $\bar{c}$; let $\bar{c}=8\%$ and $\bar{r}=6\%$

The price of the bond is given by {prf:ref}`defn-fixed-r-bond-pricing`. A 30-year term gives 60 semi-annual coupon payments. Substituting the values for $\bar{r}$, $\bar{c}$ and the number of payements into the pricing equation gives:

| Case | $\bar{r}$ (\%) | $\bar{c}$ (\%) | $V_{P}$ (USD) | $V_{B}$ (USD) |
| :----: | :---------: | :---------: | :-------: | :-------: |
| 1    | 8       | 8       | 1000    | 1000    |
| 2    | 10      | 8       | 1000    | 810.71  |
| 3    | 6       | 8       | 1000    | 1276.76 |


__source__: [Live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [a static HTML view](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-Price-TreasuryBond.jl.html).
````


#### Yield to Maturity of U.S. Treasury Bonds
U.S. Treasury bonds often do not sell for their par value i.e., the market interest rate $\bar{r}\neq\bar{c}$. However, assuming the U.S. government does not default on its debt obligations, U.S Treasury bonds will eventually mature to the par value over the bond term. 

Let’s develop a metric called yield to maturity (YTM) which measures the rate of return of a bond; the YTM accounts for both the current income generated by the coupon payments and the price increase or decrease over the bond term. The YTM is the standard measure of the total rate of return of the fixed-income security. 

Typically, investors purchasing U.S. Treasury bonds are not quoted an overall rate of return. Instead, 
investors must calculate this value from the bond price, maturity date, and coupon payments. The yield to maturity (YTM) is defined as the interest rate that makes the present value of a bond’s payments equal to its price:

````{prf:definition} Yield to Maturity 
:label: defn-yield-to-maturity

Let the term of a bond be T-years with semi-annual coupon payments (N = 2T coupon payments over the term of the bond), with an annual coupon rate of $\bar{c}$. Further, suppose the U.S. Treasury bond was purchased for $\hat{V}_{B}$ (which may be different that the _fair price_).

The yield to maturity (YTM) value is the interest rate $\bar{r}$ that makes $V_{B}=\hat{V}_{B}$:

```{math}
\hat{V}_{B} - \frac{V_{P}}{\left(1+i\right)^{N}}-\sum_{j=1}^{2T}\frac{C}{\left(1+i\right)^{j}} = 0
```

where $i=\bar{r}/2$ is set by the market at the time of purchase of the bond, and $C=\left(\bar{c}/2\right)\cdot{V_{P}}$.

````

##### Example
* Let's do an example illustrating the Yield to Maturity (YTM) calculation ({prf:ref}`defn-yield-to-maturity`). Sources: [Live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [static HTML](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-YieldToMaturity-TreasuryBond.jl.html).


### Sensitivity of Bond Prices to Interest Rate Changes
Bond investors have two actions open to them: hold the bond until maturity (and collect the coupon payments along the way), or resell the bond (and potentially benefit from a change in the bond price). The latter is possible because after the bonds are issued, bondholders may buy or resell bonds in secondary bond markets. In these markets, bond prices fluctuate inversely with the market interest rate $\bar{r}$. Thus, interest rate fluctuations are the main source of risk to the bondholder if they are not holding the bound to maturity.

```{figure} ./figs/Fig-Sensitivity-Bond-Price-Interest-Rate.pdf
---
height: 400px
name: fig-bond-price-sensitivity
---
Sensitivity of bond price to changes in the market interest rate.   
```

(content:references:bond-pricing-relationships)=
#### Malkiel’s bond-pricing rules
The relationship between the price of a bond, and the yeild (i.e., the market interest rate $\bar{r}$) was previously
studied by Malkiel {cite}`Malkiel1962`. The so-called Malkiel’s bond-pricing rules are demonstrated by the simulations shown in ({numref}`fig-bond-price-sensitivity`):

1. The price of a U.S. Treasury Bond _increases_ as the market interest rate $\bar{r}$ _decreases_; thus, there is an _inverse_ relationship between the bond yield to maturity (i.e., the market rate $\bar{r}$) and the price of the bond $V_{B}$. 
1. Changes in price as a function of changes in the interest rate are not symmetric;
an increase in a bond’s interest rate $\bar{r}$ results in a _smaller price change_ than a decrease in $\bar{r}$ of equal magnitude. For example, consider Case II in ({numref}`fig-bond-price-sensitivity`); a 50% decrease in $\bar{r}$ increases the price of this bond by approximately 75%, while a 50% increase in $\bar{r}$ decreases the bond price approximately 30%.
1. Prices of long-term bonds are more sensitive to interest rate changes than short-term bonds. For example, consider Case I and Case II in ({numref}`fig-bond-price-sensitivity`); Case I (short-term bond) is _less sensitive_ to the same magnitude change in $\bar{r}$ compared with Case II (long-term bond).
1. Interest rate risk is inversely related to a bond’s coupon rate. Prices of low coupon-rate bonds are more sensitive to changes in interest rates than prices of high-rate coupon bonds. For example, compare Case II and III in ({numref}`fig-bond-price-sensitivity`); case III (the low coupon-rate bond) is significanly more sensitive to decreases in interest rate compared with case II (the high coupon-rate bond). A similar, albeit less pronounced, trend is visible for increased
interest rate.

## Are United States Treasury Bills, Notes or Bonds really risk free?
Fill me in.

---
 
## Summary
In this lecture, we introduced fixed-income debt securities. Fixed-income debt securities are contracts between a borrower and a lender that regulate the repayment of a debt. Here we focused on an archetypal category of fixed-income debt security: [United States Treasury Securities](https://www.investor.gov/introduction-investing/investing-basics/glossary/treasury-securities). In particular, we:

* Introduced the definition of {ref}`content:references:treasury-bonds`
* Developed tools to compute the fair price of an N-coupon Treasury Bills/Notes/Bonds as a function of the par-value, market interest rate, coupon rate and instrument term.
* Introduced {ref}`content:references:bond-pricing-relationships`; Malkiel’s rules describe the sensitivity of bond price to changes in market interest rates as a function of other bond parameters such as coupon rate and term. 