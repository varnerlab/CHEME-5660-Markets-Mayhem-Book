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

# Working with Data in Julia

## Introduction
Working with data is one of the most common tasks in any programming language, including [Julia](https://julialang.org). For example, loading data into a program, doing some calculations using that data, and then saving the results to a file (either locally or in the cloud) describes the majority of programs you will write in this course. 

There are various tools and approaches to reading and writing data files in [Julia](https://julialang.org). This chapter will consider a few common approaches and introduce some patterns for working with data files. In particular, we will:

* Introduce reading and writing {ref}`content:references:julia-csv-files`, a common data format for numerical data files
* Introduce more expressive tools such as {ref}`content:references:julia-dataframes`, which are in-memory tabular data structures
* Introduce reading and writing data in {ref}`content:references:julia-binary-formats`, a common approach for large data files and more complex data structures 

---

(content:references:julia-csv-files)=
## Comma seperated value (CSV) files
Arguably, the most widely used data file format for the universe of possible applications is the [comma separated value (CSV) format](https://en.wikipedia.org/wiki/Comma-separated_values). A CVS file is a delimited text file that uses a comma to separate data values. Each line of a CSV file is called a record, where each record consists of one or more fields (data values), separated by commas; hence the name comma separated value file. 

A CSV file is typically used to store tabular data (numbers and text) in plain text, where each line has the same number of fields. However, the CSV file format is not standardized. For example, column headers may or may not be present. Further, while separating fields in records with commas is standard, various exceptions and exceptional cases sometimes make CSV files problematic, e.g., fields with commas in the data or records with a variable number of fields can make working CSV files challenging.  

Fortunately, the applications we are interested in typically involve numerical [CSV files](https://en.wikipedia.org/wiki/Comma-separated_values) that are easily handled using the [CSV.jl](https://github.com/JuliaData/CSV.jl) package. The [CSV.jl](https://github.com/JuliaData/CSV.jl) package can be downloaded and installed using the [Julia package manager](./julia-basics.md). To load the `CSV` package into your program, or the [REPL](./julia-basics.md), issue the [using](https://docs.julialang.org/en/v1/base/base/#using) or [import](https://docs.julialang.org/en/v1/base/base/#import) commands. Once loaded, the `CSV` package publishes several commands to read and write [CSV files](https://en.wikipedia.org/wiki/Comma-separated_values). 

The main methods exported by the [CSV.jl](https://github.com/JuliaData/CSV.jl) package are the [CVS.read](https://csv.juliadata.org/stable/reading.html#CSV.read) and [CVS.write](https://csv.juliadata.org/stable/writing.html#CSV.write) methods. 

* [CVS.read](https://csv.juliadata.org/stable/reading.html#CSV.read) allows the user to load a data file into one of several data structures
* [CVS.write](https://csv.juliadata.org/stable/writing.html#CSV.write) allows the user to write a tabular data structure to a CSV file. 

For most of the applications, we will be doing, the source and sink data structure will be [DataFrames](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame), a handy tabular data structure. Thus, we do not read (or write) a [DataFrame](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame) directly; instead, we store it as (or read from) a CSV file. 

(content:references:julia-dataframes)=
## DataFrames
[DataFrame.jl](https://github.com/JuliaData/DataFrames.jl) is a [Julia](https://julialang.org) package that provides tools for working with tabular data in [Julia](https://julialang.org), e.g., numerical data tables. The [DataFrame.jl](https://github.com/JuliaData/DataFrames.jl) package can be downloaded and installed using the [Julia package manager](./julia-basics.md). To load the `DataFrames` package into your program, or the [REPL](./julia-basics.md), issue the [using](https://docs.julialang.org/en/v1/base/base/#using) or [import](https://docs.julialang.org/en/v1/base/base/#import) commands. Once the `DataFrames`  package is loaded, it publishes several commands to work with tabular data.

Objects of type [DataFrame](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame) represent data tables where each column corresponds vector of values. The simplest way to construct a [DataFrame](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame) is to pass vectors holding the values for each column using keyword arguments or pairs:

```{code-cell} julia
# This example was reproduced from the DataFrames.jl package documentation
# https://dataframes.juliadata.org/stable/man/basics/#First-Steps-with-DataFrames.jl

# Load external packages
using DataFrames

# build a sample DataFrame -> store in variable df
df = DataFrame(A=1:4, B=["M", "F", "F", "M"])
```

A [DataFrame](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame) can also be created from a [Dictionary](https://docs.julialang.org/en/v1/base/collections/#Dictionaries), where the column header names are constructed from the keys of the dictionary, and the column values are the data associated with each key:

```{code-cell} julia
# This example was reproduced from the DataFrames.jl package documentation
# https://dataframes.juliadata.org/stable/man/basics/#First-Steps-with-DataFrames.jl

# Load external packages
using DataFrames

# create a dictionary w/data -> variable dict
dict = Dict(
  :customer_age => [22, 20, 25], 
  :first_name => ["Rohit", "Rahul", "Akshat"],
  :state => ["IN","CA","OR"]
);

# convert the dictionary to a DataFrame -> variable df
df = DataFrame(dict)
```

Notice the [Dictionary](https://docs.julialang.org/en/v1/base/collections/#Dictionaries) keys are of type [Symbol](https://docs.julialang.org/en/v1/base/base/#Core.Symbol) and __not__ [Strings](https://docs.julialang.org/en/v1/base/strings/#lib-strings); a [Symbol](https://docs.julialang.org/en/v1/base/base/#Core.Symbol) represents a special type of identifier in [Julia](https://julialang.org). [Symbols](https://docs.julialang.org/en/v1/base/base/#Core.Symbol) are often used as names or labels to identify an entity, e.g., as a dictionary key as shown above. [Symbols](https://docs.julialang.org/en/v1/base/base/#Core.Symbol) can be entered using the `:` quote operator or constructed from [Strings](https://docs.julialang.org/en/v1/base/strings/#lib-strings) using the `Symbol(x...)` constructor method.

### Why are DataFrames interesting?
[DataFrames](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame) are interesting because, in many ways, they act like [Arrays](https://docs.julialang.org/en/v1/base/arrays/), e.g., they can be indexed to access values, and they are [iterable](https://docs.julialang.org/en/v1/base/collections/#lib-collections-iteration), i.e., they can be used in loops. Further, entire columns can be accessed by the column names. 

For example, suppose we have a [DataFrame](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame) stored in a variable `df` that holds demographic data about clients, e.g., names, ages, etc. We can access entire columns (or the data from a collection of columns) by the column name using the syntax `df[! colname]` or with dot notation `df.colname` for a single column:

```{code-cell} julia
# modified from the DataFrames.jl package documentation
# https://dataframes.juliadata.org/stable/man/basics/#First-Steps-with-DataFrames.jl

# Load external packages
using DataFrames

# create a dictionary w/data -> variable dict
dict = Dict(
  :customer_age => [22, 20, 25], 
  :first_name => ["Rohit", "Rahul", "Akshat"],
  :state => ["IN","CA","OR"]
);

# convert the dictionary to a DataFrame -> variable df
df = DataFrame(dict);

# get all the values in the first name col -
df[!,[:first_name, :state]]
```

Finally, [DataFrames](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame) can also be used in complex data manipulation operations, e.g., [sorting](https://dataframes.juliadata.org/stable/lib/functions/#Sorting), [filtering](https://dataframes.juliadata.org/stable/lib/functions/#Filtering-rows) or [Join](https://dataframes.juliadata.org/stable/man/joins/) operations.

For example, suppose in our customer dataset, we wanted all customers from [Oregon](https://en.wikipedia.org/wiki/Oregon); we can do this with the `filter` function:

```{code-cell} julia
# modified from the DataFrames.jl package documentation
# https://dataframes.juliadata.org/stable/man/basics/#First-Steps-with-DataFrames.jl

# Load external packages
using DataFrames

# create a dictionary w/data -> variable dict
dict = Dict(
  :customer_age => [22, 20, 25], 
  :first_name => ["Rohit", "Rahul", "Akshat"],
  :state => ["IN","CA","OR"]
);

# convert the dictionary to a DataFrame -> variable df
df = DataFrame(dict);

# get all customers from OR
OR_customers = filter(:state=>x->x=="OR", df)
```

There is a large variety of [data wrangling](https://online.hbs.edu/blog/post/data-wrangling) functions published by the [DataFrame.jl](https://github.com/JuliaData/DataFrames.jl) package, please review the [Getting started](https://dataframes.juliadata.org/stable/man/getting_started/) section of the [DataFrame.jl](https://github.com/JuliaData/DataFrames.jl) documentation for more information.

### Reading and writing DataFrames
While it's easy to create a [DataFrame](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame), e.g., from a [Dictionary](https://docs.julialang.org/en/v1/base/collections/#Dictionaries), we are also often interested in applications that require reading and writing of data files from disk. 

Converting data files e.g., a table of numerical values, into a [DataFrame](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame) object, (or exporting a [DataFrame](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame) object to a file) can be done with the [CSV.jl](https://github.com/JuliaData/CSV.jl) package described above. 

#### Loading a CSV file into a DataFrame
Suppose we have a CSV file which holds numerical data, e.g., stock price values for the firm with ticker symbol `XYZ`. We can load this file from disk, and automatically convert the data to a [DataFrame](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame) using the `read` method in the [CSV.jl](https://github.com/JuliaData/CSV.jl) package:

```{code-cell} julia
# Load external packages
using CSV
using DataFrames

# setup the path to the data file -
path_to_datafile = joinpath(pwd(),"data", "AMD-OCHL-from-05-07-22-to-2022-08-05.csv")

# load the CSV file into a DataFrame -> df
df = CSV.read(path_to_datafile, DataFrame)

# show the first few rows of data 
df[1:4,:] # Indexing allows DataFrames to behave like arrays 
```

#### Saving a DataFrame to a CSV file
Conversely, suppose we have a [DataFrame](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame) holding numerical data want to save. In this case, we can take advantage of the `save` methods published by the [CSV.jl](https://github.com/JuliaData/CSV.jl) package; `save` takes two arguments, the first is the path to the file we want to save, and the second is the [DataFrame](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame) instance that we want to save. 

For example, assume we have a variable of type [DataFrame](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame) named `df`, then the following code snippet shows how we could save `df` to a CSV file:

```{code-block} julia
# Load external packages 
using CSV
using DataFrames

# some mythical process generates the DataFrame df
df = ...

# Dump df to disk as a CSV file 
path_to_csv_file = ...

# write out the file 
CSV.write(path_to_csv_file, df)
```

(content:references:julia-binary-formats)=
## Binary file formats
Binary file formats have been developed to store and organize large amounts of complex structured data. The basis of many binary formats is the [Hierarchical Data Format (HDF)](https://en.wikipedia.org/wiki/Hierarchical_Data_Format), a set of file formats initially developed by the [U.S. National Center for Supercomputing Applications (NCSA)](https://en.wikipedia.org/wiki/National_Center_for_Supercomputing_Applications). 

The [JLD2.jl](https://github.com/JuliaIO/JLD2.jl) package saves and loads [Julia](https://julialang.org) data structures in a format that is a subset of [HDF5](https://en.wikipedia.org/wiki/Hierarchical_Data_Format#HDF5), the latest iteration of the [Hierarchical Data Format (HDF)](https://en.wikipedia.org/wiki/Hierarchical_Data_Format). 

The [JLD2.jl](https://github.com/JuliaIO/JLD2.jl) package can be downloaded and installed using the [Julia package manager](./julia-basics.md). To load the `JLD2` package into your program, or the [REPL](./julia-basics.md), issue the [using](https://docs.julialang.org/en/v1/base/base/#using) or [import](https://docs.julialang.org/en/v1/base/base/#import) commands. Once the `JLD2`  package is loaded, it publishes several commands to load and save data in the [HDF5](https://en.wikipedia.org/wiki/Hierarchical_Data_Format#HDF5) format. Let's look at the {ref}`content:references:julia-binary-formats-save` and {ref}`content:references:julia-binary-formats-load` functions.

(content:references:julia-binary-formats-save)=
### save

Consider an example of saving a `JLD2` file; in this example, we downloaded stock price data for several firms from an external application programming interface (API) and saved this dataset as a [Dictionary](https://docs.julialang.org/en/v1/base/collections/#Dictionaries). The price history for each firm is stored in a [DataFrame](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame), while the overall dataset for N = 25 firms is stored as a [Dictionary](https://docs.julialang.org/en/v1/base/collections/#Dictionaries) where the ticker symbol for firm `XYZ` (of type [String](https://docs.julialang.org/en/v1/base/strings/#lib-strings)) is used as the [Dictionary](https://docs.julialang.org/en/v1/base/collections/#Dictionaries) key.

The `save` function accepts a path and an `AbstractDict` holding the key/value pairs that we wish to save, where the key is a string representing the name of the dataset and the value is its contents:

```{code-block} julia
# load external packages
using DataFrames
using JLD2
using FileIO

# external process to download data (not shown)
dd = api({arguments}); # dd -> Dict{String,DataFrame}

# path to data file 
filename = "Portfolio-Data-06-20-22.jld2"

# save
save("Portfolio-Data-06-20-22.jld2", Dict("dd" => dd)); # saved dd in Dict with key dd
```
(content:references:julia-binary-formats-load)=
### load

Consider an example of loading a `JLD2` file; in this example, a [Dictionary](https://docs.julialang.org/en/v1/base/collections/#Dictionaries) holding stock market data is loaded from disk. In particular, the price data for each of N = 25 firms is stored in a [DataFrame](https://dataframes.juliadata.org/stable/lib/types/#DataFrames.DataFrame), where the ticker symbol for each firm `XYZ` is used as the [Dictionary](https://docs.julialang.org/en/v1/base/collections/#Dictionaries) key; the ticker symbol `XYZ` is of type [String](https://docs.julialang.org/en/v1/base/strings/#lib-strings). Thus, the loaded [Dictionary](https://docs.julialang.org/en/v1/base/collections/#Dictionaries) is of type `Dict{String,DataFrame}`.

The `load` function reads a `*.jld2` file from the disk. When called with a path argument only, the `load` function loads the dataset from the given file into a [Dictionary](https://docs.julialang.org/en/v1/base/collections/#Dictionaries):

```{code-block} julia
# load external packages
using DataFrames
using JLD2
using FileIO

# set path to the data file
# joinpath is cross platform: handles / vs \
path_to_data_file = joinpath(".", "data", "Portfolio-Data-06-20-22.jld2")

# load the dataset: the original data is stored in a Dict with key `dd`
dd = load(path_to_data_file)["dd"] # dd -> Dict{String,DataFrame}
```

Taken together, the [JLD2.jl](https://github.com/JuliaIO/JLD2.jl) package provides tools to directly persist (and load) complex hierarchical data structures, which go well beyond just numerical data. For more information, please see the [JLD2.jl package documentation](https://github.com/JuliaIO/JLD2.jl).

---

## Summary

In this chpater we:
* Introduced reading and writing {ref}`content:references:julia-csv-files`, a standard data format for working with numerical data files
* Introduced more expressive tools such as {ref}`content:references:julia-dataframes`, which are in-memory tabular data structures. `DataFrames` are highly flexible data structures offering many advanced storage and query capabilities. 
* Introduced reading and writing data in {ref}`content:references:julia-binary-formats`, a common approach for large data files and more complex data structures  