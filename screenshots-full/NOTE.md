# Full-resolution screenshots go here

The three files here were downscaled to 820x1778 by mistake on 31 Aug 2026 —
they are the web-sized copies, not usable for App Store Connect.

Re-export from the simulator and drop the originals in this folder, then run
the resize step to regenerate the web copies in ../images/.

**Export at 1290 x 2796** (iPhone 16 Pro Max / 6.9"). App Store Connect wants
the 6.9" size and scales everything else down from it; the 1179 x 2556 from a
6.1" device is not one of the accepted upload sizes anyway.

Resize for the website:

```
cd images
python3 -c "
from PIL import Image
for n in (1,2,3,4):
    im = Image.open(f'../screenshots-full/img_skyline_ios_eng_{n}.png').convert('RGB')
    im.thumbnail((820, 3000), Image.LANCZOS)
    im.save(f'img_skyline_ios_eng_{n}.png', 'PNG', optimize=True)
"
```

Watch the extension case: macOS is case-insensitive so `.PNG` and `.png` are the
same file locally, but Netlify serves from a case-sensitive filesystem — a page
referencing `.png` will 404 on a file saved as `.PNG`. Keep everything lowercase.
