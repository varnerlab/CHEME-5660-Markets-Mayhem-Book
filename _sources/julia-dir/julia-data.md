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

# Working with Data 

## Introduction
Fill me in.

## Comma seperated value files
Fill me in.

## DataFrames
Objects of type ``DataFrame`` represent data tables where each column corresponds vector of values. The simplest way to construct a DataFrame is to pass vectors holding the values for each column using keyword arguments or pairs:

```{code-cell} julia
using DataFrames
df = DataFrame(A=1:4, B=["M", "F", "F", "M"])
```

## Binary file formats
Fill me in.

## Summary
Fill me in.