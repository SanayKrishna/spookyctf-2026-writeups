# SpookyCTF 2026 writeups

My writeups for [SpookyCTF 2026](https://ctftime.org/ctf/987), a beginner-friendly jeopardy CTF run by NJIT's Cyber Security Network over the Halloween weekend.

This was my first CTF. I went in as a two-person team but ended up playing solo for the weekend, and finished with 21 flags across 6 categories (3181 points, 146th place) as team `404BrainNotFound`.

I've written up the ones I think teach something reusable. More going up as I work through the rest.

## Writeups

### Crypto
- [Heads will Roll](crypto/heads-will-roll.md) rail fence cipher
- [Numerophobia](crypto/numerophobia.md) ASCII with an alternating shift, then reversed
- [I Feel Like Someone's Watching Me](crypto/i-feel-like-someones-watching-me.md) monoalphabetic substitution

### Binary / reversing
- [Cyberphobia: Overflowed Bits](pwn/cyberphobia-overflowed-bits.md) buffer overflow into a function pointer
- [Too Much Love is Scary](pwn/too-much-love-is-scary.md) out-of-bounds write

### Forensics
- [The Haunted Portrait](forensics/the-haunted-portrait.md) LSB bit-plane steg, then ROT13
- [Arachnophobia](forensics/arachnophobia.md) a ZIP hidden after the PNG's end marker
- [Tormented Tanny](forensics/tormented-tanny.md) flag split across image metadata fields

### OSINT
- [Nosocomephobia](osint/nosocomephobia.md) Morse from audio, reverse image search, then archive digging

## Notes

Flag format was `spooky{...}`. Everything here is written from my own notes after the event. If I got a detail wrong, open an issue.
