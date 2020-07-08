# Ignore extra keyword arguments as function input

```python
class Test(object):
    def __init__(self, id, name, **kwargs):
        self.id = id
        self.name = name

>>> test = Test(id=1, name='test', dummy="dummy")
>>> test.id
1
>>> test.name
'test'
>>> test.dummy
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Test' object has no attribute 'dummy'
```

[Reference](https://stackoverflow.com/questions/35862094/how-to-ignore-extra-keyword-arguments-in-python)

