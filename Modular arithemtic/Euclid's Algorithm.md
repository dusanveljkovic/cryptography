Euclid's algorithm is used to find the GCD of two positive integers.

It is based on a fact that GCD of two numbers doesn't change if you replace the bigger one with their difference. This process reduces the larger number and by applying it many times we get smaller and smaller pairs of numbers. This goes on until they become equal and then the GCD has been found. 

A more efficient version of the algorithm replaces the larger of the two numbers with the by its reminder when divided by the smaller one.

By using [[Extended Euclidean Algorithm]] the GCD can be expressed as a linear combiantion of the two numbers.

```python
def gcd(a: int, b: int) -> int:
	if b == 0:
		return a
	return gcd(b, a % b)
```