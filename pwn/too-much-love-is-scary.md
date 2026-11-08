# Too Much Love is Scary

**Category:** Binary exploitation (pwn)

## The challenge

> Last time I loved I was left broken and in shambles. That's when I realized that my heart could only hold so much, I must protect it. So I won't fall in love again, it's just too scary…

A 64-bit ELF binary with a remote service.

## Figuring it out

Running `strings` and `nm` on the binary showed a `print_flag` function that never gets called in the normal flow, plus a couple of prompts:

- "Enter where the heart breaks (Enter `<start end>`):" which reads two integers with `%d %d`.
- "Now based on our difference speak about a certain famous summer day. Make sure that it is aimed at the right spot in the heart:"

So the program takes two numbers, works out a difference, and then writes a value "at the right spot." That's an out-of-bounds write: I control an index and a value, and I can point that write somewhere it shouldn't go to hijack execution into `print_flag`.

The flavour text carries the clues. "A certain famous summer day" is Shakespeare's Sonnet 18 ("Shall I compare thee to a summer's day?"), and "the walls of Troy / where the heart breaks" describe the bounds I'm escaping.

## Solving it

I opened `main` in Ghidra to see exactly how the two integers get used: how the difference becomes an index, what array it indexes, and where the value lands. Once that was clear, I picked the index that walks the write out of bounds and onto the saved target, and set the value so execution ends up in `print_flag`.

## Flag

```
spooky{REPLACE_WITH_YOUR_FLAG}
```

## Takeaway

If a program lets you choose an index and a value and then writes with them, check whether the index is bounded. An attacker-controlled out-of-bounds write aimed at a return address or function pointer gets you to the win function. Decompiling `main` is worth the five minutes, because guessing the offsets blind rarely works.
