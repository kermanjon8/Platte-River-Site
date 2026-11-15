# Platte River Marketing website

Live site: **platterivermarketing.com** (kearneyinsider.com forwards here)

Static site. No build step. Editing a file here auto-deploys to Netlify in about a minute.
Every commit uses Netlify credits, so batch changes into one commit when you can.

## The pages

| File | Address | What it is |
|---|---|---|
| `index.html` | `/` | Homepage: all five services |
| `kearney-insider.html` | `/kearney-insider` | The printed mailer |
| `rounds.html` | `/rounds` | Past rounds of the mailer |
| `board.html` | `/board` | The Online Board. **Advertisers are added here.** |
| `deals.html` | `/deals` | Deals from board advertisers |
| `mailers.html` | `/mailers` | Solo and semi-solo mailers |
| `websites.html` | `/websites` | Website design |
| `marketing.html` | `/marketing` | Ads management and design work |
| `claim.html` | `/claim` | The contact form |
| `thanks.html` | `/thanks` | Page people land on after submitting the form |
| `site.css` | | Shared styles: top menu, footer, and the newer pages |
| `_redirects` | | Forwards kearneyinsider.com to platterivermarketing.com |
| `ads/` | | Online Board ad images |
| `rounds/` | | Photos of each mailed card |
| `examples/` | | Semi-solo card images shown on the mailers page |

## Things not to change

- **The form name `claim-a-spot` in `claim.html`.** The Netlify email notification is tied to it.
- **The top menu and footer** are repeated in every page. If you change a link in one, change it in all ten.
- **Tracking code** (Google tag and Meta Pixel) sits just before `</head>` on every page. `thanks.html` also fires the Lead event.

---

## Adding an Online Board advertiser

### 1. Size the image in Canva and export as PNG

| Tier | Exact pixels | Price |
|---|---|---|
| Logo | 400 × 400 | $25/mo |
| Promo | 800 × 400 | $50/mo |
| Spotlight | 1200 × 500 | $100/mo |

Exact dimensions. Off-spec images get cropped.

### 2. Upload the image
Open the `ads` folder, then **Add file**, **Upload files**, commit.
Filename rules: lowercase, no spaces, use hyphens. `andrew-roofing.png`

### 3. Add them to `board.html`
Open `board.html`, click the pencil, find `const ADS = [`, and add a block:

```js
{
  tier:  "promo",
  name:  "Andrew's Roofing",
  img:   "/ads/andrew-roofing.png",
  link:  "https://andrewsroofing.com",
  start: "2026-11-15",
  end:   "2026-12-15"
},
```

Three things that break it:
- Image path needs the leading slash: `/ads/...`
- Comma after the closing `}`
- Dates must be `YYYY-MM-DD`

### 4. Add their deal (optional)
Open `deals.html`, find `const DEALS = [`, and add a block. Set `ends` to the same
date as the ad's `end` so both drop off together.

## Other jobs

- **Renew someone:** change their `end` date in `board.html` (and `ends` in `deals.html`).
- **Pull someone early:** delete their block, or set the end date to yesterday.
- **Ads expire on their own.** Past the end date the spot goes back to "available."
- **Change how many open spots show:** edit `OPEN_SLOTS` in `board.html`.
- **Change board prices:** three places. The tier cards and the `PRICE` list in `board.html`, and the size cards in `claim.html`.
- **Add a mailed round:** upload both card photos to `rounds/`, then add a block at the top of `ROUNDS` in `rounds.html`. To feature it on the mailer page, change the two image paths in `kearney-insider.html`.
- **Show a finished client website:** add a block to `WORK` at the bottom of `websites.html`. The section appears once the list has an entry.

## Checking clicks

Google Analytics counts clicks out to advertisers: Reports, Engagement, Events, the `click` event.
