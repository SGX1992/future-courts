# GILTC — Munich Invitational 2027

Landing page for **GILTC (Global Innovation Leaders Tennis Club)** — a premium one-day,
32-player Swiss-format tennis invitational for founders, investors, operators and innovation
leaders. Founding Edition: Munich, Summer 2027. €290 player ticket.

## Contents

| Path | What it is |
| --- | --- |
| `index.html` | The entire site. Self-contained — all photos are embedded as data URIs, no build step, no dependencies. |
| `assets/` | Source images: founder photo + 4 tennis photos (Unsplash), plus the web-optimised `img_*.jpg` versions actually embedded in the page. |

## Run locally

Open `index.html` in a browser, or:

```sh
python3 -m http.server 4601
# http://localhost:4601
```

## Deploy

It's a single static file, so any static host works.

- **Vercel** or **Netlify**: connect this repo, framework preset "Other", no build command,
  output directory = repo root.
- Or drag `index.html` onto app.netlify.com/drop.

## Connecting the ticket form

The ticket-request form is native to the page, but it is **not connected yet**.

A browser cannot write to Notion directly (the API key can't live in a public page), so it needs
a relay:

1. In Zapier, create a Zap with trigger **Webhooks by Zapier → Catch Hook**, and copy the URL.
2. Action: **Notion → Create Database Item**, into the GILTC Applications database.
3. Map the posted fields: `first_name`, `last_name`, `email`, `company`, `role`, `linkedin`,
   `tennis_level`, `message`.
4. In `index.html`, find `var ENDPOINT = '';` and paste the webhook URL between the quotes.

Note: the form can only reach the network from a real deployment — it will not submit from the
claude.ai artifact preview, which blocks outbound requests.

### Still to do

- Update the Notion database columns to match the form fields above (it still has the older
  membership-era fields).
- Optional: a second Zap for the acceptance email (Notion Status = Approved → send email).

## Design notes

Dark-mode-first, restrained: deep bottle-green ground, warm chalk text, a single champagne-brass
accent. Serif display face, tracked uppercase labels. The hero court diagram draws itself on load;
photos are tonally shifted to sit inside the palette. Reduced-motion is respected.
