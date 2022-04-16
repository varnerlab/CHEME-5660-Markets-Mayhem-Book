# Sets, Probability, and Random Variables

What exactly is “probability”? Frequentists argue that probability is the relative frequency of an outcome. For example, if you flip a fair coin infinitely times, you expect to get heads half the time. On the other hand, Bayesians argue that probability is a subjective belief. For example, the probability of getting an A in a class is subjective because no one can take a class infinitely many times to obtain the relative frequency. Differentiation between the frequentists and Bayesian points of view is often not required; the context of your problem will typically suggest which perspective to use. For example, when you have a shortage of data, a Bayesian approach allows you to use prior knowledge. In contrast, frequentists tell us how to compute the confidence interval of an estimate, if we have a latge data set. Whether you prefer the frequentist’s or the Bayesian view, there is a more fundamental notion of probability thanks to [Andrey Kolmogorov](https://en.wikipedia.org/wiki/Andrey_Kolmogorov), namely, probability is a measure of the size of a set.

## Set theory
In mathematics, we are often interested in describing a collection of numbers or other mathematical objects, for example, the numbers $\left[a, b\right]$ on the real line, or the ordered pairs of numbers that define a circle. These collections of numbers can be abstractly defined as sets. 
A set is simply a collection of mathematical objets. Set theory is a mathematical tool that defines operations on sets. It provides the basic arithmetic for combining, separating, and decomposing sets.

````{prf:definition}
:label: defn-sets

A set is a collection of elements. We denote

$$A = \left\{a_{1},a_{2},\dots,a_{n}\right\}$$

as the set $A$, where $a_{i}$ is the ith element of the set. 
````

To denote that an object $a$ belongs to the set $A$, we write $a\in{A}$. 
For example, to show that the number $1$ belongs to the set $\left\{1, 2, 3,\dots,10\right\}$, 
we write $1\in\left\{1, 2, 3,\dots,10\right\}$. The elements of sets can be anything; real numbers, complex numbers, functions or any mathematical object.

Given a set, we often want to specify a portion of that set, which we call a subset.

````{prf:definition}
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

### Union and Intersection
We now discuss basic set operations. By operations, we mean functions of two or more sets whose output value is a set. We use these operations to combine and separate sets. Let's first describe the 
[union](https://en.wikipedia.org/wiki/Union_(set_theory)).

````{prf:definition}
:label: defn-union

The finite union of two sets $A$ and $B$ contains all elements in that are $A$ or in $B$:

$$A\cup{B} = \left\{x\,\vert\,x\in{A} \text{ or } x\in{B}\right\}$$
````

The union of two sets connects the sets using the logical _or_ operator; 
thus, the union of two sets is always larger than or equal to the individual sets.

The [intersection](https://en.wikipedia.org/wiki/Intersection_(set_theory)) operation relys on the 
logical _and_ operator. Thus, the [intersection](https://en.wikipedia.org/wiki/Intersection_(set_theory)) finds the common elements of the two sets:

````{prf:definition}
:label: defn-intersection

The finite intersection of two sets $A$ and $B$ contains all elements that are in both $A$ and in $B$:

$$A\cap{B} = \left\{x\,\vert\,x\in{A} \text{ and } x\in{B}\right\}$$
````

## Probability

A probability space is completley described by the tuple $(\Omega,\mathcal{F},P)$:

* Sample space $\Omega$: The set of all possible outcomes from an experiment.
* Event space $\mathcal{F}$: The collection of all possible events. An event E is a subset in $\Omega$ that defines an outcome or a combination of outcomes.
* Probability law $P$: A mapping from an event $A$ to a number $P(A)$ which, measures the _size_ of the event.

### Sample space $\Omega$
We start by defining the sample space $\Omega$. Given an experiment, the sample space $\Omega$ is the
set containing all possible outcomes of that experiment. These experimental outcomes can be numbers, alphabets, vectors, or functions, as well as, images, videos, EEG signals, audio speeches, etc.

### Event space $\mathcal{F}$
The sample space $\Omega$ contains all the possible outcomes. However, we typically are not interested in each of the individual outcomes; instead we are interested in sets of the outcomes where elements of these sets share some common trait 
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
A probability law $P$ is a function $P$ : $\Omega\rightarrow\left[0, 1\right]$;
the function $P$ maps an event $E\subseteq\Omega$ to a real number in $\left[0, 1\right]$.
The definition above does not specify how an event $E\subseteq\Omega$ is being mapped to a number. 
However, since probability is a measure of the size of a set, a meaningful probability law $P$ should be consistent for all $E\subseteq\Omega$. This requires rules, known as the axioms of probability, when we define the probability law $P$. 

```{prf:axiom} Axioms of Probability
:label: axiom-probability 

A probability law is a function $P:\Omega\rightarrow\left[0, 1\right]$ that maps an event $E\subseteq\Omega$
to a real number in $\left[0, 1\right]$. The function must satisfy the three axioms of probability:

* Non-negativity: $P(E)\geq{0}$, for any $E\subseteq\Omega$
* Normalization: $P(\Omega)=1$
* Additivity: For any disjoint event sets $\left\{E_{1}, E_{2}, \dots, E_{n}\right\}$ then $P\left(\bigcup_{i=1}^{n}E_{i}\right) = 
\sum_{i=1}^{n}P(E_{i})$

```

## Conditional Probability
The motivation of conditional probability is to restrict the probability to a subevent happening in the sample space. If B has happened, the probability for A to also happen is P[A∩B]/P[B]. If two events are not influencing each other, then we say that A and B are independent.

### Independence versus Disjoint
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

## Discrete Random Variables
The first step is to recognize that the sample space and the event space are all based on statements, for example, “getting a head when flipping a coin” or “winning the game.” These statements are not numbers, but we (engineers) love numbers. Therefore, we should ask a very basic question: How do we convert a statement to a number? 
The answer is a random variable; random variables are mappings from events to numbers.  

Suppose that we have constructed a random variable that translates statements to numbers. The next task is to endow the random variable with probabilities. More precisely, we need to assign probabilities to the random variable so that we can perform computations. This is done using the concept called [probability mass function (PMF)](https://en.wikipedia.org/wiki/Probability_mass_function).

````{prf:example} PMF example
:label: ex-pmf-cards

Let's consider an experiment that has four possible outcomes $\Omega=\left\{\clubsuit, \diamondsuit, \heartsuit, \spadesuit\right\}$

````
