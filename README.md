# Studio ID Photo Tool

A single-page web app for making ID photo sheets. Drag a client photo into a slot, crop and adjust it, then download a print-ready sheet.

- **35 × 45 mm** photos, 8 per **6 × 4 in** sheet (landscape)
- **2 × 2 in** photos, 6 per **4 × 6 in** (4R) sheet
- Zoom, pan, rotate, flip, brightness, contrast, saturation and background fill
- On-screen guides (never printed): passport head-size bands for 35 × 45 mm (head 32–36 mm, crown 4–6 mm from top), or an oval and eye line
- Optional cut marks in the sheet margins
- Sessions can be saved to a file and loaded on another device

Everything runs in the browser. Photos are never uploaded anywhere.

The look follows the studio website: `studio.css` holds the shared palette, fonts (Playfair Display, DM Sans, Space Mono), nav, buttons, cards and footer, and `logo.webp` is a still of the website's logo. Change them once and all three pages update.

## Freebie photo templates

`freebie-templates.html` makes the 4 × 6 in freebie sheets with the Click Lounge Studio logo. Pick the client's package and it lists the free print-outs that package includes, as one sheet per print-out. Four sheet types:

- **Minis**: 4 photos, 2 × 2 frames, logo under each
- **Besties**: 2 landscape photos, stacked, logo above each
- **Solo**: 1 large portrait, logo below
- **Strips**: 2 vertical strips of 3 photos each (6 frames), logo under each strip. Counted in strips, so "2 strips" is one sheet

Packages and their print-outs come from the studio's packages page (captured 2026-10-07) and are listed at the top of the `CATEGORIES` block in the file. Counts are photos: a Minis sheet holds 4, a Besties sheet 2, a Solo sheet 1. To change a package, edit its line there.

Special layouts are separate from the packages and can be added to any sheet list:

- **Six frames**: 6 photos in a 2 × 3 grid, logo under the bottom row
- **Strip + 2**: a strip of 4 photos, one portrait and one sideways photo
- **Strip + 3**: a strip of 4 photos and three sideways photos

Sideways frames start with the photo turned 90° and carry a sideways logo, as on the studio's samples.

Frames have rounded corners and the sheet carries the same cut marks as the studio's sheets. Photos are repositioned, zoomed and rotated inside each frame, and always fill it. Each sheet downloads as a 1200 × 1800 px PNG tagged 300 dpi.

## Printing and sending to a phone

On the freebie page, **Print this sheet** and **Print all sheets** open the browser's print dialog with one 4 × 6 in page per sheet. On the ID photo page, **Print sheet** prints the sheet at its real size (6 × 4 in landscape for 35 × 45 mm, 4 × 6 in portrait for 2 × 2 in). Choose the matching paper and 100% scale.

**Send to phone (QR code)**, on both pages, shows a QR code. The client scans it and `receive.html` opens on their phone and receives the finished sheet (a 300 dpi JPEG) straight from the staff device. The sheet is not uploaded or stored anywhere. The staff page must stay open until it says Sent, and each code works once and expires after 10 minutes. It uses PeerJS (WebRTC) from cdnjs; the free public PeerJS service only introduces the two devices, and the file travels encrypted between them (through a relay if the networks block a direct link).

## Printing

Download the sheet (PNG, 300 dpi), open it, and print at 100% / Actual size on paper matching the sheet size. Turn off "Fit to page".

## Running it

There is no build step. Open `index.html` in a browser, or serve the folder with GitHub Pages.
