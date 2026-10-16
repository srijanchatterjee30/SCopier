SCopier — local build 20261015-stable109
Made by Srijan Chatterjee
©2026 All rights reserved

Open SCopier.html, or serve work/scopier/dist at localhost. The standalone file contains the full app and offline recognition data. Existing browser storage remains compatible; no workspace data is embedded in this release.

Scale
Workspace options > Scale adjusts the entire interface: navigation, menus, tools, quick-copy controls, typography, spacing and cards. The five levels are Smallest (80%), Small (90%), Standard (100%), Large (110%) and Largest (120%). Smaller levels also fit extra card columns when there is room. Standard retains the original dimensions. Layout lengths use one shared CSS factor, without transforming the page or its pointer coordinates. The open settings panel and toggle geometry follow the same scale.

Settings and scrolling
Advanced copy is the first setting. Export backup and Import backup are the final two options. Export asks for confirmation before downloading a file. The redundant saved-status label and current-layout wording have been removed. Small page scrolls leave menus open; a net page movement of 72 pixels dismisses them using the existing spring shrink directly to zero size, without painting a compressed button circle. Manual closing returns to the trigger only while that trigger is visible and nearby. Scrolling during a manual close redirects the remaining shrink to zero. Internal menu scrolling does not dismiss a menu and does not chain into page scrolling. The top controls hide on downward scrolling and reappear on upward scrolling, keyboard focus, or near the page top.

Recognition
There is no Maps search dialog or manual search setting. Recognized locations retain Copy location and Open in Maps actions, alongside links, phones, dates and durations. Apple devices open Apple Maps; other devices open Google Maps. Recognition runs locally without an API key. These actions cannot verify every street address or resolve every ambiguous name.

GeoNames attribution
The cities1000 and countryInfo extracts downloaded 2026-10-15 provide 171,264 place records, 153,511 unique normalized primary/ASCII names, and 252 country/territory records. Names are normalized for case and accents, with contextual safeguards for ambiguous words. Common country aliases and translated country names supplement the data. Search-only metadata was removed, reducing bundled data from approximately 6.1 MB to 2.3 MB.
GeoNames: https://www.geonames.org/
Original extracts: https://download.geonames.org/export/dump/
License: Creative Commons Attribution 4.0, https://creativecommons.org/licenses/by/4.0/
Changes: selected and normalized primary/ASCII names, confidence metadata, and contextual recognition rules. Coordinates and alternative-name lists are omitted.

Development
npm ci
npm test
python3 -m unittest discover -s tests -p 'test_*.py'
npm run build
python3 -m http.server 4173 --bind 127.0.0.1 --directory work/scopier/dist

style.css is the editable source. The build generates interface.css with shared scaling for layout lengths, preserving media-query thresholds and quoted literals, then bundles all six scripts and the compiled stylesheet into outputs/SCopier.html. scripts/build-place-data.py rebuilds the recognition dataset from /tmp/scopier-cities1000.zip and /tmp/scopier-countryInfo.txt.

Validation: simulated-DOM production boot; scale profiles and persistence; open-menu resizing and toggle geometry; settings order; export confirmation/cancellation; page-scroll thresholds; internal menu scrolling; header reveal behavior; preview/copy consistency and selections; worldwide recognition; generated CSS and standalone integrity. No fresh visual Safari/Chrome rendering pass was available for this build.

Security hardening (security73)
Backup input now has known-field projection, size/count bounds and atomic merge checks. Calendar text neutralizes CR/LF injection. Standalone scripts/styles have CSP hashes; production assets have integrity checks and security headers. Publish only outputs/site on an HTTPS host configured to apply its _headers file, or equivalent headers from outputs/deployment-headers.json. No public deployment was made. Read ../SECURITY.md for findings, deployment steps, test evidence and limits. Browser source can still be reverse-engineered; stored notes and exported JSON are not encrypted.

Pressed-lens refinement (lens74)
Compared against the supplied Apple day/week/month/year and clock-pill references. Only expanded selection lenses use the new smoothly weighted curved-end field: vertical distortion is restrained, colour channels separate at the rounded ends, and the central label stays crisp. Removed the original-glyph alpha intersection and partially transparent word masks that could thin displaced strokes or leave an original image underneath. A separate subtle vertical track displacement gives the bar a curved appearance within the lens without resizing the bar's actual layout. On release the displacement strength returns continuously to zero while the same optical layer remains visible. Generic/toggle filter math and drag springs remain unchanged.
The header revealed on upward scroll now has a light/dark frosted backdrop with masked fades along its bottom and sides. Reduced transparency disables that backdrop blur. New tests sample the generated displacement maps, check mirrored end geometry and bounded gradients, verify opaque replacement masks and zero-displacement release, and cover the header state. A fresh real-browser visual comparison was not available.

Rim and Scale refinement (rim75)
Pressed selection lenses keep their approved text-only optical pipeline. The bend now peaks at the actual curved tip and falls smoothly to neutral over twelve pixels inward; the sampling field continues across the silhouette to avoid an artificial neutral seam at the outer edge. Centre text and the generic toggle field remain unchanged.
Scale now has a thumb-only drag gesture with no numbered row or resize cursor. Its number appears while held or keyboard-focused, previews the destination during movement, and disappears on release as the same liquid-lens pressure and velocity deformation settle. Scale changes commit on release to keep the rail steady during dragging; the keyboard range remains available. Empty rail/menu space retains ordinary menu stretching; pulling beyond either end stretches the surrounding menu.

Scale alignment correction (rim76)
The thumb and track now share a measured vertical centre throughout expansion and settling. Scale optics and number layers explicitly override legacy menu-row span padding. The old numbered row is removed from markup and suppressed for compatibility with stale markup. A new asset version refreshes cached scripts and styles.

Curved lettering at the rim (rim77)
Expanded selection lenses now add a modest tangential stretch to their approved tip refraction. Paired horizontal and vertical sampling coordinates follow the curved cap, magnifying lettering along the rim with a smooth inward taper. The neutral centre, generic lens field, dispersion, opaque text replacement and pressure-driven settling remain unchanged. Optical tests check tangential magnification, positive sampling gradients and symmetry. No fresh browser visual comparison was available.

Scale detents and independent track optics (scale78)
All five fixed scale dots now accept taps and keyboard activation. Their SVG outlines morph into the corresponding digit when reached under the held lens, then morph back to dots on release. The thumb restores its persisted position immediately; hidden-panel geometry has a scaled height fallback and is remeasured when the panel opens. The rail is observed for size changes. Dragging commits scale on release; surrounding menu space retains its stretch gesture.
The approved lettering refraction field is unchanged. A separate track bitmap replaces the previous normal-derived track displacement: its centre is straight and optically compressed by about seven percent in height, easing to about four percent at the ends for an outward flare. This changes only the sampled bar inside the lens, not its layout dimensions. The track and text both return smoothly to normal as pressure settles.
Validation includes direct tapping of every detent, saved-position restore with a hidden rail, dot/digit morph reversal, independent track coordinates and outward easing. A real-browser visual comparison was not available.

Shared scale coordinates (scale80)
Removed the old thumb number element and intermediate dot wrapper entirely. The line, five clickable SVG detents and glass blob are now direct children of one rail. The same measured vertical centre positions both detents and blob at all five interface scales, including when the panel starts hidden. Only a reached detent morphs into a numeral, preventing duplicate labels below the line. Updated asset URLs avoid reusing earlier in-progress scale assets.

Bar bend without thin highlight splitting (rim81)
Retains the optical bar compression and outward cap easing. A subpixel morphological opening is applied only to the background sampling branch before the bend, removing thin bright glints that otherwise form extra internal contours. The letter branch continues to sample the original scene, preserving its approved refraction, dispersion and tangential stretch. Cleanup radius follows contact pressure and returns to zero with the displacement on release. No blur/frost is added. Tests verify branch separation and pressure-scaled cleanup. A fresh Safari visual check was not available.

Search geometry after scaling (search82)
The closed search control returns to CSS-controlled dimensions instead of retaining animation pixels from an earlier scale. Open search uses local header offsets and remeasures its target on scale changes and header/slot resizing, preserving the query and open state. Closing clears width, height, top and radius overrides; reload starts with no cached search pose. Tests cover all five scales, local target bounds, resize, query preservation, and closed geometry after saved-scale restoration. No fresh browser visual pass was available.

Settled blue paint and neighbouring labels (lens83)
Selection blobs share the same settled blue gradients before and after interaction, including the scale thumb. Held selection groups rise above adjacent controls while their expanded optical mask includes intersecting neighbouring labels and icons in the local header, advanced tools or settings area. Distant controls are rejected before reading their text geometry. The approved displacement, dispersion and smooth release are unchanged.
Cards/History/Trash navigation now has a high-opacity theme-aware frosted backing. The same backing is retained on its single background paint layer during dragging, keeping content beneath subdued without changing the clear selection-lens field. Reduced transparency retains its existing opaque treatment. Added tests check nearby-control mask coverage and rejection of distant controls. Browser visuals were not independently verified.

Search, active edges and card selection (controls85)
Search opens using a single normalized time-based response for all bounds, allowing delayed frames to catch up without independent width/height springs or a late height snap. Input focus prevents scroll movement. Active search and copy tools have a restrained blue edge animation; reduced motion uses a static edge and reduced transparency keeps the flat treatment.
Select enters manual selection mode, preserving current joined/text targets. It becomes Select all without automatically selecting every card. Select all is idempotent; individual card pickers and quick buttons toggle card selection. A separate cross clears card, join and text selections and exits selection mode while retaining tool preferences. Selected cards remain draggable.
The bar-bend branch is clipped to the host bar region; outside it the original scene passes through unchanged. Neighbouring search/plus icons use SVG stroke masks with enough sampling margin for displacement, rather than button-sized rectangles. Existing letter refraction and dispersion remain unchanged. The retained glass paint excludes sampled labels/icons during settling, preventing a pale blue coating before the normal accent returns.
Regression tests cover selection entry, individual toggling without copying, Select all and cross behavior, joined/text targets, synchronized search geometry under delayed frames, vector icon masks, host-only bar bending and release paint masking. Browser visuals were not independently verified.

Selection toggle and quiet card controls (select86)
Select still enters manual selection mode. In that mode the same button now switches between Select all and Deselect all based on the actual selected cards. Deselect all clears card, joined and text targets while keeping selection mode active; the cross remains the separate exit action. Card menus are closed and hidden, and both individual and joined card copy controls are hidden until selection mode exits. The quick-copy controls retain their selection/rearrangement behavior.
Edge shimmer is retained without adding any new interior shimmer. Tests cover the full selection toggle cycle, menu closure, individual/joined copy visibility and restoration after exiting selection mode. Browser visuals remain independently unverified.

Text rectangle and compact header correction (layout88)
The retained blue selection paint now lives behind the actual labels as a sibling of the lens. It follows the lens geometry and pressure without subtracting rectangular text masks from the visible fill. The existing optical sampling mask remains inside the filter; selected text therefore keeps its original colour without exposing a rectangular hole in the blue surface. Stroke refraction, bar bending and vector icon sampling are unchanged.
The header switches to two rows at 1120px, placing navigation/search below the brand and workspace menu before the centre controls can overlap the SCopier name at larger interface scales. Search dimensions continue to follow the local header bounds. Added a production-layer regression for the blue fill's placement, geometry, opacity and absence of cutouts. Real-browser visual confirmation was not available.

Scale numerals and wide screens (scale89)
Scale uses native system-font numerals instead of interpolated hand-drawn digit paths. A shared animation shrinks/fades the dot into its centred numeral and reverses on release. SVG user-unit font sizing avoids applying the interface scale twice. The scale rail has stronger dedicated blue gradients in both themes, inherited by its resting blob paint without changing other selection pills.
At 1600px and wider, header and main workspace use 96% of the window up to a generous 2880px canvas. Standard scale fits three or four columns based on available card width; ordinary windows retain their previous two-column layout. Joined cards share the same column calculation and row markers. Smaller/larger scale profiles retain their existing column preferences. Tests cover native numerals and wide-screen column changes. Real-browser visuals remain unverified.

Daylight material and curved optical bounds (daylight91)
Light-mode selection pills now use a more substantial pearl-blue resting body. The held fill retains 52% rather than 18% of its paint strength, with no change to the dark-mode pressure response. The same continuous, thin boundary in both interaction states blends faint cyan, lavender and warm highlights around the curved ends, with restrained elevation. The dedicated blue scale tint and approved text displacement remain unchanged.
Text/icon participation now requires intersection with the actual rounded capsule, without the previous eight-pixel rectangular reach allowance. The SVG output clip also uses the true rounded silhouette, preventing rectangular corner regions from participating in the lens effect. Tests cover text outside the capsule, corner rejection, genuine edge overlap and the light/dark fill response. Real-browser visual confirmation was not available.

20261015-smooth94 — Lens continuity
Main navigation uses glyph-shaped masks without whole-word layer handoffs. Text ink follows capsule overlap and blends to its final state during release. Contact lenses use full-resolution displacement maps, a continuous end profile, narrower dispersion with subpixel smoothing of red/blue fringes only, and neutral saturation through settling. The inner track flares to unchanged height at both ends. Daylight boundaries are finer and clearer; retained lighting has no secondary transition. Automated checks cover geometry, filters and interactions; native browser appearance has not been visually verified.

20261015-edge95 — Rounded-edge softness and lift
A continuous capsule-rim mask confines subpixel colour softness to the curved ends; the clear centre and green/luminance reference stay sharp. Both colour channels return to zero softness with lift pressure. The daylight pearl boundary is more prominent while retaining its fine width. A subtle pressure-driven shadow follows the actual pill and eases out through the same release. Browser appearance is not visually verified.

20261015-curve96 — Continuous inner-bar curvature
The inner track uses its own quarter-ellipse profile across the complete rounded cap, calculated against the curved outline at each row. It no longer finishes its outward opening early or forms a flat outer shoulder. Text refraction, dispersion, rim and lift shadow retain the previous tuning. Optical-field tests verify the complete curve, symmetry and meeting the original bar at the outline. Browser appearance is not visually verified.

20261015-outline97 — Track cleanup and divider clearance
The background-only branch removes both light and dark thin source outlines before curving the inner bar; lettering still samples the untouched source. Navigation glyph masks match measured native text widths, protecting trailing curved letters against font-metric differences. Advanced-copy lenses have scale-aware left clearance without shifting the right edge; the clearance eases away during lift so expanded refraction retains its reach. Browser appearance is not visually verified.

20261015-track98 — Source-outline exclusion and continuous geometry
The original track rim and option dividers share a moving capsule cutout before optical sampling. The cutouts update together and clear on release; redundant physical borders/inset glints no longer duplicate the rim. Advanced-copy selections have equal scale-aware clearance at both sides. Contact geometry uses quarter-pixel dimensions and matching fractional radii, replacing two-pixel map changes at the curved letter edge. Regressions cover cutout movement/release, symmetric gaps and subpixel geometry. Native browser appearance remains unverified.

20261015-restore99 — Restore source contours and native type
Removed the failed moving rim/divider cutouts and their physical-border suppression. The original contour is available to the thinner track's quarter-ellipse map again. Removed all morphological erosion/dilation from contact scenes so incomplete text coverage cannot produce blocky residual letters. Text masks now cover measured native ranges rather than recreating font glyphs, and labels remain on one sampling layer throughout. Fine dispersion, lift shadow, symmetric resting gaps and subpixel geometry remain. Automated checks confirm source/filter structure and field geometry; browser rendering remains unverified and these checks do not prove the visual issue resolved.

20261015-join100 — Keep the original rim out of text refraction
The local track scene is restored across a full-height vertical strip rather than the original rounded capsule boundary. A source-bar outline mask follows the same text displacement and is subtracted only from text coverage, so the real border stays in the thinner-track branch instead of also being distorted with lettering. No source rim is cut out, no glyphs are eroded, and the existing quarter-ellipse curve is retained. Tests cover filter ownership, matched release displacement, native-type preservation and scene-region geometry. Browser appearance remains unverified.

20261015-rays101 — Correct vertical ray spacing in the inner track
An audit of the generated displacement bitmap found minimum vertical source spacing 0.3443 per output pixel near the curved cap (180x58), magnifying source contours by up to 2.9x. The row-dependent circular radius caused this local magnification. The inner-track compression now varies with horizontal position only, retaining the quarter-ellipse opening while preserving vertical source ordering and at least 1:1 spacing. The same audit now reports minimum spacing 1.0. Regression checks sample all interior pixel pairs across several integer/fractional sizes and release pressures. Text refraction, dispersion, rim styling and thin-bar amplitude remain unchanged. Native-browser visual confirmation remains outstanding.

20261015-baseline102 — Revert the unverified ray-map change
Restored the pre-rays101 inner track and curved-end logic. The numerical ray-spacing regression added with rays101 was removed because it enforced the visually rejected model. A development-only A/B page isolates parent inset lighting from the original thin-bar renderer; it is excluded from release assets. Browser launch was attempted, but macOS denied Chromium Mach-port registration inside the sandbox, so no captured-render verification occurred.

20261015-shadow103 — Cosmetic lighting after optical sampling
The user’s controlled browser comparison identified C (pill rim/shadows removed) as the variant that eliminates the unwanted inner streak; parent inset removal alone had no effect. The optical parent now retains C’s bare state. A separate sibling supplies the fine visible rim, and another supplies a blurred outline shadow 3px below the pill. Both siblings paint above the optical parent (z6/z5 versus z4), so they cannot enter its backdrop input. The shadow is masked to the exterior, follows shape/position each draw, and eases with lift pressure; the rim remains visible when settled. The restored thinner-bar map is unchanged. Regression checks cover sibling ownership, motion, exterior mask, release, scale centring and reduced transparency. Local automated Chromium launch is blocked by macOS Mach-port registration; the completed visual result has not been captured by the agent.

20261015-projection104 — A modest projected lift shadow
The independent shadow now follows the full blurred outline, including the arc transmitted through the clear pill, rather than being restricted to the exterior. Its offset grows with lift pressure (roughly 5–9px at normal sizes), and its softness and opacity relax with the same lift; no second timer is added. The contour remains faint and unfilled, with sufficient bounds for its blur. Rim, refraction and the restored thinner-bar map are unchanged.

20261015-shadow105 — Increased outline-shadow contrast in both themes. Geometry, softness, lift timing and optical maps are unchanged.

20261015-contained106 — Tightened the independent shadow blur and bounded its final footprint to the opened pill’s exact rounded rim. Lift offset, contrast, rim and refraction remain unchanged.

20261015-rim107 — Restored the softer shadow below the pill by removing its rim clipping. Reduced shadow darkness in both themes. The opened light-mode rim has a neutral grey base within the existing thin outline; no additional contour or optical layer is introduced.

20261015-shadow108 — Reduced shadow opacity by approximately 40% in both themes; geometry and motion unchanged.

20261015-stable109 — Stable lighting and active controls
Rims now exist before the first lift and keep the same daylight base colour through rest/drag/release. The independent shadow uses fixed padding instead of rounded changing bounds; open menus retain one compositor hint through stretching and settling. Active tools/search have a slow interior gradient with a static reduced-motion fallback. Select uses the card picker’s circular check geometry. Scale never allocates an outline shadow, preserves percentage-based rim positioning, and its blue fill eases fully to clear when held. Tests cover rim identity, stable bounds, clear scale fill, shadow absence and selection icon persistence. Refraction maps and the restored inner-bar curve are unchanged. Browser rendering has not been independently captured.
