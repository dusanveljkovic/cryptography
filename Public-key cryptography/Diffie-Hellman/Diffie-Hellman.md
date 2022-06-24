Set of integers modulo `n` together with the operations of both addtion and multiplication is a [[Ring]].

When the modulus is prime `n = p`, we are guaranteed an inverse of every element in the set, and so the [[Ring]] is promoted to a [[Field]]. We refer to this field as the finite field $F_p$.

Every element of $F_p$ can be used to make a subgroup $H$ under repeated action of multiplication. $$g: H = \{g, g^2, g^3, ...\}$$
If every element of $F_p$ can be written as $g^n (\textrm{mod}\ p)$ for some integer $n$.

Diffie-Hellman protocol is used because the discrete logarithm is assumed to be a "hard" computation to carefully chosen groups.

Algorithm: 
1. First choose a prime $p$ and some generator of the finite field $g$. A safe prime $p = 2*q + 1$ is usually picked such that the only factors of $p-1$ are $\{2,q\}$ where $q$ is some other large prime.
2. The user pick a secret integer $a < p$ and calculates $g^a (\textrm{mod}\ p)$ 
3. Calculate the shared secret using with the other persons $B = g^b (\textrm{mod}\ p)$ => $S = B^a (\textrm{mod}\ p)$ 
4. The other person calculates the shared secret by using $A$ => $S = A^b (\textrm{mod}\ p)$ 
5. Shared secret is the same for both parties because $$A^b = (g^a)^b = g^{ab}$$ and $$B^a = (g^b)^a = g^{ab}$$
