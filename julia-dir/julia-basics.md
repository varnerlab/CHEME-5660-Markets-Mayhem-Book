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

### Julian REPL mode
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
## Julia types, functions and multiple dispatch
Fill me in.

(content:references:julia-programs)=
## Writing and Executing Julia programs
Fill me in.
