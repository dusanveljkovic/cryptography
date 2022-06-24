Blinding attack is executed when we want to sign a message which the server refuses to sign. We trick the server into signing it regardless by letting it sign our data and then modify that signature to get a signature of the original message we wanted to sign.

Algorithm:
1. We make a new message by multiplying our wanted message with a random number $r^e$ $$M^{'} \equiv r^eM (\textrm{mod}\ N)$$
2. Then we let the server sign this message $$S^{'} \equiv (M^{'})^d (\textrm{mod}\ N)$$
3. We divide this signature by $r$ and get the signature of our original message$$\frac{S^{'}}{r} = \frac{(Mr^e)^d}{r} = \frac{(M^{d}r^{ed})}{r} = \frac{(M^{d}r^1)}{r} = M^d (\textrm{mod}\ N)$$
```python
def blinding_light():
    ADMIN_TOKEN = b'admin=True'
    token_int = int.from_bytes(ADMIN_TOKEN, 'big')
    c = Client('socket.cryptohack.org', 13376)

    c.readline()

    request = {
        'option': 'get_pubkey'
    }
    c.json_send(request)
    pubkey = c.json_recv()
    N, e = int(pubkey['N'], 16), int(pubkey['e'], 16)
    r = 1337
    forged = (token_int * pow(r, e, N)) % N

    request = {
        'option': 'sign',
        'msg': hex(forged)[2:]
    }

    c.json_send(request)
    signature = int(c.json_recv()['signature'], 16)
    correct_signature = (signature * modinv(r, N)) % N

    request = {
        'option': 'verify',
        'msg': hex(token_int)[2:], 
        'signature': hex(correct_signature)
    }

    c.json_send(request)
    print(c.json_recv())


```