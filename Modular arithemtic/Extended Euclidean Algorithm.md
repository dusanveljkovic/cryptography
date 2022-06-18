Exnteded Eucliedan Algorithm extends [[Euclid's Algorithm]] and in addition to computing GCD, computes the coefficients of [[Bezeout's identity]], which are integers `x` and `y` such that :
$ax + by = gcd(a, b)$

When `a` and `b` are coprime the integer `x` is the [[Modular Multiplicative Inverse]] of `a % b`, and `y` is the MMI of `b % a`.

Let's define the sequences $\{q_i\},\{r_i\},\{s_i\},\{t_i\}$ with $r_0=a,r_1=b$. Set i \gets 2i←2, and increase it at the end of every iteration We also want to write $r_i$ as a linear combination of $a$ and $b$, i.e., $r_i=s_i a+t_i b$. But $r_i=r_{i-2}-r_{i-1}q_i$, so

$r_i=s_{i-2}a+t_{i-2}b-(s_{i-1}a+t_{i-1}b)q_i=(s_{i-2}-s_{i-1}q_i)a+(t_{i-2}-t_{i-1}q_i)b$.

Hence, we obtain $s_i=s_{i-2}-s_{i-1}q_i$ and $t_i=t_{i-2}-t_{i-1}q_it$.

Now, we have to find the initial values of the sequences $\{s_i\}$ and $\{t_i\}$. By the definition of $r_i$, we have

$\begin{aligned} a=r_0=s_0 a+t_0 b &\implies s_0=1, t_0=0\\ b=r_1=s_1 a+t_1 b &\implies s_1=0, t_1=1. \end{aligned}$

Finally, we stop at the iteration in which we have $r_{i-1}=0$. Let's call this the $n^\text{th}$ iteration, so $r_{n-1}=0$. That means that $\gcd(a,b)=\gcd(r_0,r_1)=\gcd(r_1,r_2)=\cdots=\gcd(r_{n-2},r_{n-1})=\gcd(r_{n-2},0)=r_{n-2}$, so we found our desired linear combination:

$\gcd(a,b)=r_{n-2}=s_{n-2} a + t_{n-2} b$

```python
def wiki_extended_gcd(a: int, b: int) -> int:
    (old_r, r) = (a, b)
    (old_s, s) = (1, 0)
    (old_t, t) = (0, 1)

    while r != 0:
        quotient = old_r // r
        (old_r, r) = (r, old_r - quotient * r)
        (old_s, s) = (s, old_s - quotient * s)
        (old_t, t) = (t, old_t - quotient * t)

    #print('Bezout coefficients: {} {}'.format(old_s, old_t))
    #print('GCD: {}'.format(old_r))
    #print('quotients by the gcd {} {}'.format(t, s))
    return (old_r, old_s, old_t)

```