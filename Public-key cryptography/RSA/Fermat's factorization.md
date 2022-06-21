Fermat's factorization is based on the representation of an odd integer as the difference of two squares:
$$N = a^2 - b^2$$
We can rewrite this as:
$$N = (a+b)(a-b)$$

Algortihm:
One tries various values of $a$ hoping that $a^2 - N = b^2$ is a square
```python
from gmpy2 import isqrt, is_square

def fermats_factorization(N):
    a = isqrt(N)
    b_2 = a*a - N

    while not is_square(b_2):
        a = a + 1
        b_2 = a*a - N

    b = isqrt(b_2)
    return (a + b), (a - b)

```