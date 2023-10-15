# Chapter 02
Mutable sequences inherit all methods from immutable sequences.

Keep in mind these common traits: mutable vs immutable; container vs flat. They are helpful to extrapolate what you know about one sequence type to others

Mastering list comprehensions opens the door to generator expressions, which among other uses can produce elements to fill up sequences of any type.

In Python 3, list comprehensions, generator expressions, and their siblings set and dict comprehensions, have a local scope to
hold the variables assigned in the for clause. However, variables assigned with the “Walrus operator” := remain accessible after those comprehensions or expressions return unlike local variables in a function.
Note how the var *last* below can be captured ahd persisted:

```
>>> x = "ABC"
>>> codes = [last := ord(c) for c in x]
>>> codes
[65, 66, 67]
>>> last
67
```

Listcomps are a one-trick pony: they build lists. To generate data for other sequence types, a genexp is the way to go.

Another example of unpacking is prefixing an argument with `*` when calling a function:
```
>>> divmod(20, 8)
(2, 4)
>>> t = (20, 8)
>>> divmod(*t)
(2, 4)
>>> quotient, remainder = divmod(*t)
>>> quotient, remainder
(2, 4)
```

### Using `*` to Grab Excess Items
Defining function parameters with `*args` to grab arbitrary excess arguments is a classic Python feature.
In Python 3, this idea was extended to apply to parallel assignment as well:
```
>>> a, *body, c, d = range(5)
>>> a, body, c, d
(0, [1, 2], 3, 4)
>>> *head, b, c, d = range(5)
>>> head, b, c, d
([0, 1], 2, 3, 4)
```

Note that you can also have *Nested Unpacking*, see page 90 for details.

## Structural Pattern Matching
This is very cool and powerful. Have a look at [Carol Willing's introduction](https://docs.python.org/3.10/whatsnew/3.10.html#pep-634-structural-pattern-matching)
Note that *Sequence Patterns* may be written as tuples or lists, or any combination of nested tuples and lists: in a *Sequence Pattern*, square brackets and parentheses mean the same thing.

Note that Instances of str, bytes and bytearray are not handled as sequences in the context of match/case. A match subject of one of those types is treated as an *atomic* value - for example the integer 987 is treated as one value, not a sequence of digits. If you want to treat an object of those types as a sequence subject, convert it in the match clause. For example:
```
match tuple(phone):
    case ["1", *rest]: # North America and Caribbean
        ...
    case ["2", *rest]: # Africa and some territories
        ...
    case ["3"|"4", *rest]: # Europe
        ...
```

I was a bit confused at first by some of the patterns on Page 99 for Evaluating an Expression:
```
match exp:
    case ['lambda', [*parms], *body] if body:
```
This has multiple starred names (parms and body) but it's OK because parms is inside a sequence.
So, this match is:
- The literal `lambda`
- A sequence (in square brackets or parenths) all bound to the variable *parms*
- The rest of the items all bound to the variable *body*
- So *parms* and *body* will be lists
- Note the guard that ensures *body* cannot be empty
