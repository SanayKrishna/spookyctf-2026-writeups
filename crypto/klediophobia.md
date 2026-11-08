# Klediophobia

**Category:** Crypto

## The challenge

A PKI-flavoured challenge: four intermediate certificates with their matching CSRs, and a server that would hand over the flag if I could sign a fresh audit message as the right authority.

## Figuring it out

I compared the four intermediate certs against their CSRs and noticed `ST-ISS-03` was flagged `OBJ-0003-R`, which singled it out as the one to look at. The usual reason a specific key gets called out in these is weak key generation, so I tested small private scalars against the public keys.

`ST-ISS-03` turned out to use the P-384 private scalar **1963**. Tiny, which is the whole vulnerability.

## Solving it

1. Verify the scalar `1963` against the certificate's public key.
2. Request a fresh audit message from the challenge server.
3. Sign it with ECDSA-SHA384 using that key.
4. Submit the Base64 DER signature.

The server accepted it and returned the flag.

## Flag

```
spooky{4T_L345T_1T_15NT_F0UR}
```

## Takeaway

When one key in a set is explicitly marked or named, suspect weak generation. A private scalar small enough to brute force (here it was 1963) breaks the whole signing identity, and from there you just sign whatever the server asks for.
