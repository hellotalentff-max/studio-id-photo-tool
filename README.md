# Studio ID Photo Tool

A single-page web app for making ID photo sheets. Drag a client photo into a slot, crop and adjust it, then download a print-ready sheet.

- **35 × 45 mm** photos, 8 per **153 × 102 mm** sheet (landscape)
- **2 × 2 in** photos, 4 per **4 × 6 in** (101.6 × 152.4 mm) sheet: exactly 2.000 in (600 px) each, edge to edge at the top of the sheet; the bottom 2 in is left blank
- **2 × 2 in and 1 × 1 in mix** on a full **4 × 6 in** sheet: 4 big (2.000 in) + 4 small (1.000 in), no margin; the bottom inch of the sheet is left blank. Thin cut lines between the photos can be switched off
- Zoom, pan, rotate, flip, brightness, contrast, saturation and background fill
- **Text on photo**: up to 3 lines per slot (name, ID number), with font, size, position, colour and an optional band behind the text. It scales with the photo, so it looks the same on 2 × 2 in and 1 × 1 in photos, and prints with the photo. "Apply this text to all slots" copies it; each slot can still be changed
- **Remove background** with an edge cleanup slider. The cutout then shows the chosen background fill (white, blue, red, grey or custom). The outline is recoloured from the subject's own colours, so a white or light studio backdrop does not leave a pale rim on a new colour. It runs in the browser with a portrait-matting model (MODNet, Apache-2.0, via Transformers.js), so photos are not uploaded. The first use downloads about 26 MB from huggingface.co and jsDelivr, and the browser keeps it afterwards
- On-screen guides (never printed): passport head-size bands for 35 × 45 mm (head 32–36 mm, crown 4–6 mm from top), or an oval and eye line
- Optional cut marks: in the sheet margins for 35 × 45 mm, and for the 2 × 2 in sheet small ticks on the edges (top and bottom for the vertical cut, sides for the horizontal cuts), because that sheet has no margin and the white backgrounds hide where one photo ends
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

**Extra sheets cost money.** Sheets that come with the package are free. A sheet added with the Add a sheet buttons costs ₱50, a special layout ₱70 (the 8 × 10 in layout ₱200) and a large 8 × 24 in sheet ₱450. The page shows a reminder next to the buttons, and each time someone adds a sheet a box shows the price and asks "Add it?" first. Nothing is totalled. The prices are `PRICE_STD` and `PRICE_SPECIAL` in the file, and a template can set its own `price` (the large sheets).

**Client timer.** A countdown at the top of the page guides the client: 1–2 sheets get 5 minutes, 3–5 sheets get 10 minutes and 6–10 sheets get 15 minutes (more than 10 also get 15). Only Start and Reset: once started it cannot be paused and the time cannot be changed. **Resetting needs a 4-digit staff PIN.** The first time Start is pressed on a device, staff are asked to create the PIN (before handing the device to the client). The PIN is kept on that device only, as a salted hash, never in the page code. Three wrong tries lock the PIN for one minute, and "Change PIN" under the timer changes it. A started timer survives a page reload, so refreshing the page does not restart the clock. If browser data is cleared the PIN and timer are lost, and a new PIN is created at the next Start. When the timer panel scrolls out of view, a floating card at the bottom right keeps showing the time, so the client can always see it. It turns amber in the last minute and red at zero, and the timer beeps once at one minute and three times at zero. The rules are `TIMER_RULES` in the file.

**Client's photos.** The client can first choose all their photos in the Client's photos panel (several at once, or dropped in). They wait there, shown as small pictures marked new or placed, until they are put into frames: tap a photo to place it in the selected frame (the next empty frame is then selected), drag it onto a frame on the sheet, or press Fill empty frames to place the photos not used yet, in order. A photo can be used on several sheets, and the × on a picture removes it from the list only. The photos are held in the page's memory, never uploaded, and reloading the page clears them.

**Remove this sheet** sits beside the sheet list, so any sheet can be removed without scrolling to the preview.

Special layouts are separate from the packages and can be added to any sheet list:

- **Six frames**: 6 photos in a 2 × 3 grid, logo under the bottom row
- **Strip + 2**: a strip of 4 photos, one portrait and one sideways photo
- **Strip + 3**: a strip of 4 photos and three sideways photos
- **8 × 10 in**: one photo over the whole 8 × 10 in sheet, edge to edge, with a small light logo (`logo-white.png`, transparent background) in the bottom right corner, 10 mm tall and 10 mm from the right and bottom edges. The logo is near-white, so it reads best on mid to dark photos. For light photos, tick **Dark logo (for light photos)** under the sheet preview (shown on this sheet only, set per sheet) to switch to the same logo in the studio's dark green-black (`logo-dark.png`). Built from a description, not a sample, so the sizes are an estimate. It exports at 300 dpi (2400 × 3000 px) as a JPG tagged 300 dpi and prints on an 8 × 10 in page. Costs ₱200 per sheet (`price` on `photo8x10`), not the ₱70 of the other special layouts

**Large 8 × 24 in sheets** have their own row and cost ₱450 each:

- **8 × 24 · 3 frames**: three equal rounded frames stacked down the sheet, with the studio's stacked logo at the bottom
- **8 × 24 · full sheet**: one photo over the sheet, edge to edge, with the same bottom space as the 3-frame sheet for the studio's stacked logo

They are built from the studio's description (no sample), so the frame sizes are an estimate. They export at 250 dpi (2000 × 6000 px, because phones cannot make canvases much bigger) as a JPG tagged 250 dpi, which keeps the file small. Printing uses an 8 × 24 in page, and a single print job holds one paper size: "Print all sheets" prints the sheets that share the first sheet's size and says how many were left out.

Sideways frames start with the photo turned 90° and carry a sideways logo, as on the studio's samples.

Frames have rounded corners and the sheet carries the same cut marks as the studio's sheets. Photos are repositioned, zoomed and rotated inside each frame, and always fill it. Each sheet downloads as a 1205 × 1807 px PNG tagged 300 dpi.

## Photo booth

`photobooth.html` turns an iPad, tablet or laptop with a camera into a self-service photo booth, in the spirit of apps like Lumabooth. It runs full screen as a kiosk:

1. **Start screen**: the studio logo and event name over the live camera. Guests tap anywhere.
2. **Pick your photo**: Photo strips (3 photos, two identical 2 × 6 in strips on one 4 × 6 in print), Four-up (4 photos), Big photo (1 photo), Animated GIF (4 photos that flip) or Boomerang (a 1.5 second back-and-forth clip). If only one layout is switched on, this step is skipped.
3. **Get ready**: the camera preview is cut to the shape of the photo, so what guests see is what prints. They can pick a filter (Natural, Black & white, Warm, Vintage) and press Start.
4. **Countdown and shots** with big numbers, beeps, a white flash and a shutter sound. Each shot is shown for a moment.
5. **Review**: the finished print (4 × 6 in, 300 dpi JPEG) or GIF, with Retake, Print, Send to my phone (the same QR code transfer as the other pages) and Done. It goes back to the start screen by itself after the chosen time.

Every print shows the studio logo, plus the event name and date if set, in one of four sheet colours (cream, white, studio green, black). For event artwork, staff can upload a **custom overlay** per print layout: a 1200 × 1800 px PNG drawn on top of the sheet, with see-through holes where the photos go.

**AI background removal** (no green screen needed). In the settings, Background replacement → How → AI. MediaPipe's selfie segmenter (Apache-2.0, from jsDelivr and Google's model storage, about 10 MB the first time) finds the people in each camera frame on the device, nothing is uploaded, and the background is replaced live, the same way as the green screen below. "Cut closer to people" and "Edge softness" tune the edge. It works best with 1 to 4 people, waist up, within about 2 m, in good light; hair and props can be soft or cut off, so a green screen still gives the cleanest edges.

**Green screen.** Switch on "Replace the background behind guests" and choose Green screen, and the green behind guests is swapped for a background live on screen, so guests see the result before the countdown. It works on prints, GIFs and boomerangs. Guests pick the background on the get-ready screen (or staff fix one). Four backgrounds are built in (Studio green, Cream studio, Golden hour, Party lights), and staff can add their own JPG or PNG pictures (landscape 4 : 3, at least 1600 × 1200 px fits best); they are kept on the booth device. The settings show a live preview with:
- **Backdrop colour**, with "Read it from the camera" (step out of the picture first; it reads the top corners)
- **How much green to remove**, **Edge softness** and **Green glow cleanup** (removes green light reflected on hair and edges)

The keying runs on the device's graphics chip (WebGL), after the method of OBS Studio's chroma key filter, so it stays smooth on an iPad. The backdrop colour is matched by hue, so a real, slightly dull green behaves like pure green. Background pictures are never shown mirrored, so text on them reads correctly on screen and on the print. For a clean result, light the backdrop evenly with no shadows or wrinkles, keep guests about 1 m in front of it, and ask them not to wear green.

**Staff settings** open from the small gear on the start screen and need a 4-digit staff PIN (created the first time, kept on the device as a salted hash, 3 wrong tries lock it for a minute; the same scheme as the freebie timer, but its own PIN). Settings: event name and date, sheet colour, which layouts guests can pick, overlays, camera, countdown lengths, mirroring, filters, retake, Print and Send to phone buttons, print automatically, and the return-to-start time. Settings stay on that device.

**Photos taken on this device**: every result is kept in the browser's storage (IndexedDB) on the booth device, so staff can save, print, re-send or delete them, or Download all after the event. They stay until deleted or the browser data is cleared.

Notes:
- The camera only works over https (GitHub Pages) or on localhost. Allow camera access when the browser asks.
- On iPad, use Share → Add to Home Screen and open the booth from the home screen icon for a full-screen app, and turn on Guided Access (Settings → Accessibility) so guests cannot leave it. On a laptop, use Full screen in the settings.
- Printing opens the browser's print box on a 4 × 6 in page. For one-tap printing on a laptop, start Chrome with `--kiosk-printing` and set the photo printer as the default printer.
- GIFs are made in the browser with gifenc (MIT) from jsDelivr, loaded once when a GIF layout is switched on, so the booth needs internet the first time.
- Nothing is uploaded. Send to my phone goes straight from the booth to the guest's phone over WebRTC.

## Video editor

`video-editor.html` (ClickCut) is a CapCut-style video editor that runs in the browser. Import videos, photos and music, arrange them on a timeline (a magnetic main track plus overlay, text and audio layers), then trim, split, reorder and export.

- Canvas sizes 9:16 (TikTok/Reels), 16:9, 1:1, 4:5 and 3:4; black, white or blurred background
- Per clip: volume (up to 200%), speed (0.25x to 4x), fade in/out, scale, position, rotation, opacity, 12 filters and brightness/contrast/saturation
- Text styles and emoji stickers with fade, pop, slide and typewriter animations; drag and resize them in the preview
- Undo/redo and keyboard shortcuts (listed in the right panel when nothing is selected)
- **✨ Auto → Beat highlights**: pick a song and the clips to use, and it builds the edit for you. It finds the song's beat (BPM), scores every half second of each clip on motion, sharpness, colour, exposure and the clip's own loudness (cheers, laughs), skips dark, blurry and dull parts, and cuts the best moments exactly on the beat, starting on the first bar where the music begins. Length 15 s, 30 s, 60 s or the whole song; pace Fast (every beat), Medium (about every second), Slow (every bar) or Auto (faster cuts when the music gets louder). Options: keep clips in time order, start with the best moment, fill the frame, a zoom punch on each cut, and mute the clips' own sound. If there is not enough good footage the video comes out shorter rather than using weak shots. It replaces the timeline, and Undo brings the old one back
- Songs on the timeline show their beats as yellow dots (bigger on the first beat of each bar), and clips snap to them when dragged or trimmed
- Export at 720p or 1080p with sound: MP4 in Chrome, WebM where MP4 recording is not available. Export plays the video once in real time, so keep the tab open and in front

Use Chrome or Edge (Safari does not apply the filters and may not export). Projects are not saved, and media never leaves the device.

## Printing and sending to a phone

On the freebie page, **Print this sheet** and **Print all sheets** open the browser's print dialog with one 102 × 153 mm page per sheet. On the ID photo page, **Print sheet** prints the sheet at its real size (153 × 102 mm landscape for 35 × 45 mm, 101.6 × 152.4 mm (4 × 6 in) portrait for 2 × 2 in). Choose the matching paper and 100% scale.

**Send to phone (QR code)**, on both pages, shows a QR code. The client scans it and `receive.html` opens on their phone and receives the finished sheet (a 300 dpi JPEG) straight from the staff device. The sheet is not uploaded or stored anywhere. The staff page must stay open until it says Sent, and each code works once and expires after 10 minutes. It uses PeerJS (WebRTC) from cdnjs; the free public PeerJS service only introduces the two devices, and the file travels encrypted between them (through a relay if the networks block a direct link).

## Printing

Download the sheet (PNG, 300 dpi), open it, and print at 100% / Actual size on paper matching the sheet size. Turn off "Fit to page".

## Running it

There is no build step. Open `index.html` in a browser, or serve the folder with GitHub Pages.

## Paper size

The freebie sheets and the 35 × 45 mm sheet are made for **102 × 153 mm** photo paper (1205 × 1807 px at 300 dpi). 35 × 45 mm photos are 413 × 531 px. The 2 × 2 in and mixed ID sheets are made for 4 × 6 in paper (1200 × 1800 px at 300 dpi) so the photos are exactly 2 in and 1 in.
