# Studio ID Photo Tool

A single-page web app for making ID photo sheets. Drag a client photo into a slot, crop and adjust it, then download a print-ready sheet.

- **35 × 45 mm** photos, 8 per **6 × 4 in** sheet (landscape)
- **2 × 2 in** photos, 6 per **4 × 6 in** (4R) sheet
- Zoom, pan, rotate, flip, brightness, contrast, saturation and background fill
- On-screen guides (never printed): passport head-size bands for 35 × 45 mm (head 32–36 mm, crown 4–6 mm from top), or an oval and eye line
- Optional cut marks in the sheet margins
- Sessions can be saved to a file and loaded on another device

Everything runs in the browser. Photos are never uploaded anywhere.

## Freebie photo templates

`freebie-templates.html` makes the 4 × 6 in freebie sheets with the Click Lounge Studio logo. Pick the client's package and it lists the free print-outs that package includes, as one sheet per print-out. Three sheet types:

- **Minis**: 4 photos, 2 × 2 frames, logo under each
- **Besties**: 2 landscape photos, stacked, logo above each
- **Solo**: 1 large portrait, logo below

Packages and their print-outs come from the studio's packages page (captured 2026-10-07) and are listed at the top of the `CATEGORIES` block in the file. Counts are photos: a Minis sheet holds 4, a Besties sheet 2, a Solo sheet 1. To change a package, edit its line there.

Special layouts are separate from the packages and can be added to any sheet list:

- **Six frames**: 6 photos in a 2 × 3 grid, logo under the bottom row
- **Strip + 2**: a strip of 4 photos, one portrait and one sideways photo
- **Strip + 3**: a strip of 4 photos and three sideways photos

Sideways frames start with the photo turned 90° and carry a sideways logo, as on the studio's samples.

Frames have rounded corners and the sheet carries the same cut marks as the studio's sheets. Photos are repositioned, zoomed and rotated inside each frame, and always fill it. Each sheet downloads as a 1200 × 1800 px PNG tagged 300 dpi.

## Printing

Download the sheet (PNG, 300 dpi), open it, and print at 100% / Actual size on paper matching the sheet size. Turn off "Fit to page".

## Running it

There is no build step. Open `index.html` in a browser, or serve the folder with GitHub Pages.
