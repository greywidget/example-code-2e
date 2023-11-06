# 05 Data Classes

## Initialisation Variables that are not Fields.
See this example from page 325:
```
@dataclass
class C:
i: int
j: int = None
database: InitVar[DatabaseType] = None
def __post_init__(self, database):
if self.j is None and database is not None:
self.j = database.lookup('j')
c = C(10, database=my_database)
```
This doesn't work as is because there is no definition for `DatabaseType`. (from the code above it would have to have a `lookup` method too.) 
I changed it to:
```
@dataclass
class C:
    i: int
    j: str = None
    database: InitVar[str] = None

    def __post_init__(self, database):
        if self.j is None and database is not None:
            self.j = database


c = C(10, database="mysql")
```
When I ran the above, I was confused because my database (`mysql`) appeared to be an instance variable - I could see that `c.j == "mysql"`. But thinking about it, `j` was not passed to the constuctor - `j` initially had its default value of `None`. What was passed to the constructor was a keyword argument `database` from which we derived `j`. *See the difference?*