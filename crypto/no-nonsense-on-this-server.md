# No Nonsense on this Server

**Category:** Crypto

## The challenge

I could authenticate to a server as a low-privilege user (`general`) with a supplied key. The flag lived in `/home/admin/flag.txt`, so I needed to become `admin`.

## Figuring it out

Logged in as `general`, I could read `/var/log/auth.log`. The log held signed records for `admin`, and two of those ECDSA signatures **reused the same nonce**. You can spot it because a reused nonce produces the same `r` value in both signatures.

ECDSA with a repeated nonce is game over: the private key falls out algebraically from the two signatures and the two signed messages. This is the same bug that leaked the PS3 signing key.

## Solving it

1. Pull the two `admin` signatures with the matching `r` from the log, along with the messages they signed.
2. Recover the admin private key from the nonce reuse.
3. Authenticate as `admin` with that key.
4. Read `/home/admin/flag.txt`.

## Flag

```
spooky{reused_k_no_nons3nse_89f3ae32316e}
```

## Takeaway

Equal `r` values across two ECDSA signatures means a reused nonce, and that hands you the private key. The challenge name is a straight hint: no reusing `k`.
