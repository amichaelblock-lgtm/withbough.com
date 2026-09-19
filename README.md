# Bough website (portable static example)

A self-contained marketing and legal site for Bough. Plain HTML and CSS, no
framework and no build step. Built as an **example** that is trivially portable
to the real site later: copy the folder to any static host and it works.

## What's here

| File | Route | Purpose |
|---|---|---|
| `index.html` | `/` | Landing page: the living family space, the everyday together, made together, the tree, past/present/future, how it works, privacy, pricing |
| `terms/index.html` | `/terms/` | Terms of Service (complete draft for attorney review) |
| `privacy/index.html` | `/privacy/` | Privacy Policy (complete draft for attorney review) |
| `support/index.html` | `/support/` | Support and contact, data export, account deletion, data + removal requests, FAQ |
| `styles.css` | — | One shared stylesheet (brand tokens, layout, responsive, dark theme) |
| `assets/bough-mark.svg` | — | Brand mark, also used as the favicon |

The legal and support pages use a directory-index layout (`terms/index.html`,
etc.) so they resolve at clean paths (`/terms`, `/privacy`, `/support`) on any
static host with no rewrite rules. This matches the URLs the iOS app and App
Store Connect point at. Links are all relative (subpages reference `../styles.css`
and `../terms/`), so the site also works served from a subpath. Fonts (Fraunces,
Karla) load from Google Fonts; everything else is inline.

## Preview locally

Open `index.html` in a browser, or serve the folder:

```
cd apps/website
python3 -m http.server 8080
# then open http://localhost:8080
```

## Deploy to a static host

The whole folder is the site root. No build command.

- **Cloudflare Pages / Vercel / Netlify:** point the project at `apps/website`,
  leave the build command empty, and set the output/publish directory to the
  same folder (it already contains `index.html`).
- **S3 + CloudFront:** upload the files to a bucket, set `index.html` as the
  index document, and front it with CloudFront.

Clean paths (`/terms`, `/privacy`, `/support`) work out of the box: each is a
directory with an `index.html`, so no "clean URLs" / rewrite configuration is
needed on any host.

## Design

On-brand with the app: the founder-locked lab v9 palette (cream paper, sage,
amber, terracotta) and the Fraunces + Karla type pairing, per `DESIGN.md`. Copy
follows the voice rules in `DESIGN.md` §10 (plain, concrete, sentence case; no
em-dashes, emoji, or upsell language). The site leads on connection and
aliveness, with keepsake depth as the substance beneath. The hero is a
hand-built family tree in inline SVG, populated with life (a shared photo, an
"added today" marker); a second, larger tree lower down draws its branches in
once as it scrolls into view (respecting reduced-motion). Layout is editorial
and asymmetric rather than a stack of centered cards. Light paper is the primary
look, with a restrained warm-dark theme that follows the reader's system
setting.

## Kept out of the workspace

This folder has **no `package.json`** on purpose, so it stays out of the pnpm
workspace and cannot affect `pnpm install`, `typecheck`, or Turborepo. It is
pure static files.

## Before this is the real site

- Register and point DNS for **withbough.com**.
- Legal review: the Terms and Privacy pages are complete, attorney-review-ready
  drafts built on the parameters for MAABLAB LLC (California; Los Angeles County
  venue; no arbitration; liability cap the greater of 12-month spend or USD 100;
  13+/16+ age policy). Each doc ends with a "Notes for counsel review" block
  listing the embedded business decisions to ratify and the few factual items to
  verify (PostHog region, Nominatim hosting, Gemini no-training terms, full
  mailing address). Set the effective dates to the actual go-live date.
- The `Get Bough` buttons (header, hero, pricing, closing) link to the App Store
  listing at `https://apps.apple.com/app/id6780286740`.
