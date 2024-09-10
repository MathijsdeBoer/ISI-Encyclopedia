Python Enhancement Proposal (PEP) [484](https://peps.python.org/pep-0484/) introduced the concept of type hints to Python v3.5. These extra bits of text in your code let you, and a static analyzer, know what you intend a certain value or argument to be. Take for example the function `foo(a, b)`. It's clear that it takes 2 arguments, `a` and `b`, but what are these values supposed to be? Does the function return anything? With type hinting we can annotate `foo()` to inform the user what it wants.

```python
def foo(a, b):
	return a + b
```
turns into
```python
def foo(a: int, b: int) -> int:
	return a + b
```
A function that doesn't return anything would be
```python
def bar() -> None:
	print("Type hints are the only type of hints men get")
```
This shows that with only a little bit of extra typing, you can improve the usability and readability of your code immensely! It's suggested you keep the habit of including type hints as you create new classes and functions, just so you don't have to go back later and include them post-hoc.

> [!caution]
Type hints are just that, hints. It will not prevent you from putting a different datatype in `foo()` anyway. The user (usually you!) should take these as a "buyer beware" and accept any unexpected behavior or crashing as a result of overriding the type hints. Conversely, weird behavior and unexpected crashes are _potentially_ the result of you ignoring a type hint.

## Multiple types
What if your function supports multiple types for a given input? In the following definition of `foo()` we add `a` to itself. Many datatypes, such as numerical ones, support this operation.
```python
def foo(a):
	return a + a
```
There's some options you could use, depending on your needs and expectations. For example, if you know you only want to use a limited set of datatypes here, you can use the following:
```python
# All versions >=3.5
from typing import Union

def foo(a: Union[int, float]) -> Union[int, float]:
	return a + a

# All versions >= 3.10
def foo(a: int | float) -> int | float:
	return a + a

# All versions >= 3.12
def foo[T](a: T) -> T:
	return a + a

# or 
from typing import TypeVar

T = TypeVar('T')

def foo(a: T) -> T:
	return a + a
```
The above code block shows that every few versions of Python a new way of declaring type hints are introduced, each adding a little more power, or simply increasing some readability. It is not unlikely that future versions of Python will start introducing some more "syntactic sugar" to the typing system, so you should check out the current state of them every once in a while!