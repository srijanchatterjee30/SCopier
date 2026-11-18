# SCopier

A local clipboard workspace for keeping text in cards, combining selections, and copying the result in the format you need.

Made by Srijan Chatterjee. ©2026 All rights reserved.

Documentation updated **17 November 2026**, covering Version 2 and the changes made after `20261015-stable109`.

## Getting started

Open `index.html` or `SCopier.html` in your browser. The standalone app includes its scripts, styles and offline place-name data; it needs no installation or API key. Keep `help.html` and `version1.html` beside it to use the separate guide and older version.

In the source checkout, run a local server with:

```sh
python3 -m http.server 4173 --bind 127.0.0.1 --directory work/scopier/dist
```

Then open `http://127.0.0.1:4173`.

Cards and preferences are saved in browser storage when available. Storage belongs to the browser and origin: moving between a local file, localhost and a hosted site may show a different workspace. Export a backup before moving your data or clearing browser storage.

Browser permissions can restrict clipboard access, especially for local files. SCopier provides a manual-copy fallback.

## Cards and copying

- Create, rename, edit, duplicate and rearrange cards.
- Copy from a card or its numbered button in the bottom quick-copy dock.
- Search titles and text in Cards, History or Trash.
- Reuse copied text and earlier edits from History.
- Restore cards from Trash, or confirm their permanent removal.

The workspace allows up to 1,000 cards, including Trash, and up to two empty cards at a time. Filling the last empty card creates a spare.

Turn on **Advanced copy** from the workspace menu to combine these tools:

- **Numbers:** extract numeric values from the current source.
- **Select text:** collect chosen words or characters across cards.
- **Join:** copy selected cards together.
- **Select:** enter card-selection mode, then select individual cards, select all or deselect all. The separate × control exits the mode.
- **Letter case:** choose Original, UPPERCASE, lowercase or Title Case.
- **Separators and order:** choose New line, Space, Comma or None, with Card order or Selection order.
- **Preview:** inspect and copy the resulting output before pasting it elsewhere.

These tools change the copied result without rewriting the original card text. Reset restores the copy settings. The delete control stays visible and explains what to select when there is no active selection.

## Additions and refinements since stable109

### Responsive Advanced copy controls

The toolbar adapts to available width. Letter case follows Select; separator and order controls wrap together, while Preview, Reset and Delete form a separate action group. On phone-sized layouts, Numbers, Select text, Join and Select use circular icon buttons. Preview retains its text label.

### Quick-copy dock

The dock supports a scrolling row and an expanded, wrapped layout. Its enclosing surface resizes with the buttons. The first time an added button makes the row overflow, the dock briefly opens and closes to reveal where that button went. This introduction is saved and does not repeat for every new card.

The guide’s adaptive-dock example runs from three to ten copy buttons and expands automatically when its sample row becomes crowded.

### Larger History and Trash collections

History and Trash initially render ten entries, then add further batches as you scroll. New entries fade and drop gently into view when motion is enabled. Switching sections no longer requires rendering the whole collection upfront.

### Menus, switches and refractive surfaces

Menus open from a circular trigger into a rounded enclosure. Their own text begins blurred, bends and inverts near the moving edge, and resolves as the menu opens. Background frosting remains separate from the text animation. Closing begins with clear text and introduces distortion as the shape contracts.

Pressed selection pills retain curved-edge lettering, colour dispersion and independent track bending. The scale thumb stretches independently of its surrounding menu. Switches expand while travelling, reach their largest size near the destination, then settle in one overlapping motion; their interiors use clearer sampling. Ordinary Advanced copy toggles avoid rebuilding the card list.

Notifications rise from below, widen and settle, with refractive surfaces and swipe-to-dismiss behaviour. Undo or Restore appears when the action supports it. The timer uses a glass surface consistent with the copy controls.

### Help & Guide for SCopier

The searchable guide includes Functionality, Design and Contact sections, with interactive demonstrations and direct links to individual topics.

- Scrolling upward reveals the top navigation. Clicking its active section retains the fixed-duration return to top. Choosing another section starts a faster upward scroll alongside the pill movement, then changes the content when the pill reaches its destination.
- Appearance, motion and transparency demonstrations place prominent blue action buttons above their previews. Clicking a preview points users toward the relevant button.
- Demonstrations reflect the responsive copy toolbar, circular controls, notifications and current menu design.
- **#29 — Menu morphodynamics:** inspect opening and closing with playback controls, speed adjustment and a draggable timeline. The active endpoint joins the bar while the opposite point stays detached. Pull the pill to the detached point, or click that point, to switch direction repeatedly without releasing the drag.
- **#30 — Live surface refraction:** enter your own text and drag the glass over it. Centred sliders below the preview adjust Refraction and Blur. Blur ranges from 0–30 px, applies a uniform Gaussian blur to sampled content and adds a subtle background-colour tint. Arrow keys move the glass; Home centres it.

The guide supports light and dark themes. Expanded optical surfaces refresh their colours when the theme changes.

### Version switching

The workspace menu includes **Version 1 (old)** and **Version 2 (new)**. Version 1 opens from a separate file and uses isolated browser storage. Returning to Version 2 after editing Version 1 asks whether to discard those legacy changes. Cancelling keeps you in Version 1; returning preserves the Version 2 workspace.

## Appearance and accessibility

Choose light or dark mode, reduced motion, and reduced transparency. Reduced transparency replaces much of the glass treatment with more solid, simpler surfaces.

Scale adjusts the complete interface through five levels: Smallest (80%), Small (90%), Standard (100%), Large (110%) and Largest (120%). Layout dimensions share one scale factor while pointer coordinates remain in normal page space. The scale control supports dragging, fixed detents and keyboard input.

Top controls hide during downward scrolling and return on upward scrolling, keyboard focus or near the page top. Menus distinguish page scrolling from scrolling inside a menu.

## Browser rendering

Chromium browsers with SVG backdrop-filter support refract the live background. Safari uses dedicated renderers for pressed pills and menu lettering, plus native backdrop blur and a locally rendered refractive edge for section surfaces. The undistorted centre retains the real browser backdrop.

Recent Safari work removes unintended grey fills around sampled text, avoids copying GPU output into a second canvas, batches scroll redraws and anchors local demonstrations to their containers during elastic overscroll.

The two rendering paths can differ, particularly around complex background content. Automated checks and native WebKit captures cover specific interactions; they do not guarantee identical rendering or frame rates on every browser and device.

## Smart actions and location recognition

Card menus recognise links, phone numbers, places, dates, durations, latitude/longitude pairs and IPv4/IPv6 addresses. Copying a recognised value is separate from opening its destination. Locations open Apple Maps on Apple devices and Google Maps elsewhere; dates provide calendar actions, and durations can start timers.

Recognition is automatic and entirely offline. A compact, data-backed recogniser uses the bundled place list, postal-code membership and context rules. It is not a neural model and does not require a paid API, background request, server, localhost service, NLP installation or extra search dialog.

- A locality and its country/region, such as **Kolkata, India**, become one location with the existing Copy location and Maps actions.
- Lists of cities or countries remain separate destinations. Labelled addresses and numbered streets retain their locality and postal-code suffix.
- Known PIN/postal codes are recognised locally, including a standalone Indian PIN or a code labelled PIN, ZIP or postal code. Order, invoice, OTP and phone contexts are excluded. Numeric codes in unrelated prose are not automatically promoted to locations.
- Decimal, hemisphere and degrees/minutes/seconds coordinates are validated locally. IPv4/IPv6 values offer **Copy IP address** only; IP geolocation is not performed.
- Notes without a recognised entity get no additional location menu actions. Copying and other existing smart actions keep their usual behaviour.

There are no OpenStreetMap lookup buttons, “Find locations in text”, analysis dialogs or optional spaCy services. Maps opens only when the user chooses the existing Maps action; viewing a map uses that external app/site. Recognition itself remains offline.

Context rules are conservative, not an understanding of every sentence. Ambiguous names and numeric postal codes can still need a locality, country or address label.

### Postal-code data

The bundled exact-membership index contains **4,284,045 unique country/code pairs across 124 countries**, built from **5,045,914 source rows** downloaded on 17 November 2026. It combines GeoNames `allCountries.zip` with the full UK, Canadian and Dutch extracts. The app stores compact numeric ranges and postal-sector bitmaps rather than millions of address objects. These data add about 5.3 MiB to the offline bundle; no postal index is built on every keystroke.

The dataset does not contain every code in every country. Some source countries provide partial codes, and source data can be missing or outdated; membership is not delivery/address verification. See the [GeoNames postal dataset and coverage notes](https://download.geonames.org/export/zip/readme.txt). The full UK extract contains Royal Mail copyright and database right 2022. GeoNames postal data is licensed under CC BY 4.0.

To rebuild from downloaded source archives in `work/scopier/data`, run `python3 scripts/build-postal-data.py`. The app itself needs only the generated bundled data, never Python or a server.

### GeoNames attribution

The bundled `cities1000` and `countryInfo` extracts were downloaded on 15 October 2026. They supply 171,264 place records, 153,511 unique normalised primary/ASCII names and 252 country/territory records. Common aliases and translated country names supplement recognition.

Data was filtered and normalised for case and accents. Search-only metadata, coordinates and alternative-name lists were omitted, reducing the bundled index from approximately 6.1 MB to 2.3 MB. Contextual rules help reject ambiguous ordinary words.

- Source: [GeoNames](https://www.geonames.org/)
- Original extracts: [GeoNames download directory](https://download.geonames.org/export/dump/)
- Licence: [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/)

GeoNames does not endorse SCopier.

### Detailed India and Germany coverage

The offline recogniser also includes the full GeoNames India and Germany extracts downloaded on 17 November 2026: **660,065 India records** and **222,326 Germany records**. These include recorded villages, neighbourhoods, administrative areas, buildings, landmarks, roads, water features and terrain rather than only large cities. Primary names, ASCII spellings, alternate names and postal locality names supply **830,901 distinct local names**, with **811,155 additional names** beyond the original global city index. Names are stored in compact prefix buckets and searched without constructing a million-entry JavaScript map.

German PLZ/Postleitzahl labels and street-name-before-house-number addresses are supported, along with local-name and location-context handling. The datasets are not a list of every building, business or road, and do not contain billions of places. Real-world coverage is limited by the source; the app does not invent missing places. See the [GeoNames country-extract format and coverage](https://download.geonames.org/export/dump/readme.txt).

Run `python3 scripts/build-local-places.py` after the base city build to regenerate this extension from the local country and postal archives in `work/scopier/data`. The full app remains offline; the larger datasets increase the standalone HTML size.

## Backups and security

Export and import are available from the workspace menu. Export asks before downloading a JSON backup; import validates the file and asks before merging its cards. Browser storage and exported backups are not encrypted.

Backup validation includes known-field projection, size/count limits and atomic merge checks. Calendar output neutralises CR/LF injection. Generated releases include Content Security Policy metadata; hosted assets include integrity checks and deployment headers.

For hosting, publish only `outputs/site` and configure the host to apply its `_headers` file or the equivalent `outputs/deployment-headers.json`. Do not publish the source checkout, tests or QA artifacts. See `SECURITY.md` in the source checkout for details. Browser-delivered source remains inspectable.

## Development

From the source checkout:

```sh
npm ci
npm test
python3 -m unittest discover -s tests -p 'test_*.py'
npm run build
```

Editable app files live in `work/scopier/dist`. The build compiles `style.css` into `interface.css`, generates guide controls from `work/scopier/design/snippets.js`, and produces standalone files alongside the allowlisted `outputs/site` deployment.

`scripts/build-place-data.py` rebuilds the recognition index from `/tmp/scopier-cities1000.zip` and `/tmp/scopier-countryInfo.txt`.

Latest local validation: 205 JavaScript tests and 12 Python tests passed. Additional Chromium and native WebKit checks exercised menus, toggle sequencing, theme refresh, sampled background colours, continuous dragging and local scroll alignment. Negative elastic-scroll offsets were simulated; physical Safari rubber-band behaviour still warrants checking on the target device.
