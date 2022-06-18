Modular exponentiation is exponentiation performed over a modulus. It is useful in the field of public-key cryptography, where it is used in both [[Diffie-Hellman]] and [[RSA]].

Modular exponentiation is efficient to compute even for very large integers. On the other hand computing the modular [[Discrete Logarithm]] is believed to be difficult.

```python
def power_mod(b, e, m):  
    " Without using builtin function "  
    x = 1  
    while e > 0:  
        b, e, x = (  
            b * b % m,  
            e // 2,  
            b * x % m if e % 2 else x  
        )  
   
    return x
```