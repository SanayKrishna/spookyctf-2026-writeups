# Cyberphobia: Formatting Nightmare

**Category:** Binary / reversing (binrev)

## The challenge

C source plus a remote service. The name gives away the bug class.

## The bug

The vulnerable line is a format string being controlled by the user:

```c
printf(input, secret);
```

Here `input` is my input and it's passed as the *format string* instead of as an argument. `secret` is the first variadic argument. When the format string is attacker-controlled, I get to decide what `printf` reads and prints.

## Solving it

Since `secret` is the first argument after the format string, I just ask `printf` to print it as a string:

```
%1$s
```

The service printed the secret back: `f0rm4tStr1ngVulN3r4b1lityIsSc4rY`. The challenge says to wrap the answer in `spooky{}`.

## Flag

```
spooky{f0rm4tStr1ngVulN3r4b1lityIsSc4rY}
```

## Takeaway

`printf(user_input, ...)` is a format-string vulnerability: user input should never be the format string. `%1$s` reads the first argument directly; without the positional form, `%s`/`%p` walk the stack until you find the value you want.
