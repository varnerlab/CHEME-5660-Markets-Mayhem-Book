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

The finite union of two sets $A$ and $B$ contains all elements in $A$ or in $B$:

$$A\cup{B} = \left\{x\,\vert\,x\in{A} \text{ or } x\in{B}\right\}$$
````

The union of two sets connects the sets using the logical _or_ operator; 
thus, the union of two sets is always larger than or equal to the individual sets.

The [intersection](https://en.wikipedia.org/wiki/Intersection_(set_theory)) operation relys on the 
logical _and_ operator. Thus, the [intersection](https://en.wikipedia.org/wiki/Intersection_(set_theory)) finds the common elements of the two sets:

````{prf:definition}
:label: defn-intersection

The finite intersection of two sets $A$ and $B$ contains all elements in $A$ and in $B$:

$$A\cap{B} = \left\{x\,\vert\,x\in{A} \text{ and } x\in{B}\right\}$$
````