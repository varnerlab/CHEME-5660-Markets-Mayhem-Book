---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Julia
  language: julia
  name: julia-1.8
---

# Probability, Random Variables and Stochastic Processes

## Introduction
Probability is many things to many people. 
[Frequentists](https://en.wikipedia.org/wiki/Frequentist_probability) argue that probability is the relative frequency or propensity of a particular outcome in the set of all possible outcomes. For example, if you flip a fair coin infinitely many times, you expect to get heads about half the time (assuming a fair coin). On the other hand, [Bayesians](https://en.wikipedia.org/wiki/Bayesian_probability) argue that probability is a subjective belief. For example, the probability of getting an A in a class is subjective because no one can take a class infinitely many times to obtain the relative frequency. The context of your problem will typically suggest which perspective to use. For example, when you have a shortage of data, a Bayesian approach allows you to use prior knowledge or belief. On the other hand, when in a data-rich environment, a [frequentist](https://en.wikipedia.org/wiki/Frequentist_probability) approach calculates the probability of an event directly from the data, along with confidence intervals on your estimate. 

However, whether you prefer the [frequentist’s](https://en.wikipedia.org/wiki/Frequentist_probability) or the [Bayesian view](https://en.wikipedia.org/wiki/Bayesian_probability), there is a more fundamental notion of probability thanks to [Andrey Kolmogorov](https://en.wikipedia.org/wiki/Andrey_Kolmogorov), namely, the probability is a measure of the size of a set. 

Thus, we'll begin this lecture by reviewing some of the basic tenants of [Set Theory](https://en.wikipedia.org/wiki/Set_theory) and then progress to probability and random variables. In particular, we will:

* Introduce {ref}`content:references:set-theory` and operations on sets such as {ref}`content:references:union-intersection` of sets.
* Introduce {ref}`content:references:probability` the Axioms of Probablity ({prf:ref}`axiom-probability`)
* Introduce {ref}`content:references:random-variables`, {ref}`content:references:prob-mass-functions` for discrete random variables, and {ref}`content:references:prob-distribution-functions` for continuous random variables.

---

(content:references:set-theory)=
## Set theory
In mathematics, we are often interested in describing a collection of numbers or other mathematical objects, for example, the numbers $\left[a, b\right]$ on the real line, or the ordered pairs of numbers that define a circle. These collections of numbers can be abstractly defined as sets. 
A set is simply a collection of mathematical objets. Set theory is a mathematical tool that defines operations on sets. It provides the basic arithmetic for combining, separating, and decomposing sets.

````{prf:definition} Sets
:label: defn-sets

A set is a collection of elements. We denote

$$A = \left\{a_{1},a_{2},\dots,a_{n}\right\}$$

as the set $A$, where $a_{i}$ is the ith element of the set. 
````

To denote that an object $a$ belongs to the set $A$, we write $a\in{A}$. 
For example, to show that the number $1$ belongs to the set $\left\{1, 2, 3,\dots,10\right\}$, 
we write $1\in\left\{1, 2, 3,\dots,10\right\}$. The elements of sets can be anything; real numbers, complex numbers, functions or any mathematical object.

Given a set, we often want to specify a portion of that set, which we call a subset.

````{prf:definition} Subsets
:label: defn-subsets

$B$ is a subset of $A$ if for any $x\in{B}$, $x$ is also in $A$. We write

$$B \subseteq A$$

to denote that $B$ is a subset of $A$. 
The set $B$ is called a proper subset of $A$ if $B$ is a subset of $A$ and $B\neq{A}$. 
We denote a proper subset as $B\subset A$. 
Two sets $A$ and $B$ are equal if and only if $A \subseteq B$ and $B \subseteq A$.
````

Finally, there are two special types of sets, 
the empty set $\emptyset$ and the universal set $\Omega$. The empty set contains no elements. For example, if the set $A$ is empty we say $A=\emptyset$. On the other hand, the universal set is the set containing all elements. Thus, if set $A$ contains all possible elements, we say $A=\Omega$.

(content:references:union-intersection)=
### Union and Intersection
We now discuss basic set operations. By operations, we mean functions of two or more sets whose output value is a set. We use these operations to combine and separate sets. Let's first describe the 
[union](https://en.wikipedia.org/wiki/Union_(set_theory)).

````{prf:definition} Union
:label: defn-union

The finite union of two sets $A$ and $B$ contains all elements in that are $A$ or in $B$:

$$A\cup{B} = \left\{x\,\vert\,x\in{A} \text{ or } x\in{B}\right\}$$
````

The union of two sets connects the sets using the logical _or_ operator; 
thus, the union of two sets is always larger than or equal to the individual sets.

The [intersection](https://en.wikipedia.org/wiki/Intersection_(set_theory)) operation relys on the 
logical _and_ operator. Thus, the [intersection](https://en.wikipedia.org/wiki/Intersection_(set_theory)) finds the common elements of the two sets:

````{prf:definition} Intersection
:label: defn-intersection

The finite intersection of two sets $A$ and $B$ contains all elements that are in both $A$ and in $B$:

$$A\cap{B} = \left\{x\,\vert\,x\in{A} \text{ and } x\in{B}\right\}$$
````

(content:references:set-complement)=
### Complement
In addition to the union and intersection of sets, 
there is a third basic operation called the [set complement](https://en.wikipedia.org/wiki/Complement_(set_theory)). 
Suppose you had a set $A\subset\Omega$. Then the complement of $A$, denoted by $\bar{A}$, is 
everything that is in $\Omega$, but __not__ in $A$.

````{prf:definition} Complement
:label: defn-complement

The abosulte complement of a set $A$, denoted by $\bar{A}$, is the set containing all elements that are in $\Omega$ but not in $A$:

```{math}
\bar{A} = \left\{x\  \vert\ x\in\Omega \text{ and } x\notin{A} \right\}
```

The complement has a number of interesting properties, known collectively as the Complement laws. 

* P1: $A\cup{\bar{A}} = \Omega$. The set $A$ and it's complement $\bar{A}$ make up the universal set $\Omega$.
* P2: $A\cup{\bar{A}} = \emptyset$. There are no elements outside of $A$ and it's complement $\bar{A}$.
* P3: $\bar{\emptyset} = \Omega$. The complement of the emptyset $\emptyset$ is the universal set $\Omega$.
* P4: $\bar{\Omega} = \emptyset$. There is nothing outside of the universal set $\Omega$.
* P5: $\bar{\bar{A}} = A$. The complement of the complement returns the original set $A$.

````

(content:references:set-disjoint)=
### Disjoint Sets and Partitions
The last set-theoretic concepts that we explore before turning our attention to probability (and its relationship to sets)
is the [disjoint](https://en.wikipedia.org/wiki/Disjoint_sets) relationship, and the idea of a partition.
Suppose we had two sets $A$ and $B$; the sets $A$ and $B$ are disjoint if they have no elements in common. 

````{prf:definition} Disjoint
:label: defn-disjoint

Two sets $A$ and $B$ are said to be disjoint if thier intersection is the emptyset $\emptyset$ (they have no common elements):

```{math}
A\cap{B} = \emptyset
```

For a collection of sets $\left\{A_{1},A_{2},\dots, A_{n}\right\}$, then the collection is disjoint if:


```{math}
A_{i}\cap{A_{j}} = \emptyset
```

for all pairs of sets $A_{i}$ and $A_{j}$ where $i\neq{j}$.

````

Now that we understand disjoint sets ({prf:ref}`defn-disjoint`), we can define a partition of the universal set $\Omega$.
````{prf:definition} Partition
:label: defn-partition

A collection of sets $\left\{A_{1},A_{2},\dots, A_{n}\right\}$ is a partition of $\Omega$ if the following 
two conditions are true:

__Condition 1__: the collection of sets $\left\{A_{1},A_{2},\dots, A_{n}\right\}$ is disjoint

```{math}
A_{i}\cap{A_{j}} = \emptyset
```

for all pairs of sets $A_{i}$ and $A_{j}$ where $i\neq{j}$.

__Condition 2__: The union of the sets $\left\{A_{1},A_{2},\dots, A_{n}\right\}$ gives the universal set $\Omega$:

```{math}
\bigcup_{i=1}^{n}A_{i} = \Omega
```
````

The partition ({prf:ref}`defn-partition`) of the universal set $\Omega$ is a collection of smaller non-overlapping subsets whose union gives back the universal set $\Omega$. 
Partitions are important because they allow us to decompose the universal set $\Omega$ into a collection of smaller subsets. Since these smaller subsets are disjoint, i.e., they do not overlap, we can analyze them separately from each other. 

In the context of probability, partitions are essential tools because they allow us to decouple complex events
into many smaller disconnected events. 
For example, suppose the collection of sets $\left\{A_{1},A_{2},\dots, A_{n}\right\}$ is a partition of $\Omega$.
Then, for any set $B\subseteq\Omega$ we can decompose $B$ into smaller disjoint components $B\cap{A_{i}}$ 
(the elements of $B$ that are in $A_{i}$):

```{math}
:label: eqn-decomp-partition
\bigcup_{i=1}^{n}B\cap{A_{i}} = B
```

(content:references:probability)=
## Probability Space

A probability space is completley described by the tuple $(\Omega,\mathcal{F},P)$:

* Sample space $\Omega$: The set of all possible outcomes from an experiment.
* Event space $\mathcal{F}$: The collection of all possible events. An event E is a subset in $\Omega$ that defines an outcome or a combination of outcomes.
* Probability law $P$: A mapping from an event $A$ to a number $P(A)$ which, measures the _size_ of the event.

### Sample space $\Omega$
We start by defining the sample space $\Omega$. Given an experiment, the sample space $\Omega$ is the
set containing all possible outcomes of that experiment. These experimental outcomes can be numbers, alphabets, vectors, or functions, as well as, images, videos, EEG signals, audio speeches, etc. 

````{prf:example} Sample space $\Omega$ 
:label: ex-sample-space-dice

Suppose we were intersted in the outcome of experiment where a six sided dice was rolled on time. 
Then the sample space for this experiment $\Omega$ is given by:

$$\Omega=\left\{1,2,3,4,5,6\right\}$$
 
The cardinality of this sample space $\dim\left(\Omega\right) = 6$.
````

### Event space $\mathcal{F}$
The sample space $\Omega$ contains all the possible outcomes of an experiment. 
However, we typically are not interested in individual outcomes; instead we are interested in sets of the outcomes 
where the elements of these sets share some common trait 
e.g., even integers, or the set of face cards, etc. These subsets are called events $E\subseteq\Omega$ and 
the set of all possible events, denoted as $\mathcal{F}$, is called the event space. 
Thus, the event space $\mathcal{F}$ is a special set of sets, it's the sets of all possible subsets.

````{prf:example} Enumerate the event space $\mathcal{F}$ 
:label: ex-event-card-suits

Let's construct the event space $\mathcal{F}$ for the sample space 
$\Omega=\left\{\clubsuit, \diamondsuit, \heartsuit, \spadesuit\right\}$. 
The cardinality of $\Omega$ is given by $\dim\left(\Omega\right) = 4$. 
Thus, the $\dim(\mathcal{F}) = 2^n$ or $\dim(\mathcal{F}) = 16$. 

The elements of the sample space $\mathcal{F}$ correspond to the binary representation of $i=0,\dots,\dim(\mathcal{F})-1$. 
For example, the bitstring `0000`, which corresponds to $i=0$, represents the empty set $\emptyset$ while
the bitstring `1111`, which corresponds to $i=15$, corresponds to $\left\{\clubsuit, \diamondsuit, \heartsuit, \spadesuit\right\}$.

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
However, since probability is a measure of the size of a set, a meaningful probability law $P$ should be consistent for all $E\subseteq\Omega$. This requires rules, known as the axioms of probability, when we define the probability law $P$. 

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
Conditional probability deals with situations where two events $A$ and $B$ are related. 
However, what if the two events are unrelated? In other words, information about one event says nothing 
about the second event. In this case, the events $A$ and $B$ are said ot be independent:

````{prf:definition} Statistical Independence
:label: defn-independence

Two events A and B are statistically independent if:

$$P\left(A\cap{B}\right) = P(A)P(B)$$
````

However, independence says nothing about whether two events are disjoint. Suppose events $A$ and $B$ were disjoint, then we
know that $A\cap{B} = 0$ and:

$$P\left(A\cap{B}\right) = 0$$

But, this says nothing about whether $P(A\cap{B})$ can be factorized into the product $P(A)P(B)$.
The only case when disjoint implies independence is if either $P(A) = 0$, or $P(B) = 0$.


### Bayes’ theorem and the law of total probability
[Bayes' theorem](https://en.wikipedia.org/wiki/Bayes%27_theorem) named after [Thomas Bayes](https://en.wikipedia.org/wiki/Thomas_Bayes), describes the probability of an event, based on prior knowledge of conditions that might be related to the event.

````{prf:theorem} Bayes' theorem
:label: bayes-theorem

For any two events $A$ and $B$ where $P(A) > 0$ and $P(B) > 0$, the conditional probability $P(A\vert{B})$ is given by:

$$P(A\vert{B}) = \frac{P\left(A\cap{B}\right)}{P\left(B\right)}$$
````

Bayes’ theorem provides two views of the intersection $P\left(A\cap{B}\right)$ using two different conditional probabilities. 
To see this, we use the fact that the order of the events $A$ and $B$ is arbitrary:

$$P(A\,\vert{B})P(B) = P(B\,\vert{A})P(A) = P(A \cap B)$$

Thus, Bayes’ theorem offers a mechanism to interconvert $P(A\vert{B})$ and $P(B\vert{A})$.
The law of Total Probability allows us to decompose an event into smaller events:

````{prf:theorem} Law of Total Probability
:label: defn-law-total-probability

Let $\left\{A_{1},\dots,A_{n}\right\}$ be a partition of the sample space $\Omega$ where the 
partitions $A_{\star}$ are disjoint and $\Omega=A_{1}\cup{A_{2}}\cup\dots\cup{A_{n}}$. 
Then for $B\subseteq\Omega$:


$$P(B) = \sum_{i=1}^{n}P\left(B\,\vert{A_{i}}\right)P\left(A_{i}\right)$$

````

---

(content:references:random-variables)=
## Random Variables and Stochastic Processes
The sample space and the event space are all based on statements, for example, getting a head when flipping a coin, winning the game, or drawing a card, etc. These statements are not numbers; how do we convert a statement to a number? The answer is a random variable; random variables are mappings from events to numbers, these numbers are probabilities.

### Moments of discrete random variables

It is often helpful to extract characteristics such as the mean, standard deviation, or other quantities of interest from financial data sets.  However, markets (and hence asset prices) are random; thus, we compute these parameters of interest from random market data using 
a concept called the [moments of a random variable](https://en.wikipedia.org/wiki/Moment_(mathematics)). 

 The mean, variance, skew, kurtosis, etc are all examples of the [moments of a random variable](https://en.wikipedia.org/wiki/Moment_(mathematics)). 
Let the daily close price of `XYZ` be a discrete random variable denoted by $X$. 
Then the moments of `XYZ` are defined as:


````{prf:definition} Moments
:label: defn-moments

Let $X$ denote a discrete random variable which takes on values in the finite sample space $X(\Omega)$. Then, the kth moment of $X$ is given by:

```{math}
\mathbb{E}\Biggl[\left(\frac{X - a}{b}\right)^k\Biggr] = \sum_{x\in{X(\Omega)}}\left(\frac{X - a}{b}\right)^{k}p_{X}(x)
```

where $p_{X}(x)$ denotes the probability that random variable $X=x$, 
$X(\Omega)$ denotes sample space for $X$, and $a\geq{0}$ 
and $b\geq{1}$ are constants.

Important moments:

* $k=1$ and $(a,b) = (0,1)$: The first (raw) moment is the [expectation](https://en.wikipedia.org/wiki/Expected_value) (mean) of $X$. The [expectation](https://en.wikipedia.org/wiki/Expected_value) measures the central tendency in the data.

* $k=2$ and $(a,b)=(\mu,1)$: The second (central) moment is the [variance](https://en.wikipedia.org/wiki/Variance) of $X$. The [variance](https://en.wikipedia.org/wiki/Variance) measures dispersion in the data, i.e., how far data points are spread out from their expected value. 

* $k=3$ and $(a,b)=(\mu,~\sigma)$: The third (normalized central) moment is the [skewness](https://en.wikipedia.org/wiki/Skewness) of $X$. The [skewness](https://en.wikipedia.org/wiki/Skewness) measures the asymmetry of a random variable about its expectation. Skewness can be positive, zero, negative, or undefined.

* $k=4$ and $(a,b)=(\mu,~\sigma)$: The fourth (normalized central) moment is the [kurtosis](https://en.wikipedia.org/wiki/Kurtosis) of $X$. The [kurtosis](https://en.wikipedia.org/wiki/Kurtosis) measures the heaviness of the tail of the distribution relative to a normal distribution of the same variance.

where $\mu = \mathbb{E}(X)$ denotes the mean, and $\sigma$ denotes the standard deviation.

````

#### Expectation
The [expectation](https://en.wikipedia.org/wiki/Expected_value) (or mean), which measures the central tendency of a random variable $X$, is given by (discrete $X$):

```{math}
:label: eqn-expectation

\mathbb{E}\left[X\right] = \sum_{x\in{X}(\Omega)}xp_{X}(x)

```

The expectation of a random variable $X$ (discrete or continuous) has several useful (and important) properties: 
* $\mathbb{E}\left(c\right) = c$ for any constant $c$
* $\mathbb{E}\left(cX\right) = c\times\mathbb{E}\left(X\right)$ for any constant $c$
* $\mathbb{E}\left(g(X)\right) = \sum_{x\in{X(\Omega)}}g(x)p_{X}(x)$
* $\mathbb{E}\left(g(X)+h(X)\right) = \mathbb{E}(g(X)) + \mathbb{E}(h(X))$
* $\mathbb{E}\left(X+c\right) = \mathbb{E}(X) + c$ for any constant $c$

#### Variance

The [variance](https://en.wikipedia.org/wiki/Variance) measures the expected dispersion for
individual values of $X$, i.e., the average distance that values of $X$ are spread out from their expected value (mean). The [variance](https://en.wikipedia.org/wiki/Variance) is given by:

```{math}
:label: eqn-variance
\text{Var}(X) = \mathbb{E}\Bigl[(X-\mu)^{2}\Bigr]
```

where $\mu = \mathbb{E}(X)$ denotes the expected value (mean) of the random variable $X$.
Like the mean, the variance $\text{Var}(X)$ has a few interesting (and important) properties:

* $\text{Var}(X) = \mathbb{E}\left(X^{2}\right) - \left(\mu\right)^2$
* $\text{Var}(cX) = {c^2}\text{Var}(X)$ for any constant $c$
* $\text{Var}(X+c) = \text{Var}(X)$ for any constant $c$

The more common quantity that is used to measure dispersion, the standard deviation $\sigma$, 
is related to the variance: $\sigma_{X} = \sqrt{\text{Var}(X)}$.

#### Skewness
The [skewness](https://en.wikipedia.org/wiki/Skewness) measures the expected asymmetry of a random variable about its mean (expected value): 

```{math}
:label: eqn-skewness
\gamma(X) = \mathbb{E}\Biggl[\left(\frac{X - \mu}{\sigma}\right)^3\Biggr]
```

where $\mu$ denotes the mean (expected value), and $\sigma$ denotes the standard deviation.
The skewness parameter $\gamma(X)$ can be positive, zero, negative, or undefined. 

#### Kurtosis

The [kurtosis](https://en.wikipedia.org/wiki/Kurtosis) measures the heaviness of the tail of the distribution relative to a normal distribution of the same variance. 
The [kurtosis](https://en.wikipedia.org/wiki/Kurtosis) of a random variable $X$, denoted as
$\text{Kurt}(X)$, is defined as:

```{math}
:label: eqn-kurtosis

\kappa(X) = \mathbb{E}\Biggl[\left(\frac{X - \mu}{\sigma}\right)^4\Biggr]
```

Large $\kappa(X)$ values arise when most $X$ values are near the mean, but a few values are very far away from the mean. Additionally, $\kappa(X)$ can arise from the majority of $X$ being near the tail of the distribution.


<!-- High values of  arise when $X$ is concentrated around the mean and the data-generating process produces occasional values very far away from the mean, or
when $X$ is concentrated in the tails of the distribution. -->
---

(content:references:prob-mass-functions)=
## Probability mass functions
In the case of discrete random variables, for example, dice roles, coin flips etc, this is done using a concept called a [probability mass function (PMF)](https://en.wikipedia.org/wiki/Probability_mass_function). 


````{prf:definition} Probability Mass Function
:label: defn-pmf

The probability mass function (PMF) of a discrete random variable $X$ is a function that specifies the probability of 
obtaining $X = x$, where $x$ is a particular event:

$$p_{X}(x) = P\left(X=x\right)$$

The set of all possible outcomes for a discrete random variable $X$ is denoted as $X\left(\Omega\right)$. A PMF must satisfy the condition:

$$\sum_{x\in{X(\Omega)}}p_{X}(x)=1$$
````

The PMF is the weighing function for discrete random variables. To illustrate this idea, lets consider an example:

````{prf:example} PMF example
:label: ex-pmf-double-coin-flip

Let's consider an experiment where we flip a coin 2 times. The sample space $\Omega$ is given by:

$$\Omega = \left\{(HH),(HT),(TH),(TT)\right\}$$

````

### Bernoulli random variable
A Bernoulli random variable, the simplest random variable, models a coin-flip or some other type of binary
outcome. Bernoulli random variable have two states: either 1 or 0. The probability of getting 1 is $p$, while the probability of getting a value of 0 is $1 − p$. Bernoulli random variables model many binary events: coin flips (H or T), binary bits (1 or 0), true or false, yes or no, present or absent, etc.

````{prf:definition} Bernoulli Random Variable
:label: defn-pmf-bernouli

Let $X$ be a Bernoulli random variable. Then, the probability mass function of the Bernoulli random variable $X$ is:

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

### Binomial random variable
The binomial distribution is the probability of getting exactly $k$ successes in $n$ independent Bernoulli trials. For example, the chance of getting four heads in 6 coin tosses. 

````{prf:definition} Binomial Random Variable
:label: defn-pmf-binomial

Suppose we do repeated Bernoulli trials $X(\Omega) \in [0,1]^n$, i.e., $n$ trials of an independent binary experiment.
The probability of getting exactly $k$ successes in $n$ independent Bernoulli trials is governed by the binomial probability mass function:

$$p_{X}(k) = \binom{n}{k}p^{k}\left(1-p\right)^{n-k}\qquad{k=0,1,\dots,n}$$

where $k$ denotes the number of successes in $n$ independent experiments, the binomial parameter $0<p<1$ is the probability 
of a successful trial and:

$$\binom{n}{k} = \frac{n!}{k!\left(n-k\right)!}$$

The expectation of a binomial random variable is given by:

```{math}
\mathbb{E}\left[X\right] = np
```

while the variance $\text{Var}(X)$ is given by:

```{math}
\text{Var}\left[X\right] = np(1-p)
```

````

### Geometric random variable
We may be interested in doing a binary experiment, e.g., a coin flip until a specified outcome is obtained.
A geometric random variable governs the outcome of this type of experiment; 
a geometric random variable gives the probability that the first occurrence of success requires $k$ independent trials, each with success probability $p$. In other words, 
a geometric random variable describes the number of failures obtained before final success.

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

### Poisson random variable
The Poisson distribution is a discrete probability distribution that expresses the probability of a given number of events occurring during a fixed interval if these events occur with a known constant mean rate and independently of the time since the last event. In other words, a Poisson distribution can be used to estimate how likely it is that something will happen `X` number of times. For example, the number of car crashes in a city of a given size or the number of cheeseburgers sold at a fast-food chain on a Friday night.

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

(content:references:prob-distribution-functions)=
## Probability distribution functions
Fill me in.

---

## Summary

In this lecture:
* We introduced {ref}`content:references:set-theory` and the {ref}`content:references:union-intersection` of sets
* We introduced {ref}`content:references:probability` the Axioms of Probablity ({prf:ref}`axiom-probability`)
* We introduced {ref}`content:references:random-variables`