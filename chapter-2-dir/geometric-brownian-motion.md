# Geometric Brownian Motion (GBM)
Unfortunately, Eqn. {eq}`eq-SDE-BM` has a critical flaw, namely, it's solution can admit negative values. Thus, as a model for stock price (or the price of another risky asset), it is not widely used. Instead, we often model asset price using a geometric brownian motion (gbm) model:

```{math}
:label: eq-SDE-GBM
\frac{dS\left(t\right)}{S(t)} = \mu{dt}+\sigma{dW(t)}
```

The use of geomtric Brownian motion as a model in mathematical finance is primary due to the work of Samuleson in the 1960s. 