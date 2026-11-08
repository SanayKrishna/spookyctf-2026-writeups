# Nosocomephobia

**Category:** OSINT

## The challenge

> There is this bottle I found washed on the shore yesterday.. Within it contained a cassette which sounded like simple beeping? [...] In addition, there was this picture within the bottle as well [...] Can you please give the recording a listen and find when and from where the recording is from?

Flag format: `spooky{(Location Name).(Year of Recording)}`. We got an MP3 and an old black-and-white photo.

## Figuring it out

Two artifacts, so two leads. The name was the first clue: nosocomephobia is the fear of hospitals, which turned out to frame the whole thing.

**The audio.** "Simple beeping" is Morse code. I ran the MP3 through an online Morse audio decoder. It came out noisy but readable: a first-person message from someone who doesn't know where they are, surrounded by "patients", "doctors", shocks, screaming, and weekly screenings of an educational film. That's an old psychiatric hospital, an asylum.

**The photo.** A ruined castle on a hill above a town. I reverse-image-searched it (Google Lens) and it came back as **Denbigh, Wales**, with Denbigh Castle on the hill.

## Solving it

Putting the two together: searching "Denbigh asylum" lands on the **North Wales Hospital** (historically the Denbigh Asylum / North Wales Counties Lunatic Asylum).

For the year, the recording mentioned weekly recreational events including an educational film. Wikipedia didn't have that detail, so I searched more specifically and found an article from Denbighshire Archives, "Entertaining Patients in the North Wales Hospital," which includes an image of a **weekly activities bulletin dated 1966**. That matched the recording's "weekly events" far better than the photo's own date (the postcard is from the 1880s, which is a deliberate red herring, the photo's age is not the recording's age).

## Flag

```
spooky{north_wales_hospital.1966}
```

## Takeaway

Beeping audio is almost always Morse. An old photo means reverse image search to get the place, then let the story details become your search terms. One thing that cost me time: Google's AI summary skipped right over the image that held the year, so for this kind of thing you have to open the original source instead of trusting the summary.
