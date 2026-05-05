# 3D Print Shop — CLAUDE.md

This file helps future Claude sessions pick up right where we left off.

## What This Is

A single-file static HTML/CSS/JS website for Jake's 3D print shop.
- Hosted on GitHub Pages (free)
- No payment processing — cart sends a `mailto:` email to `jakeycuso@gmail.com`
- Payment collected via Venmo `@imcuso` / CashApp `$imcsuo` after order confirmation
- Ships nationwide or hand-delivers in Dayton, OH

## Design System

Cyberpunk/hacker aesthetic:
- Colors: `--bg:#0A0A0F`, `--card:#12121A`, `--accent:#00FF88` (green), `--accent2:#00D4FF` (cyan), `--accent3:#FF00FF` (magenta), `--danger:#FF3366`
- Fonts: Orbitron (headers) + JetBrains Mono (body/terminal) via Google Fonts
- Effects: Matrix rain canvas (hero), CSS glitch animation on title, IntersectionObserver scroll reveals
- All styles are inline in `index.html` — no separate CSS file

## File Structure

```
3d-shop-website/
├── index.html                  ← entire site (HTML + CSS + JS, ~2200 lines)
└── assets/
    └── images/
        ├── arm/
        │   ├── arm-1.jpeg … arm-5.jpeg   ← V1 arm build photos
        │   ├── arm-jake.jpeg              ← Jake holding arm V1 (from doc)
        │   ├── arm-belt-pulley.jpg        ← belt-pulley drive closeup (from doc)
        │   ├── arm-overview.png           ← overview/about section image
        │   └── charts/
        │       ├── mass-v1.png            ← V1 segment mass (front-loaded problem)
        │       ├── mass-v2switch.png      ← V2Switch segment mass (balanced)
        │       ├── com-comparison.png     ← CoM: 340mm → 185mm
        │       ├── can-bus.png            ← CAN bus run lengths comparison
        │       └── radar.png              ← V1 vs V2Switch performance radar
        ├── printers/
        │   ├── x1c.jpeg                   ← Bambu X1 Carbon
        │   └── h2c.jpeg                   ← Bambu H2C
        └── products/
            ├── fidget-ball/hex/cube/ray/trilobyte.webp
            ├── catring.webp, dog-leash.webp
            ├── vase1–5.webp
            ├── nfc-tag.webp               ← real NFC WiFi tag product image
            ├── photo-demo-original.png    ← "before" for photo-to-3D demo
            ├── photo-demo-print.png       ← "after" for photo-to-3D demo
            └── home/
                ├── happy-pot.webp
                ├── honeycomb-organizer.webp
                ├── desk-set.webp
                ├── cable-clips.webp (placeholder — product has no image yet)
                ├── phone-stand-keychain.webp (placeholder)
                └── key-holder.webp (placeholder)
```

## Products (22 items)

| id | category | name | price | notes |
|----|----------|------|-------|-------|
| twisty-ball | fidgets | TWISTY SPHERE | $10 | |
| hex-large | fidgets | HEX MODULE [LG] | $14 | |
| hex-small | fidgets | HEX MODULE [SM] | $10 | |
| infinity-cube | fidgets | INFINITY CUBE | $15 | |
| ray-fidget | fidgets | RAY UNIT | $12 | |
| trilobyte | fidgets | TRILOBYTE | $13 | |
| cat-ring | pet | CAT RING TOY | $12 | variant: Ball / Donut |
| dog-leash | pet | DOG LEASH HOLDER | $16 | petName input |
| vase-twist | vases | TWIST VASE | $22 | |
| vase-hex | vases | HEX CELL VASE | $24 | |
| vase-spiral | vases | SPIRAL TOWER | $26 | |
| vase-wave | vases | WAVE FORM | $24 | |
| vase-geo | vases | GEO FACET | $28 | |
| happy-pot | home | HAPPY PLANTER | $14 | |
| honeycomb-organizer | home | HONEYCOMB DESK ORGANIZER | $24 | |
| desk-set | home | DESIGNER DESK SET | $28 | variant: Gray+Green / Black+Cyan |
| cable-clips | home | CABLE CLIP PACK [×4] | $10 | |
| phone-keychain | home | PHONE STAND KEYCHAIN | $12 | |
| key-holder | home | WALL KEY HOLDER | $14 | |
| nfc-wifi-tag | home | NFC WIFI TAG | $25 | nfcProduct:true, accordion setup instructions |
| makerworld | custom | MAKERWORLD EXPLORER | — | makerworld:true, quote needed |
| photo-print | custom | PHOTO TO 3D ART | varies | photoUpload:true, size/B&W selector |
| custom | custom | CUSTOM FABRICATION | — | custom:true |

Color picker populates from `filamentColors` array (25+ colors from `filament colors.txt`).

## Key JS Functions

- `buildProductCard(p)` — branches on `p.makerworld / p.photoUpload / p.nfcProduct / p.custom`
- `addToCart(id)` — captures color, qty, petName, variant
- `addDonation(amount)` — donate buttons ($10/$20/$50/$100) in About section
- `addPhotoToCart()` — uses `photoState` {size, bw, file}
- `addMakerworldRequest()` — reads mw-link, mw-color, mw-notes inputs
- `toggleNfcInfo(el)` — accordion for NFC setup instructions
- `submitOrder()` — builds mailto: body, opens mail client

## Page Sections (top to bottom)

1. **Hero** — matrix rain, glitch title "MANCUSO FABRICATION", CTA buttons
2. **Machines** — X1C card, H2C card, Robot Arm V1 card (gallery with 7 photos)
3. **Arm Evolution** — V1 vs V2Switch stats panels + 5 engineering charts + 2 build photos
4. **About** — Jake bio, payment info, stats, donate buttons
5. **Shop** — tabbed product catalog (Fidgets / Pet / Vases / Desk+Home / Custom)
6. **Cart** — sticky sidebar, Submit Order button → mailto

## STL Source Files

`~/Desktop/3D-Print-Shop/printable objects/` — each product subfolder has a `source.txt` with Printables/MakerWorld URL for Jake to download himself (Printables requires login).

## To Deploy / Update

```bash
cd ~/Desktop/3d-shop-website
git add .
git commit -m "your message"
git push
```

GitHub Pages auto-deploys from `main` branch root. Live at:
`https://jakemancuso.github.io/3d-shop` (update this once repo is created)

## Things That Could Be Added Later

- Real product images for cable-clips, phone-stand-keychain, key-holder
- More products (the STL folder has more items)
- Order tracking / confirmation page
- Gallery section with finished print photos
- Customer reviews section
