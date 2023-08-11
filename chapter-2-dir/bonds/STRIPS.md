(content:references:term-structure-of-interest-rates)=
# STRIPS Bonds and the Term Structure of Interest Rates

```{topic} Learning Objectives
* We'll introduce the [bootstrapping method to estimate the term structure of interest rates](content:references:STRIPS-TSoIR).
The bootstrapping method is a technique for constructing a zero-coupon yield curve from the prices of zero-coupon bonds with different maturities created by stripping a single coupon bond.
```
---

## Introdcution
[Registered Interest and Principal of Securities (STRIPS) bonds](https://en.wikipedia.org/wiki/United_States_Treasury_security#STRIPS) are a unique type of fixed-income investment that provides an alternative way to access the income and coupon payments of Treasury securities. STRIPS bonds are created by separating a Treasury security’s coupon and principal components and trading them as individual zero-coupon securities ({numref}`fig-SStrips-Schematic`). 

```{figure} ./figs//Fig-STRIPS-Schematic.svg
---
height: 440px
name: fig-SStrips-Schematic
---
Schematic of United States Treasury Registered Interest and Principal of Securities (STRIPS) debt instrument. 
```

For example, the 5-year Treasury note with annual coupon payments of $C$ USD and a face (par) value of $V_{P}$ (USD) in {numref}`fig-SStrips-Schematic` can be stripped into six separate zero-coupon securities, i.e., five zero-coupon bonds, each with face values of $C$ and maturity of `T = 1,2,3,4 and 5 years`, and a six security with face (par) value of $V_{P}$ USD with a duration of $T$ = 5 years. In the general case, a treasury note or bond with $N=\lambda{T}$ coupon payments, where $T$ denotes the maturity in years, and $\lambda$ represents the number of coupon payments per year, can be stripped into $N+1$ separate zero-coupon securities. 

(content:references:STRIPS-TSoIR)=
## Term Structure of Interest Rates and STRIPS
Beyond thier immediate value as investment tools, STRIPS bonds are interesting because they provide another look at the [Term Structure of Interest Rates](https://www.investopedia.com/terms/t/termstructure.asp#:~:text=Essentially%2C%20term%20structure%20of%20interest,current%20state%20of%20an%20economy), i.e., how the change in the [short rates](https://en.wikipedia.org/wiki/Short-rate_model) influences the price and yeild the bond. The process of using the prices of STRIPS bonds to estimate the term structure of interest rates is known as _bootstrapping_.

### Bootstrapping
We can estimate the _short rates_, which represent the market rate of interest between periods $j\rightarrow{j+1}$ and are denoted by $r_{j+1,j}$, by analyzing the prices of the various STRIPS zero coupon products based on their maturity. Using a discrete discounting model, the short rates are calculated according.:

$$
\begin{eqnarray}
\frac{V_{P,1}}{V_{B,1}} & = & \left(1+r_{1,0}\right) \\
\frac{V_{P,2}}{V_{B,2}} & = & \left(1+r_{2,1}\right)\cdot\left(1+r_{1,0}\right) \\
\vdots & = & \vdots \\
\frac{V_{P,N}}{V_{B,N}} & = & \prod_{i=1}^{N}\left(1+r_{i,i-1}\right) \\
\end{eqnarray}
$$

where $V_{P,i}$ and $V_{B,i}$ denote the face (par) value and price of the $i^{th}$ zero-coupon bond (both of which are known). Thus, we can solve for $r_{1,0}$, then insert that into the following expression to solve for $r_{2,1}$, and so on. Systematically, we can solve for the log-transformed short rates as a system of linear algebraic equations (LAEs) of the from:

$$
\mathbf{A}\mathbf{x} = \mathbf{b}
$$

where $x_{i} = \log\left(1+r_{i,i-1}\right)$, $b_{i} = \log\left(V_{P,i}/V_{B,i}\right)$ and $\mathbf{A}$ is a lower-triangular matrix of `1`'s. We solve for the log-transformed short rates by computing the inverse of the matrix $\mathbf{A}$:

$$
\mathbf{x} = \mathbf{A}^{-1}\mathbf{b}
$$

and then transform these back to linear coordinates for each period:

$$
r_{i,i-1} = 10^{x_{i}} - 1
$$

---

## Summary
Fill me in.