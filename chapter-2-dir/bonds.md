# Fixed Income Debt Securities

Fixed-income securities offer predetermined cashflows on specific dates. One classic example is United States Treasury Debt Securities, which represent debt obligations issued by the U.S. Department of the Treasury. These securities are considered safe investments due to their risk-free nature and the full faith and credit of the United States government backing them. The U.S. government has never defaulted on its debt obligations.

<!-- Fixed-income securities are financial instruments with predefined cashflows at selected dates over the lifetime of the instrument. While there are several types of fixed-income securities, we'll focus on an archetypal category: [United States Treasury Debt Securities](https://www.investor.gov/introduction-investing/investing-basics/glossary/treasury-securities). Treasury debt securities, e.g., [Treasury bills, notes, and bonds](https://www.treasurydirect.gov/indiv/products/prod_tbonds_glance.htm), are debt obligations issued by the United States Department of the Treasury to holder of the security. U.S. Treasury debt securities are a mechanism used by the United States government to borrow money, from bondholders, with a fixed set of repayment terms. Treasury debt securities are viewed as one of the safest possible investments, e.g., defacto risk-free, because Treasury debt securities are backed by the full faith and credit of the United States government. [The U.S. government has never defaulted on its debt obligations (at least in recent memory)](https://thehill.com/opinion/finance/575722-the-us-has-never-defaulted-on-its-debt-except-the-four-times-it-did/).   -->


```{topic} Outline
* {ref}`content:references:treasury-bonds` are fixed-income securities issued by the US government to fund its operations and meet financial obligations. Treasury bills have a short-term maturity of less than a year, while Treasury notes and bonds have longer maturities ranging from two to thirty years. These securities are regarded as some of the safest investment options globally, backed by the US government’s full faith and credit.

* {ref}`content:references:bond-pricing-relationships` are utilized to determine the equitable value of a bond, considering its maturity, coupon rate, and current market interest rates. As per Malkiel’s guidelines, the bond’s price will fluctuate inversely with changes in interest rates. Long-term bonds will be more affected than short-term bonds. 

* {ref}`content:references:term-structure-of-interest-rates` describes the correlation between fixed-income security interest rates and their maturity period. This concept represents the market’s outlook on future interest rates. The shape of the term structure - whether it’s upward-sloping, flat, or inverted - offers valuable insights into the economy’s present and potential future state. 

```

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
A fixed-income debt security is a contract between a borrower and a lender. United States treasury bills, notes, and bonds are examples of government debt securities. For United States treasury debt instruments, the borrower is the U.S. government; the government issues (i.e., sells) a bond to a lender (you) for some cash. This arrangement obligates the U.S. Treasury to make specified payments to the bondholder (you) on specified dates over the lifetime of the instrument ({numref}`fig-bill-notes-bonds-schematic`).

There are many types of U.S. government debt securities. However, the various debt instruments share several similarities:

* U.S. Treasury debt securities have specified term lengths, meaning the duration of the borrowing contract between the borrower and the lender is fixed. 
* U.S. Treasury debt securities have a par value, i.e., the face value of the instrument, a price (which may not be the same as the par value), and an interest rate paid to the lender.
* U.S. Treasury debt securities have interest payments (historically called coupons) which pay the lender a specified amount of cash on a fixed schedule over the term of the debt instrument. 
* Interest income from U.S. Treasury debt securities is exempt from state and local income taxes but subject to federal income taxes.
* You can buy U.S Treasury debt (meaning lend money to the U.S. government) directly from the [United States Treasury via TreasuryDirect](https://www.treasurydirect.gov/indiv/products/prod_tbonds_glance.htm) or through a bank or broker.



```{figure} ./figs/Fig-Zero-Coupon-Schematic.pdf
---
height: 320px
name: fig-bill-payout-schematic
---
Schematic of a zero-coupon United States Treasury Bills. The holder purchases the bill for $V_{B}$ (current). At the term of the bill, the treasury pays the bondholder the face (par) value of the bill $V_{P}$.    
```

### Treasury Bills
T-bills, or Treasury bills, are debt instruments with short-term maturity periods ranging from a few days to 52 weeks ({numref}`fig-bill-payout-schematic`). T-bills are zero-coupon fixed-income investments, i.e., they are no coupon payments during their term. Instead, bills are priced so that the bill-holder receives the par value at the end of the term ({prf:ref}`defn-zero-coupon-bond-pricing`): 

````{prf:definition} Zero Coupon Bond Pricing
:label: defn-zero-coupon-bond-pricing

A zero-coupon treasury bill (T-bill) has a T-year term with an annual market interest rate of $\bar{r}$. The fair price of a zero-coupon treasury bill is the future face (par) value of the bill discounted to today by the market interest rate $\bar{r}$:

```{math}
:label: eqn-zero-coupon-bill-bond
V_{B} = \frac{V_{P}}{\left(1+\bar{r}\right)^{T}}
```

The quantity $V_{B}$ denotes the current price of the treasury bill, and $V_{P}$ represents the face (par) value of the treasury bill.  Treasury bills are issued for specific periods, such as 4, 8, 13, 26, and 52 weeks, and are auctioned off regularly. 
````

The price of the bill $V_{B}$ is computed with respect to a value of the market interest rate $\bar{r}$ on the day the bill is purchased. However, the market interest rate $\bar{r}$ varies; hence, the market price of the bill can change over its term ({prf:ref}`example-zero-coupon-t-bill`):


````{prf:example} Pricing of a Treasury Bill
:class: dropdown
:label: example-zero-coupon-t-bill

Compute the fair price for a zero-coupon treasury bill with a par value of \$1,000 and T = 26-week and T = 52-week duration as a function of annualized market interest rate $\bar{r}$. 

The fair price for a zero-coupon treasury bill, denoted by $V_{B}$, is the future face (par) value $V_{P}$ of the bill discounted at $\bar{r}$ to the time of the purchase (current dollars):

$$V_{B} = \frac{V_{P}}{\left(1+\bar{r}\right)^{T}}$$

Solving this expression as a function of $\bar{r}$ for different values of the T-bill term $T$ gives the results shown in {numref}`fig-zcbill-price`:

```{figure} ./figs/Fig-Price-Zero-Coupon-Bill.pdf
---
height: 400px
name: fig-zcbill-price
---
Price of a zero coupon treasury bill for a term of 0.5 (dark blue) and one year (light blue) as a function of the market interest rate. Face value $V_{P}$ = 1000 USD.
```

The treasury bill pricing calculations shown in {prf:ref}`example-zero-coupon-t-bill` have some interesting properties:

* There is an _inverse_ relationship between the current price of a zero-coupon bill and the market interest rate $\bar{r}$; this must be true as the par value (which is in future dollars) is fixed. Thus, higher market interest rates imply lower initial T-bill prices. 

* The relationship between $V_{B}$ and $\bar{r}$ is _not_ linear (dashed versus solid lines); even though it may appear to be the case from the parameters used in the example, the relationship between price and interest rate is convex

* Finally, the longer duration treasury bills are more sensitive to interest rate changes; the T = 1-year slope is larger than the T = 0.5-year case.

````

### Treasury Notes and Bonds
T-notes, also known as Treasury notes, are debt instruments that offer a fixed interest rate every six months until they reach maturity. They are available in 2, 3, 5, 7, and 10-year terms. The price of a T-note can be more or less than its par value, but when it matures, the lender receives the full par value. T-notes are coupon debt instruments, meaning that the lender gets regular interest payments that correspond to a coupon rate throughout the T-note’s life ({numref}`fig-bond-payout-schematic`):

```{figure} ./figs/Fig-Bond-Asset-Timeline-Schematic.pdf
---
height: 320px
name: fig-bond-payout-schematic
---
Schematic of the lifetime of a Treasury Bond with semiannual coupon payments. The bond is purchased now and the bondholder receives semi-annual coupon payments until the maturity of the bond T-years into the future. At maturity, the bondholder receives a final coupon payment plus the face value of the bond.    
```

Treasury bonds, like T-notes, are debt instruments that pay a fixed rate of interest every six months. However, treasury bonds are long-term U.S. Treasury debt instruments with terms of 20 or 30 years. When a bond reaches maturity, the bondholder receives the bond’s face value. Bonds can be held until maturity or sold before maturity. 

#### Pricing of U.S. Treasury Bonds
A bond’s coupon payments, and the eventual repayment of the face value, occurs many years in the future. Thus, the price an investor is willing to pay for a claim to those payments depends on the future value of the dollars that will be received versus the present value of the face value of the bond 
({prf:ref}`defn-fixed-r-bond-pricing`):

````{prf:definition} Fixed Coupon Rate Bond Pricing
:label: defn-fixed-r-bond-pricing

Let the term of a bond be T-years with semiannual ($\lambda = 2$) coupon payments per year; $N = \lambda{T}$ coupon payments over the bond term. Further, let $\bar{c}$ denote the annual coupon rate, and $\bar{r}$ denote the annual market interest rate. Then, the _fair price_ for the bond $V_{B}$ is the present value of coupon payments $C$ plus the discounted par value $V_{P}$ of the bond:

```{math}
V_{B} = \frac{V_{P}}{\left(1+i\right)^{N}}+\sum_{j=1}^{N}\frac{C}{\left(1+i\right)^{j}}
```

The coupon payment $C=\left(\bar{c}/\lambda\right)\cdot{V_{P}}$ is set when the bond is purchased, and the market interest rate $i=\bar{r}/\lambda$ varies with the market. The contract between the U.S. government, the issuer, and the bondholder (you) includes the bond’s coupon rate, maturity date, and par value.
````

Let's do an example illustrating bond pricing ({prf:ref}`defn-fixed-r-bond-pricing`).

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


#### Yield to Maturity of U.S. Treasury Bonds
U.S. Treasury bonds often do not sell for their par value i.e., the market interest rate $\bar{r}\neq\bar{c}$. However, assuming the U.S. government does not default on its debt obligations, U.S Treasury bonds will eventually mature to the par value over the bond term. 

Let’s develop a metric called yield to maturity (YTM) which measures the rate of return of a bond; the YTM accounts for both the current income generated by the coupon payments and the price increase or decrease over the bond term. The YTM is the standard measure of the total rate of return of the fixed-income security. 

Typically, investors purchasing U.S. Treasury bonds are not quoted an overall rate of return. Instead, 
investors must calculate this value from the bond price, maturity date, and coupon payments. The yield to maturity (YTM) is defined as the interest rate that makes the present value of a bond’s payments equal to its price:

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


### Sensitivity of Bond Prices to Interest Rate Changes
Bond investors have two actions open to them: hold the bond until maturity (and collect the coupon payments along the way), or resell the bond (and potentially benefit from a change in the bond price). The latter is possible because after the bonds are issued, bondholders may buy or resell bonds in secondary bond markets. In these markets, bond prices fluctuate inversely with the market interest rate $\bar{r}$. Thus, interest rate fluctuations are the main source of risk to the bondholder if they are not holding the bound to maturity.

```{figure} ./figs/Fig-Sensitivity-Bond-Price-Interest-Rate.pdf
---
height: 420px
name: fig-bond-price-sensitivity
---
Sensitivity of bond price to changes in the market interest rate.   
```

(content:references:bond-pricing-relationships)=
#### Malkiel’s bond-pricing guidelines
The relationship between the price of a bond, and the yeild (i.e., the market interest rate $\bar{r}$) was previously studied by Malkiel {cite}`Malkiel1962`. The so-called Malkiel’s bond-pricing rules are demonstrated by the simulations shown in ({numref}`fig-bond-price-sensitivity`):

1. The price of a U.S. Treasury Bond _increases_ as the market interest rate $\bar{r}$ _decreases_; thus, there is an _inverse_ relationship between the bond yield to maturity (i.e., the market rate $\bar{r}$) and the price of the bond $V_{B}$. 
1. Changes in price as a function of changes in the interest rate are not symmetric;
an increase in a bond’s interest rate $\bar{r}$ results in a _smaller price change_ than a decrease in $\bar{r}$ of equal magnitude. For example, consider Case II in ({numref}`fig-bond-price-sensitivity`); a 50% decrease in $\bar{r}$ increases the price of this bond by approximately 75%, while a 50% increase in $\bar{r}$ decreases the bond price approximately 30%.
1. Prices of long-term bonds are more sensitive to interest rate changes than short-term bonds. For example, consider Case I and Case II in ({numref}`fig-bond-price-sensitivity`); Case I (short-term bond) is _less sensitive_ to the same magnitude change in $\bar{r}$ compared with Case II (long-term bond).
1. Interest rate risk is inversely related to a bond’s coupon rate. Prices of low coupon-rate bonds are more sensitive to changes in interest rates than prices of high-rate coupon bonds. For example, compare Case II and III in ({numref}`fig-bond-price-sensitivity`); case III (the low coupon-rate bond) is significanly more sensitive to decreases in interest rate compared with case II (the high coupon-rate bond). A similar, albeit less pronounced, trend is visible for increased
interest rate.

(content:references:term-structure-of-interest-rates)=
## Term structure of interest rates
Fill me in.

---
 
## Summary
In this lecture, we introduced fixed-income debt securities. Fixed-income debt securities are contracts between a borrower and a lender that regulate the repayment of a debt. Here we focused on an archetypal category of fixed-income debt security: [United States Treasury Securities](https://www.investor.gov/introduction-investing/investing-basics/glossary/treasury-securities). In particular, we:

* Introduced the definition of {ref}`content:references:treasury-bonds`
* Developed tools to compute the fair price of Treasury Bills/Notes/Bonds as a function of the par value, market interest rate, and coupon rate.
* Introduced {ref}`content:references:bond-pricing-relationships`; Malkiel’s rules describe the sensitivity of bond price to changes in market interest rates as a function of other bond parameters such as coupon rate and term. 