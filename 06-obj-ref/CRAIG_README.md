# 06 Object References

## Mutable Types as Parameter Defaults: Bad Idea
In the Haunted Bus example:
```
class HauntedBus:
    """A bus model haunted by ghost passengers"""

    def __init__(self, passengers=[]):  # <1>
        self.passengers = passengers  # <2>

    def pick(self, name):
        self.passengers.append(name)  # <3>

    def drop(self, name):
        self.passengers.remove(name)
```
I know there is a problem, but didn't quite follow the references in the book text with regard to the `passengers` argument being bound to the `default list object`  

Looking further into it, in this example, what it means is:
- The `HauntedBus` Class variable has a Special variable `__init__` (the initialiser method) which in turn has a Special Variable called `__defaults__`, which initially has the value `([],)` e.g. it is a tuple holding default values for the function arguments.
- In the case of creating a `HauntedBus` without passengers `bus1 = HauntedBus`, `bus1.passengers` becomes an `alias` for the above default, and so when later we run `bus1.pick("Carrie")` we actually change the `__defaults__` variable in `__init__` for the `HauntedBus` Class so it looks like: `(["Carrie"],)`. Hence the next `Bus` we create without specifying passengers will get a passenger list that already includes `Carrie`.
- I was able to verify this using the `VSCode` debugger and Debug Console and looking at the variables:
- `Locals`
    - `class variables`
        - `HauntedBus`
            - `special variables`
                - `__init__`
                    - `special variables`
                        - `__defaults__: (["Carrie"],)`
                        
Or, to put it another way, having created `bus2 = HauntedBus()`
```
>>> vars()["HauntedBus"].__init__.__defaults__[0] is bus2.passengers
True
```
