# Xenoglossophobia

**Category:** Misc

## The challenge

A serial/UART log of numbered data packets.

## Figuring it out

The log was a stream of numbered packets, each with a header and a checksum, which is how XMODEM-style transfers look. So step one was to rebuild the original file: take the packets in order, strip each packet's header and checksum, and concatenate the payloads.

The reconstructed bytes were a JPEG, with extra text tacked on after the JPEG's end-of-image marker.

## Solving it

1. Parse the log and reassemble the packets into the raw file.
2. Notice the trailing text after the JPEG: a Latin word, `supermercado`.
3. That's the hint for the next layer. Run Steghide on the JPEG using `supermercado` as the passphrase.
4. Steghide returned the start of the flag plus a run of decimal numbers.
5. Decode those decimals as ASCII and append them to finish the flag.

## Flag

```
spooky{mu1tipl3_l@ngu@ges}
```

## Takeaway

Numbered packets with headers and checksums usually mean a framed transfer (XMODEM here), so rebuild the file before anything else. After that it stacked layers: data after a JPEG's end marker, a Steghide passphrase hidden in plain sight, then decimal-to-ASCII. The challenge name ("fear of foreign languages") fit the Latin clue and the multi-language flag.
