# SCopier

A local clipboard workspace for keeping text in cards, combining selections, and copying the result in the format you need.

Made by Srijan Chatterjee. ©2026 All rights reserved.

Documentation updated **25 October 2026**, covering Version 2 and the changes made after `20261015-stable109`.

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

Automatic recognition runs locally using GeoNames, Compromise and coordinate/IP parsers. Coordinates support decimal pairs, hemisphere notation, latitude/longitude labels and degrees/minutes/seconds. Opening a website, map, calling app or calendar hands the chosen value to that service or application. Natural-language candidates are not verified addresses; ambiguous names may need a city or country. English NLP is best-effort and does not recognise every location or language.

### Optional online lookups and local spaCy

The card menu offers **Find locations in text…**. Review the text and choose **Analyze text** to combine browser candidates with optional spaCy analysis on the local SCopier server. This analysis does not geocode or send the full text to a public provider. Use **Search this place** and then **Search** to geocode an individual candidate.

Recognised locations also offer **Find on OpenStreetMap**; public IPs offer **Locate IP**. Opening either dialog makes no network request. Search sends only the reviewed place or coordinates to Nominatim; IP lookup sends only the reviewed public IP to ip-api.com. Private/local/reserved IPs are rejected. IP locations are approximate network locations, not a person’s position. Do not submit confidential queries to public providers.

Start the optional service from the source checkout:

```sh
python3.11 -m venv .venv-geo311
.venv-geo311/bin/pip install -r requirements-geo.txt
.venv-geo311/bin/python -m spacy download en_core_web_sm
.venv-geo311/bin/python scripts/serve.py --recognition --spacy-model en_core_web_sm
```

Open **http://127.0.0.1:4174**. The standalone `file://` app retains browser recognition, but online lookups require this same-origin server. Browser storage differs between file and localhost origins; use a backup to move cards. Omitting `--spacy-model` keeps the browser recognizer and online lookups; omitting `--recognition` disables the API entirely.

Nominatim requests are user-triggered, queued below one request per second across processes sharing the cache, cached for 30 days, identified as SCopier and attributed to OpenStreetMap contributors. There is no geocoding autocomplete. Set `SCOPIER_NOMINATIM_URL` to another compatible HTTPS endpoint to change providers. The public service has no availability guarantee and is intended for modest use: [Nominatim usage policy](https://operations.osmfoundation.org/policies/nominatim/).

The free [ip-api endpoint](https://ip-api.com/docs/api:json) is enabled for this personal/non-commercial build. Its HTTP-only upstream runs through the local server; the selected IP is transmitted without HTTPS encryption. Requests are cached for one day, limited below 45 per minute and honor provider cooldown headers. Do not use this free provider commercially.

Local spaCy uses the English `en_core_web_sm` pipeline with GPE, LOC and FAC entities. Compromise 14.19.0 is bundled under the MIT licence; see `THIRD_PARTY_COMPROMISE_LICENSE.txt`. Neither library requires a hosted NLP API key. The server binds only to loopback, accepts same-origin JSON POSTs and keeps its SQLite lookup cache in `.cache/location-api.sqlite3` outside the published files. Delete that file while the server is stopped to clear cached lookup results. Never publish the cache, Python environment or source directory.

### GeoNames attribution

The bundled `cities1000` and `countryInfo` extracts were downloaded on 15 October 2026. They supply 171,264 place records, 153,511 unique normalised primary/ASCII names and 252 country/territory records. Common aliases and translated country names supplement recognition.

Data was filtered and normalised for case and accents. Search-only metadata, coordinates and alternative-name lists were omitted, reducing the bundled index from approximately 6.1 MB to 2.3 MB. Contextual rules help reject ambiguous ordinary words.

- Source: [GeoNames](https://www.geonames.org/)
- Original extracts: [GeoNames download directory](https://download.geonames.org/export/dump/)
- Licence: [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/)

GeoNames does not endorse SCopier.

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

Latest local validation: 202 JavaScript tests and 19 Python tests passed. Additional Chromium and native WebKit checks exercised menus, toggle sequencing, theme refresh, sampled background colours, continuous dragging and local scroll alignment. Negative elastic-scroll offsets were simulated; physical Safari rubber-band behaviour still warrants checking on the target device.
