# Python Style Guide

This is a style guide for writing code in Python 3.

## PEP 8 Style Guide

As a base guide, the [PEP 8 Style Guide](https://www.python.org/dev/peps/pep-0008/) should be followed.
The [pycodestyle](https://pypi.org/project/pycodestyle/) style checker can be used to check this.

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

from local_module import first_thing, second_thing, third_thing
import second_local_module
import z_another_local_module
```
