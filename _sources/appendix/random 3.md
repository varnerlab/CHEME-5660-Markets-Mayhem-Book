# Random variables and probability
Random variables and probability are central concepts in understanding uncertainty.  Random variables represent quantities that can take on different values with a particular probability distribution. They are used to model uncertainty and randomness in various fields, including finance, physics, and engineering. Probability theory provides a framework for understanding and quantifying the likelihood of different events occurring based on the underlying distribution of the random variables involved.

* A [random variable](https://en.wikipedia.org/wiki/Random_variable) is a variable $X$ that takes on different values $x$ according to the outcome of a random event or process. There are two types of random variables: discrete random variables and continuous random variables. Discrete random variables can take on a countable number of distinct values, while continuous random variables can take on any value in a continuous range. 
* [Probability](https://en.wikipedia.org/wiki/Probability) measures the likelihood that a particular event or outcome will occur and is commonly used to quantify uncertainty in various fields, such as science, engineering, economics, and finance. For a discrete random variable, the likelihood that $X=x$ is described by a [Probability Mass Function (PMF)](https://en.wikipedia.org/wiki/Probability_mass_function) and a [Probability Density Function (PDF)](https://en.wikipedia.org/wiki/Probability_density_function) for continuous random variables. 

(content:references:probability)=
## Probability spaces
[Frequentists](https://en.wikipedia.org/wiki/Frequentist_probability) argue that probability is the relative frequency or propensity of a particular outcome in the set of all possible outcomes. On the other hand, [Bayesians](https://en.wikipedia.org/wiki/Bayesian_probability) argue that probability is a subjective belief. The context of your problem will typically suggest which perspective to use. For example, when you have a shortage of data, a Bayesian approach allows you to use prior knowledge or belief. On the other hand, when in a data-rich environment, a [frequentist](https://en.wikipedia.org/wiki/Frequentist_probability) approach calculates the probability of an event directly from the data, along with confidence intervals on your estimate. 

Whether you prefer the [frequentist’s](https://en.wikipedia.org/wiki/Frequentist_probability) or the [Bayesian view](https://en.wikipedia.org/wiki/Bayesian_probability), there is a more fundamental notion of probability thanks to [Andrey Kolmogorov](https://en.wikipedia.org/wiki/Andrey_Kolmogorov), namely, the probability is a measure of the size of a set ({prf:ref}`defn-prob-space-kolmogorov`):

````{prf:definition} Probability space
:label: defn-prob-space-kolmogorov

A probability space is described by the tuple of objects $(\Omega,\mathcal{F},P)$:
* The sample space $\Omega$ holds the set of all possible outcomes from an experiment.
* The event space $\mathcal{F}$ is the collection of all possible events. An event $E$ is a subset in $\Omega$ that defines an outcome or a combination of outcomes.
* The probability law $P$ is a mapping from an event $E$ to a number $P(E)$ which, measures the _size_ of the event $E$.
````

The sample space and the event space are all based on statements, for example, getting a head when flipping a coin, winning the game, or drawing a card, etc. These statements are not numbers; how do we convert a statement to a number? The answer is a random variable; random variables are mappings from events to numbers, these numbers are probabilities.

### Sample space $\Omega$
Given an experiment, the sample space $\Omega$ is the set containing all possible outcomes of that experiment. These outcomes can be numbers, alphabets, vectors, or functions, as well as, images, videos, EEG signals, audio speeches, etc. 

Let's consider an example of a six sided dice ({prf:ref}`ex-sample-space-dice`):

````{prf:example} Sample space $\Omega$ of six sided dice
:class: dropdown
:label: ex-sample-space-dice

Suppose we were intersted in the outcome of experiment where a six sided dice was rolled on time. 
Then the sample space for this experiment $\Omega$ is given by:

$$\Omega=\left\{1,2,3,4,5,6\right\}$$
 
The [cardinality](https://en.wikipedia.org/wiki/Cardinality) of this sample space $\dim\left(\Omega\right) = 6$.
````

### Event space $\mathcal{F}$
The sample space $\Omega$ contains all the possible outcomes of an experiment. 
However, we may not be interested in an individual outcome. 
Rather we may be interested in combinations of individual outcomes where the elements of these sets share some common trait, e.g., even integers or the collection of face cards, etc. These subsets are called events $E\subseteq\Omega$, and the set of all possible events, denoted as $\mathcal{F}$, is called the event space. 
Thus, the event space $\mathcal{F}$ is a particular set of sets; it’s the set of all possible subsets.

Let's enumerate the event space for the four suits of a typical deck of cards ({prf:ref}`ex-event-card-suits`):

````{prf:example} Enumerate the event space $\mathcal{F}$ 
:class: dropdown
:label: ex-event-card-suits

Construct the event space $\mathcal{F}$ for the sample space $\Omega=\left\{\clubsuit, \diamondsuit, \heartsuit, \spadesuit\right\}$. The cardinality of $\Omega$ is $\dim\left(\Omega\right) = 4$. 

__Solution__: The $\dim(\mathcal{F}) = 2^n$ where the elements of $\mathcal{F}$ correspond to the first $\dim(\Omega)$ digits of the binary representation of the integers $i=0,\dots,\dim(\mathcal{F})-1$. For example, the bitstring `0000`, which corresponds to $i=0$, represents the empty set $\emptyset$ while the bitstring `1111`, which corresponds to $i=15$, corresponds to $\left\{\clubsuit, \diamondsuit, \heartsuit, \spadesuit\right\}$.

| index | bitstring | $x\in\mathcal{F}$ |
| --- | --- | --- |
0 | `0000` | $\emptyset$
1 | `0001` | $\left\{\spadesuit\right\}$
2 | `0010` | $\left\{\heartsuit\right\}$
3 | `0011` | $\left\{\heartsuit, \spadesuit\right\}$
. | .... | ...
9 | `1001` | $\left\{\clubsuit, \spadesuit\right\}$
. | .... | ...
14 | `1110` | $\left\{\clubsuit, \diamondsuit, \heartsuit\right\}$
15 | `1111` | $\left\{\clubsuit, \diamondsuit, \heartsuit, \spadesuit\right\}$
````

### Probability law $P$
A probability law $P$ is a function $P$ : $\mathcal{F}\rightarrow\left[0, 1\right]$;
the function $P$ maps an event (set) $E\subseteq\Omega$ to a real number in $\left[0, 1\right]$.
The definition above does not specify how an event $E\subseteq\Omega$ is being mapped to a number. 
However, since probability is a measure of the size of a set, a meaningful probability law $P$ should be consistent for all $E\subseteq\Omega$. 

This requires rules, known as the axioms of probability ({prf:ref}`axiom-probability`):

```{prf:axiom} Axioms of Probability
:label: axiom-probability 

A probability law $P$ is a function $P:\mathcal{F}\rightarrow\left[0, 1\right]$ that maps an event $E\subseteq\Omega$
to a real number on the interval $\left[0, 1\right]$. The function $P$ must satisfy the three axioms of probability:

* Non-negativity: $P(E)\geq{0}$, for any $E\in\mathcal{F}$
* Normalization: $P(\Omega)=1$
* Additivity: For any disjoint event sets $\left\{E_{1}, E_{2}, \dots, E_{n}\right\}$ then $P\left(\bigcup_{i=1}^{n}E_{i}\right) = 
\sum_{i=1}^{n}P(E_{i})$

```

### Conditional Probability
The motivation of conditional probability is to restrict the probability to a subevent happening in the sample space. If B has happened, the probability for A to also happen is P[A∩B]/P[B]. If two events are not influencing each other, then we say that A and B are independent.

#### Independence versus Disjoint
Conditional probability deals with situations where two events, $A$ and $B$, are related.  However, what if the two events are unrelated, i.e., information about one event says nothing about the second event? In this case, the events $A$ and $B$ are independent ({prf:ref}`defn-independence`):

````{prf:definition} Statistical independence of events
:label: defn-independence

Two events A and B are statistically independent if:

$$P\left(A\cap{B}\right) = P(A)P(B)$$
````

However, independence says nothing about whether two events are disjoint. Suppose events $A$ and $B$ were disjoint, then we know that $A\cap{B} = 0$ and:

$$P\left(A\cap{B}\right) = 0$$

But, this says nothing about whether $P(A\cap{B})$ can be factorized into the product $P(A)P(B)$.
The only case when disjoint implies independence is if either $P(A) = 0$ or $P(B) = 0$.

### Bayes’ theorem
[Bayes' theorem](https://en.wikipedia.org/wiki/Bayes%27_theorem), named after [Thomas Bayes](https://en.wikipedia.org/wiki/Thomas_Bayes), describes the likelihood of an event based on prior knowledge of conditions related to the event ({prf:ref}`bayes-theorem`):

````{prf:theorem} Bayes' theorem
:label: bayes-theorem

For any two events $A$ and $B$ where $P(A) > 0$ and $P(B) > 0$, the conditional probability $P(A\vert{B})$ is given by:

$$P(A\vert{B}) = \frac{P\left(A\cap{B}\right)}{P\left(B\right)}$$
````

Bayes’ theorem provides two views of the intersection $P\left(A\cap{B}\right)$ using two different conditional probabilities. To see this, we use the fact that the order of the events $A$ and $B$ is arbitrary:

$$P(A\,\vert{B})P(B) = P(B\,\vert{A})P(A) = P(A \cap B)$$

Thus, Bayes’ theorem offers a mechanism to interconvert $P(A\vert{B})$ and $P(B\vert{A})$.

### Law of Total Probability
The law of total probability is a fundamental concept in probability theory that allows us to compute the probability of an event by considering all the possible ways in which it can occur ({prf:ref}`defn-law-total-probability`):

````{prf:theorem} Law of Total Probability
:label: defn-law-total-probability

Let $\left\{A_{1},\dots,A_{n}\right\}$ be a partition of the sample space $\Omega$ where the 
partitions $A_{\star}$ are disjoint and $\Omega=A_{1}\cup{A_{2}}\cup\dots\cup{A_{n}}$. 
Then for $B\subseteq\Omega$:


$$P(B) = \sum_{i=1}^{n}P\left(B\,\vert{A_{i}}\right)P\left(A_{i}\right)$$
````

### Probability mass functions
In the case of discrete random variables, for example, dice roles, coin flips etc, the likelihood that $X=x$ is described by a [Probability Mass Function (PMF)](https://en.wikipedia.org/wiki/Probability_mass_function) ({prf:ref}`defn-pmf`):

````{prf:definition} Probability Mass Function
:label: defn-pmf

The probability mass function (PMF) of a discrete random variable $X$ is a function that specifies the probability of obtaining $X = x$, where $x$ is a particular event in the set of possible events we're interested in $\mathcal{F}\subseteq{X\left(\Omega\right)}$:

$$p_{X}(x) = P\left(X=x\right)$$

where $\mathcal{F}$ is the event space, and $\Omega$ is the sample space. A probability mass function must satisfy the condition: 

$$\sum_{x\in{X(\Omega)}}p_{X}(x)=1$$
````

Thus, in the context of the [von Neumann-Morgenstern theorem](https://en.wikipedia.org/wiki/Von_Neumann–Morgenstern_utility_theorem), the probability mass function is a weight for discrete random variables which model uncertain payoffs. 

In [Julia](https://julialang.org), probability mass (or density) functions can be constructed and sampled using the [Distributions.jl](https://juliastats.org/Distributions.jl/stable/) package. Let's look at a few common probability mass functions.

#### Bernoulli random variable
A Bernoulli random variable, the simplest random variable, models a coin flip or some other type of binary
outcome ({prf:ref}`defn-pmf-bernouli`):

````{prf:definition} Bernoulli Random Variable
:label: defn-pmf-bernouli

Let $X$ be a Bernoulli random variable. Then, the probability mass function of $X$ is given by:

```{math}
p_{X}(x) =
\begin{cases}
  p & \text{if } x = 1 \\
  1 - p & \text{if } x = 0
\end{cases}
```

where $0<p<1$ is called the Bernoulli parameter. For a Bernoulli random variable $X(\Omega) \in [0,1]$ the expectation is given by:

```{math}
\mathbb{E}\left[X\right] = p
```

while the variance $\text{Var}(X)$ is given by:

```{math}
\text{Var}\left[X\right] = p(1-p)
```
````

Bernoulli random variables, named after the Swiss mathematician [Jacob Bernoulli](https://en.wikipedia.org/wiki/Jacob_Bernoulli), have two states: either `1` or `0`. The probability of getting `1` is $p$, while the likelihood of getting a value of `0` is $1 − p$. Bernoulli random variables model many binary events: coin flips (H or T), binary bits (1 or 0), true or false, yes or no, present or absent, etc.

```julia
# load the distributions package, and some other stuff
using Distributions
using Statistics
using PrettyTables

# Details of Bernoulli distribution: 
# https://juliastats.org/Distributions.jl/stable/univariate/#Discrete-Distributions

# setup constants -
p = 0.64;
number_of_samples = 100;

# build a Bernoulli distribution
d = Bernoulli(p)

# sample (check expectation, and variance)
samples = rand(d,number_of_samples);

# build a table -
data_for_table = Array{Any,2}(undef, 2, 3)
table_header = ["", "E(X)", "Var(X)"]

# row 1: model
data_for_table[1,1] = "model"
data_for_table[1,2] = mean(d);
data_for_table[1,3] = var(d);

# row 2: samples
data_for_table[2,1] = "samples"
data_for_table[2,2] = mean(samples);
data_for_table[2,3] = var(samples);
pretty_table(data_for_table, header=table_header);
```

#### Binomial random variable
The binomial distribution is the probability of getting exactly $k$ successes in $n$ independent Bernoulli trials, e.g., the chance of getting four heads in 6 coin tosses ({prf:ref}`defn-pmf-binomial`):

````{prf:definition} Binomial Random Variable
:label: defn-pmf-binomial

Suppose we perform repeated Bernoulli trials $X(\Omega) \in [0,1]^n$, i.e., $n$ trials of an independent binary experiment. The probability of getting exactly $k$ successes in $n$ independent Bernoulli trials is governed by the binomial probability mass function:

$$p_{X}(k) = \binom{n}{k}p^{k}\left(1-p\right)^{n-k}\qquad{k=0,1,\dots,n}$$

where $k$ denotes the number of successes in $n$ independent experiments, the binomial parameter $0<p<1$ is the probability 
of a successful trial and:

$$\binom{n}{k} = \frac{n!}{k!\left(n-k\right)!}$$

is the binomial coefficient. The expectation of a binomial random variable is given by:

```{math}
\mathbb{E}\left[X\right] = np
```

while the variance $\text{Var}(X)$ is given by:

```{math}
\text{Var}\left[X\right] = np(1-p)
```
````

```julia
# load the distributions package, and some other stuff
using Distributions
using Statistics
using PrettyTables

# Details of Binomial distribution: 
# https://juliastats.org/Distributions.jl/stable/univariate/#Distributions.Binomial

# setup constants -
number_of_trials = 100;
p = 0.64;
number_of_samples = 100;

# build a Bernoulli distribution
d = Binomial(number_of_trials,p)

# sample (check expectation, and variance)
samples = rand(d,number_of_samples);

# build a table -
data_for_table = Array{Any,2}(undef, 2, 3)
table_header = ["", "E(X)", "Var(X)"]

# row 1: model
data_for_table[1,1] = "model"
data_for_table[1,2] = mean(d);
data_for_table[1,3] = var(d);

# row 2: samples
data_for_table[2,1] = "samples"
data_for_table[2,2] = mean(samples);
data_for_table[2,3] = var(samples);
pretty_table(data_for_table, header=table_header);
```

#### Geometric random variable
Geometric random variables are a type of discrete probability distribution that models the number of trials required to obtain the first success in a sequence of independent Bernoulli trials ({prf:ref}`defn-pmf-geometric`):

````{prf:definition} Geometric Random Variable
:label: defn-pmf-geometric

Let $X$ be a geometric random variable. The probability mass function for a geometric random variable is given by:

$$p_{X}(k) = (1-p)^{(k-1)}p\qquad{k=1,2,\dots}$$

where $p$ denotes the geometric parameter $0<p<1$. The expectation of a geometric random variable $X$ is given by:

```{math}
\mathbb{E}\left[X\right] = \frac{1}{p}
```

while the variance $\text{Var}(X)$ is given by:

```{math}
\text{Var}\left[X\right] = \frac{1-p}{p^2}
```
````

#### Poisson random variable
Poisson random variables are a type of discrete probability distribution that models the number of occurrences of an event in a fixed interval of time or space ({prf:ref}`defn-pmf-poisson`): 

````{prf:definition} Poisson Random Variable
:label: defn-pmf-poisson

Let $X$ be a Poisson random variable. The probability mass function for a Poisson random variable is given by:

```{math}
p_{X}(x) = \frac{\lambda^{x}}{x!}\exp\left(-\lambda\right)
```

where $\lambda>0$ denotes the Poisson parameter, and $!$ denotes the factorial function. The expectation of a Poisson random variable $X$ is given by:

```{math}
\mathbb{E}\left[X\right] = \lambda
```

while the variance $\text{Var}(X)$ is given by:

```{math}
\text{Var}\left[X\right] = \lambda
```
````

Poisson random variables estimate how likely something will happen $x$ number of times in a fixed interval, e.g., the number of car crashes in a city of a given size or the number of cheeseburgers sold at a fast-food chain on a Friday night.

## Moments of a random variable
Moments of a random variable are a way to summarize its distribution and provide important information about its properties. Specifically, moments are mathematical quantities that describe the shape, center, and spread of a distribution, and they can be used to calculate other statistical measures such as variance and skewness.Let's look at the first and second moments of a random variable, namely the {ref}`content:references:random-variable-expectation` and the {ref}`content:references:random-variable-variance`.

(content:references:random-variable-expectation)=
### Expectation
The [expectation](https://en.wikipedia.org/wiki/Expected_value) of a discrete random variable $X$ measures the central tendency of the values of that random variable ({prf:ref}`defn-discrete-random-variable-expectation`):

````{prf:definition} Expectation discrete random variable
:label: defn-discrete-random-variable-expectation

Let $X$ denote a discrete random variable with the probability space $\left(\Omega,\mathcal{F}, P\right)$, where $\Omega$ denotes the sample space, $\mathcal{F}$ denotes the event space, and $P$ denotes the probability measure. Then, the expected value of the random variable $X$ is given by:

```{math}
:label: eqn-expectation
\mathbb{E}\left[X\right] = \sum_{x\in\Omega}xp_{X}(x)
```

where $x$ denotes a value for the discrete random variable $X$, and $p_{X}(x)$ denotes the probability of $X=x$. The value of $p_{X}(x)$ is governed by a [Probability Mass Function (PMF)](https://en.wikipedia.org/wiki/Probability_mass_function).

````

The expectation of a discrete random variable has a few interesting properties ({prf:ref}`obs-expectation-props`):

````{prf:observation} Properties of expectation
:label: obs-expectation-props
The expectation of a random variable $X$ has several useful (and important) properties: 
1. $\mathbb{E}\left(c\right) = c$ for any constant $c$
1. $\mathbb{E}\left(cX\right) = c\times\mathbb{E}\left(X\right)$ for any constant $c$
1. $\mathbb{E}\left(g(X)\right) = \sum_{x\in{X(\Omega)}}g(x)p_{X}(x)$
1. $\mathbb{E}\left(g(X)+h(X)\right) = \mathbb{E}(g(X)) + \mathbb{E}(h(X))$
1. $\mathbb{E}\left(X+c\right) = \mathbb{E}(X) + c$ for any constant $c$
````

(content:references:random-variable-variance)=
### Variance
The [variance](https://en.wikipedia.org/wiki/Variance) measures the expected dispersion for
individual values of a random variable $X$, i.e., the average distance that values of $X$ are spread out from their expected value ({prf:ref}`defn-discrete-random-variable-variance`):

````{prf:definition} Variance discrete random variable
:label: defn-discrete-random-variable-variance

Let $X$ denote a discrete random variable with the probability space $\left(\Omega,\mathcal{F},P\right)$, where $\Omega$ denotes the sample space, $\mathcal{F}$ denotes the event space, and $P$ denotes the probability measure. Then, the variance of the random variable $X$ is given by:

```{math}
:label: eqn-variance
\text{Var}(X) = \mathbb{E}\Bigl[(X-\mu)^{2}\Bigr]
```

where $\mu = \mathbb{E}(X)$ denotes the expected value of the random variable $X$.

````

The variance of a discrete random variable has a few interesting properties ({prf:ref}`obs-variances-var`):

````{prf:observation} Properties of variance
:label: obs-variances-var

The variance of a random variable $X$ has a few interesting (and important) properties:

* $\text{Var}(X) = \mathbb{E}\left(X^{2}\right) - \mathbb{E}\left(X\right)^2$
* $\text{Var}(cX) = {c^2}\text{Var}(X)$ for any constant $c$
* $\text{Var}(X+c) = \text{Var}(X)$ for any constant $c$

````

The more common quantity that is used to measure dispersion, the standard deviation $\sigma$, is related to the variance: $\sigma_{X} = \sqrt{\text{Var}(X)}$.