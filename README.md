# Larkhaven Renovation Estimate | Portfolio Demo

**A polished, single-file, mobile-responsive client-facing prototype.** Fictional company and illustrative pricing, intended for showing the capabilities of a potential freelance project.

## Open

Double-click `index.html` in Chrome, Edge or Safari. No hosting, API key, build system, package installation or internet connection is necessary.

## What the demo does

- Four-step project quote flow with three service types: flooring, interior painting, wall tile.
- Room selector, 30–5,000 sq ft area validation, tiered materials, optional services.
- Deterministic, itemized USD pricing with labor, material, add-ons and minimum charge. Every line is rounded to the cent, so the line items always add up to the total.
- Planning range ±15%, clearly marked as illustrative. While the area is invalid, the live estimate shows "—" instead of a price.
- `Edit demo pricing` lets a contractor edit labor, materials, add-on rates and minimum fees. Browser-local price book persists where allowed.
- Step 4 validates name, email and ZIP field by field, saves a demo inquiry locally and lets you export a CSV. Spreadsheet-formula injection is sanitized in the export.
- Printable estimate with business line, date, quote reference and customer (after saving), and a "demo / not a binding quote" notice. Responsive phone layout.

## Verify with these scenarios

Starting prices may be changed in Settings. With default prices:

| Scenario | Calculation | Expected total |
| --- | --- | --- |
| Flooring, 200 sq ft, Luxury vinyl plank, no add-ons | 200 × ($4.25 + $3.75) | **$1,600** |
| Painting, 100 sq ft, Standard paint, no add-ons | 100 × ($0.80 + $1.90) = $270; $650 minimum applies | **$650** |
| Wall tile, 150 sq ft, Porcelain tile, both add-ons | 150 × ($9 + $9.50 + $3 + $2.75) | **$3,637.50** (headline rounds to $3,638) |
| Flooring, 102 sq ft, Luxury vinyl plank, both add-ons | $433.50 + $382.50 + $153.00 + $127.50 | **$1,096.50** (headline $1,097) |
| Flooring, 0 / 29 / 5001 / 200.5 sq ft | invalid | continue blocked, live estimate shows "—" |
| Step 4 with a bad email or a 3-digit ZIP | invalid | save blocked, that field is highlighted and focused |

## Limitations to explain honestly to clients

**This is a front-end prototype, not an operational contractor site.** No quote requests are sent to a business, no authentication, no server, no database, no payment processing, no tax or permit calculations. Data is held only within the visitor's browser and can be exported. Real deployment requires replacing the fictional sample rates, validating business rules, implementing a secure backend or CRM integration, spam prevention, privacy policy and tests with real contractor examples. Local browser persistence may be unavailable when opened via file:// in some browsers.

The brand `Larkhaven` is fictitious. It must not be represented as an existing client or completed paid project.

## Prototype QA performed on 2026-11-14

- Browser-based desktop and mobile flow tested in headless Chromium.
- Expected amounts verified: $1,600 flooring, $650 painting minimum, $3,637.50 tile with add-ons (rounded $3,638 in UI).
- Invalid coverage prevented progression.
- Inquiry capture and CSV download tested.
- Changed a pricing rate and verified recalculation.
- No runtime JavaScript exceptions in the tested flows; mobile screenshot at 390px viewport had no horizontal overflow.

## Review pass on 2026-11-14

Fixed after a second round of browser testing:

- After saving an inquiry, `Back` used to show the success panel under the Options/Materials titles. The step controls are now hidden on the success screen; `Start a new estimate` returns to step 1.
- Line items were rounded to whole dollars independently, so they could disagree with the total by $1 (102 sq ft flooring with both add-ons showed lines summing to $1,098 against a $1,097 total). The breakdown now shows cents and always adds up.
- Negative, empty or out-of-range areas used to produce prices (and negative line items) in the live estimate.
- Step 4 named no specific field in its error; it now points at the first invalid field.
- Printing showed the marketing headline and no date, reference, customer or demo notice.
- On short phone screens, `Continue` left the next step's title above the viewport; the panel now scrolls into view.
- Pricing dialog copy said changes apply instantly; they apply when saved.
- Added a meta description and favicon so a shared link looks finished.

All scenarios in the table above were re-run in Chromium after these changes (desktop and 375px mobile), plus CSV export, pricing edit/validation/reset, and the print layout. `preview-mobile.png` shows the current version. The old desktop screenshot was removed because it showed the previous brand; capture a new 1440-wide `preview-desktop.png` after deployment.

## Deploy

Upload only this folder (`index.html` plus the images; `README.md` is harmless to include) to any static host: Netlify, Cloudflare Pages or GitHub Pages all work on a free plan. Keep the `business/` folder (sales and delivery templates) out of the public site. After deploying you can add `<meta property="og:image" content="https://YOUR-URL/preview-desktop.png">` so link previews show a screenshot.

Sales and delivery templates live in `../business/`.
