# Is comparison

The `is` operator roughly translates to mean "is thing1 _exactly the same 
thing_ as thing2?" Where this becomes important is if you have 2 different 
instances of the same class, it will evaluate as `False`.

In order to get around this, you have to use a `singleton` style object - which 
is to say just an object which no matter what is always the same. That is what 
`None` is, so that's why the use of `if x is None` is a common moniker in 
Python.

One way I leverage this is with a "Default" object, which I use to explicitly 
indicate I'd like to use a default value. To quote the [Zen of Python](zen.md), 
"Explicit is better than implicit".

```Python
#Round-about way of extending 'None' data type using pure python...
#other methods seem to require the use of a compiled C extension
#More information @
#  https://stackoverflow.com/questions/20833081/implementation-of-nonetype-reasons-and-details

class Default(object):
  _instance = None
  def __new__(cls, *args, **kwargs):
    if Default._instance is None:
      Default._instance = object.__new__(cls, *args, **kwargs)
    return Default._instance
```

