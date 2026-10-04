# Platte River Marketing — The Kearney Insider Online Board

Live site: **kearneyinsider.com**

Static site. No build step. Editing a file here auto-deploys to Netlify in about a minute.

| File | What it is |
|---|---|
| `index.html` | The board. **This is the only file you edit regularly.** |
| `claim.html` | The "Claim a spot" form |
| `thanks.html` | Page they land on after submitting |
| `ads/` | Advertiser images live here |

---

## Adding an advertiser

### 1. Size the image in Canva and export as PNG

| Tier | Exact pixels | Price |
|---|---|---|
| Logo | 400 × 400 | $25/mo |
| Promo | 800 × 400 | $50/mo |
| Spotlight | 1200 × 500 | $100/mo |

Exact dimensions. Off-spec images make the grid look sloppy.

### 2. Upload the image
Open the `ads` folder → **Add file** → **Upload files** → commit.

Filename rules: lowercase, no spaces, use hyphens. `andrew-roofing.png`

### 3. Make a Bitly link
Paste their website or Facebook page into bitly.com. This is how clicks get counted.

### 4. Add them to `index.html`
Click `index.html` → pencil icon → find `const ADS = [` → add a block:

```js
{
  tier:  "promo",
  name:  "Andrew's Roofing",
  img:   "/ads/andrew-roofing.png",
  link:  "https://bit.ly/andrew-roofing",
  start: "2026-08-24",
  end:   "2026-09-24"
},
```

Three things that break it:
- Image path needs the leading slash: `/ads/...`
- Comma after the closing `}`
- Dates must be `YYYY-MM-DD`

### 5. Commit
Live in about a minute.

---

## Other jobs

**Renew someone** — change their `end` date. That's it.

**Pull someone early** — delete their block, or set `end` to yesterday.

**Ads expire on their own.** Past the `end` date they disappear and the spot goes back to "available." Nothing to remember.

**Change how many open spots show** — edit `OPEN_SLOTS` in `index.html`.

**Change prices** — two places: the tier cards in the HTML *and* the `PRICE` config near the bottom. Update both.

---

## Checking clicks

Log into Bitly. Each link shows its click count. That number is what renews or loses a spot at the end of the month.

---

## Before you post publicly

- [ ] Site visibility set to public in Netlify
- [ ] Form detection enabled + email notification set up
- [ ] Test the form end to end with a real image
- [ ] At least 2 real advertisers on the board
