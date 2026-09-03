# ClearLabel

A free, open-source product safety scanner — like Yuka, but yours. One HTML file,
no account, no ads, no tracking, no server of your own. Scan the barcode of any
food or cosmetic product in the world, see every ingredient explained, and get a
0–100 safety score computed entirely on your phone.

**Data sources:** [Open Food Facts](https://world.openfoodfacts.org) and
[Open Beauty Facts](https://world.openbeautyfacts.org) — the same open databases
Yuka was originally built on. 3+ million products, contributed by people worldwide,
free forever under the ODbL licence.

## Features

- **Barcode scanning** with your iPhone camera (EAN-8/13, UPC-A/E, Code 128/39)
- **Works for products that aren't in any database** — if a barcode isn't found,
  point the camera at the ingredients list printed on the pack: ClearLabel reads it
  with on-device OCR (Tesseract.js), understands **E-numbers, INS numbers (Indian
  labels), class notation like "Preservative (211)", and full ingredient names**,
  scores it, and saves it to *your products* on your phone — so that barcode works
  instantly (and offline) from then on
- **4 open databases checked in parallel** — Open Food Facts, Open Beauty Facts,
  Open Products Facts and Open Pet Food Facts — plus automatic barcode-variant
  retries (a 12-digit UPC is also tried in its 13-digit zero-padded EAN form and
  vice versa), which fixes many false "not found" results
- **Manual barcode entry** and **search by product name** as backups
- **Food scoring** — Yuka-style: 60% nutrition (Nutri-Score), 30% additives, 10% organic,
  with a built-in risk table of 60+ E-number additives (EFSA / IARC / EU assessments)
- **Cosmetic scoring** — ingredient lists checked against a 45+ entry watchlist
  (parabens, formaldehyde releasers, endocrine disruptors, allergens…), each with
  a plain-English explanation of the concern
- **Allergen display, NOVA ultra-processing group, nutrition facts**
- **History** of your last 50 scans, stored only on your device
- **Your products** — everything you add via label scanning is stored only in your
  browser (editable and removable from the result screen)
- Add to Home Screen → works like a native app

## Put it on your iPhone (2 minutes, free)

iPhones only allow camera access on pages served over **https://**, so the file
needs free hosting first. GitHub Pages is the easiest:

1. Create a free account at [github.com](https://github.com) if you don't have one.
2. Click **+ → New repository**, name it `clearlabel`, set it **Public**, create it.
3. Click **uploading an existing file**, upload `index.html`, and commit.
4. Go to **Settings → Pages**, under "Branch" choose `main` and **Save**.
5. Wait ~1 minute. Your app is live at `https://YOURNAME.github.io/clearlabel/`
6. Open that link in **Safari** on your iPhone → tap **Share → Add to Home Screen**.

That's it. Tap the icon, tap **Start camera**, allow camera access, and scan.

> Alternatives: Netlify Drop (drag the file onto netlify.com/drop) or Cloudflare
> Pages also host single files for free over https.

## How the scores work

**Food** — starts from the product's Nutri-Score (A=60 … E=5 points), adds up to
30 points for a clean additive list (each additive deducts by risk level), and a
10-point bonus for certified organic. Any additive with high-level concerns
(e.g. nitrites, titanium dioxide, BHA) caps the score at 49 ("Poor") no matter
how good the nutrition is — same philosophy Yuka uses.

**Cosmetics** — starts at 100 and deducts per flagged ingredient (−30 high,
−12 moderate, −4 limited concern). Any high-concern ingredient caps the score at 49.

**Bands:** 75–100 Excellent · 50–74 Good · 25–49 Poor · 0–24 Bad.

## Make it truly yours

Everything lives in one file. Open `index.html` and edit:

- `ADDITIVES` — the food additive risk table (add E-numbers, change risk levels)
- `COSMETIC_RISKS` — the cosmetic watchlist (add ingredients you personally avoid)
- Scoring weights in `scoreFood()` / `scoreCosmetic()`
- Colors and fonts in the `:root` CSS variables

If a product isn't found in any database, the app no longer dead-ends: it offers
to **scan the ingredients label** with your camera (or lets you type it), scores it
on the spot, and remembers it on your device. You can also add the product at
openfoodfacts.org or openbeautyfacts.org (photo + barcode, 30 seconds) so it works
for everyone — that's the open-data deal: everyone's scans get better.

## Disclaimer

Scores are informational, computed from community-contributed open data and
published assessments (EFSA, IARC, EU CosIng, SCCS). They are not medical advice.
Always read the physical label for allergy decisions.

## Licence

Code: MIT — do anything you like with it. Product data: © Open Food Facts /
Open Beauty Facts contributors, ODbL.
