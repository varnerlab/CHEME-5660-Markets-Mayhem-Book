---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Julia
  language: julia
  name: julia-1.7
---

# Introduction to Julia Basics

## Introduction
[Julia](https://julialang.org) is a dynamically typed compiled programming language developed at [MIT](https://julia.mit.edu) for general purpose computing. [Julia](https://julialang.org) has a number of interesting features, and is an [open source project available under the MIT license](https://github.com/JuliaLang/julia). 

In this chapter, we will introduce some of the key features of [Julia](https://julialang.org):

* {ref}`content:references:julia-repl`
* {ref}`content:references:types-functions-md`
* {ref}`content:references:julia-programs`
* {ref}`content:references:julia-basics-using-external-packages`
---

(content:references:julia-repl)=
## The Julia REPL
You interact with [Julia](https://julialang.org) through the [Read Evaluate Print Loop (REPL)](https://docs.julialang.org/en/v1/stdlib/REPL/). The [REPL](https://docs.julialang.org/en/v1/stdlib/REPL/) allows for quick and easy evaluation of [Julia](https://julialang.org) commands; it has a searchable history, tab-completion, many helpful keybindings, and dedicated help and shell modes. The REPL can be started by launching Julia from the [Terminal on macOS](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac) or [by installing Windows Subsystem for Linux and launching Julia from an xterm](https://docs.microsoft.com/en-us/windows/wsl/install), or by double-clicking on the [Julia](https://julialang.org) executable, or finally by starting [Julia](https://julialang.org) from the command line in the [terminal of VSCode](https://code.visualstudio.com/docs/terminal/basics).

Once the [REPL](https://docs.julialang.org/en/v1/stdlib/REPL/) is started, there are __four__ possible modes that it can be in: 

* [Julian mode](https://docs.julialang.org/en/v1/stdlib/REPL/#The-Julian-mode): Default mode where commands and expressions are evaluated.
* [Help mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Help-mode): Launches the Julia ``help system mode`` where users can view documenation about functions or other Julia features.
* [Shell mode](https://docs.julialang.org/en/v1/stdlib/REPL/#man-shell-mode): Launches the ``shell mode`` which allows users to interact with the operating system shell. For Windows users, Julia's shell mode does not expose windows shell commands.
* [Package mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Pkg-mode): Launches the [Julia package manager](https://docs.julialang.org/en/v1/stdlib/Pkg/) which allows users to add or delete external packages. 

Let's go through each of these modes. 

### Julian mode
The [Julian REPL mode](https://docs.julialang.org/en/v1/stdlib/REPL/#The-Julian-mode) is the default mode of operation; each new line initially starts with the ``julia>`` prompt. [Julia](https://julialang.org) commands are entered at the prompt and the results are printed to the screen; hitting return or enter after a complete expression has been entered at the prompt will evaluate the entry and show the result of the last expression. 

```{figure} ./figs/Fig-Julian-mode-terminal.png
---
height: 460px
name: fig-julian-mode-terminal
---
The [Julian REPL mode](https://docs.julialang.org/en/v1/stdlib/REPL/#The-Julian-mode) in the [Terminal on macOS](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac).
```

{numref}`fig-julian-mode-terminal` shows a case where we enter values for two variables `x` and `y`and compute the result of `x + 2y`.

### Help mode
Users enter the [help mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Help-mode) by typing a ``?`` character at the prompt. Once in the [help mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Help-mode), which is indicated by the ``help?>`` prompt, users can type a command they have a question about (or use ``TAB`` for a list of autcomplete possibilities), hit enter and the documentation for that command is displayed.


```{figure} ./figs/Fig-Help-mode-terminal.png
---
height: 460px
name: fig-help-mode-terminal
---
The [help mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Help-mode) in the [Terminal on macOS](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac).
```

{numref}`fig-help-mode-terminal` shows the documentation for the `varinfo` command; `varinfo` returns a markdown table with information about exported global variables in a module, which (optionally) can be restricted to those matching `pattern`. 

If no search command is entered at the ``help?>`` prompt, the user can exit [help mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Help-mode) by typing the `backspace` key (which is the `delete` key on macOS).

### Shell mode
The [shell mode](https://docs.julialang.org/en/v1/stdlib/REPL/#man-shell-mode) is an advanced mode that allows the user to drop down to the [operating system shell](https://en.wikipedia.org/wiki/Shell_(computing)) i.e., a program that exposes an operating system's services and resources to a user (or other programs). 

Users enter the [shell mode](https://docs.julialang.org/en/v1/stdlib/REPL/#man-shell-mode) by typing the ``;`` character at the Julia prompt. Once in [shell mode](https://docs.julialang.org/en/v1/stdlib/REPL/#man-shell-mode), which is indicated by the ``shell>`` prompt, shell commands can be entered and the results displayed. 


```{figure} ./figs/Fig-Shell-mode-terminal.png
---
height: 560px
name: fig-shell-mode-terminal
---
The [shell mode](https://docs.julialang.org/en/v1/stdlib/REPL/#man-shell-mode) in the [Terminal on macOS](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac).
```

{numref}`fig-shell-mode-terminal` shows the results of the `ls -al` shell command; `ls -al` returns a list of file and directory names in long format for the current directory (my home directory on macOS). To exit [shell mode](https://docs.julialang.org/en/v1/stdlib/REPL/#man-shell-mode), a user types the `backspace` key (which is the `delete` key on macOS).

A list of basic [Unix shell commands can be found here](https://swcarpentry.github.io/shell-novice/reference.html).

(content:references:julia-repl-pkg-mode)=
### Package mode
The [package mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Pkg-mode) allows the user to add, delete or update external [Julia](https://julialang.org) packages. A user enters [package mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Pkg-mode) by hitting the ``]`` key which brings up the [package mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Pkg-mode) prompt ``pkg>``. At this prompt, users can manage the packages that are installed globally, or in the local project environment.

```{figure} ./figs/Fig-pkg-mode-terminal.png
---
height: 560px
name: fig-pkg-mode-terminal
---
The [package mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Pkg-mode) in the [Terminal on macOS](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac).
```

The results of the ``add Distributions`` command, which installs the [Distributions.jl](https://github.com/JuliaStats/Distributions.jl) package into the ``local_example_project`` project environment is shown in {numref}`fig-pkg-mode-terminal`. In addition to adding packages, users can update package versions globally or in the local project environment using the ``up`` command; packages can also be deleted using the ``rm <package>`` command. A full list of 
commands for managing packages in [package mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Pkg-mode) can be found [here](https://pkgdocs.julialang.org/v1/managing-packages/#**3.**-Managing-Packages). 

To exit [package mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Pkg-mode), a user types the `backspace` key (the `delete` key on macOS).

Loading installed packages into the [REPL](https://docs.julialang.org/en/v1/stdlib/REPL/) (or your program) is done with the [using](https://docs.julialang.org/en/v1/base/base/#using) or [import](https://docs.julialang.org/en/v1/base/base/#import) functions; we discuss what these functions do, and the differences between them, in the {ref}`content:references:julia-basics-using-external-packages` section. 

(content:references:types-functions-md)=
## Julia types, functions and syntax
Julia is a just-in-time compiled language (which gives it a runtime advantage over other popular interpreted languages). However, unlike other languages such as `C`, Julia code is compiled when you run it; a separate compile step is unnecessary. Thus, Julia gives the convenience and performance of a compiled language without the burden of manual compilation. 

Further, Julia is a dynamically-typed language. This means you are not required to declare the type of variables before you use them. Instead, when your Julia code is compiled, the compiler uses sophisticated logic to infer, i.e., guess your data types. However, users can also specify types, potentially lessening the compiler’s burden. Further, many users find codes with the types annotated to be easier to read and maintain; remember, you may be supporting codes for _decades_, thus, making them easy to understand is critical.

### Variable types
Variables are values that you tell your computer to associate with a specific name so that you can later recover or change their values.  Variables can be of different types; [Julia](https://julialang.org) has an extensive [type system](https://docs.julialang.org/en/v1/manual/types/). However, in this course we will primarily use [floating point numbers](https://docs.julialang.org/en/v1/manual/integers-and-floating-point-numbers/#Floating-Point-Numbers), [integers](https://docs.julialang.org/en/v1/manual/integers-and-floating-point-numbers/#Integers) and [Strings](https://docs.julialang.org/en/v1/manual/strings/).

In [Julia](https://julialang.org), we do not have to declare a variable name or specify the variable type as in other languages such as `C`; we can just set the variable, and the compiler will figure out the rest. For example, suppose we wanted to store a floating point value (of type `Float64`) in the variable `x`:

```{code-cell} julia
# Set the value for the variable x
x = 3.1;

# typeof prints the type of the arg passed in
typeof(x)
```

or store an integer (type `Int64`):

```{code-cell} julia
# Set the value for the variable x
x = 1;

# typeof prints the type of the arg passed in
typeof(x)
```

or a String:

```{code-cell} julia
# Set the value for the variable x
x = "HelloWorld";

# typeof prints the type of the arg passed in
typeof(x)
```

However, in some cases we may want to specify the type of a variable by using the `::` annotation, e.g., when composing the list of input arguments or the type of data returned from a function, or the type of items that are stored in a collection of items.

### Collections and Data Structures
There are several [Collections and Data Structures](https://docs.julialang.org/en/v1/base/collections/#Collections-and-Data-Structures) that come with [Julia](https://julialang.org), for example [Arrays](https://docs.julialang.org/en/v1/base/arrays/#Core.Array-Tuple{UndefInitializer,%20Any}), [Tuples](https://docs.julialang.org/en/v1/manual/functions/#Tuples), [Dictionaries](https://docs.julialang.org/en/v1/base/collections/#Base.Dict) and [Sets](https://docs.julialang.org/en/v1/base/collections/#Base.Set). 

In addition to the built-in collection types, a particularly useful data structure is called a [DataFrame](https://dataframes.juliadata.org/stable/) which is provided by the [DataFrames.jl](https://github.com/JuliaData/DataFrames.jl) package. We'll discuss [DataFrames](https://dataframes.juliadata.org/stable/) in the [Working with Data chapter](./julia-data.md).

#### Arrays
[Arrays](https://docs.julialang.org/en/v1/base/arrays/#lib-arrays) are collections that hold ordered lists of items of the same type (typcially). Arrays can be initialized empty (and filled with an arbitraty number of elements) or the number of elements of an Array can be specified when the Array is initialized. 

For example, this code block initializes an empty array of Float64 types:
```{code-cell} julia
# initialize an empty array of Floats -
x = Array{Float64,1}()

# typeof: prints the type of the arg passed in 
# length: returns number of elements in a 1d Array
typeof(x), length(x)
```

To add elements to an array that has no length, use the `push!` command:
```{code-cell} julia
# initialize an empty array of Floats -
x = Array{Float64,1}()

# add a Float64 -
push!(x,1.32)
push!(x,6.54)

# show the array x -
@show x;
```

Alternatively, we can specify the type and number of elements that we need:
```{code-cell} julia
# initialize an array of Float64 with 100 elements
# initially each element of the array is of type undef (undefined)
x = Array{Float64,1}(undef,100)

# typeof: prints the type of the arg passed in 
# length: returns number of elements in a 1d Array
typeof(x), length(x)
```

To add elements to an Array with specified dimensions, we can use the Array indexes; the first index is the row number, while the second is the column number of a two-dimensional Array. For example, this code block initializes a 2 x 2 matrix (a two-dimensional array), fills the matrix with ones, and then updates the 1,2-element with a random value:

```{code-cell} julia
# initialize a 2 x 2 array A 
A = Array{Float64,2}(undef,2,2)

# fill A with 1's
fill!(A, 1.0)

# update the 1,2 element with a random value -
A[1,2] = rand()

# show A -
@show A;
```

Please read through the [Array documentation](https://docs.julialang.org/en/v1/base/arrays/#lib-arrays) for a detailed discussion of the properties of Arrays and [the various functions that can operate on Arrays](https://docs.julialang.org/en/v1/base/arrays/#Basic-functions).

(content:references:julia-basics-tuples)=
#### Tuples
Julia has a built-in data structure called a [tuple](https://docs.julialang.org/en/v1/manual/functions/#Tuples); a [tuple](https://docs.julialang.org/en/v1/manual/functions/#Tuples) is a fixed-length container that can hold a mixture of values of any type, but cannot be modified i.e., it is immutable once the values have been added to the [tuple](https://docs.julialang.org/en/v1/manual/functions/#Tuples). In other words, [tuples](https://docs.julialang.org/en/v1/manual/functions/#Tuples); a [tuple](https://docs.julialang.org/en/v1/manual/functions/#Tuples) are read-only once constructed. [Tuples](https://docs.julialang.org/en/v1/manual/functions/#Tuples) are constructed with commas and parentheses, and can be accessed via indexing:

```{code-cell} julia
# initialize a tuple of stuff -
x = (0.0, "hello", 6*7)

# what is held in index 2?
@show x[2];
```

Further, you can optionally give the values held in a tuple a name; these types of data structures are called [NamedTuples](https://docs.julialang.org/en/v1/manual/functions/#Named-Tuples). 

```{code-cell} julia
# initialize a named tuple of stuff -
x = (firstname="Fred", lastname="Rogers")

# what is the first name?
@show x.firstname;
```

You can access the values stored in a [NamedTuple](https://docs.julialang.org/en/v1/manual/functions/#Named-Tuples) using `dot notation` (as shown above). However, because a [NamedTuple](https://docs.julialang.org/en/v1/manual/functions/#Named-Tuples) is just a fancy [Tuple](https://docs.julialang.org/en/v1/manual/functions/#Tuples), you can also access data through indexing:

```{code-cell} julia
# initialize a named tuple of stuff -
x = (firstname="Fred", lastname="Rogers")

# what is the first name?
@show x[1];
```

#### Dictionaries
One the most useful built-in data structures in Julia is the [Dictionary](https://docs.julialang.org/en/v1/base/collections/#Dictionaries); [Dictionaries](https://docs.julialang.org/en/v1/base/collections/#Dictionaries) allow the user to store `key => value` pairs, where the (key, value) pairs can be anytype. 

There are several ways to create [Dictionaries](https://docs.julialang.org/en/v1/base/collections/#Dictionaries) in Julia. For example, [Dicts](https://docs.julialang.org/en/v1/base/collections/#Base.Dict) can be created by passing pair objects constructed with the `=>` operator to a [Dict](https://docs.julialang.org/en/v1/base/collections/#Base.Dict) constructor: 

```{code-cell} julia
# build a Dict -
d = Dict("A"=>1, "B"=>2)

@show d;
```

This call attempts to infer type information stored in the dictionary from the keys and values, i.e. this example creates a Dict{String, Int64}. However, you can also explicitly specify the types of the `key => value` pairs by initializing the constructor with type information `Dict{KeyType,ValueType}(...)`: 

```{code-cell} julia
# build a Dict -
d = Dict{String,Int32}("A"=>1, "B"=>2)

@show typeof(d);
```

Given a dictionary `D`, the syntax `D[x]` returns the value stored in `D` with key `x` (if key `x` exists) or throws an error. On the other hand, a statement like `D[x] = y` stores the key-value pair `x => y` in `D` (replacing any existing value for the key `x`). Multiple arguments to `D[...]` are converted to [tuples](https://docs.julialang.org/en/v1/manual/functions/#Tuples); for example, the syntax `D[x,y]` is equivalent to `D[(x,y)]`, i.e. it refers to the value with a key equal to the tuple (x,y).

[Dictionaries](https://docs.julialang.org/en/v1/base/collections/#Dictionaries) have fast data lookup, insertion, and deletion. Thus, they are ideal for in-memory storage of all kinds of data. However, [Dictionaries](https://docs.julialang.org/en/v1/base/collections/#Dictionaries) do not maintain order, i.e., the keys in [Dictionary](https://docs.julialang.org/en/v1/base/collections/#Dictionaries) are not ordered. Thus, if the order of data is important then a [Dictionary](https://docs.julialang.org/en/v1/base/collections/#Dictionaries) may not by an appropriate data structure.
Further, [Dictionaries](https://docs.julialang.org/en/v1/base/collections/#Dictionaries) by default are mutable, i.e., they can be changed after they are constructed; this is a good thing most of the time, but care should be taken to regulate changes to dictionaries. 

For use cases where data should not be changed, i.e., configuration data or other such applications, an immutable dictionary can be created, see [ImmutableDict](https://docs.julialang.org/en/v1/base/collections/#Base.ImmutableDict).

There are many methods for working with [Dictionaries](https://docs.julialang.org/en/v1/base/collections/#Dictionaries), check out the [Julia documentation](https://docs.julialang.org/en/v1/base/collections/#Base.haskey).

#### Sets
[Sets](https://docs.julialang.org/en/v1/base/collections/#Base.Set), like arrays, hold a mutable collection of objects. However, unlike an array, the items in a [Set](https://docs.julialang.org/en/v1/base/collections/#Base.Set) must be unqiue. Further, [Sets](https://docs.julialang.org/en/v1/base/collections/#Base.Set) do not maintain order. Thus, a useful mental model for a [Set](https://docs.julialang.org/en/v1/base/collections/#Base.Set) is a sack of unique objects. 

[Sets](https://docs.julialang.org/en/v1/base/collections/#Base.Set) are constructured by passing an interable collection of items into the constructor:

```{code-cell} julia
# build a set S (notice the brackets)
# We are adding repeated elements, we have two 3's what is going to happen?
S = Set([1, 3, 4, 5, 3]);

@show S;
```

When adding objects to a set, if the object is already present, any repeated objects will not be added. [Sets](https://docs.julialang.org/en/v1/base/collections/#Base.Set) can also be initialized empty, then items added using the `push!` function:

```{code-cell} julia
# build an empty set of type Int
S = Set{Int}();

# add some items to the set S -
push!(S,1);
push!(S,3);
push!(S,5);
push!(S,1); # repeat: will not get added to S

# show the set -
@show S;
```

However, unlike arrays, [sets](https://docs.julialang.org/en/v1/base/collections/#Base.Set) can not be indexed, i.e., there is not an order hence no indexes. Thus, to retrieve an item from a [set](https://docs.julialang.org/en/v1/base/collections/#Base.Set) use the [pop!](https://docs.julialang.org/en/v1/base/collections/#Base.pop!) function which removes a _random_ element from the [set](https://docs.julialang.org/en/v1/base/collections/#Base.Set). 

```{code-cell} julia
# build a set S -
S = Set([1,2])
println("Output 1: Set S = $(S)")

# remove element -
x = pop!(S)
println("Output 2: what value of x did we get = $(x)")

# show the S -
@show S;
```

Many functions that work with other collection types, e.g., the [length](https://docs.julialang.org/en/v1/base/arrays/#Base.length-Tuple{AbstractArray}) function for arrays, have an equilvent implementation for [sets](https://docs.julialang.org/en/v1/base/collections/#Base.Set):

```{code-cell} julia
# another way to build a set - array comprehension
S = Set{Int}([2i for i = 1:5])

# how many elements?
println("The number of elements of set S = $(length(S))")
```

Finally, there are several set-specific concepts, [which are useful in the context of probability](../chapter-2-dir/probability-random-variables.md), that have been implemented in Julia. For example, the [intersection](https://en.wikipedia.org/wiki/Intersection_(set_theory)) or [union](https://en.wikipedia.org/wiki/Union_(set_theory)) of sets is encoded in the [intersect](https://docs.julialang.org/en/v1/base/collections/#Base.intersect) and [union](https://docs.julialang.org/en/v1/base/collections/#Base.union) functions.

### Program Control Flow
Julia provides several tools for [program control flow](https://docs.julialang.org/en/v1/manual/control-flow/#Control-Flow) and [repeated evaluation](https://docs.julialang.org/en/v1/manual/control-flow/#man-loops); let's review a few important examples: `if` statements, `while` loops and `for` loops.

#### If-else-end statements
Fill me in.

#### While loops
A `while` loop consists of a control statement and a body:

```{code-block} julia
while statement == true
  body
end
```

In a `while` loop, a control statement is evaluated, and as long as the control statement remains true, the code in the body of the `while` loop is executed. For example:

```{code-cell} julia
# declarations -
counter = 1       # loop counter, we start at 1
const limit = 5   # how many times do we want to go around?

# main loop -
while (counter <= limit)

  # body to execute (for now, print info about the counter) -
  delta = limit - counter; # how many more times around?
  println("Counter = $(counter), remaining = $(delta)")

  # update the counter value -
  global counter = counter + 1
end
```

In this example, the `while` loop continues to execute as long the statement $\text{counter}\leq\text{limit}$ evaluates to `true`. However, the value of $\text{counter}$ is updated each pass through the loop. Thus, when the value of $\text{counter} = 6$, the control statement fails (evaluates to `false`) and the loop stops.

If the control statement evaluates to `false` when the `while` loop is first reached, the body of the `while` statement is never evaluated. 

#### For loops
The `for` loop makes repeated evaluation of a code block easier to write; since counting like the `while` loop is such a common programming task, it can be expressed more concisely with a `for` loop:

```{code-block} julia
for range
  body
end
```

where `range` represent the list of items to iterate over. For example, we can re-write the `while` loop shown above as a the `for` loop:

```{code-cell} julia
# declarations -
const limit = 5   # how many times do we want to go around?

# main loop -
for i = 1:limit

  # body that is executed (for now, print info about the index) -
  delta = limit - i; # how many more times around?
  println("index i = $(i), remaining = $(delta)")

end
```

where the 1:limit is a [range object](https://docs.julialang.org/en/v1/base/math/#Base.range), which in this case represents the sequence of numbers $1,2,\dots,\text{limit}$. The `for` loop iterates through these values, assigning each one to the loop index variable $i$. 

One important difference between the `while` loop example and the equivlant `for` loop form is the scope in which variables are visible. If the loop index variable $i$ has not been introduced previously in another scope, in the `for` loop form, it is visible only inside of the `for` loop, and not outside/afterwards. For more information on variable score, see the [scope of variables documentation](https://docs.julialang.org/en/v1/manual/variables-and-scoping/#scope-of-variables).

### Functions
In [Julia](https://julialang.org), a function is an object that maps a [tuple](https://docs.julialang.org/en/v1/manual/functions/#Tuples) of argument values to a return value. Unlike pure mathematical functions, [Julia](https://julialang.org) functions can alter their arguments and change the global state of the program. The basic syntax for defining functions in [Julia](https://julialang.org) is:

```{code-cell} julia

# declare the add function -
function add(x::Float64, y::Float64)::Float64
  return (x+y)
end

# compute the sum of two numbers -
value_1 = add(3.0, 2.0);

# print the resulting value -
println("Value from the add function: $(value_1)")
```

The `add` function accepts two arguments `x` and `y` (both of type `Float64`) and returns the sum (also of type `Float64`). Notice that when we declared the `add` function, we specified the types of the arguments and the return type using the `::` operator. 

Thus, if we pass in arguments that are not of the correct type, an error will occur:

```{code-cell} julia

# declare the add function -
function add(x::Float64, y::Float64)::Float64
  return (x+y)
end

try 
  
  # compute the sum of two numbers -
  value_1 = add(3.0, "Two");

  # print the resulting value -
  println("Value from the add function: $(value_1)")

catch error
  
  bt = backtrace()
  msg = sprint(showerror, error, bt)
  println(msg)
end
```

[Julia](https://julialang.org) function arguments follow the pass-by-sharing convention, i.e., values are __not__ copied when they are passed to functions. Instead, function arguments act as new variable bindings (new locations that can refer to values), but the values they refer to are identical to the passed values. 

#### Multiple dispatch and generics
In the example above, the `add` function takes arguments of type `Float64`, but what if we want to sum arguments of type `Int64` or some other numerical format such as `Float32` (which is popular in the machine learning community), or a combination of these arguments? 

[Julia](https://julialang.org) approaches this problem using a technique called [multiple dispatch](https://en.wikipedia.org/wiki/Multiple_dispatch). In particular, program developers can write different versions of the `add` function that accept different argument types; these different `add` versions are called [methods](https://docs.julialang.org/en/v1/manual/methods/#Methods). At runtime, [Julia](https://julialang.org) dynamically determines which [method](https://docs.julialang.org/en/v1/manual/methods/#Methods) to call based upon the argument types. For example:

```{code-cell} julia

# declare the add function that works on Float64
function add(x::Float64, y::Float64)::Float64
  return (x+y)
end

# declare the add function that works on Int64
function add(x::Int64, y::Int64)::Int64
  return (x+y)
end

# Julia determines which version of add to call
value_1 = add(3.0, 2.0);
value_2 = add(2,6)

# print the resulting value -
println("Values from the add methods: value_1 = $(value_1), value_2 = $(value_2)")
```

In this case, the correct version of `add` is called based on the type of arguments. However, writing different `add` methods for each argument type (or combination of argument types) would be a burden. 

Toward this challenge, [Julia](https://julialang.org) has [parametric methods](https://docs.julialang.org/en/v1/manual/methods/#Parametric-Methods) in which the argument type itself is variable. In particular, instead of specifying the specific argument type, e.g., `Float64` or `Int64`, we declare rules that generate a set of permissible types that we expect the function can operate on. For example, the parametric `add` function:

```{code-block} julia
function add(x::T1, y::T2)::Number where {T1, T2 <: Number} 
  return (x+y)
end
```

specifies that the argument types `T1` and `T2` are a [subtype](https://docs.julialang.org/en/v1/devdocs/reflection/#Subtypes) (defined using the `<:` operator) of [Number](https://docs.julialang.org/en/v1/base/numbers/#Core.Number), the supertype for all numbers in [Julia](https://julialang.org); thus, we expect the parametric `add` function to work on _any_ combination of real and complex numbers. This is possible because the `+` operator that appears in the `add` function is itself a function with 206 methods (which can be listed using the [methods](https://docs.julialang.org/en/v1/base/base/#Base.methods) function).

```{code-cell} julia

# declare the add function -
function add(x::T1, y::T2)::Number where {T1, T2 <: Number} 
  return (x+y)
end

# Julia determines which version of add to call
value_1 = add(3.0, 2);
value_2 = add(2,6)

# print the resulting values -
println("Values from the add methods: value_1 = $(value_1), value_2 = $(value_2)")
```

(content:references:julia-programs)=
## Writing and Executing Julia Programs
Julia programs are files with the extension ``.jl``. To load a Julia program contained in ``Program.jl``, the user executes the [include](https://docs.julialang.org/en/v1/manual/code-loading/) command in the [REPL](https://docs.julialang.org/en/v1/stdlib/REPL/) where the path to ``Program.jl`` is passed in as an argument of type ``String`` to the [include](https://docs.julialang.org/en/v1/manual/code-loading/) command. 

```{code-block} julia
julia> include("Program.jl")
```

The code block above loads the code contained in the ``Program.jl`` file into the [REPL](https://docs.julialang.org/en/v1/stdlib/REPL/). If ``Program.jl`` is an _executable script_ then ``Program.jl`` will be executed, otherwise, the variables, data structures and functions encoded in ``Program.jl`` will be loaded into the memory of the [REPL](https://docs.julialang.org/en/v1/stdlib/REPL/). To make ``Program.jl`` executable, a `main` method is called (which in turn can load data, call other functions, etc):

```{code-block} julia

function example()

    # stuff happens here
    # ...
end

function main()
    
    # load data 
    # ...

    # call other functions -
    example()

end

# call main method
main()
```

For example, consider the following executable script:

```{code-cell} julia
function example()

    # stuff happens here
    println("A message from inside the example method ... ")
end

function main()
    
    # print a message -
    println("A message from inside the main method ...")

    # call other functions -
    example()
end

# call the main method -
main()
```

The `example` method is loaded into the [REPL](https://docs.julialang.org/en/v1/stdlib/REPL/) memory before the `main` method (code is parsed by [Julia](https://julialang.org) from top to bottom of the file) but `example` is _not_ executed until is called from the `main` method. 

(content:references:julia-basics-using-external-packages)=
## Using external packages
External packages in [Julia](https://julialang.org) are organized as [Modules](https://docs.julialang.org/en/v1/manual/modules/); the basic structure of a module is given by:

```{code-block} julia

module SomeModule

# export, using, import statements are usually here; we discuss these below

include("file1.jl")
include("file2.jl")

end

```

Thus, [modules](https://docs.julialang.org/en/v1/manual/modules/) in [Julia](https://julialang.org) are just containers that organize functions, and perhaps [user defined types](https://docs.julialang.org/en/v1/manual/types/#Composite-Types) or other data, into a unit. While constructing your own [modules](https://docs.julialang.org/en/v1/manual/modules/) is not difficult, it's beyond the scope of this introduction. For more information on building (and registering) your own [modules](https://docs.julialang.org/en/v1/manual/modules/), please consult the [Julia documentation](https://docs.julialang.org/en/v1/). 

Let's assume that you have used the {ref}`content:references:julia-repl-pkg-mode` to install some external [Julia](https://julialang.org) package called `Foo.jl`. To use that package in your `Program.jl` (or in the [REPL](https://docs.julialang.org/en/v1/stdlib/REPL/)) you'll need to load `Foo.jl` module into memory. There are two ways to do that, the [using](https://docs.julialang.org/en/v1/base/base/#using) or [import](https://docs.julialang.org/en/v1/base/base/#import) functions.

* The [using](https://docs.julialang.org/en/v1/base/base/#using) function will load the `Foo` package and make its [exported names](https://docs.julialang.org/en/v1/base/base/#export) available for _direct_ use, i.e., the functions and data contained in the package that are visible are loaded directly into memory for the users of the package. However, names can also be accessed via dot syntax (e.g., Foo.foo to access the name foo), whether exported or not.

* The [import](https://docs.julialang.org/en/v1/base/base/#import) function is similar to [using](https://docs.julialang.org/en/v1/base/base/#using) with one key exception; [import](https://docs.julialang.org/en/v1/base/base/#import) will load the package `Foo`. However, names from the imported `Foo` module can _only_ be accessed with dot syntax (e.g., Foo.foo to access the name foo).

Let's do an example. Suppose we wanted to generate samples from and then visualize a [Laplace distribution](https://en.wikipedia.org/wiki/Laplace_distribution) using [Distributions.jl](https://github.com/JuliaStats/Distributions.jl), a [Julia](https://julialang.org) package for probability distributions and associated functions, and [StatsPlots.jl](https://github.com/JuliaPlots/StatsPlots.jl), a [Julia](https://julialang.org) package for statistical visualization. Further, suppose we have already installed [Distributions.jl](https://github.com/JuliaStats/Distributions.jl) and [StatsPlots.jl](https://github.com/JuliaPlots/StatsPlots.jl) using the {ref}`content:references:julia-repl-pkg-mode`.

The code block:

```{code-block} julia

# load packages -
using Distributions
using StatsPlots

# Build a Laplace distribution (from the Distributions package)
d = Laplace(0,1); # initialize Laplace distribution with (0,1)

# plot the distribution (from StatsPlots package) -
plot(d,lw=2, label="(μ,b) = (0,1)")
xlabel!("Value for x (AU)", fontsize=18)
ylabel!("Laplace(x) proability density (AU)", fontsize=18)
```

where the `Laplace` and `plot` functions are exported from [Distributions.jl](https://github.com/JuliaStats/Distributions.jl) and [StatsPlots.jl](https://github.com/JuliaPlots/StatsPlots.jl), respectively,  produces the plot:

```{figure} ./figs/Fig-LaplaceDistribution-PDF.pdf
---
height: 420px
name: fig-laplace-pdf
---
Plot of a [Laplace distribution](https://en.wikipedia.org/wiki/Laplace_distribution) using [Distributions.jl](https://github.com/JuliaStats/Distributions.jl) and [StatsPlots.jl](https://github.com/JuliaPlots/StatsPlots.jl)
```


## Summary
In this chapter, we introduced some key features of [the Julia programming language](https://julialang.org):

* Working with {ref}`content:references:julia-repl`
* {ref}`content:references:types-functions-md`
* {ref}`content:references:julia-programs`

For more information on [Julia](https://julialang.org), please consult the [Julia documentation](https://docs.julialang.org/en/v1/).