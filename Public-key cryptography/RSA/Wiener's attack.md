The Wiener's attacks uses the [[Continued Fraction]] method to expose the private key `d` or primes `p` and `q` when `d` is small.

How Wiener's attack works:
$ed \equiv 1 (\textrm{mod}\ \varphi(n))$
$ed = k\varphi(n) + 1$
$ed - k\varphi(n) = 1$
dividing everything with $k\varphi(n)$ we get
$$\frac{ed}{k\varphi(n)} - 1 = \frac{1}{k\varphi(n)}$$
Multiplying with $\frac{k}{d}$
$$\frac{e}{\varphi(n)} - \frac{k}{d} = \frac{1}{d\varphi(n)}$$
Now $\frac{1}{d\varphi(n)}$ is small so $\frac{k}{d}$ becomes [[Rational Approximation]] of $\frac{e}{\varphi(n)}$

Wiener's theorem states that when $d < \frac{1}{3}N^{\frac{1}{4}}$ , $d$ can be efficiently recovered by searching the right $\frac{k}{d}$ amond the convergents of $\frac{e}{N}$ 

The algorithm:
1. Find the convergents of the [[Continued Fraction]] expansion of $\frac{e}{N}$.
2. Iterate through the convergents $\frac{d_i}{k_i}$
	1. Compute $\varphi_i(N)$ using $k_i$ and $d_i$
	2. Ascertain correctness through factoring $N$ with $\varphi_i(N)$

```python
def contfrac_to_rational_iter(contfrac): 
    n0, d0 = 0, 1
    n1, d1 = 1, 0
    for q in contfrac:
        n = q * n1 + n0
        d = q * d1 + d0
        yield n, d
        n0, d0 = n1, d1
        n1, d1 = n, d


def convergents_from_contfrac(contfrac):
    n_, d_ = 1, 0
    for i, (n, d) in enumerate(contfrac_to_rational_iter(contfrac)):
        if i % 2 == 0:
            yield n + n_, d + d_
        else:
            yield n, d
        n_, d_ = n, d
def rational_to_contfrac(x: int, y: int):
    _a = []
    while y != 0:
        a = x // y
        _a.append(a)
        x, y = y, x - a * y
    return _a

def wieners_attack(e: int, n: int):
    f_ = rational_to_contfrac(e, n)
    for pk, pd in convergents_from_contfrac(f_):
        if pk == 0:
            continue
        print(pk, pd)
        ed = e * pd
        phi = (ed) // pk

        x = phi - n - 1
        discriminant = x ** 2 - 4*n 
        if discriminant > 0:
            p = (-x + isqrt(discriminant)) // 2
            q = (-x - isqrt(discriminant)) // 2
            if p*q == n:
                return (p, q)

```