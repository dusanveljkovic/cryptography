The private key `d` is used to decrypt ciphertexts created with the corresponding public key.

In [[RSA]] the private key is the [[Modular Multiplicative Inverse]] of the exponent `e` modulo the [[Euler Totient]] of `N`.

```python
def rsa_decrypt(ciphertext: int, private_key: int, public_key: (int, int)) -> int:
    N, _ = public_key

    return _hex(pow(ciphertext, private_key, N))


```