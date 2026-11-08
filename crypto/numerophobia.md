# Numerophobia

**Category:** Crypto

## The challenge

A story about a missing man who was "last seen walking out at midnight screaming random numbers in tongues never spoken before," plus a few oddly specific details: a book about dyslexia, and every other step on a staircase missing and marked with a 13. The attached file was just a long list of numbers.

## Figuring it out

The numbers mostly sat between 32 and 126, which is the printable ASCII range, so my first guess was that each number is a character code. `65` is `A`, `123` is `{`, and so on.

The rest of the story is the recipe:

- "every other step was missing and marked with a 13" every second number has had 13 added to it, so I subtract 13 back off the alternating ones.
- "a book about dyslexia" letters in the wrong order, so the final text reads backwards.

The one thing I had to test was *which* alternating numbers get the 13 removed, the even-indexed or the odd-indexed ones. Starting from the first number (index 0) gave clean text, the other way gave garbage.

## Solving it

```python
nums = list(map(int, open('numerophobia.txt').read().split()))

out = ''
for i, n in enumerate(nums):
    if i % 2 == 0:
        n -= 13
    out += chr(n)

print(out[::-1])
```

The output is a row of filler characters, then the flag, then more filler.

## Flag

```
spooky{th3_4n5w3r_h45_4lw4y5_b33n_42}
```

The answer being 42 is a nice touch.

## Takeaway

A list of numbers in the printable ASCII range almost always wants `chr()`. After that, map the story onto operations: a number on the wall ("13") is usually an add or subtract, and "dyslexia / backwards" is a reversal.
