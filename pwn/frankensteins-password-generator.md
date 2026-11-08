# Frankenstein's Password Generator

**Category:** Binary / reversing (binrev)

## The challenge

> Dr. Frankenstein left behind a strange password generator in an abandoned NJIT laboratory. The machine refuses to start without an activation phrase. His last notebook entry reads, "A bolt at midnight gave it life." Can you figure out what the program expects and wake the creature?

A binary that won't run until you give it the right activation phrase.

## Figuring it out

The binary checks a **14-character** activation phrase, one character at a time, against a table of stored bytes. Each character is transformed before the comparison, so I pulled the per-character rule out of the disassembly:

```
((char ^ 0x5d) + 7*i + 0x0b) mod 256
```

where `i` is the character's index. Since I had the stored target bytes and the exact transform, I inverted it per position to recover the input that produces them.

That gave the phrase `BOLTATMIDNIGHT`, which matches the notebook hint ("a bolt at midnight").

## Solving it

1. Recover the 14 target bytes and the per-character formula from the binary.
2. Invert the formula at each index to get the activation phrase `BOLTATMIDNIGHT`.
3. Feed it back in. The program uses the phrase to decode its 29-byte secret, which prints the flag.

## Flag

```
spooky{its_alive_at_midnight}
```

## Takeaway

When a binary validates input character by character with a reversible formula, you don't brute force it, you invert the formula. Having the stored target bytes plus the transform means you can solve straight for each input character.
