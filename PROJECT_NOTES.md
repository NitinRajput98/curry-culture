# Project Notes — Curry Culture Website

Working context/history for whoever (human or AI assistant) picks this
project back up in a future session. `README.md` covers the technical
how-to; this file covers *how we got here* and *what's still open*.

## What this project is

A real website being built for **Curry Culture Indian Kitchen & Bar**, an
operating restaurant at 38 Tarbert Street, Alexandra 9320, Central Otago,
New Zealand. The site owner (the person driving this project) has confirmed
they are the **owner/authorized representative** of this real business —
this is not a fictional practice project, and the real business
name/address/phone/menu are meant to be published.

## Timeline / how the content was sourced

1. Project started as a "dummy learning project" idea for a generic Indian
   restaurant in NZ, using reference sites: kohinoorfl.com,
   route-des-inde-restaurant-nice.com, loha.au, moderntailors.co.za.
2. The user then found a real restaurant of this name via a Google Maps
   listing screenshot and asked to use its real data. Because that raised an
   impersonation risk (unaffiliated use of a real business's identity), the
   assistant paused and asked about affiliation — user initially said "not
   affiliated, keep it private/local only."
3. Menu content was transcribed **by hand from photos of the physical menu**
   the user shared (photographed by a Google reviewer, "John Huân Vũ") —
   text/prices only, no images copied from those photos.
4. The business's listed website (`currycultureindiankitchenandbar.com`)
   was checked and found to 301-redirect to an unrelated business ("The
   Mooring Fish Cafe Raro") — it has almost certainly lapsed/expired and been
   re-registered by someone else. **Do not try to recover that exact
   domain** — register a fresh one (ideas are in `README.md` §5.2).
5. Later, the user clarified: **"treat as a real project"** — confirmed via
   follow-up question that they are the actual owner/authorized rep of this
   restaurant. At that point all "practice project" disclaimers were removed
   from the site, `robots.txt` was flipped to allow crawling, and fabricated
   placeholder review quotes on the homepage were replaced with a link to
   real Google reviews (inventing customer quotes would be misleading
   advertising — don't reintroduce that).
6. Real opening hours were provided and are now wired into the JSON-LD,
   homepage footer, homepage blurb, and a full per-day table on
   `contact.html`: **Closed Monday; Tue–Thu 6:00–9:30pm; Fri–Sun
   5:00–9:30pm.**
7. The user supplied ~22 real photos (`assets/img/`), which were reviewed,
   renamed to descriptive filenames, and wired into the header logo, hero
   background, homepage, about page, menu category banners, contact page,
   and a full gallery page. See "Known issues" below for two files lost
   during renaming and a since-removed low-res duplicate.
   - Note: the assistant initially flagged several of these (the
     `download*.webp` / `imgproc-thumbnail*` files) as likely stock/food-blog
     photos rather than the restaurant's own photography (suspicious
     filenames, duplicate resolutions, stock-style studio lighting). The
     user overrode this and confirmed there are no copyright issues, so all
     photos were used as directed. Worth keeping in mind if this ever comes
     up again (e.g. a takedown notice) — the call to use them was the
     owner's, made with that context in front of them.

## Current site structure

Plain HTML/CSS/JS, no build step, no framework:
- `index.html`, `menu.html`, `about.html`, `gallery.html`, `contact.html`
- `css/style.css` (single stylesheet, dark/gold design system)
- `js/main.js` (mobile nav toggle)
- `assets/img/` — real photos, descriptively named (see below)
- `assets/favicon/` — full favicon package (2026-09-03), supplied by the
  owner (looks like standard output from a favicon generator tool, e.g.
  realfavicongenerator.net): `favicon.ico` (32/48px), `favicon-96x96.png`,
  `favicon.svg` (a raster logo re-embedded in an SVG wrapper via base64 —
  not true vector art, but scales fine as a favicon), `apple-touch-icon.png`
  (180px), `web-app-manifest-192x192.png` / `-512x512.png`, and
  `site.webmanifest`. All 5 pages now link this set:
  `<link rel="icon" type="image/png" href="assets/favicon/favicon-96x96.png" sizes="96x96">`,
  an SVG icon link, `rel="shortcut icon"` → `favicon.ico`,
  `rel="apple-touch-icon"` → `apple-touch-icon.png`, and
  `rel="manifest"` → `site.webmanifest`.
  - The manifest arrived with generator placeholder values (`"name":
    "MyWebSite"`, white theme/background, and icon `src` paths with a
    leading `/` implying site-root, which didn't match their actual
    location alongside the manifest in `assets/favicon/`) — fixed name/
    short_name to the real business name, `theme_color`/`background_color`
    to match the site's dark palette (`#14100d`), and dropped the leading
    slash from icon paths so they resolve relative to the manifest.
  - This replaced an earlier throwaway attempt where the assistant manually
    cropped/resized `curry-culture-logo.jpg` with Jimp to build a favicon
    (documented previously in this file) — that approach is now moot; the
    owner-supplied package is what's live. The old standalone
    `assets/favicon.ico` / `assets/favicon-32.png` files were deleted.
- `robots.txt` (allows crawling, points to sitemap.xml)
- `sitemap.xml` (still has `YOUR-DOMAIN-HERE` placeholder — needs the real
  domain once purchased)

### Photo inventory (`assets/img/`)
`curry-culture-logo.jpg`, `restaurant-exterior-evening.jpg`,
`dining-room-mural.jpg`, `dining-room-window-table.jpg`,
`dining-room-table-artwork.jpg`, `dine-in-menu-table.jpg`,
`outdoor-courtyard.jpg`, `outdoor-courtyard-dusk.webp`, `biryani-bowl.jpg`,
`butter-chicken-rice.jpg`, `starters-pakora-veg-cutlets.jpg`,
`chicken-biryani-kadai.webp`, `naan-bread-stack.webp`, `aloo-gobi.webp`,
`lamb-kofta-curry-rice.webp`, `onion-bhaji-plate.webp`,
`chicken-tikka-skewers.webp`, `tandoori-prawn-skewers-thumb.webp`,
`tandoori-chicken-drumsticks-thumb.webp`.

(`restaurant-exterior-day.webp` was removed at the user's request in favour
of reusing `restaurant-exterior-evening.jpg` everywhere an exterior shot was
needed — all references were updated first.)

## Known issues / quirks to remember

- **Two files were lost during a rename batch** and can't be recovered:
  `imgproc-thumbnail=200,200` and `imgproc-thumbnail=200,200_`. A `mv` on the
  first one failed with "No such file or directory" mid-way through a
  chained command, which halted the rest of the chain (that's why
  `logo.jpg` needed a separate follow-up rename) — and oddly, the source
  files themselves were gone afterward (confirmed via both `ls` and
  PowerShell `Get-ChildItem`), even though a failed `mv` shouldn't delete
  its source. Root cause unconfirmed (possibly a non-ASCII/homoglyph
  character in the original filename that didn't round-trip through the
  typed command). Net effect: `tandoori-chicken-drumsticks-thumb.webp` is
  only an **11KB thumbnail** — the higher-res source is gone. If a bigger
  version of that photo exists elsewhere, swap it in.
- If you ever rewrite `README.md` (or any existing file) with the `Write`
  tool, double check its encoding afterward (`file README.md` should say
  UTF-8). The original repo's placeholder `README.md` was UTF-16LE, and
  overwriting it in place once **inherited that UTF-16LE encoding**
  silently. Deleting the file first and then writing fresh fixed it.
- Local preview: no system Python; use `npx serve .` (Node is installed) or
  VS Code Live Server. `serve` redirects `/foo.html` → `/foo` — that's
  normal, not a bug.

## Order Online (Uber Eats)

An "Order Online" button linking to the restaurant's Uber Eats store page
was added on 2026-09-03:
`https://www.ubereats.com/nz/store/curry-culture-indian-kitchen-%26-bar/y7F8v4P-XNav4LB9QAreiw`
(the owner supplied this URL directly — the assistant does not scrape/guess
real business URLs). It appears as the primary CTA in the header nav on all
5 pages, the homepage hero, and the contact page action row. On mobile, the
compact header only shows the logo + hamburger toggle (`.nav__cta .btn` is
hidden below 880px, same as before); "Order Online" and "Call to Book" are
duplicated as full-width buttons inside the expanding mobile menu
(`.nav__links-mobile-cta`) so they stay reachable on small screens. If the
Uber Eats store link ever changes (e.g. Uber Eats re-issues store IDs),
search-replace this URL across `index.html`, `menu.html`, `about.html`,
`gallery.html`, `contact.html`.

## Alcohol content removed (2026-09-03)

Per the owner's instruction ("not allowed for projecting alcohol"), all
drinks/alcohol marketing content was stripped from the site:
- `menu.html`: removed the entire "Drinks Menu" section (beer/cider, wine,
  non-alcoholic drinks, happy hour) and its nav-jump link; trimmed "and
  drinks" from the meta description.
- `index.html`: removed the "Full Bar" feature card (grid changed from
  `grid--3` to `grid--2` for the remaining 2 cards); removed "and a full
  bar" from the hero paragraph, meta description, and `og:description`.
- `about.html`: removed "alongside a full bar" from the story paragraph.
- **Not changed**: the business's legal name, "Curry Culture Indian Kitchen
  & Bar", still appears in titles, alt text, JSON-LD `name`, and copyright
  lines — that's the real registered business name, not alcohol marketing,
  and renaming it would misrepresent the business. Flag this distinction if
  asked to do a further alcohol-content pass.

## Outstanding TODO (also tracked in `README.md` §5.4)

- [ ] **Choose and buy a domain** — old domain has lapsed, don't chase it;
  see naming ideas in `README.md` §5.2. Nothing else in "go live" can
  finish until this is decided (canonical URLs, sitemap, robots.txt
  sitemap reference, JSON-LD `image`/`logo` URLs all still say
  `YOUR-DOMAIN-HERE` and need a global find/replace once picked).
- [ ] **Wire the contact form to a real backend** (Formspree/Netlify Forms
  etc.) — currently `contact.html`'s form just shows a JS `alert()`.
- [ ] **Add 2–3 real review excerpts** to the homepage once the owner has
  quotes they're allowed to use — do not invent/paraphrase reviews.
- [ ] Decide on hosting (Netlify/Vercel/GitHub Pages/Cloudflare Pages — see
  `README.md` §5.3) and deploy.
- [ ] After going live, update the "Website" link on the real Google
  Business Profile to point to the new domain (the old link is dead).
- [ ] Optional: replace the low-res `tandoori-chicken-drumsticks-thumb.webp`
  if a better source photo turns up.
