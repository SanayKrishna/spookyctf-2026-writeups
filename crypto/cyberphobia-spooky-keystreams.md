# Cyberphobia: SpOoKy KeYsTrEaMs

**Category:** Crypto

## The challenge

A `backup.py` script plus a known plaintext message, its ciphertext, and the encrypted flag.

## The bug

`backup.py` encrypts with **AES-CTR using a fixed nonce and a fixed initial counter**. That's the classic keystream-reuse mistake. CTR mode turns the block cipher into a stream cipher: it generates a keystream and XORs it with the plaintext. If the nonce and counter are the same every time, the keystream is the same every time.

## Solving it

Because XOR is reversible, a known plaintext and its ciphertext leak the keystream directly:

```
keystream = known_plaintext XOR known_ciphertext
```

Then reuse that keystream on the encrypted flag:

```
flag = keystream XOR encrypted_flag
```

## Flag

```
spooky{cs351JKS}
```

## Takeaway

AES-CTR (or any stream cipher) with a reused nonce/counter is broken. One known plaintext/ciphertext pair recovers the keystream, and the same keystream decrypts anything else sent under it. Never reuse a nonce.
