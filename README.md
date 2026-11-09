# SpookyCTF 2026 writeups

My writeups for [SpookyCTF 2026](https://ctftime.org/ctf/987), a beginner-friendly jeopardy CTF run by NJIT's Cyber Security Network over the Halloween weekend.

This was my first CTF at any real scale. I played as a two-person team with Aniruddha under the name `404BrainNotFound` (the team is now `ornithorhynchus.sh`).

| Result | |
|---|---|
| Placement | 156th of 780 teams (top 20%) |
| Points | 2,779 |
| Flags | 21, across all 6 categories |

| Category | Solved |
|---|---|
| Crypto | 7 |
| Pwn / reversing | 6 |
| Forensics | 3 |
| Web | 2 |
| Misc | 2 |
| OSINT | 1 |

Below is every challenge I solved. Linked entries have a full writeup; the rest are still being written up.

## Crypto

- [Heads will Roll](crypto/heads-will-roll.md): rail fence cipher
- [Numerophobia](crypto/numerophobia.md): ASCII with an alternating shift, then reversed
- [I Feel Like Someone's Watching Me](crypto/i-feel-like-someones-watching-me.md): monoalphabetic substitution
- [Cyberphobia: SpOoKy KeYsTrEaMs](crypto/cyberphobia-spooky-keystreams.md): AES-CTR keystream reuse
- [No Nonsense on this Server](crypto/no-nonsense-on-this-server.md): ECDSA nonce reuse leaks the private key
- [Klediophobia](crypto/klediophobia.md): brute-forceable private scalar, then forging signatures
- There is no good name for the fear of math *(writeup coming)*

## Forensics

- [The Haunted Portrait](forensics/the-haunted-portrait.md): LSB bit-plane steg, then ROT13
- [Arachnophobia](forensics/arachnophobia.md): a ZIP hidden after the PNG's end marker
- [Tormented Tanny](forensics/tormented-tanny.md): flag split across image metadata fields

## Pwn / reversing

- [Cyberphobia: Overflowed Bits](pwn/cyberphobia-overflowed-bits.md): buffer overflow into a function pointer
- [Too Much Love is Scary](pwn/too-much-love-is-scary.md): out-of-bounds write into a win function
- [Frankenstein's Password Generator](pwn/frankensteins-password-generator.md): inverting a per-character check
- [Cyberphobia: Formatting Nightmare](pwn/cyberphobia-formatting-nightmare.md): format-string read off the stack
- [Elves can be Spooky Too](pwn/elves-can-be-spooky-too.md): ELF quine with overlapping headers
- Trypophobia *(writeup coming)*

## Web

- J*b Application: prompt injection against an "AI" screener *(writeup coming)*
- Hemophobia *(writeup coming)*

## Misc

- [Xenoglossophobia](misc/xenoglossophobia.md): XMODEM reassembly, then layered steg
- [Demented Memories](misc/demented-memories.md): flag pieces hidden in Git history and dotfiles

## OSINT

- [Nosocomephobia](osint/nosocomephobia.md): Morse from audio, reverse image search, then archive digging

## Tools I leaned on

Ghidra, CyberChef, steghide, binwalk, exiftool, quipqiup, `strings`, and Python for the glue.

## Notes

Flag format was `spooky{...}`. Everything here is written from my own notes after the event. If I got a detail wrong, open an issue.
