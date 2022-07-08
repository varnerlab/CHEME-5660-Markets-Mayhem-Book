# Fixed Income Securities

## Introduction
Fixed-income securities are financial instruments with predefined cashflows at selected dates over the lifetime of the instrument. While there are several types of fixed-income securities, in this lecture, we focus on a single archetypal category: [United States Treasury Securities](https://www.investor.gov/introduction-investing/investing-basics/glossary/treasury-securities). 

Treasury securities, e.g., [Treasury bills, notes, and bonds](https://www.treasurydirect.gov/indiv/products/prod_tbonds_glance.htm), are debt obligations issued by the United States Department of the Treasury.  Thus, treasury securities are a mechanism used by the United States government to borrow money, from bond holders, with a fixed set of repayment terms. Treasury securities are one of the safest investments, e.g., defacto risk-free, because they are backed by the full faith and credit of the United States government. [The U.S. government has never defaulted on it's debt obligations (at least in recent memory)](https://thehill.com/opinion/finance/575722-the-us-has-never-defaulted-on-its-debt-except-the-four-times-it-did/).

In this lecture, we will discuss three types of treasury securities:

* The definition and valuation of {ref}`content:references:treasury-bonds`


---

(content:references:treasury-bonds)=
## Treasury Bills, Notes and Bonds
A fixed-income debt security is a contract between a borrower and a lender. In the context of this lecture, 
we'll focus on U.S. Treasury Bills, Notes, and Bonds, examples of government debt securities. 
For United States treasury debt instruments, the borrower is the U.S. government; the government issues (i.e., sells) a bond to a lender (you) for some cash. This arrangement obligates the U.S. Treasury to make specified payments to the bondholder (you) on specified dates.

There are several types of U.S. government debt securities. However, they share several similarities:

* U.S. Treasury debt securities have specified term lengths, meaning the duration of the borrowing contract between the borrower and the lender is fixed. 
* U.S. Treasury debt securities have a par value, i.e., the face value of the instrument, a price (which may not be the same as the par value), and an interest rate paid to the lender.
* U.S. Treasury debt securities have interest payments (historically called coupons) which pay the lender a specified amount of cash on a fixed schedule over the term of the debt instrument. 
* Interest income from U.S. Treasury debt securities is exempt from state and local income taxes but subject to federal income taxes.
* You can buy U.S Treasury debt (meaning lend money to the U.S. government) directly from the [United States Treasury via TreasuryDirect](https://www.treasurydirect.gov/indiv/products/prod_tbonds_glance.htm) or through a bank or broker.


### Treasury Bills
Treasury bills (also called T-bills) are short-term debt instruments sold in terms ranging from a few days to 52 weeks. T-bills are typically sold at a discount from the par amount; rarely they are sold at a price equal to the par amount. When a T-bill matures, you are paid its par amount. 

Treasury bills are issued for terms of 4, 8, 13, 26, and 52 weeks; 4-week, 8-week, 13-week, 26-week, and 52-week bills are auctioned on a regular schedule.  

T-bills are an example of a zero-coupon instrument (no interest payments); thus, T-bills are usually sold at a discount and the difference between the purchase price and the par amount is the interest accrued over the term of the T-bill.

### Treasury Notes
Treasury notes, sometimes called T-notes, are a medium-term debt instrument that earns a fixed rate of interest every six months until maturity. T-notes are issued in terms of 2, 3, 5, 7, and 10 years. The price of a T-note can be greater than, less than, or equal to the T-note's par value. However, at maturity, the par value of the T-note is paid to the owner of the T-note (lender). 

T-notes are an example of a non-zero coupon debt instrument; thus, the lender receives periodic interest payments over the term of the T-note.

### Treasury Bonds
Treasury Bonds are long-term U.S Treasury debt instruments. Treasury bonds pay a fixed rate of interest (the coupon rate) every six months until the bond's maturity. The U.S. Treasury issues bonds with terms of 20 or 30 years. When a bond matures, the bondholder receives the face value of the bond. Bonds can be held until maturity or sold before maturity. 

When a U.S. Treasury bond matures, the U.S government repays the debt by paying the bond's par value. The bond's coupon rate determines the interest payment: the annual payment is the coupon rate times the bond's par value. The coupon rate, maturity date, and par value of the bond are part of the contract between the issuer, the U.S. government, and the bondholder (you).

#### Pricing of U.S. Treasury Bounds
A bond’s coupon payments, and the eventual repayment of the face value, occurs at least 20 years in the future. Thus, the price an investor is willing to pay for a claim to those payments depends on the future value of the dollars that will be received versus the present value of the face value of the bond. 

````{prf:definition} Fixed Coupon Rate Bond Pricing
:label: defn-fixed-r-bond-pricing

Let the term of a bond be T-years with semi-annual coupon payments (2T coupon payments over the term of the bond), with an annual coupon rate of $\bar{c}$, and an annual market interest rate of $\bar{r}$. 

Then, the _fair price_ for the bond, denoted by $V_{B}$, is the present value of coupon payments $C$ plus the discounted par value $V_{P}$ of the bond:

```{math}
V_{B} = \frac{V_{P}}{\left(1+\bar{r}\right)^{2T}}+\sum_{t=1}^{2T}\frac{C}{\left(1+\bar{r}\right)^{t}}
```

where $\bar{r}$ is set by the market at time of purchase of the bond, and $C=\left(\bar{c}/2\right)\cdot{V_{P}}$. If $\bar{c}=\bar{r}$, the fair price equals the par value $V_{P}$.
````

##### Example
* Let's do an example to illustrate bond pricing ({prf:ref}`defn-fixed-r-bond-pricing`). Sources: [Live Pluto notebook](https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks) or [static HTML](https://htmlview.glitch.me/?https://github.com/varnerlab/CHEME-5660-Markets-Mayhem-Example-Notebooks/blob/main/pluto-notebooks/html/Example-Price-TreasuryBond.jl.html).

#### Yield to Maturity of U.S. Treasury Bounds
U.S. Treasury bonds typically do not sell for their par value. However, assuming the U.S. government does not default on its debt obligations, U.S Treasury bonds will mature to the par value over the bond term. Let’s develop a metric called yield to maturity to measure the rate of return that accounts for both the current income generated by the coupon payments and the price increase or decrease over the bond term. The yield to maturity (YTM) is the standard measure of the total rate of return of the fixed-income security. 

Typically, investors purchasing U.S. Treasury bonds are not quoted an overall rate of return. Instead, 
investors must calculate this value from the bond price, maturity date, and coupon payments. The yield to maturity (YTM) is defined as the interest rate that makes the present value of a bond’s payments equal to its price:

````{prf:definition} Yield to Maturity 
:label: defn-yield-to-maturity

Let the term of a U.S. Treasury bond be $T$-years, with an annual coupon rate of $i$. Further, suppose
the U.S. Treasury bond was purchased for $\hat{V}_{B}$ (which may be different that the _fair price_).

The yield to maturity (YTM) value is the interest rate $\bar{r}$ that makes $V_{B}=\hat{V}_{B}$:

```{math}
\hat{V}_{B} - \frac{V_{P}}{\left(1+\bar{r}\right)^{T}}-\sum_{t=1}^{T}\frac{C}{\left(1+\bar{r}\right)^{t}} = 0
```

where $C=\bar{r}\cdot{V_{P}}$.

````

##### Example
* Let's do an example to illustrate the Yield to Maturity calculation ({prf:ref}`defn-yield-to-maturity`).

#### Sensitivity of Bond Prices
Bond investors have two actions open to them: hold the bond until maturity (and collect the coupon payments along the way), or resell the bond (and potentially benefit from a change in the bond price). The latter is possible because after the bonds are issued, bondholders may buy or sell bonds in secondary bond markets. In these markets, bond prices fluctuate inversely with the market interest rate (the coupon rate). 

Interest rate fluctuations are the main source of risk in the secondary fixed-income bond market. 






<!-- 
````{prf:example} U.S. Treasury Bond Maturity Calculation
:label: example-30-year-bond

Consider a U.S. Treasury bond with a par value of B = \$1,000, a coupon rate of 8%, and T = 30-year maturity. 

a) Coupon payments: The coupon rate is quoted as an _annual_ percentage. Thus, the bondholder can expect 0.08$\times$B = \$80 per year (or \$40 per coupon payment) every year for 30-years. 
```` -->

---
 
## Summary
Fill me in.