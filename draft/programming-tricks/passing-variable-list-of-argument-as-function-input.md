---
layout: post
title: Python Minor Tips
categories:
  - Python
---

# Passing variable list of argument as function input

```python
def foo (*args):
    for arg in args:
        print (arg)

>>> foo (1, 2, 3)
1
2
3
>>> foo_var = (4, 5)
>>> foo(*foo_var)
4
5
>>> asdf = [6, 7]
>>> foo(*asdf)
6
7
```

```python
def foo (test1, test2):
    print(test1)
    print(test2)

>>> foo_var = {'test1':1, 'test2':345}
>>> foo(**foo_var)
1
345
```

[Reference](https://pythontips.com/2013/08/04/args-and-kwargs-in-python-explained/)

