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

#### Python version

> Every release is more optimized.

The latest version should have the best performance, so make sure you always use the latest version. At least choose Python 3 over Python 2.

#### Data structure

> Using the most appropriate data structure is critical to speed up the code.

Python has some built-in data structures (namely: list, tuple, set, and dictionary). It is also possible to use additional data structures by importing modules (like [NumPy array](https://numpy.org/doc/stable/reference/generated/numpy.array.html) and [pandas DataFrame](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html)).

One of the most common mistakes is using the **list** structure for all cases. For example, if your list has elements of a single type (like real numbers), you might consider using a NumPy array to optimise the code.

#### Assign variables

> Avoid assign variables inside loops.

Variables assigned within loops are recreated whenever the loop is iterated.

> Multiple assignments

If there is more than one variable to assign, you can perform a multiple assignment. The code:

```python
x, y, z = 1, 2, 3
```

is more efficient than

```python
x = 1
y = 2
z = 3
```

#### Library function and dot operation

> Library functions are designed to be as efficient as possible.

Instead of writing your own functions, whenever possible use functions from existing libraries. Also, when using a library function, avoid using the dot operation. The following code:

```python
from math import sqrt

x = sqrt(4)
```

is more efficient than the code with dot operation:

```python
import math

x = math.sqrt(4)
```

that is more efficient than the code with a homemade function:

```python
x = 4 ** 0.5
```

#### List comprehension

> List comprehension is a very concise syntax to create a new list

Create lists using *list comprehension* whenever possible. List comprehension can be used over:

- loops
- lambda function
- map()
- filter()
- reduce()

For example, to create a list of even numbers, you can change the following code:

```python
x = []
for i in range(100):
    if i%2 == 0:
      x.append(i)
```

for a list comprehension:

```python
x = [i for i in range(100) if i%2 == 0]
```

#### If-else ladder

> Put high probability if-statements first!

Putting low probability if-statements early will make your code perform more operations than necessary.

---

### CPU profiling

Once the code is performing the desired task and has been written following best practices, the next step  is profiling the code to find possible bottlenecks. By profiling your code you can identify what part demands more execution time and focus your attention in this part.

There are different approaches to profiling the code, here I will suggest one that is easy to install/use, while producing meaningful results: the `line_profiler` module. It can be installed through command prompt typing either:

- `pip install line_profiler`
- `conda install line_profiler` (for Anaconda Python)

To use the `line_profiler` module it is necessary to follow two steps:

1. add a `@profile` decorator
2. command prompt: `kernprof -l -v file.py`

```python
@profile
def primes(n):
    if n==2:
        return [2]
    elif n<2:
        return []

    s=list(range(3,n+1,2))  # I updated this line for Python 3 syntax
    mroot = n ** 0.5
    half=(n+1)//2-1
    i=0
    m=3

    while m <= mroot:
        if s[i]:
            j=(m*m-3)//2  # I updated this line for Python 3 syntax
            s[j]=0
            while j<half:
                s[j]=0
                j+=m
        i=i+1
        m=2*i+3
    return [2]+[x for x in s if x]

primes(100)
```

Then go to the command prompt and type:

```bash
kernprof -l -v pyscript.py
```
