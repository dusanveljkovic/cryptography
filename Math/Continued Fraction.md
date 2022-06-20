A continued fraction is an expression obtained through an iterative process of representing a number as the sum of its integer part and the reciprocal of another number, then writing this other number as the sum of its integer part and another reciprocal and so on.

```python
def rational_to_contfrac(x: int, y: int):
    _a = []
    while y != 0:
        a = x // y
        _a.append(a)
        x, y = y, x - a * y
    return _a
```