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

# Working with Data in Julia

## Introduction
Working with data is one of the most common tasks in any programming language, including [Julia](https://julialang.org). For example, loading data into a program, doing some calculations using that data, and then saving the results to a file (either locally or in the cloud) describes the majority of programs you will write in this course. 

There are various tools and approaches to reading and writing data files in [Julia](https://julialang.org). This chapter will consider a few common approaches and introduce some patterns for working with data files. In particular, we will:

* Introduce reading and writing {ref}`content:references:julia-csv-files`, a common data format for numerical data files
* Introduce more expressive tools such as {ref}`content:references:julia-dataframes`, which are in-memory tabular data structures
* Introduce reading and writing data in {ref}`content:references:julia-binary-formats`, a common approach for large data files and more complex data structures 

---

(content:references:julia-csv-files)=
## Comma seperated value files
Arguably, the most widely used data file format for the universe of possible applications is the [comma separated value (CSV) format](https://en.wikipedia.org/wiki/Comma-separated_values). A CVS file is a delimited text file that uses a comma to separate data values. Each line of a CSV file is called a record, where each record consists of one or more fields (data values), separated by commas; hence the name comma separated value file. 

A CSV file is typically used to store tabular data (numbers and text) in plain text, where each line has the same number of fields. However, the CSV file format is not standardized. Thus, while separating fields in records with commas is standard, various exceptions and exceptional cases sometimes make CSV files problematic, e.g., fields with commas in the data or records with a variable number of fields can make working CSV files challenging. 

Fortunately, the applications we are interested in typically involve numerical [CSV files](https://en.wikipedia.org/wiki/Comma-separated_values) that are easily handled using the [CSV.jl](https://github.com/JuliaData/CSV.jl) package. The [CSV.jl](https://github.com/JuliaData/CSV.jl) package can be downloaded and installed using the [Julia package manager](./julia-basics.md). To load the `CSV` package into your program, or the [REPL](./julia-basics.md), issue the [using](https://docs.julialang.org/en/v1/base/base/#using) or [import](https://docs.julialang.org/en/v1/base/base/#import) commands. Once loaded, the `CSV` package publishes several commands to read and write [CSV files](https://en.wikipedia.org/wiki/Comma-separated_values). 


(content:references:julia-dataframes)=
## DataFrames
Objects of type ``DataFrame`` represent data tables where each column corresponds vector of values. The simplest way to construct a DataFrame is to pass vectors holding the values for each column using keyword arguments or pairs:

```{code-cell} julia
using DataFrames
df = DataFrame(A=1:4, B=["M", "F", "F", "M"])
```

(content:references:julia-binary-formats)=
## Binary file formats
Binary file formats have been developed to store and organize large amounts of complex structured data. The basis of many binary formats is the [Hierarchical Data Format (HDF)](https://en.wikipedia.org/wiki/Hierarchical_Data_Format), a set of file formats initially developed by the [U.S. National Center for Supercomputing Applications (NCSA)](https://en.wikipedia.org/wiki/National_Center_for_Supercomputing_Applications). 

The [JLD2.jl](https://github.com/JuliaIO/JLD2.jl) package saves and loads [Julia](https://julialang.org) data structures in a format that is a subset of [HDF5](https://en.wikipedia.org/wiki/Hierarchical_Data_Format#HDF5), the latest iteration of the [Hierarchical Data Format (HDF)](https://en.wikipedia.org/wiki/Hierarchical_Data_Format). 

The [JLD2.jl](https://github.com/JuliaIO/JLD2.jl) package can be downloaded and installed using the [Julia package manager](./julia-basics.md). To load the `JLD2` package into your program, or the [REPL](./julia-basics.md), issue the [using](https://docs.julialang.org/en/v1/base/base/#using) or [import](https://docs.julialang.org/en/v1/base/base/#import) commands. Once the `JLD2  package is loaded, it publishes several commands to load and save data in the [HDF5](https://en.wikipedia.org/wiki/Hierarchical_Data_Format#HDF5) format.


---

## Summary

In this chpater we:
* Introduced reading and writing {ref}`content:references:julia-csv-files`, a standard data format for working with numerical data files
* Introduced more expressive tools such as {ref}`content:references:julia-dataframes`, which are in-memory tabular data structures. `DataFrames` are highly flexible data structures offering many advanced storage and query capabilities. 
* Introduced reading and writing data in {ref}`content:references:julia-binary-formats`, a common approach for large data files and more complex data structures  