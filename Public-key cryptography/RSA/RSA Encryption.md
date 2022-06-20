RSA encryption is [[Modular Exponentiation]] of a message with an exponent `e` and a modulus `N` which is normally a product of two primes: `N = p * q`

Together the exponent and the modulus form an RSA "public key" `(N, e)`. The most common value for `e` is `0x10001` or `65537`

```python
def rsa_encrypt(message: bytes, public_key: (int, int)) -> int:
    message_int = int.from_bytes(message, 'big')

    N, e = public_key

    return _hex(pow(message_int, e, N))

```