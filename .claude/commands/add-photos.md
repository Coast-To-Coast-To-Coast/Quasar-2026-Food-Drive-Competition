---
description: Add holiday sweater photos to the photo book. Give the photos plus each person's first name and office.
argument-hint: (photo files, first names and offices)
---

# Add sweater photos

Nate gives one or more sweater photos, each with a first name and an office. Follow these steps in order. Use plain language and never use em dashes.

## 1. Get the latest version

Run `git pull --ff-only` in this repo first. If it fails, stop and explain.

## 2. Check what you have

For each photo you need:
- **The image file on disk.** If Nate pasted an image but there's no file path to work from, ask him for the file (he can drag the file into the chat to paste its path).
- **A first name only.** Never add surnames.
- **An office:** Vancouver, Timmins, North Bay, Woodbridge, Toronto or Ottawa.

Ask for anything missing. Only add photos people sent through the sweater photo form (they asked to be shared). If a photo shows other people, a computer screen, an ID badge or anything else private, flag it to Nate before adding it.

## 3. Resize and clean each photo

Save each photo into the `photos` folder as a JPG, about 1000px wide and under 300 KB, with phone rotation fixed and hidden data (like GPS location) removed. Write this script to the scratchpad (never into the repo) and run it once per photo with `python -I <script> <original> photos/<new-name>.jpg`:

```python
import sys, pathlib
from PIL import Image, ImageOps
src, dst = pathlib.Path(sys.argv[1]), pathlib.Path(sys.argv[2])
im = ImageOps.exif_transpose(Image.open(src)).convert("RGB")
im.thumbnail((1000, 1250))
for q in (82, 76, 70, 64, 58):
    im.save(dst, "JPEG", quality=q, optimize=True, progressive=True)
    if dst.stat().st_size <= 300_000:
        break
print(dst.name, im.size, dst.stat().st_size // 1000, "KB")
```

Saving without the original metadata is what strips the location data, so don't add an `exif=` argument. If a photo is HEIC (iPhone) and won't open, ask Nate to export it as a JPG.

File names: lowercase first name and office with hyphens and no spaces, for example `jordan-ottawa.jpg`. If that name is taken, add a number: `jordan-ottawa-2.jpg`.

## 4. Add the lines to the photo block

In index.html, in the block marked "SWEATER PHOTOS: ADD ONE LINE PER PHOTO", add one line per photo inside the brackets, in the same format as the example:

```
  { file: "jordan-ottawa.jpg", name: "Jordan", office: "Ottawa" },
```

## 5. Preview and confirm

Open the page in the preview, scroll to the photo book, click a photo to check the larger view opens and closes, and show Nate a screenshot. Wait for his OK before committing.

## 6. Commit and push

- Run `git status`. Only index.html and the new files in `photos/` should be changed. Never commit the original photos, screenshots or anything outside `photos/`. If something unexpected shows up, stop and ask.
- Commit with a message like "Add 3 sweater photos" and push to main. If the push needs a GitHub sign-in that can't appear here, ask Nate to run `git push origin main` in a terminal opened in this folder.
- Remind Nate the site updates in about a minute, and to hard refresh with Ctrl + F5.
