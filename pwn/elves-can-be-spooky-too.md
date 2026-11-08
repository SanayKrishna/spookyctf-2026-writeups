# Elves can be Spooky Too

**Category:** Binary / reversing (binrev)

## The challenge

Write an ELF64 quine: a program whose output is its own exact bytes. The checker only accepted an exact match.

## Figuring it out

The name is the hint doubled up: "Elves" = ELF files, and a quine is a program that prints its own source (here, its own binary). The trick to making it tiny is to overlap the ELF header and the program header so the executable can map its own bytes, then just write those bytes to stdout.

## Solving it

I built a **112-byte ELF64** where the ELF header also doubles as the program header (`phdr` living inside `ehdr`). That overlap lets the file map itself into memory, so the program can:

1. Write its own mapped bytes to stdout.
2. Exit cleanly with status 0.

I iterated on it locally until the checker reported `PASS exact quine`.

## Flag

```
spooky{phdr_in_ehdr_c2d021cc4fc5}
```

## Takeaway

ELF quines get small when you overlap the ELF header and program header so the binary can reference its own bytes. The flag basically spells out the technique: `phdr_in_ehdr`.
