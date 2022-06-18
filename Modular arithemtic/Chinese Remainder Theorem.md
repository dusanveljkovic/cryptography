Chinese remainder theorem gives a unique solution to a set of linear congruences if their moduli are coprime.

Given a set of arbitrary integers $a_i$ and pairwise coprime integers $n_i$, such that the following linear congruences hold:

x ≡ a1 mod n1  
x ≡ a2 mod n2  
...  
x ≡ an mod nn

There is a unique solution $x \equiv a (\textrm{mod}\ N)$ where $N = n_1 * n_2 * ... * n_n$

Algorithm:
1. Compute $N = n_1 * n_2 * ... * n_n$
2. For each $i = 1, 2, ..., k$, compute
$$y_i = \frac{N}{n_i}$$
3. For each $i = 1,2,...,k$, compute $z_i \equiv y_{i}^{-1} (\textrm{mod}\ n_i)$ using [[Extended Euclidean Algorithm]]
4. The integer $x = \sum_{i=1}^k a_{i}y_{i}z_{i}$ is the solution to the system of congruences 

```python
def chinese(a: [int], n: [int]) -> int:
    N = reduce(lambda a, b: a * b, n, 1)
    y = list(map(lambda a: N // a, n))
    z = list(map(lambda a: wiki_extended_gcd(a[0], a[1])[1], list(zip(y, n))))
    x = reduce(lambda a, b: a + b[0]*b[1]*b[2], zip(a, y, z), 0)
    return x

```