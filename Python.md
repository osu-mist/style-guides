# Python Style Guide ![python3](https://img.shields.io/badge/python-3-blue.svg)

This is a style guide for writing code in Python 3.

## Flake8 Style Guide

As a base guide, the [Flake8 Style Guide](http://flake8.pycqa.org/en/latest/) should be followed.

> Note: Flake8 is a wrapper around the following linting tools:
> * [PyFlakes](https://pypi.org/project/pyflakes/)
> * [pycodestyle](https://pypi.org/project/pycodestyle/)
> * [Ned Batchelder’s McCabe script](https://pypi.org/project/mccabe/)

## Binary Operator Line Breaks

When splitting statements over multiple lines, line breaks should occur **before** binary operators

Example:
```python3
first_number
+ second_number
- third_number
```

Example:
```python3
first_boolean
and second_boolean
and (
    third_boolean
    or not fourth_boolean
)
```

## Multiline if-statements

When the conditional of an if-statement needs to be split over multiple lines, it should adhere to the following format:

```python3
if (
    this_is_one_thing
    and this_is_another_thing
):
    do_stuff()
    do_some_other_stuff()
```

## Imports

PEP 8 specifies [three different import groups](https://www.python.org/dev/peps/pep-0008/#imports) each separated by a blank line:
> 1. Standard library imports.
> 2. Related third party imports.
> 3. Local application/library specific imports.

Within each of these groups, imports should be sorted alphabetically.

Example:
```python3
import os
import sys

from requests import Session
import yaml

import local_module
from second_local_module import first_thing, second_thing, third_thing
import z_another_local_module
```

## Docstrings

[Python Docstrings](https://www.python.org/dev/peps/pep-0257/) may be used to add documentation to Python code.
The [reStructuredText (reST) Docstring Format](https://www.python.org/dev/peps/pep-0287/) is the preferred docstring format.

### Related Tools

* **Visual Studio Code**: [autoDocstring](https://marketplace.visualstudio.com/items?itemName=njpwerner.autodocstring) plugin.
    Add `"autoDocstring.docstringFormat": "sphinx"` to your `settings.json`
* **Vim**: [vim-pydocstring](https://github.com/heavenshell/vim-pydocstring) plugin. Uses reST by default.
* **Command Line**: [pyment](https://github.com/dadadel/pyment). Uses reST output docstring format by default.

### Examples

#### Basic example

```python3
def sum(a, b):
    """Computes the sum of two numbers

    :param a: The first number
    :param b: The second number
    :returns: The sum of a and b
    """
    return a + b
```

#### Example with types

```python3
from types import number


def sum(a: number, b: number) -> number:
    """Computes the sum of two numbers

    :param number a: The first number
    :param number b: The second number
    :returns: The sum of a and b
    :rtype: number
    """
    return a + b
```

**Note**: Parameter types can also be placed on separate lines:

```python3
    :param a: The first number
    :type a: number
```

but return types must be on a separate line using `:rtype`
