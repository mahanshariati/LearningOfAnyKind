# 🐍 The Quick Python Book, Fourth Edition (Manning, 2025)

The Quick Python Book, Fourth Edition, is intended for people who already have experience in one or more programming languages and want to learn the basics of Python 3 as quickly and directly as possible.

## Part 2: The Essentials

this chapter starts from the absolute basics of what makes a Python program and moves through Python's built-in data types and control structures, as well as defining functions and using modules.

## Chapter 4 --- The Absolute Basics

### Indentation and Code Blocks

Python uses indentation to define blocks of code. Unlike languages that
use braces, indentation is part of Python's syntax.

``` python
if condition:
    statement
```

Important rules: - A colon (`:`) starts a block. - Lines in the same
block must have the same indentation. - The common style is 4 spaces. -
Mixing tabs and spaces can cause errors.

### Comments

Comments are ignored by Python and explain code.

``` python
# This is a comment
```

Good comments explain why something is done, not obvious actions.

### Variables and Assignment

Variables are created when values are assigned.

``` python
name = "Python"
age = 30
```

Important: - Python is dynamically typed. - Variables reference
objects. - A variable can refer to different types during execution.

Multiple assignment:

``` python
x, y = 10, 20
```

Swapping:

``` python
a, b = b, a
```

### Variable Naming

Rules: - Names can contain letters, numbers, and underscores. - Names
cannot start with a number. - Avoid reserved words.

Python style uses `snake_case`:

``` python
student_name
total_price
```

### Type Hints

Python supports optional type hints:

``` python
age: int = 20
```

They improve readability and help development tools, but they are not
automatically enforced.

### Expressions and Operators

Expressions produce values.

#### Arithmetic Operators

Operator | Meaning |
|--|--|
| \+   | Addition |
| \-   | Subtraction |
| \*   | Multiplication |
| /    | Division |
| //   | Floor division |
| \%   | Remainder |
| \*\* | Power |

#### Comparison Operators

``` python
== != < > <= >=
```

Return `True` or `False`.

#### Logical Operators

``` python
and
or
not
```

Used for combining conditions.

### Numbers

Common numeric types:

-   `int` → whole numbers
-   `float` → decimal numbers
-   `complex` → complex numbers

Useful functions:

``` python
abs(-5)
round(3.14159, 2)
```

### Strings

Strings represent text.

``` python
message = "Hello Python"
```

Both single and double quotes can be used.

Escape characters:

  Escape   Meaning
  -------- -----------
  `\n`     New line
  `\t`     Tab
  `\\`     Backslash

Modern formatting uses f-strings:

``` python
name = "Sara"
age = 20

f"{name} is {age}"
```

### User Input

`input()` reads text from users.

``` python
name = input("Name: ")
```

Important: `input()` always returns a string.

Convert values when needed:

``` python
age = int(input("Age: "))
```

### Python Style

Python values readability.

Important habits: - Use meaningful names. - Keep code simple. - Use 4
spaces for indentation. - Follow PEP 8 conventions.

Example:

``` python
total_price = price * quantity
```

is clearer than using unclear variable names.

## Chapter 5 --- Lists, Tuples, and Sets

### Lists Are Like Arrays

Lists are Python's general-purpose sequence type. They store multiple
values in a single object and can contain different data types.

``` python
numbers = [1, 2, 3]
```

Important: - Lists are ordered. - Lists are mutable, meaning their
contents can be changed after creation. - List elements are accessed by
index.

### List Indices

Python uses zero-based indexing.

``` python
items = ["a", "b", "c"]

items[0]
```

returns:

``` python
"a"
```

Negative indices count from the end:

``` python
items[-1]
```

returns the last element.

Slicing creates a new list:

``` python
items[1:]
```

returns all elements from index 1 onward.

### Modifying Lists

Lists can be changed after creation.

Common operations:

``` python
items.append("d")
items.insert(1, "x")
items.remove("b")
```

Important: - `append()` adds an item at the end. - `insert()` adds an
item at a specific position. - `remove()` removes the first matching
value.

Deleting by index:

``` python
del items[0]
```

### Sorting Lists

Lists can be sorted in place:

``` python
numbers.sort()
```

This changes the original list.

To create a sorted copy:

``` python
sorted_numbers = sorted(numbers)
```

Custom sorting uses the `key` argument:

``` python
names.sort(key=len)
```

### Common List Operations

Membership:

``` python
"value" in items
```

Concatenation:

``` python
[1, 2] + [3, 4]
```

Repetition:

``` python
[0] * 5
```

Useful functions:

``` python
len(items)
min(numbers)
max(numbers)
```

Searching:

``` python
items.index("x")
```

Counting:

``` python
items.count("x")
```

### Nested Lists and Copies

Lists can contain other lists:

``` python
matrix = [[1, 2], [3, 4]]
```

Accessing nested elements:

``` python
matrix[0][1]
```

returns:

``` python
2
```

A shallow copy only copies the outer list. Nested objects are still
shared.

``` python
copy = original[:]
```

For independent copies of nested structures, use `copy.deepcopy()`.

### Tuples

Tuples are similar to lists, but they are immutable.

``` python
point = (10, 20)
```

Important: - Tuples cannot be modified after creation. - They support
indexing, slicing, and many list-like operations. - They are useful for
fixed collections of values.

A tuple cannot be changed:

``` python
point[0] = 5
```

causes an error.

### One-Element Tuples Need a Comma

Parentheses alone do not create a tuple.

Correct:

``` python
single = (5,)
```

Incorrect:

``` python
single = (5)
```

The comma tells Python it is a tuple.

### Packing and Unpacking Tuples

Packing:

``` python
person = "Alice", 25
```

Unpacking:

``` python
name, age = person
```

This is commonly used for swapping values.

``` python
a, b = b, a
```

### Converting Lists and Tuples

List to tuple:

``` python
tuple([1, 2, 3])
```

Tuple to list:

``` python
list((1, 2, 3))
```

### Sets

Sets store unique values and are unordered collections.

``` python
numbers = {1, 2, 3}
```

Important: - Sets cannot contain duplicate values. - Sets are mutable. -
Elements must be hashable.

Example:

``` python
{1, 1, 2}
```

becomes:

``` python
{1, 2}
```

### Set Operations

Union:

``` python
a | b
```

Intersection:

``` python
a & b
```

Difference:

``` python
a - b
```

Membership:

``` python
value in my_set
```

Sets are useful when checking whether something exists or removing
duplicates.

### Frozen Sets

A `frozenset` is an immutable set.

``` python
values = frozenset([1, 2, 3])
```

Because it cannot change, it can be used where a normal set cannot, such
as inside another set or as a dictionary key.



## Chapter 6 --- Strings

### Strings as Sequences of Characters

Strings are sequences of characters. This means you can use indexing and
slicing with strings.

``` python
text = "Hello"

text[0]
text[-1]
text[1:]
```

Important: - Python does not have a separate character type. - A single
character is still a string with length 1. - Strings are immutable,
meaning they cannot be changed after creation.

Example:

``` python
text = "Hello"

text[0] = "Y"
```

causes an error because the original string cannot be modified.

### Basic String Operations

Concatenation uses `+`:

``` python
"Hello " + "World"
```

String repetition uses `*`:

``` python
"x" * 5
```

Useful function:

``` python
len(text)
```

returns the number of characters.

### Escape Sequences

Escape sequences begin with a backslash (`\`) and represent special
characters.

  Escape   Meaning
  -------- --------------
  `\n`     New line
  `\t`     Tab
  `\\`     Backslash
  `\"`     Double quote

Example:

``` python
message = "Hello\nWorld"
```

### String Quotes

Strings can use single or double quotes.

``` python
"Hello"
'Hello'
```

Using different quote types can avoid unnecessary escaping:

``` python
"Don't need escaping"
```

For multiline strings, use triple quotes:

``` python
text = """This is
a multiline string"""
```

### Converting Objects to Strings

The `str()` function converts objects into strings.

``` python
number = 123

text = str(number)
```

### Formatting Strings

F-strings are the modern way to insert values into strings.

``` python
name = "Sara"
age = 20

message = f"{name} is {age} years old"
```

Expressions can also be used inside f-strings:

``` python
f"Total: {price * quantity}"
```

### Common String Methods

String methods return new strings. They do not modify the original
string.

Changing case:

``` python
text.upper()
text.lower()
text.title()
```

Searching:

``` python
text.find("word")
text.index("word")
```

Checking beginning or end:

``` python
text.startswith("A")
text.endswith(".")
```

Replacing:

``` python
text.replace("old", "new")
```

Removing surrounding whitespace:

``` python
text.strip()
text.rstrip()
text.lstrip()
```

### Checking String Contents

Useful methods:

``` python
text.isdigit()
text.isalpha()
text.islower()
text.isupper()
```

### Splitting and Joining Strings

Splitting creates a list from a string:

``` python
words = "one two three".split()
```

Joining combines strings:

``` python
" ".join(["one", "two", "three"])
```

### Converting Strings to Lists

Strings cannot be modified directly, but they can be converted to lists.

``` python
letters = list("Hello")
```

After modification, they can be joined again:

``` python
"".join(letters)
```

### Bytes

Python also has a `bytes` type for binary data.

Strings contain text, while bytes contain raw byte values.

``` python
data = b"Hello"
```

Convert between strings and bytes using encoding:

``` python
text.encode()
data.decode()
```


## Chapter 7 --- Dictionaries

### Dictionaries

Dictionaries store data as **key-value pairs**.

Unlike lists, which use numeric indexes, dictionaries use keys to access values.

```python
person = {
    "name": "Alice",
    "age": 25
}
```

Important:
- Dictionaries are mutable.
- Keys must be unique.
- Keys must be hashable objects.
- Values can be any object.

Accessing a value:

```python
person["name"]
```

---

### Creating Dictionaries

Empty dictionary:

```python
data = {}
```

Using the `dict()` constructor:

```python
data = dict(name="Alice", age=25)
```

Keys and values can be different types:

```python
data = {
    1: "one",
    "two": 2
}
```

---

### Accessing Dictionary Values

Using square brackets:

```python
dictionary[key]
```

If the key does not exist, Python raises a `KeyError`.

Using `get()`:

```python
dictionary.get(key)
```

`get()` returns `None` when the key does not exist.

A default value can be provided:

```python
dictionary.get("age", 0)
```

---

### Adding and Updating Values

Adding a new key:

```python
person["city"] = "London"
```

Updating an existing key:

```python
person["age"] = 30
```

Dictionaries can grow or shrink during execution.

---

### Removing Items

Remove a key:

```python
del person["age"]
```

Using `pop()`:

```python
age = person.pop("age")
```

`pop()` removes the item and returns its value.

Remove the last inserted item:

```python
person.popitem()
```

---

### Dictionary Methods

Getting keys:

```python
person.keys()
```

Getting values:

```python
person.values()
```

Getting key-value pairs:

```python
person.items()
```

Example:

```python
for key, value in person.items():
    print(key, value)
```

---

### Checking Dictionary Contents

Check whether a key exists:

```python
"name" in person
```

Important:

Membership checks keys, not values.

```python
"Alice" in person
```

checks whether `"Alice"` is a key.

---

### Copying Dictionaries

Assignment creates another reference to the same dictionary:

```python
copy = original
```

Changing one affects the other.

A shallow copy:

```python
copy = original.copy()
```

creates a new dictionary, but nested objects are still shared.

---

### Dictionary Merging

Dictionaries can be merged using `update()`:

```python
person.update(other_person)
```

Existing keys are replaced by new values.

Modern Python also supports the merge operator:

```python
combined = first | second
```

---

### Dictionary Keys

Dictionary keys must be hashable.

Valid keys:

```python
1
"username"
(1, 2)
```

Invalid keys:

```python
[1, 2]
{"a": 1}
```

because lists and dictionaries are mutable.

A tuple can only be a key if all of its contents are hashable.

---

### Nested Dictionaries

Dictionaries can contain other dictionaries.

```python
student = {
    "name": "Sara",
    "grades": {
        "math": 90,
        "science": 85
    }
}
```

Accessing nested values:

```python
student["grades"]["math"]
```

---

### Dictionary Comprehensions

Dictionary comprehensions create dictionaries using a compact syntax.

```python
squares = {x: x*x for x in range(5)}
```

General form:

```python
{key_expression: value_expression for item in iterable}
```

---

### Sparse Data Representation

Dictionaries are useful when most possible values are empty or missing.

Instead of storing every possible item, only store existing values.

Example:

```python
scores = {
    "Alice": 90,
    "Bob": 85
}
```

This makes dictionaries useful for mappings, lookup tables, and structured data.


## Chapter 8 --- Control Flow

### Conditional Statements

Python uses `if`, `elif`, and `else` statements to control which code runs.

```python
if condition:
    statement
elif another_condition:
    statement
else:
    statement
```

Important:
- Conditions must evaluate to `True` or `False`.
- `elif` allows checking additional conditions.
- `else` runs when all previous conditions are false.

---

### Truth Values

Python treats some values as false when used in conditions.

False values include:

```python
False
None
0
0.0
""
[]
{}
set()
```

Most other objects evaluate to `True`.

Example:

```python
username = ""

if username:
    print(username)
```

The block does not execute because an empty string is considered false.

---

### Comparison Operators

```python
==
!=
<
>
<=
>=
```

Example:

```python
age >= 18
```

Comparison expressions return Boolean values:

```python
True
False
```

---

### Combining Conditions

Logical operators combine multiple conditions.

```python
and
or
not
```

Example:

```python
age >= 18 and has_ticket
```

Rules:

- `and` → all conditions must be true.
- `or` → at least one condition must be true.
- `not` → reverses the result.

Example:

```python
if not is_logged_in:
    print("Please log in")
```

---

### Conditional Expressions

A short form of `if-else` used for simple assignments.

Syntax:

```python
value_if_true if condition else value_if_false
```

Example:

```python
status = "adult" if age >= 18 else "child"
```

---

### The `match-case` Statement

`match-case` performs pattern matching.

Syntax:

```python
match value:
    case pattern:
        statement
```

Example:

```python
command = "start"

match command:
    case "start":
        print("Running")
    case "stop":
        print("Stopped")
```

Default case:

```python
match command:
    case _:
        print("Unknown command")
```

`_` matches anything that has not matched earlier cases.

---

### `while` Loops

A `while` loop repeats while a condition is true.

```python
while condition:
    statement
```

Example:

```python
count = 0

while count < 5:
    print(count)
    count += 1
```

Important:
- The condition is checked before every iteration.
- The loop must eventually become false to avoid infinite loops.

---

### `for` Loops

`for` loops iterate over items in an iterable.

Syntax:

```python
for item in iterable:
    statement
```

Example:

```python
names = ["Ali", "Sara", "John"]

for name in names:
    print(name)
```

Common iterables:

- Lists
- Tuples
- Strings
- Dictionaries
- Sets

---

### The `range()` Function

`range()` generates a sequence of numbers.

```python
range(stop)
```

Example:

```python
for number in range(5):
    print(number)
```

Output:

```text
0
1
2
3
4
```

Other forms:

```python
range(start, stop)

range(start, stop, step)
```

The `stop` value is not included.

Example:

```python
for number in range(2, 10, 2):
    print(number)
```

Output:

```text
2
4
6
8
```

---

### Loop Control

### `break`

Stops the loop immediately.

```python
for number in numbers:
    if number == 5:
        break
```

---

### `continue`

Skips the current iteration and moves to the next one.

```python
for number in numbers:
    if number < 0:
        continue

    print(number)
```

---

### Loop `else`

A loop can have an `else` block.

```python
for item in items:
    if item == target:
        break
else:
    print("Not found")
```

The `else` block runs only when the loop finishes normally without `break`.

---

### Iterating Through Dictionaries

Iterating over keys:

```python
for key in dictionary:
    print(key)
```

Iterating over values:

```python
for value in dictionary.values():
    print(value)
```

Iterating over both:

```python
for key, value in dictionary.items():
    print(key, value)
```

---

### Nested Loops

A loop can contain another loop.

Example:

```python
for row in table:
    for item in row:
        print(item)
```

The inner loop completes all its iterations before the outer loop continues.



## Chapter 9 --- Functions

### Defining Functions

Functions are reusable blocks of code that perform a specific task.

A function is defined using the `def` keyword.

```python
def function_name():
    statement
```

Example:

```python
def greet():
    print("Hello Python")
```

Calling a function:

```python
greet()
```

Important:
- Function code does not run when it is defined.
- The function runs only when it is called.
- Functions help avoid repeating code.

---

### Function Parameters and Arguments

Parameters are variables defined in the function definition.

Arguments are the values passed when calling the function.

```python
def greet(name):
    print(f"Hello {name}")
```

Calling:

```python
greet("Sara")
```

Here:
- `name` is the parameter.
- `"Sara"` is the argument.

---

### Returning Values

Functions can return values using `return`.

```python
def add(a, b):
    return a + b
```

Using the result:

```python
result = add(3, 5)
```

Important:

- `return` sends a value back to the caller.
- A function without `return` automatically returns `None`.

---

### Multiple Return Values

Python functions can return multiple values.

```python
def get_user():
    return "Sara", 25
```

Python returns them as a tuple.

Unpacking:

```python
name, age = get_user()
```

---

### Default Parameters

Parameters can have default values.

```python
def greet(name="Guest"):
    print(name)
```

Calling without an argument:

```python
greet()
```

uses the default value.

Important:
- Parameters with defaults must come after parameters without defaults.

Correct:

```python
def example(a, b=10):
    pass
```

Incorrect:

```python
def example(a=10, b):
    pass
```

---

### Keyword Arguments

Arguments can be passed using parameter names.

```python
def describe(name, age):
    print(name, age)
```

Calling:

```python
describe(age=20, name="Sara")
```

Benefits:
- Improves readability.
- Allows arguments to be provided in different order.

---

### Variable-Length Arguments

Python allows functions to accept an arbitrary number of arguments.

### `*args`

Collects extra positional arguments into a tuple.

```python
def total(*numbers):
    return sum(numbers)
```

Example:

```python
total(1, 2, 3, 4)
```

---

### `**kwargs`

Collects extra keyword arguments into a dictionary.

```python
def profile(**data):
    print(data)
```

Example:

```python
profile(name="Sara", age=20)
```

---

### Argument Unpacking

Python can unpack sequences when calling functions.

Using `*`:

```python
numbers = [1, 2, 3]

function(*numbers)
```

Using `**` for dictionaries:

```python
data = {"name": "Sara", "age": 20}

function(**data)
```

The keys must match the function parameters.

---

### Variable Scope

A variable's scope determines where it can be accessed.

Local variables exist inside functions.

```python
def example():
    x = 10
```

`x` cannot be accessed outside the function.

---

### Global Variables

Variables created outside functions are global.

```python
x = 10

def show():
    print(x)
```

Functions can read global variables, but changing them requires `global`.

```python
count = 0

def increase():
    global count
    count += 1
```

Using global variables is usually discouraged because it makes code harder to maintain.

---

### Local and Global Names

Python searches for variables in this order:

1. Local scope
2. Enclosing scope
3. Global scope
4. Built-in scope

This is called the **LEGB rule**.

---

### Lambda Functions

Lambda functions are small anonymous functions.

Syntax:

```python
lambda arguments: expression
```

Example:

```python
square = lambda x: x * x
```

Lambda functions are commonly used with functions like `map()` and `sorted()`.

Example:

```python
names.sort(key=lambda x: len(x))
```

---

### Docstrings

A docstring describes what a function does.

```python
def add(a, b):
    """Return the sum of two numbers."""
    return a + b
```

Docstrings are used by documentation tools and help explain functions.

---

### Type Hints in Functions

Functions can include optional type hints.

```python
def add(a: int, b: int) -> int:
    return a + b
```

Type hints:
- Improve readability.
- Help editors and tools.
- Are not enforced automatically.

---

### Functions as Objects

Functions are objects in Python.

They can be:

- Stored in variables.
- Passed as arguments.
- Returned from other functions.

Example:

```python
def greet():
    return "Hello"

message = greet
```

Now `message` refers to the function.

---

### Nested Functions

Functions can be defined inside other functions.

```python
def outer():
    def inner():
        print("Inside")

    inner()
```

Nested functions are commonly used with closures and decorators.



## Chapter 10 --- Classes and Objects

### Classes and Objects

Python is an object-oriented programming language. Classes define the structure and behavior of objects.

A class is a blueprint, while an object is an instance created from that class.

```python
class Person:
    pass
```

Creating an object:

```python
person = Person()
```

Important:
- A class defines attributes and methods.
- An object is a specific instance of a class.
- Multiple objects can be created from one class.

---

### The `__init__()` Method

The `__init__()` method initializes a new object.

It runs automatically when an object is created.

```python
class Person:
    def __init__(self, name):
        self.name = name
```

Creating an object:

```python
person = Person("Sara")
```

Important:
- `__init__()` is called the constructor method.
- It is used to set initial object state.

---

### The `self` Parameter

`self` refers to the current object instance.

Example:

```python
class Person:
    def __init__(self, name):
        self.name = name
```

Here:

- `self.name` is an attribute belonging to the object.
- `name` is a local parameter.

Important:
- `self` is automatically passed when calling a method.
- It is not written when calling the method.

---

### Instance Attributes

Attributes store data inside objects.

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
```

Each object has its own attributes:

```python
person1 = Person("Sara", 20)
person2 = Person("Ali", 25)
```

`person1` and `person2` have different values.

---

### Instance Methods

Methods are functions defined inside classes.

```python
class Person:
    def greet(self):
        print("Hello")
```

Calling a method:

```python
person.greet()
```

Python automatically passes the object as `self`.

---

### Class Attributes

Class attributes belong to the class itself and are shared by all objects.

```python
class Person:
    species = "Human"
```

Access:

```python
Person.species
```

or:

```python
person.species
```

Important:
- Instance attributes belong to individual objects.
- Class attributes are shared.

---

### Instance vs Class Attributes

Example:

```python
class Student:
    school = "Python Academy"

    def __init__(self, name):
        self.name = name
```

Here:

- `school` is shared by all students.
- `name` is unique for each student.

---

### Object Representation

Python provides special methods for object representation.

### `__str__()`

Controls what is displayed when using `print()`.

```python
class Person:
    def __str__(self):
        return "A person object"
```

Example:

```python
print(person)
```

---

### `__repr__()`

Provides a developer-friendly representation.

It is used by:

```python
repr(object)
```

A good `__repr__()` helps with debugging.

---

### Class Methods

Class methods work with the class instead of individual objects.

They use `cls` as the first parameter.

```python
class Person:
    count = 0

    @classmethod
    def show_count(cls):
        return cls.count
```

Calling:

```python
Person.show_count()
```

---

### Static Methods

Static methods do not receive `self` or `cls`.

They behave like normal functions placed inside a class.

```python
class Math:
    @staticmethod
    def add(a, b):
        return a + b
```

Calling:

```python
Math.add(2, 3)
```

---

### Inheritance

Inheritance allows one class to reuse another class's behavior.

Parent class:

```python
class Animal:
    def speak(self):
        print("Sound")
```

Child class:

```python
class Dog(Animal):
    pass
```

The child inherits methods from the parent.

---

### Overriding Methods

A child class can replace inherited behavior.

```python
class Dog(Animal):
    def speak(self):
        print("Bark")
```

The child version is used instead of the parent version.

---

### Using `super()`

`super()` calls methods from the parent class.

Example:

```python
class Dog(Animal):
    def __init__(self, name):
        super().__init__()
        self.name = name
```

Useful when extending parent behavior.

---

### Multiple Inheritance

Python allows a class to inherit from multiple classes.

```python
class Child(Parent1, Parent2):
    pass
```

Python uses the Method Resolution Order (MRO) to determine which method is used.

---

### Properties

Properties allow controlling access to attributes.

Instead of directly exposing an attribute:

```python
object.value
```

you can define controlled access.

```python
@property
def value(self):
    return self._value
```

Properties are commonly used for validation and encapsulation.

---

### Private-Like Attributes

Python does not have true private attributes, but naming conventions exist.

Single underscore:

```python
_variable
```

means internal use.

Double underscore:

```python
__variable
```

triggers name mangling.

---

### Dataclasses

Python provides `dataclasses` for classes mainly used to store data.

Example:

```python
from dataclasses import dataclass

@dataclass
class Person:
    name: str
    age: int
```

Dataclasses automatically provide useful methods like:

- `__init__()`
- `__repr__()`
- `__eq__()`

---

### Key Takeaways

- Classes define objects and their behavior.
- Objects are instances of classes.
- `__init__()` initializes objects.
- `self` refers to the current instance.
- Attributes store object data.
- Methods define object behavior.
- Inheritance allows code reuse.
- `super()` accesses parent behavior.
- Class methods use `cls`.
- Static methods do not depend on objects.
- Properties control attribute access.


## Chapter 11 --- Python Programs

### Programs vs Modules

A Python file can be used in two different ways:

- As a program that runs directly.
- As a module that is imported by another program.

A good Python file should be designed so that importing it does not accidentally execute program code.

---

### The `__name__` Variable

Every Python module has a built-in `__name__` variable.

When a file is run directly:

```python
__name__ == "__main__"
```

When a file is imported:

```python
__name__
```

contains the module name.

This allows code to behave differently depending on how the file is used.

---

### The `if __name__ == "__main__"` Pattern

Common structure:

```python
def main():
    print("Program starts here")


if __name__ == "__main__":
    main()
```

Important:

- Functions and classes can be imported without running the program.
- The main program logic only runs when the file is executed directly.
- This makes code easier to reuse and test.

---

### Creating a Main Function

A main function provides a clear entry point for a program.

Example:

```python
def main():
    data = get_data()
    process(data)
    display(data)


if __name__ == "__main__":
    main()
```

Benefits:

- Keeps global code minimal.
- Makes testing easier.
- Separates setup from reusable functions.

---

### Command-Line Arguments

Python programs can receive arguments from the command line.

The `sys` module provides access to them.

```python
import sys

print(sys.argv)
```

Example command:

```text
python program.py hello
```

`sys.argv` contains:

```python
[
    "program.py",
    "hello"
]
```

Important:

- The first item is always the program name.
- Remaining items are user-provided arguments.

---

### Processing Command-Line Arguments

Example:

```python
import sys

if len(sys.argv) > 1:
    print(sys.argv[1])
```

Always validate arguments before using them.

---

### Running Programs with `python -m`

Python can run modules as programs.

Example:

```text
python -m module_name
```

This runs the module while allowing Python to handle imports correctly.

---

### Testing Programs

A program should be tested while it is being developed.

A common approach is creating a test mode.

Example:

```python
def test():
    print("Running tests")


if __name__ == "__main__":
    test()
```

Testing helps detect problems when code changes.

---

### Modules as Testable Components

A module should contain reusable code that can be tested independently.

Good structure:

```python
def calculate(value):
    return value * 2


def main():
    print(calculate(5))


if __name__ == "__main__":
    main()
```

The function can be tested without running the whole program.

---

### Distributing Python Applications

Python applications can be distributed in several ways.

Common approaches:

- Source files
- Packages
- Executable archives
- Standalone applications

The best approach depends on the needs of the users and the application.

---

### Wheel Packages

Wheels are the standard format for distributing Python packages.

Advantages:

- Easier installation.
- Better dependency handling.
- Works with Python package tools.

Typical installation:

```text
pip install package_name
```

---

### Executable Zip Applications (`zipapp`)

Python can package applications as executable zip files.

A zip application requires:

```text
__main__.py
```

The `__main__.py` file acts as the program entry point.

Example structure:

```
my_app.zip
|
├── __main__.py
├── module1.py
└── module2.py
```

Run:

```text
python my_app.zip
```

---

### Standalone Applications

Tools can create applications that run without requiring a separate Python installation.

Examples:

- `py2exe` for Windows
- `py2app` for macOS
- `freeze`

Important:

Standalone applications are usually larger and more complex than normal Python programs.

---

### Key Takeaways

- A Python file can be both a program and a module.
- `__name__ == "__main__"` prevents code from running during imports.
- A `main()` function provides a clean program entry point.
- Command-line arguments are available through `sys.argv`.
- Testing is easier when code is organized into functions.
- Python applications can be distributed using packages, wheels, or executable archives.



## Chapter 12 --- Working with Databases

### Why Use Databases?

Databases store and organize data so that programs can retrieve and modify it efficiently.

Compared with storing data in files, databases provide:

- Structured data storage.
- Faster searching.
- Data consistency.
- Support for large amounts of data.

Python can work with many database systems, including SQLite, PostgreSQL, and MySQL.

---

### Relational Databases

Most traditional databases are relational databases.

Data is stored in tables:

```
Table
|
├── Rows → Records
└── Columns → Fields
```

Example:

| id | name | age |
|---|---|---|
| 1 | Sara | 20 |
| 2 | Ali | 25 |

Important concepts:

- A row represents one record.
- A column represents one attribute.
- A table stores related data.

---

### SQL

SQL (Structured Query Language) is used to interact with relational databases.

Common operations:

- Create data.
- Read data.
- Update data.
- Delete data.

These operations are often called CRUD:

| Operation | SQL command |
|---|---|
| Create | `INSERT` |
| Read | `SELECT` |
| Update | `UPDATE` |
| Delete | `DELETE` |

---

### SQLite

SQLite is a lightweight database included with Python.

It stores the database in a single file and does not require a separate server.

Import:

```python
import sqlite3
```

Connecting:

```python
connection = sqlite3.connect("database.db")
```

If the file does not exist, SQLite creates it.

---

### Database Connections and Cursors

A connection represents the database connection.

A cursor is used to execute SQL commands.

Example:

```python
cursor = connection.cursor()
```

The cursor sends SQL statements to the database.

---

### Creating a Table

SQL commands can be executed from Python.

Example:

```python
cursor.execute("""
CREATE TABLE users (
    id INTEGER,
    name TEXT
)
""")
```

Important:

- Table names and column names define the structure.
- Data types describe what values can be stored.

---

### Inserting Data

Adding data uses `INSERT`.

Example:

```python
cursor.execute(
    "INSERT INTO users VALUES (?, ?)",
    (1, "Sara")
)
```

Important:

Use placeholders (`?`) instead of building SQL strings manually.

This prevents SQL injection problems.

---

### Saving Changes

Database changes must be committed.

```python
connection.commit()
```

Without committing, changes may not be permanently stored.

---

### Querying Data

Reading data uses `SELECT`.

Example:

```python
cursor.execute(
    "SELECT * FROM users"
)
```

Fetching results:

```python
rows = cursor.fetchall()
```

Other methods:

```python
cursor.fetchone()
cursor.fetchmany()
```

---

### Updating Data

Changing existing records uses `UPDATE`.

Example:

```python
cursor.execute(
    "UPDATE users SET name=? WHERE id=?",
    ("Ali", 1)
)
```

Always use conditions carefully.

Without `WHERE`, all rows may be updated.

---

### Deleting Data

Removing records uses `DELETE`.

Example:

```python
cursor.execute(
    "DELETE FROM users WHERE id=?",
    (1,)
)
```

Like updates, deleting without `WHERE` can remove all records.

---

### Parameterized Queries

Never build SQL using string formatting.

Bad:

```python
sql = f"SELECT * FROM users WHERE name='{name}'"
```

Better:

```python
cursor.execute(
    "SELECT * FROM users WHERE name=?",
    (name,)
)
```

Benefits:

- Prevents SQL injection.
- Handles special characters correctly.
- Separates code from data.

---

### Using Context Managers

Database connections can be managed with `with`.

Example:

```python
with sqlite3.connect("database.db") as connection:
    cursor = connection.cursor()
```

The connection is automatically handled when the block finishes.

---

### Object Relational Mapping (ORM)

ORM tools allow working with databases using Python objects instead of writing SQL directly.

Example idea:

Instead of:

```sql
SELECT * FROM users;
```

you work with:

```python
User.objects.all()
```

Advantages:

- Less SQL code.
- Easier integration with Python programs.

Disadvantages:

- Can hide database details.
- Complex queries may still require SQL.

---

### Database Design Basics

Good database design avoids unnecessary duplication.

Important concepts:

- Primary key → uniquely identifies a record.
- Foreign key → connects tables together.
- Relationships → describe how tables are connected.

---

### Transactions

A transaction groups multiple database operations into one unit.

Example:

```python
connection.commit()
```

Save changes.

```python
connection.rollback()
```

Undo changes.

Transactions help keep data consistent.


## Chapter 13 --- Reading and Writing Files

### Files and Paths

Files allow programs to store and retrieve data permanently.

Python provides tools for:

- Opening files.
- Reading data.
- Writing data.
- Managing file paths.

---

### Opening Files

The `open()` function creates a connection to a file.

Syntax:

```python
open(filename, mode)
```

Example:

```python
file = open("data.txt", "r")
```

Important:
- Files should be closed after use.
- The mode determines how the file is accessed.

---

### File Modes

Common modes:

| Mode | Meaning |
|---|---|
| `r` | Read |
| `w` | Write (overwrites existing content) |
| `a` | Append |
| `x` | Create a new file |
| `b` | Binary mode |
| `t` | Text mode |

Examples:

```python
open("data.txt", "r")
```

Read text.

```python
open("image.png", "rb")
```

Read binary data.

---

### Reading Files

Reading the whole file:

```python
file.read()
```

Reading a specific number of characters:

```python
file.read(10)
```

Reading one line:

```python
file.readline()
```

Reading all lines:

```python
file.readlines()
```

---

### Writing Files

Writing text:

```python
file.write("Hello Python")
```

Writing multiple lines:

```python
file.writelines(lines)
```

Important:

- `write()` replaces nothing by itself, but opening with `"w"` removes existing content.
- Use `"a"` when adding new content.

---

### Closing Files

Files should be closed after use.

```python
file.close()
```

Closing releases system resources and ensures data is saved properly.

---

### Using `with` for Files

The recommended approach is using a context manager.

```python
with open("data.txt", "r") as file:
    data = file.read()
```

Important:

- The file is automatically closed.
- It is safer when errors occur.

---

### Reading Files Line by Line

Files are iterable, so they can be used directly in loops.

```python
with open("data.txt") as file:
    for line in file:
        print(line)
```

This is efficient for large files because the entire file is not loaded into memory.

---

### Text and Binary Files

Text files store characters.

Examples:

- `.txt`
- `.csv`
- `.json`

Binary files store bytes.

Examples:

- Images
- Audio files
- Executable files

Binary mode:

```python
open("image.png", "rb")
```

Important:

Binary data uses `bytes`, not strings.

---

### File Paths

Python can work with file paths using strings or the `pathlib` module.

Example:

```python
"path/to/file.txt"
```

---

### The `pathlib` Module

`pathlib` provides an object-oriented way to work with paths.

```python
from pathlib import Path

path = Path("data.txt")
```

Useful methods:

```python
path.exists()
path.name
path.parent
```

---

### Reading and Writing with `pathlib`

Reading text:

```python
path.read_text()
```

Writing text:

```python
path.write_text("Hello")
```

Reading bytes:

```python
path.read_bytes()
```

Writing bytes:

```python
path.write_bytes(b"Hello")
```

---

### File Position

Files keep an internal position indicating where the next operation occurs.

Example:

```python
file.read()
```

moves the position forward.

The position can be checked using:

```python
file.tell()
```

Move the position using:

```python
file.seek(position)
```

---

### Pickling Objects

Python can save objects directly using the `pickle` module.

Writing:

```python
import pickle

with open("data.pkl", "wb") as file:
    pickle.dump(object, file)
```

Reading:

```python
with open("data.pkl", "rb") as file:
    data = pickle.load(file)
```

Important:

- Pickle stores Python objects.
- Do not load pickle files from untrusted sources because they can execute malicious code.

---

### Terminal Input and Output

Python can read input from users using `input()`.

```python
name = input("Name: ")
```

Important:

`input()` always returns a string.

Convert when needed:

```python
number = int(input("Number: "))
```

---

### Standard Input and Output

The `sys` module provides access to:

```python
sys.stdin
sys.stdout
sys.stderr
```

Example:

```python
import sys

sys.stdout.write("Hello")
```

These are useful for advanced command-line programs and redirection.


## Chapter 14 --- Exceptions

### What Are Exceptions?

Exceptions are events that occur during program execution and interrupt the normal flow of a program.

Examples:

```python
10 / 0
```

causes:

```text
ZeroDivisionError
```

```python
int("hello")
```

causes:

```text
ValueError
```

Important:
- Exceptions are objects.
- They represent errors or unexpected situations.
- Python uses exceptions instead of returning error codes.

---

### Handling Exceptions

Python uses `try` and `except` blocks to handle exceptions.

Syntax:

```python
try:
    statement
except:
    statement
```

Example:

```python
try:
    number = int(input("Number: "))
except:
    print("Invalid input")
```

Important:

- Code inside `try` is monitored for errors.
- Code inside `except` runs only when an exception occurs.

---

### Catching Specific Exceptions

Avoid catching all exceptions unless necessary.

Better:

```python
try:
    number = int(value)
except ValueError:
    print("Not a valid number")
```

Common exceptions:

| Exception | Meaning |
|---|---|
| `ValueError` | Correct type but invalid value |
| `TypeError` | Wrong type of object |
| `IndexError` | Invalid sequence index |
| `KeyError` | Missing dictionary key |
| `FileNotFoundError` | File does not exist |
| `ZeroDivisionError` | Division by zero |

---

### Multiple Exception Handlers

A `try` block can have multiple `except` blocks.

```python
try:
    value = data[index]
except IndexError:
    print("Invalid index")
except TypeError:
    print("Wrong type")
```

Python checks handlers from top to bottom.

---

### Accessing Exception Objects

An exception object can be stored using `as`.

```python
try:
    value = int(text)
except ValueError as error:
    print(error)
```

The variable contains information about the exception.

---

### The `else` Block

A `try` statement can include `else`.

```python
try:
    result = calculate()
except Exception:
    print("Failed")
else:
    print(result)
```

The `else` block runs only if no exception occurs.

---

### The `finally` Block

`finally` always runs, whether an exception occurs or not.

```python
try:
    file = open("data.txt")
finally:
    file.close()
```

Common uses:

- Closing files.
- Releasing resources.
- Cleaning up operations.

---

### Raising Exceptions

Programs can create exceptions using `raise`.

```python
raise ValueError("Invalid value")
```

Example:

```python
def set_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative")
```

Important:

Use `raise` when a situation should be considered an error.

---

### Creating Custom Exceptions

Custom exceptions are created by inheriting from `Exception`.

```python
class InvalidAgeError(Exception):
    pass
```

Using it:

```python
raise InvalidAgeError("Invalid age")
```

Custom exceptions make programs easier to understand.

---

### Exception Hierarchy

Exceptions are organized in a class hierarchy.

Example:

```
BaseException
    |
    Exception
        |
        ValueError
        |
        TypeError
```

Catching a parent exception also catches its child exceptions.

Example:

```python
except Exception:
```

can catch many common errors.

---

### Exception Chaining

Python can preserve the original cause of an exception.

Example:

```python
try:
    int("abc")
except ValueError as error:
    raise RuntimeError("Conversion failed") from error
```

This keeps both errors visible.

---

### Avoiding Bare `except`

A bare `except` catches everything.

Example:

```python
try:
    code()
except:
    pass
```

Problems:

- Hides programming mistakes.
- Makes debugging harder.
- Can catch unexpected errors.

Prefer:

```python
except ValueError:
```

or another specific exception.

---

### Exceptions and Program Flow

Exceptions change the normal execution path.

Normal flow:

```
statement 1
statement 2
statement 3
```

With an exception:

```
statement 1
error occurs
exception handler runs
```

---

### Exceptions vs Returning Errors

Exceptions are useful when:

- An operation cannot continue normally.
- The error should be handled separately.
- The problem is exceptional.

Returning values is often better for normal expected situations.

