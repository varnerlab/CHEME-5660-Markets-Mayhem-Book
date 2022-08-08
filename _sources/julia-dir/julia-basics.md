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

* Working with {ref}`content:references:julia-repl`
* {ref}`content:references:types-functions-md`
* {ref}`content:references:julia-programs`

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

### Package mode
The [package mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Pkg-mode) allows the user to add, delete or update external [Julia](https://julialang.org) packages. A user enters [package mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Pkg-mode) by hitting the ``]`` key which brings up the [package mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Pkg-mode) prompt ``pkg>``. At this prompt, users can manage the packages that are installed globally, or in the local project environment.

```{figure} ./figs/Fig-pkg-mode-terminal.png
---
height: 560px
name: fig-pkg-mode-terminal
---
The [package mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Pkg-mode) in the [Terminal on macOS](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac).
```

{numref}`fig-pkg-mode-terminal` shows the results of the ``add Distributions`` command, which installs the [Distributions.jl](https://github.com/JuliaStats/Distributions.jl) package into the ``local_example_project`` project environment. In addition to adding packages, users can update package versions globally or in the local project environment using the ``up`` command; packages can also be deleted using the ``rm <package>`` command. A full list of 
commands for managing packages in [package mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Pkg-mode) can be found [here](https://pkgdocs.julialang.org/v1/managing-packages/#**3.**-Managing-Packages). To exit [package mode](https://docs.julialang.org/en/v1/stdlib/REPL/#Pkg-mode), a user types the `backspace` key (the `delete` key on macOS).

(content:references:types-functions-md)=
## Julia types, functions and syntax
Julia is a just-in-time compiled language (which gives it a runtime advantage over other popular interpreted languages). However, unlike other languages such as `C`, Julia code is compiled when you run it; a separate compile step is unnecessary. Thus, Julia gives the convenience and performance of a compiled language without the burden of manual compilation. 

Further, Julia is a dynamically-typed language. This means you are not required to declare the type of variables before you use them. Instead, when your Julia code is compiled, the compiler uses sophisticated logic to infer, i.e., guess your data types. However, users can also specify types, potentially lessening the compiler’s burden. Further, many users find codes with the types annotated to be easier to read and maintain; remember, you may be supporting codes for _decades_, thus, making them easy to understand has an upside.

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

However, in some cases we may want to specify the type of a variable by using the `::` annotation, e.g., when composing 
the list of input arguments or the type of data returned from a function, or the type of items that are stored in a collection of items.

### Collections and Data Structures
There are several [Collections and Data Structures](https://docs.julialang.org/en/v1/base/collections/#Collections-and-Data-Structures) that come with [Julia](https://julialang.org), for example [Arrays](https://docs.julialang.org/en/v1/base/arrays/#Core.Array-Tuple{UndefInitializer,%20Any}), [Tuples](https://docs.julialang.org/en/v1/manual/functions/#Tuples), [Dictionaries](https://docs.julialang.org/en/v1/base/collections/#Base.Dict) and [Sets](https://docs.julialang.org/en/v1/base/collections/#Base.Set). However, in addition to the built-in collection types, a particularly useful data structure is called a [DataFrame](https://dataframes.juliadata.org/stable/) which is provided by the [DataFrames.jl](https://github.com/JuliaData/DataFrames.jl) package. 

#### Arrays
Fill me in.

#### Tuples
Fill me in.

#### Dictionaries
Fill me on.

#### Sets
Fill me in.

#### DataFrames
Objects of type ``DataFrame`` represent data tables where each column corresponds vector of values. The simplest way to construct a DataFrame is to pass vectors holding the values for each column using keyword arguments or pairs:

```{code-cell} julia
using DataFrames
df = DataFrame(A=1:4, B=["M", "F", "F", "M"])
```

### Program Control Flow
Fill me in.

### Functions
In [Julia](https://julialang.org), a function is an object that maps a [tuple](https://docs.julialang.org/en/v1/manual/functions/#Tuples) of argument values to a return value. Unlike pure mathematical functions, [Julia](https://julialang.org) functions can alter and be affected by the global state of the program. The basic syntax for defining functions in [Julia](https://julialang.org) is:

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


(content:references:julia-programs)=
## Writing and Executing Julia Programs
Julia programs are written in files with the extension ``.jl``. To load a Julia program contained in ``Program.jl``, the user executes the [include](https://docs.julialang.org/en/v1/manual/code-loading/) command in the [REPL](https://docs.julialang.org/en/v1/stdlib/REPL/) where the path to ``Program.jl`` is passed in as an argument of type ``String`` to the [include](https://docs.julialang.org/en/v1/manual/code-loading/) command. 

````{prf:example} Include command
:label: include-example-julia-program

Julia code can be loaded using the [include](https://docs.julialang.org/en/v1/manual/code-loading/) command. 
For example, to load Julia code in the ``Program.jl`` file, the user would execute the command in the [Julia REPL](https://docs.julialang.org/en/v1/stdlib/REPL/):

```julia
julia> include("Program.jl")
```

````

{prf:ref}`include-example-julia-program` loads the code contained in the ``Program.jl`` file into the [REPL](https://docs.julialang.org/en/v1/stdlib/REPL/). If ``Program.jl`` is an _executable script_ then ``Program.jl`` will be executed, otherwise, the variables, data structures and functions encoded in ``Program.jl`` will be loaded into the memory of the [REPL](https://docs.julialang.org/en/v1/stdlib/REPL/). To make ``Program.jl`` executable, a `main` method is called (which in turn can load data, call other functions, etc):

````{prf:example} Executable Program.jl
:label: executable-julia-program-template

```julia

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
````