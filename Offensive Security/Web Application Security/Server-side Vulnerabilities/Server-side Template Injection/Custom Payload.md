There will be times where we will be needing to construct a custom payload to exploit SSTI vulnerabilities. For example, a template engine that executes templates inside a sandbox, which can make exploitation difficult or impossible.
## Custom Jinja2 Payload
1. The first step is to understand Python's hierarchy. Using `__mro__` or `mro()`, we can go back up the three of inherited objects in the Python environment.
```python
import flask

s = 'HTB'
s.__class__.mro()[1].__subclasses__()

[<class 'type'>, <class 'weakref'>, <class 'weakcallableproxy'>, <class 'weakproxy'>, <class 'int'>, <class 'bytearray'>, <class 'bytes'>, <class 'list'>, <class 'NoneType'>, <class 'NotImplementedType'>, <class 'traceback'>, <class 'super'>, <class 'range'>, <class 'dict'>, <class 'dict_keys'>, <class 'dict_values'>, <class 'dict_items'>, <class 'dict_reversekeyiterator'>, <class 'dict_reversevalueiterator'>, <class 'dict_reverseitemiterator'>, <class 'odict_iterator'>, <class 'set'>, <class 'str'>, <class 'slice'>, <class 'staticmethod'>, <class 'complex'>, <class 'float'>, <class 'frozenset'>, <class 'property'>, <class 'managedbuffer'>, <class 'memoryview'>, <class 'tuple'>, <class 'enumerate'>, <class 'reversed'>, <class 'stderrprinter'>, <class 'code'>, <class 'frame'>, <class 'builtin_function_or_method'>, <class 'method'>,
 <SNIP>
```
2. Next is to look for useful classes that can facilitate remote code execution.
```python
s.__class__.mro()[1].__subclasses__()
```