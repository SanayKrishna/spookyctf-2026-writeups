# Heads will Roll

**Category:** Crypto

## The challenge

> While chasing Ichabod Crane through Sleepy Hollow, the Headless Horseman got as close as he could, then threw his head! While rolling, rolling, rolling, rolling, through the air, his pumpkin head shouted…what? His perfect aim knocked Ichabod to the ground near the rails, but what did he say?

Attached was a text file with a scrambled string.

## Figuring it out

First thing I did was stare at the ciphertext. Every character of a `spooky{...}` flag was in there (the braces, the letters) but shuffled into the wrong order. That's the tell for a transposition cipher: the letters don't change, their positions do. If it were a substitution the `s` and `p` would have been turned into something else.

So which transposition? The description hands it over twice. "Near the rails" is the cipher name, and "rolling" said four times is the key.

## Solving it

I dropped the text into CyberChef and added **Rail Fence Cipher Decode**, key 4, offset 0.

Out came a readable sentence with the flag on the end.

## Flag

```
spooky{5l33py_h0ll0w_h34d5}
```

## Takeaway

When all the original characters are present but jumbled, think transposition, not substitution. And read the flavour text like it's a hint sheet, because here it named both the cipher and the key.
