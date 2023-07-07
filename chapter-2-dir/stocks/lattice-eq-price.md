# Lattice Models of Equity Pricing

```{topic} Outline
In this lecture, we'll discuss our first type of model of equity pricing, namely lattice models. We'll start with this simple model and then add complexity to it in subsequent lectures. Today, we'll discuss the following topics:

* [Introduction to lattice models](content:lattice-models-introduction). Lattice models discretize the possible furture states of the world, e.g., the share price of a stock, into a finite number of states. For example, a Binomial lattice model has two future states, up and down. We'll discuss how to build a lattice model and how to use it to price assets.

* [Risk-neutral pricing](content:lattice-models-risk-neutral-pricing) is a alternative hypothetical pricing framework that allows us to price assets assuming that investors are risk-neutral. We'll discuss how to use risk-neutral pricing to price assets in a lattice model.

* [Testing the lattice model](content:lattice-models-testing-lattice-model) is an important step in the model building process. We'll discuss how to test the lattice model using real-world versus risk-neutral probabilities. We'll also discuss how to test the lattice model using the implied volatility of options.

```
(content:lattice-models-introduction)=
## Introduction to lattice models
Fill me in.

(content:lattice-models-risk-neutral-pricing)=
## Single-period binomial model
Consider a single-period binomial model which goes from an initial time `0` to a final time `1` ({numref}`example-oneste-binomial-lattice-schematic`). The initial share price at time `0` is $S_{\circ}$ and the share price at time `1` is $S_{1}$. During the transition from time `0`$\rightarrow$`1` the world moves from a current state to the `up` state with probability $p$ or the `down` state with probability $(1-p)$.



```{figure} ./figs/Fig-OneStep-Binomial-Lattice-Schematic.svg
---
height: 320px
name: example-oneste-binomial-lattice-schematic
---
Schematic of a single-period binomial lattice model. In the future, the world can probabilistically move to the `up` with probability $p$ or the `down` state with probability $(1-p)$. The share price at time `1` is $S_{1}$ and can take on one of two possible values: $S^{u}$ if the world moves to the `up` state, or $S^{d}$ if the world moves to the `down` state.
```

At the time `1`, the share price $S_{1}$ can take on one of two possible values: $S^{u} = u\cdot{S_{\circ}}$ if the world moves to the `up` state, or $S^{d} = d\cdot{S_{\circ}}$ if the world moves to the `down` state. The `up` and `down` factors $u$ and $d$, and the probability $p$ can be defined in various ways.  

Let's consider two approaches for computing the tuple $(u,d,p)$: real-world probabilities, which can be estimated from historical data, and risk-neutral probabilities, which are hypothetical probabilities that allow us to price assets as if investors are risk-neutral. 

<!-- Finally, let $\bar{r}>0$ denote the annualized risk-free rate (which we approximate as the spot rate of 10-year U.S. 
Treasury notes).  -->

### Real-world probability
We can estimate real-world values for the `up` and `down` factors $u$ and $d$, and the probability $p$ by analyzing realized prices (the real world realization of the _hidden_ pricing process for an asset). For example, consider the following strategy:

```{admonition} Real-world $(u,d,p)$ strategy
We can estimate the real world probability $p$ by counting the number of times the share price went up and dividing by the total number of observations. Similarly, we can estimate the `up` and `down` factors $u$ and $d$ by computing the average change in the share price when the share price went up and down, respectively.
```

#### Implementation: Real-world $(u,d,p)$ strategy
To create a binomial lattice model for share price projections using real-world probabilities, we estimate the three critical parameters: $p$, $u$, and $d$ from historical data:

* The $p$ parameter represents the probability of a share price increase or an `up` move between two periods $j\rightarrow{j+1}$. As a binary lattice model only allows `up` and `down` moves, the probability of a `down` move is $1-p$.
* The $u$ parameter represents the amount of an `up` move. If $S_{j}$ stands for the share price in period $j$, and $S_{j+1}$ is the share price in the next period, then an `up` move will give $S_{j+1} = u\cdot{S}_{j}$.
* The $d$ parameter represents the amount of a `down` move. If $S_{j}$ stands for the share price in period $j$, and $S_{j+1}$ is the share price in the next period, then a `down` move will give $S_{j+1} = d\cdot{S}_{j}$.


We can calculate the number of `up` and `down` moves, and the magnitude of these moves by analyzing a training dataset. To do this, we assume a share price model of the form:

$$
S_{j} = \exp\left(\mu_{j,j-1}\cdot\Delta{t}\right)\cdot{S_{j-1}}
$$

where $\mu_{j,j-1}$ denotes the _growth rate_ (units: 1/time) and $\Delta{t}$ (units: time) denotes the step size during the time period $(j-1)\rightarrow{j}$. Solving for the growth rate parameter $\mu_{j,j-1}$ gives the expression:

$$
\mu_{j,j-1} = \left(\frac{1}{\Delta{t}}\right)\cdot\ln\left(\frac{S_{j}}{S_{j-1}}\right)
$$

Assuming we use daily data the natural time frame between $S_{j-1}$ and $S_{j}$ is a single _trading_ day. However, subsequently, it will be easier to use an annualized value for the $\mu$ parameter; thus, we let $\Delta{t} = 1/252$, i.e., the fraction of a year that occurs in a single _trading_ day. If we use a different ferquency of data, e.g., weekly, then we would need to adjust the $\Delta{t}$ parameter accordingly. 

```{code-block} julia
:caption: Script to compute the growth rate array
:linenos:

# initialize -
max_number_of_records = nrow(firm_data) # how many records do we have?
Δt = (1.0/252.0); # daily data: assume time step is 1 x trading data
μ = Array{Float64,1}(undef, max_number_of_records - 1) # initialize growth rate array

# main loop: compute the growth rate, store in the μ array
for j ∈ 2:max_number_of_records
    
    S₁ = firm_data[j-1,:volume_weighted_average_price];
    S₂ = firm_data[j,:volume_weighted_average_price];
    μ[j-1] = (1/Δt)*log(S₂/S₁);
end

```

Finally to estimate $p$, after calculating $\mu_{j,j-1}$ for each trading day in the training dataset, we count the number of times the share price went up, i.e., $\mu_{j,j-1}>0$, and divide by the total number of observations. The magnitude of the `up` and `down` moves can be estimated by computing the average change in the share price factors when the share price went up and down, respectively, transforming these values, i.e., $u(j)= \exp\left(\mu_{j,j-1}\cdot\Delta{t}\right)$ when $\mu_{j,j-1}>0$ and $d(j)= \exp\left(\mu_{j,j-1}\cdot\Delta{t}\right)$ when $\mu_{j,j-1}<0$, and then taking the average of these values.

Assuming we have already calculated the $\mu_{j,j-1}$ values for each trading period in the training dataset, the following code snippet defines the `analyze` function which estimates the $p$, $u$, and $d$ parameters from the $\mu_{j,j-1}$ values:

```{code-block} julia
:caption: The `analyze` function 
:linenos:

"""
    analyze(R::Array{Float64,1};  
        Δt::Float64 = (1.0/252.0)) -> Tuple{Float64,Float64,Float64}

Computes the probability of an up move and the up and down factors for a binomial lattice model. 
The `R` argument is an array of growth rate values, and the `Δt` argument is the fraction of a 
year that occurs in a single lattice step (default: 1 trading day). The function returns a 
tuple of the form $(p,u,d)$
"""
function analyze(R::Array{Float64,1};  
    Δt::Float64 = (1.0/252.0))::Tuple{Float64,Float64,Float64}
    
    # initialize -
    u,d,p = 0.0, 0.0, 0.0;
    darray = Array{Float64,1}();
    uarray = Array{Float64,1}();
    N₊ = 0;

    # up - compute the up moves, and estimate the average u value -
    index_up_moves = findall(x->x>0, R);
    for index ∈ index_up_moves
        R[index] |> (μ -> push!(uarray, exp(μ*Δt)))
    end
    u = mean(uarray);

    # down - compute the down moves, and estimate the average d value -
    index_down_moves = findall(x->x<0, R);
    for index ∈ index_down_moves
        R[index] |> (μ -> push!(darray, exp(μ*Δt)))
    end
    d = mean(darray);

    # probability -
    N₊ = length(index_up_moves);
    p = N₊/length(R);

    # return -
    return (u,d,p);
end
```

We implemented the `analyze` function on the `μ` array we computed above for some common stocks ({prf:ref}`tbl-binomial-parameters`):

```{prf:observation} Real-world Binomial parameters for common stocks
:label: tbl-binomial-parameters

Real-world values for the $p$, $u$, and $d$ parameters for some common stocks. The data is based on the daily volume weighted average price for the period `2018-01-03` to `2022-12-31`. The `id` column is the unique identifier for the stock in the `firm_data` table. 

| id  | ticker | name                   | sector                 | probability | up    | down   |
|-----|--------|------------------------|------------------------|-------------|-------|--------|
|  11 |    AMD | Advanced Micro Devices | Information Technology |      0.5331 | 1.022 | 0.9785 |
| 241 |    IBM |                    IBM | Information Technology |      0.5227 |  1.01 | 0.9892 |
| 487 |    WFC |            Wells Fargo |             Financials |      0.5227 | 1.013 | 0.9854 |
| 221 |     GS |          Goldman Sachs |             Financials |       0.502 | 1.013 | 0.9875 |
| 437 |   TSLA |                  Tesla | Consumer Discretionary |      0.5283 | 1.027 | 0.9744 |



For the five tickers in the table, the probability of an `up` move is between 50% and 53%, and the average `up` and `down` factors are between 0.97 and 1.03. 
```


### Risk neutral probability
In finance, risk-neutral pricing is an important concept that helps investors determine the value of financial instruments. This approach assumes that market participants are not affected by risk and are only motivated by their expected returns. By using risk-neutral pricing, investors can estimate the fair value of securities by discounting their expected future cash flows at a risk-free rate. This is particularly useful in derivatives valuation, and other financial models as it allows investors to account for uncertainty in their investment decisions and make informed choices in the marketplace. 

In the one-period binomial model described above, the expected value of the future risk neutral price is governed by:

```{math}
:label: eqn-binomial-no-arbitrage-risk-neutral
\mathcal{D}_{1,0}(\bar{r},\Delta{t})\cdot{S_{\circ}} = \mathbb{E}_{Q}\left(S_{1}\right)
```

where $\mathcal{D}_{1,0}(\bar{r},\Delta{t})$ denotes the discount factor between period `0` and `1`,  $\Delta{t}$ is the length of the time between periods `0` and `1` (in years) , and $\bar{r}$ denotes the annualized risk-free rate. The expectation operator $\mathbb{E}_{Q}(\dots)$ is taken with respect to a _risk neutral probability measure_ $Q$. The risk neutral probability $Q$ is a hypothetical probability measure that allows us to price assets as if investors are risk neutral. For a binomial model, we can expand the expectation operator $\mathbb{E}_{Q}(\dots)$ on the right-hand side of Eqn. {eq}`eqn-binomial-no-arbitrage-risk-neutral` as:

```{math}
:label: eqn-binomial-risk-neutral-probability-expectation
\mathcal{D}_{1,0}(\bar{r},\Delta{t})\cdot{S_{\circ}} = q\cdot{S^{u}} + (1-q)\cdot{S^{d}}
```

where $q$ is the risk neutral probability of the share price in the `up` state. We can solve for $q$ to given an expression for the risk neutral probability of the share price being in the `up` state at time `1`:

```{math}
:label: eqn-risk-neutral-probability-exression-almost
q = \frac{\mathcal{D}_{1,0}(\bar{r},\Delta{t})\cdot{S_{\circ}} - S^{d}}{S^{u} - S^{d}}
```

Finally, we can model the `up` and `down` share price as the product of an `up` factor $u$ (or a `down` factor $d$) and the initial share price, i.e., $S^{u} = u\cdot{S_{\circ}}$ and $S^{d} = d\cdot{S_{\circ}}$. Substituting $S^{u}$ (and $S^{d}$) into Eqn. {eq}`eqn-risk-neutral-probability-exression-almost` to arrive at:

```{math}
q = \frac{\mathcal{D}_{1,0}(\bar{r},\Delta{t}) - d}{u - d}
```

Putting these ideas gives us a defintion of the risk-neutral probability ({prf:ref}`defn-risk-neutral-probability`):

````{prf:definition} Risk neutral probability
:label: defn-risk-neutral-probability

Let `0` denote the index of the current state, and `1` denote a one-step ahead future state. The future state exists in one of two possible configurations, an `up` or `down` configuration. The risk neutral probability that the world transitions to the `up` configuration between `0`$\rightarrow$`1` is given by:


```{math}
:label: eqn-risk-neutral-probability-final
q = \frac{\mathcal{D}_{1,0}(\bar{r},\Delta{t}) - d}{u - d}
```

where $\mathcal{D}_{1,0}(\bar{r},\Delta{t})$ denotes the discount factor evaluated using the effective annualized risk free rate $\bar{r}$, $\Delta{t}$ denotes the length of time (in years) between states `0` and `1`, and the factors $u$ and $d$ denote the `up` and `down` factors, respectively. 

````

To determine the risk-neutral probability, we can adjust the `analyze` function mentioned earlier, where we assume (for now) the realized average `up` factors are the same as the real-world case, but the moves are symmetric, namely $d = 1/u$. This assumption will be relaxed when dealing with derivatives pricing; specific models for `u` are typically applied to calculate `q` in the case of derivatives.

The modified function, called `riskneutralanalyze`, is defined below:

```{code-block} julia
:caption: The `risk-neutral analyze` function 
:linenos:

"""
    riskneutralanalyze(R::Array{Float64,1};  Δt::Float64 = (1.0/252.0), 
        r̄::Float64 = 0.040) -> Tuple{Float64,Float64,Float64}
"""
function riskneutralanalyze(R::Array{Float64,1};  Δt::Float64 = (1.0/252.0), 
    r̄::Float64 = 0.040)::Tuple{Float64,Float64,Float64}
    
    # initialize -
    u,d,q = 0.0, 0.0, 0.0;
    darray = Array{Float64,1}();
    uarray = Array{Float64,1}();

    # up - compute the up moves, and estimate the average u value -
    index_up_moves = findall(x->x>0, R);
    for index ∈ index_up_moves
        R[index] |> (μ -> push!(uarray, exp(μ*Δt)))
    end
    u = mean(uarray);
    d = 1/u;

    # risk neutral probability -
    q = (exp(r̄*Δt) - d)/(u - d);

    # return -
    return (u,d,q);
end
```


We implemented the `riskneutralanalyze` function and processed the `μ` array for some common stocks ({prf:ref}`tbl-binomial-parameters-risk-neutral-probability`):

```{prf:observation} Risk-neutral Binomial parameters for common stocks
:label: tbl-binomial-parameters-risk-neutral-probability

Risk-neutral values for the $q$, $u$, and $d$ parameters for some common stocks. The data is based on the daily volume weighted average price for the period `2018-01-03` to `2022-12-31`. The `id` column is the unique identifier for the stock in the `firm_data` table. 


| id  | ticker | name                   | sector                 | probability | up    | down   |
|-----|--------|------------------------|------------------------|-------------|-------|--------|
|  11 |    AMD | Advanced Micro Devices | Information Technology |      0.4982 | 1.022 | 0.9783 |
| 241 |    IBM |                    IBM | Information Technology |      0.5058 |  1.01 | 0.9902 |
| 487 |    WFC |            Wells Fargo |             Financials |      0.5029 | 1.013 |  0.987 |
| 221 |     GS |          Goldman Sachs |             Financials |      0.5029 | 1.013 |  0.987 |
| 437 |   TSLA |                  Tesla | Consumer Discretionary |      0.4965 | 1.027 |  0.974 |

For the five tickers in the table, the risk-neutral probability of an `up` move is approximately 50%, i.e., a coin-flip.
```

Notice, the risk-neutral probability is approximately 50% for all the stocks in the table. This is not surprising, since the risk-neutral probability is a function of the risk-free rate, which is the same for all the stocks.


(content:lattice-models-testing-lattice-model)=
## Real-world versus risk-neutral probabilities
Fill me in.

---

## Summary
Fill me in.