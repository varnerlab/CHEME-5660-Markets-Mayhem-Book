# Sets, Probability, and Random Variables

What exactly is “probability”? Frequentists argue that probability is the relative frequency of an outcome. For example, flipping a fair coin has a probability of 1/2 of getting a head; if you flip the coin many times, you get a head half the time. On the other hand, Bayesians argue that probability is a subjective belief. For example, the probability of getting an A in a class is subjective because no one would want to take a class infinitely many times to obtain the relative frequency. Both the frequentists and Bayesians have valid points. However, differentiation between the frequentists and Bayesian points of view is often not required; the context of your problem will often suggest which perspective to use. For example, when you have a shortage of data, a Bayesian approach allows you to use prior knowledge. In contrast, frequentists tell us how to compute the confidence interval of an estimate, if we have a latge data set.

## Set theory
No matter whether you prefer the frequentist’s or the Bayesian’s view, there is a more fundamental foundation of probability thanks to [Andrey Kolmogorov](https://en.wikipedia.org/wiki/Andrey_Kolmogorov). The development of this fundamental definition will take some effort on our part, but we can distill it's essence: probability is a measure of the size of a set.
In mathematics, we are often interested in describing a collection of numbers, for example, a positive interval [a, b] on the real line or the ordered pairs of numbers that define a circle on a graph with two axes. These collections of numbers can be abstractly defined as sets. In a nutshell, a set is simply a collection of things. These things can be numbers, but they can also be alphabets, objects, or anything. Set theory is a mathematical tool that defines operations on sets. It provides the basic arithmetic for us to combine, separate, and decompose sets.

````{prf:definition}
:label: defn-sets

A set is a collection of elements. We denote

$$A = \left\{a_{1},a_{2},\dots,a_{n}\right\}$$

as the set $A$, where $a_{i}$ is the ith element of the set. 
````

To denote that an object $a$ belongs to the set $A$, we write $a\in{A}$. For example, the number $1$ belongs to the set ${1, 2, 3,\dots,10}$; we can write $1\in{1, 2, 3,\dots,10}$. The elements of sets can be anything; real numbers, complex numbers, functions or any mathematical object.

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