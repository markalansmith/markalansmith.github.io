---
layout: post
title: pybind11 - Fast Looping 
---

pandas and numpy are great at performing vectorized operations fast. Occasionally, there are situations where an operation you want to perform on a pandas dataframe or numpy array can't be vectorized easily. I ran into such a problem recently and wanted to explore using pybind11 as an option to speed up the calculation. 

## Resources

* <a href="https://github.com/pybind">pybind11</a> - <a href="http://pybind11.readthedocs.io/en/latest/index.html">Documentation</a>
* <a href="https://github.com/pybind/python_example">pybind11 - python_example</a> 
* <a href="http://people.duke.edu/~ccc14/sta-663-2016/18G_C++_Python_pybind11.html">Duke - Computational Statistics in Python</a>

## Problem

Keeping track of state is very difficult in a vectorized operation. Consider a case where you wanted to filter out rows in a dataframe based on how far the value has deviated from the last filtered value. Here is a snippet of code that would accomplish this goal. 

{% gist 1af6ffc01bb328535c640379acffc79d %}

Using the pandas selection syntax you could simply take all rows in which 'chg' is True and you have a solution.

The problem is that looping in python and pandas is extremely slow.

## Solution

Using pybind11 we could write a simple method that can perform the looping. Here is an example of such a loop.


{% gist 76923dfede3ce58ae3d46651a397b327 %}


You can call the pybind11 method via Python in the following way


{% gist 3c4fcca5e9b922110ba619dfa30d93eb %}

The pybind looping will be many multiples faster than using the pandas iterrows method. This is to be expected.

Alternatives to the above solution exist (numba, Cython, etc...) but the pybind11 solution is very concise and easy to implement. I look forward to exploring pybind11 more in the future.
