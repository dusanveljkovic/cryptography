RSA signing has the following steps:
1. Use [[RSA Encryption]] to encrypt the message $C = M^{e_0} (\textrm{mod}\ N_0)$ 
2. Calcualte the hash of the mssage `H(M)` and 'encrypt' this with your private key $S = H(M)^{d_1}$ 

Then the message can be verified  by:
1. Use [[RSA Decryption]] to decrypt the message $m = C^{d_0} (\textrm{mod}\ N_0)$ 
2. Calculate $s = S^{e_1} (\textrm{mod}\ N_1)$ 
3. Compute `H(m)` and compare it to `s`: `assert H(m) == s` 

```python
def rsa_sign(message: bytes, private_key: int, public_key: (int, int)) -> (int, int):
    ciphertext = rsa_encrypt(message, public_key)

    h = hashlib.sha256(message).digest()

    s = rsa_encrypt(h, (public_key[0], private_key))

    return (ciphertext, s)

```