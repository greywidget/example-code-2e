# 07 First Class Functions

## Parameters
I can never quite remember the rules and syntax, so here is a nice example from [what's new in 3.8](https://docs.python.org/3/whatsnew/3.8.html#positional-only-parameters)

```
def f(a, b, /, c, d, *, e, f):
    print(f"{a=}, {b=}, {c=}, {d=}, {e=}, {f=}")
```

In the above example:
- `a` and `b` are *Positional Only*
- `c` and `d` can be *Positional* or *Keyword*
- `e` and `f` are *Keyword Only*

Also remember that if you use `*` with an identifier, it will gather up any extra positional arguments e.g:
```
>>> def f(a, b, /, c, d, *r, e, f):
...     print(r)

>>> f(10 , 20, 30, 40, "a", "b", f=50, e=60)
('a', 'b')
```

## The Awesome Operator Module
I realised that you could use `itemgetter` for things like picking items out of sequences etc:
```
>>> from operator import itemgetter
>>> third_fourth = itemgetter(3, 4)
>>> third_fourth("craig richards")
('i', 'g')
```
Which also makes it great as a function for sorting etc.
But I didn't realise that because *itemgetter uses the `[]` operator, it supports not only sequences but also mappings and any class that implements `__getitem__`*
So:
```
>>> d = {"name": "craig", "age": 60}
>>> first = itemgetter("name")
>>> first(d)
'craig'
```

`methodcaller` is pretty cool
```
>>> from operator import methodcaller
>>> s = 'The time has come'
>>> upcase = methodcaller('upper')
>>> upcase(s)
'THE TIME HAS COME'
>>> hyphenate = methodcaller('replace', ' ', '-')
>>> hyphenate(s)
'The-time-has-come'
```

Freezing Arguments with `functools.partial` is nice too;
```
>>> from operator import mul
>>> from functools import partial
>>> triple = partial(mul, 3)
>>> triple(7)
21
>>> list(map(triple, range(1, 10)))
[3, 6, 9, 12, 15, 18, 21, 24, 27]
```