# Demented Memories

**Category:** Misc

## The challenge

A `.7z` archive containing a Git repository.

## Figuring it out

"Memories" plus a Git repo is a strong hint to dig through history, because Git keeps things you think you deleted. The flag came in three pieces:

1. The `README` supplied one fragment in plain sight.
2. An earlier commit held a deleted file, `retrospective.c`, which carried another fragment.
3. A hidden file, `.fog61.fog`, held the last fragment as hex.

## Solving it

1. Extract the `.7z`.
2. Walk the Git history (`git log`, checking old commits) and recover the deleted `retrospective.c`.
3. Read the fragment in the `README`.
4. Decode the hex in `.fog61.fog` to get the third fragment.
5. Join the three pieces in order.

## Flag

```
spooky{the_g00d_the_l0st_@nd_th3_void}
```

## Takeaway

A Git repo in a forensics/misc challenge means the history is in scope. Deleted files still live in old commits, and hidden dotfiles are easy to miss with a plain `ls`. The flag being split three ways (the good, the lost, the void) matched where each piece was hiding.
