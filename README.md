# Studio ID Photo Tool

A single-page web app for making ID photo sheets. Drag a client photo into a slot, crop and adjust it, then download a print-ready sheet.

- **35 × 45 mm** photos, 8 per **153 × 102 mm** sheet (landscape)
- **2 × 2 in** photos, 6 per **102 × 153 mm** sheet
- **2 × 2 in and 1 × 1 in mix** on a full **102 × 153 mm** sheet: 4 big + 8 small. Thin cut lines between the photos can be switched off
- Zoom, pan, rotate, flip, brightness, contrast, saturation and background fill
- **Text on photo**: up to 3 lines per slot (name, ID number), with font, size, position, colour and an optional band behind the text. It scales with the photo, so it looks the same on 2 × 2 in and 1 × 1 in photos, and prints with the photo. "Apply this text to all slots" copies it; each slot can still be changed
- **Remove background** with an edge cleanup slider. The cutout then shows the chosen background fill (white, blue, red, grey or custom). The outline is recoloured from the subject's own colours, so a white or light studio backdrop does not leave a pale rim on a new colour. It runs in the browser with a portrait-matting model (MODNet, Apache-2.0, via Transformers.js), so photos are not uploaded. The first use downloads about 26 MB from huggingface.co and jsDelivr, and the browser keeps it afterwards
- On-screen guides (never printed): passport head-size bands for 35 × 45 mm (head 32–36 mm, crown 4–6 mm from top), or an oval and eye line
- Optional cut marks in the sheet margins
- Sessions can be saved to a file and loaded on another device, including cutouts. Photos used in several slots are stored once

Everything runs in the browser. Photos are never uploaded anywhere.

The look follows the studio website: `studio.css` holds the shared palette, fonts (Playfair Display, DM Sans, Space Mono), nav, buttons, cards and footer, and `logo.webp` is a still of the website's logo. Change them once and all three pages update.

## Freebie photo templates

`freebie-templates.html` makes the 102 × 153 mm freebie sheets with the Click Lounge Studio logo. Pick the client's package and it lists the free print-outs that package includes, as one sheet per print-out. Four sheet types:

- **Minis**: 4 photos, 2 × 2 frames, logo under each
- **Besties**: 2 landscape photos, stacked, logo above each
- **Solo**: 1 large portrait, logo below
- **Strips**: 2 vertical strips of 3 photos each (6 frames), logo under each strip. Counted in strips, so "2 strips" is one sheet

Packages and their print-outs come from the studio's packages page (captured 2026-10-07) and are listed at the top of the `CATEGORIES` block in the file. Counts are photos: a Minis sheet holds 4, a Besties sheet 2, a Solo sheet 1. To change a package, edit its line there.

**Extra sheets cost money.** Sheets that come with the package are free. A sheet added with the Add a sheet buttons costs ₱50, a special layout ₱70 and a large 8 × 24 in sheet ₱450. The page shows a reminder next to the buttons, and each time someone adds a sheet a box shows the price and asks "Add it?" first. Nothing is totalled. The prices are `PRICE_STD` and `PRICE_SPECIAL` in the file, and a template can set its own `price` (the large sheets).

**Client timer.** A countdown at the top of the page guides the client: 1–2 sheets get 5 minutes, 3–5 sheets get 10 minutes and 6–10 sheets get 15 minutes (more than 10 also get 15). Only Start and Reset: once started it cannot be paused and the time cannot be changed. **Resetting needs a 4-digit staff PIN.** The first time Start is pressed on a device, staff are asked to create the PIN (before handing the device to the client). The PIN is kept on that device only, as a salted hash, never in the page code. Three wrong tries lock the PIN for one minute, and "Change PIN" under the timer changes it. A started timer survives a page reload, so refreshing the page does not restart the clock. If browser data is cleared the PIN and timer are lost, and a new PIN is created at the next Start. When the timer panel scrolls out of view, a floating card at the bottom right keeps showing the time, so the client can always see it. It turns amber in the last minute and red at zero, and the timer beeps once at one minute and three times at zero. The rules are `TIMER_RULES` in the file.

**Remove this sheet** sits beside the sheet list, so any sheet can be removed without scrolling to the preview.

Special layouts are separate from the packages and can be added to any sheet list:

- **Six frames**: 6 photos in a 2 × 3 grid, logo under the bottom row
- **Strip + 2**: a strip of 4 photos, one portrait and one sideways photo
- **Strip + 3**: a strip of 4 photos and three sideways photos

**Large 8 × 24 in sheets** have their own row and cost ₱450 each:

- **8 × 24 · 3 frames**: three equal rounded frames stacked down the sheet, with the studio's stacked logo at the bottom
- **8 × 24 · full sheet**: one photo over the whole sheet, no logo

They are built from the studio's description (no sample), so the frame sizes are an estimate. They export at 250 dpi (2000 × 6000 px, because phones cannot make canvases much bigger) as a JPG tagged 250 dpi, which keeps the file small. Printing uses an 8 × 24 in page, and a single print job holds one paper size: "Print all sheets" prints the sheets that share the first sheet's size and says how many were left out.

Sideways frames start with the photo turned 90° and carry a sideways logo, as on the studio's samples.

Frames have rounded corners and the sheet carries the same cut marks as the studio's sheets. Photos are repositioned, zoomed and rotated inside each frame, and always fill it. Each sheet downloads as a 1205 × 1807 px PNG tagged 300 dpi.

## Printing and sending to a phone

On the freebie page, **Print this sheet** and **Print all sheets** open the browser's print dialog with one 102 × 153 mm page per sheet. On the ID photo page, **Print sheet** prints the sheet at its real size (153 × 102 mm landscape for 35 × 45 mm, 102 × 153 mm portrait for 2 × 2 in). Choose the matching paper and 100% scale.

**Send to phone (QR code)**, on both pages, shows a QR code. The client scans it and `receive.html` opens on their phone and receives the finished sheet (a 300 dpi JPEG) straight from the staff device. The sheet is not uploaded or stored anywhere. The staff page must stay open until it says Sent, and each code works once and expires after 10 minutes. It uses PeerJS (WebRTC) from cdnjs; the free public PeerJS service only introduces the two devices, and the file travels encrypted between them (through a relay if the networks block a direct link).

## Printing

Download the sheet (PNG, 300 dpi), open it, and print at 100% / Actual size on paper matching the sheet size. Turn off "Fit to page".

## Running it

There is no build step. Open `index.html` in a browser, or serve the folder with GitHub Pages.

## Paper size

All sheets are made for **102 × 153 mm** photo paper (1205 × 1807 px at 300 dpi). Photo sizes stay exact: 2 × 2 in is 600 px, 35 × 45 mm is 413 × 531 px.
