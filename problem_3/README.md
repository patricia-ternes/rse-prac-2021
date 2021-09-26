# Problem 3

A researcher has approached you with a piece of Python code which seems to be running slower than she expects. The original code:

```python
1 |  def primes(n):
2 |     if n==2:
3 |         return [2]
4 |     elif n<2:
5 |         return []
6 |
7 |     s=range(3,n+1,2)
8 |     mroot = n ** 0.5
9 |     half=(n+1)//2-1
10|     i=0
11|     m=3
12| 
13|     while m <= mroot:
14|         if s[i]:
15|             j=(m*m-3)/2
16|             s[j]=0
17|             while j<half:
18|                 s[j]=0
19|                 j+=m
20|         i=i+1
21|         m=2*i+3
22|     return [2]+[x for x in s if x]
23| 
24|  primes(100)
```

She doesn’t want you to fix the code, but would like you to explain some general principles she can apply herself to investigate the code and work out where the problems are.

What would you suggest?

## Solution

> To speed up any Python code four steps can be followed:

1. Before moving on to more advanced techniques, it is recommended to review the code, following a series of good practices. Some tips from these best practices (which lead to better code performance) are listed in the [General tips](#general-tips) session.
2. Once you have ensured that your code is *well written*, it is recommended to profile your code (see [CPU profiling](#cpu-profiling) and [Memory profiling](#memory-profiling) sessions).
3. It is possible to translate the Python function to an optimized code (see [Native-speed code](#native-speed-code) session).
4. Finally, it is possible to separate the running process in several processes to be run in parallel (see [Multiprocessing](#multiprocessing)).

---

### General tips

Quickly looking at the code three things catch my immediate attention:

1. Lines 7 (`s=range(3,n+1,2)`), 15 (`j=(m*m-3)/2`) and 16 (`s[j]=0`) indicates that the code was written in Python 2.
2. Line 7 (`s=range(3,n+1,2)`) assign a integer list to `s` instead an array.
3. Line 8 (`mroot = n ** 0.5`) is a homemade function that has an equivalent library function available.

These two practices, for example, are not ideal and can slow down your code. So, before moving on to more advanced techniques, it is necessary to ensure that the code is written in the best possible way. Below, some practices considered ideal will be presented.

- [Problem 3](#problem-3)
  - [Solution](#solution)
    - [General tips](#general-tips)
      - [Python version](#python-version)
      - [Data structure](#data-structure)
      - [Assign variables](#assign-variables)
      - [Library function and dot operation](#library-function-and-dot-operation)
      - [List comprehension](#list-comprehension)
      - [If-else ladder](#if-else-ladder)
    - [CPU profiling](#cpu-profiling)
    - [Memory profiling](#memory-profiling)
    - [Native-speed code](#native-speed-code)
    - [Multiprocessing](#multiprocessing)
    - [Comentario do Evy](#comentario-do-evy)