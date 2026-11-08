# Cyberphobia: Overflowed Bits

**Category:** Binary exploitation (pwn)

> This was my first binary exploitation challenge, so the writeup is deliberately step-by-step.

## The challenge

> I can't trust computers anymore. I trusted the input, it overflowed.

We got the source (`main.c`) and the compiled binary, plus a remote service to connect to with `nc`.

## The bug

The interesting function:

```c
void vuln() {
    struct {
        char buf[64];
        void (*direction)();
    } s;

    s.direction = center_of_corn_maze;   // the "try again" function
    printf("New sign direction: ");
    read(0, s.buf, 128);                 // reads 128 bytes into a 64-byte buffer
    s.direction();
}
```

`buf` is 64 bytes, and right after it in the struct sits a function pointer, `direction`, which starts out pointing at `center_of_corn_maze` (a dead end). But `read` is allowed to pull in **128** bytes. So I can write past the end of `buf` and straight over `direction`.

There's a function I actually want to reach, `corn_maze_exit`, which reads and prints the secret.

## The plan

1. Fill all 64 bytes of `buf`.
2. The bytes after that land on `direction`, so overwrite it with the address of `corn_maze_exit`.
3. When `s.direction()` runs, it jumps to my address and prints the flag.

## Solving it

Grab the target address from the binary:

```bash
nm main | grep corn_maze_exit
```

The binary is 64-bit, so the address is 8 bytes and goes in little-endian order. Then it's 64 bytes of padding followed by that address, sent to the service.

## Flag

Solved during the event. I didn't save the exact flag string, so it's not reproduced here. The technique above is the point.

## Takeaway

When a program reads more bytes than the buffer can hold, that's your overflow. If there's a function pointer sitting right after the buffer, you don't need anything fancy, just run the buffer over into the pointer and replace it with the address of whatever function prints the flag.
