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
