# Arachnophobia

**Category:** Forensics

## The challenge

> Something about the SpookyCTF logo feels off… like something's tangled in the webs.

The file was `tangled.png`, the event's spider logo.

## Figuring it out

Plaintext search and the image metadata gave me nothing. "Tangled in the webs" sounded like something was mixed into the file rather than shown in the picture, so I looked at the raw bytes, specifically the end of the file.

A PNG is supposed to stop at its `IEND` chunk. I dumped the tail:

```powershell
Format-Hex .\tangled.png | Select-Object -Last 30
```

Right after `IEND®B'`, there were more bytes: `PK`, followed by `flag.txt`. `PK` is the magic number for a ZIP archive, so someone had glued a ZIP onto the back of the PNG. Image viewers read up to `IEND` and ignore the rest, so the logo still displays normally while hiding a whole file.

## Solving it

Python's `zipfile` can find the archive even with the image bytes in front of it:

```python
import zipfile
print(zipfile.ZipFile('tangled.png').read('flag.txt').decode())
```

(7-Zip's "Open archive" does the same thing if you'd rather click.)

## Flag

```
spooky{8_l3gs_4nd_4_z1p}
```

## Takeaway

Bytes after a PNG's `IEND` marker are a classic place to hide an appended file. `PK` means ZIP, so open the image as an archive. On Linux, `binwalk -e tangled.png` would have pulled it out in one command, which is a good reason to keep a Linux box or WSL around.
