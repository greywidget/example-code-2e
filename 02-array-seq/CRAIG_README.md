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