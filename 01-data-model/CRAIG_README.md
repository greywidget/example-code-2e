The **Python Data Model** is the `API` that we use to make our own objects play well with the most idiomatic language features.

You can think of the data model as a description of Python as a framework. It formalizes the interfaces of the building blocks of the language itself, such as sequences, functions, iterators, coroutines, classes, context managers and so on.

When using a framework, we spend a lot of time coding methods that are called by the framework. The same happens when we leverage the Python Data Model to build new classes. The Python interpreter invokes special methods to perform basic object operations, often triggered by special syntax. E.g. the *Dunder Methods*

By implementing special methods, you objects can behave like the *built-in* types, enabling the expressive coding style the community considers *Pythonic*

It took me a while to get clear on the Collection API on page 48. My understanding was helped greatly by the [collections.abc documentation](https://docs.python.org/3/library/collections.abc.html#module-collections.abc). It's also useful to know that there is a *built-in* `issubclass`:
```
import collections
>>> issubclass(list, collections.abc.Container)
True
```
