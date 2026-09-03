# Curry Culture Indian Kitchen & Bar — Website

A static, multi-page website for Curry Culture Indian Kitchen & Bar
(38 Tarbert Street, Alexandra 9320, Central Otago, NZ): plain HTML/CSS/JS,
styled after the restaurant's own black-and-gold menu branding, with SEO
and NZ-appropriate UI/UX built in.

---

## 1. Project structure

```
curry-culture/
├── index.html        Home page
├── menu.html          Full menu, anchor-linked sections
├── about.html         Story / ambience
├── gallery.html       Photo grid (placeholders — swap for real photos)
├── contact.html       Address, hours, map embed, enquiry form
├── css/style.css      Design system (colors, type, layout) — single stylesheet
├── js/main.js         Mobile nav toggle + active-link highlighting
├── assets/            Images, favicon.svg
├── robots.txt         Allows crawling, points to sitemap.xml
└── sitemap.xml        Page list for search engines
```

No build tools, no framework, no dependencies — open any `.html` file directly
in a browser, or serve the folder with any static file server.

---

## 2. Design decisions (UI/UX)

**Visual direction** — dark background with warm gold accents and a serif/script
display font, echoing the restaurant's own menu design and the reference
sites you shared (Kohinoor FL, Route des Indes, Loha.au): elegant, moody,
food-forward, not "generic template."

**NZ-specific UX conventions applied:**
- **Mobile-first**: most local diners search "restaurant near me" on their
  phone — nav collapses to a hamburger under 880px, tap targets are large,
  `tel:` links let people call straight from the phone number.
- **Above-the-fold clarity**: hero states what it is (Indian restaurant),
  where (implied via NZ phone/address format), and immediate actions
  (View Menu, Get Directions) — NZ consumers expect to find hours/location
  fast, not after scrolling through a slideshow.
- **Local trust signals**: star rating, review count, price range (NZ$20–30)
  shown early, linking out to real Google reviews rather than fabricated
  quotes — matches how Kiwis evaluate hospitality businesses.
- **Correct NZ formatting**: `+64 3 448 9238` phone format, NZ$ currency,
  postcode format (Alexandra 9320), `en-NZ` `lang` attribute (affects
  spelling suggestions and some search behaviour).
- **Accessibility basics**: skip-to-content link, semantic headings,
  sufficient color contrast on the dark theme, focus states on form fields,
  `aria-current` on nav links, alt-text-ready placeholders for images.
- **Dietary transparency**: vegan/vegetarian tags on menu items — increasingly
  expected on NZ hospitality sites, not just table menus.

---

## 3. SEO, explained

SEO for a small local business is mostly **technical basics + local signals**,
not tricks. What's implemented and why:

| What | Where | Why it matters |
|---|---|---|
| Unique `<title>` + `<meta description>` per page | every `.html` `<head>` | These are literally what Google shows in search results — generic/duplicate titles hurt click-through and rankings. |
| `canonical` link | every page | Prevents duplicate-content confusion if the same page is ever reachable via multiple URLs (with/without `www`, trailing slash, etc). |
| Open Graph + Twitter card tags | `index.html` | Controls how the link looks when shared on Facebook/Instagram/WhatsApp — critical for a restaurant, since most referral traffic is social shares, not organic search. |
| `Restaurant` structured data (JSON-LD) | `index.html` | Lets Google show rich results — opening hours, price range, cuisine type — directly in search, which increases click-through without ranking higher. |
| Semantic HTML (`<header>`, `<nav>`, `<main>`, `<footer>`, one `<h1>` per page) | all pages | Search engines (and screen readers) use heading structure to understand page hierarchy. |
| Fast, dependency-free static HTML | whole site | Page speed is a direct Google ranking factor; a static site with no framework/JS bundle is about as fast as it gets. |
| `sitemap.xml` + `robots.txt` | root | Sitemap tells Google every page that exists; robots.txt now allows crawling and points to the sitemap. |
| Descriptive, keyword-natural copy | all pages | "Indian restaurant in Alexandra, Central Otago" appears naturally in headings/copy — matches how people actually search, without keyword-stuffing. |

**Before/at launch, also do:**
- **Claim/verify your Google Business Profile** if you haven't already (it
  already exists with 328 reviews) — this is the single highest-impact thing
  for local SEO, more so than anything on the site itself. Update its
  "Website" link to your new domain once live (the old link currently
  redirects to an unrelated business — see the domain note below).
- Real, compressed photos with descriptive `alt` text and filenames
  (`butter-chicken-alexandra-nz.jpg`, not `IMG_2931.jpg`).
- Submit `sitemap.xml` via **Google Search Console**.
- List on NZ directories (Zomato, Yelp NZ, Neighbourly, Central Otago /
  Alexandra tourism listings) with **identical** name/address/phone
  everywhere — inconsistent NAP (Name-Address-Phone) data hurts local
  rankings.

---

## 4. How to preview locally

**Option A — just open the file**
Double-click `index.html`, or in a terminal: `start index.html` (Windows).

**Option B — a tiny local server (recommended, avoids path quirks)**
```bash
npx serve .
# then open the URL it prints, e.g. http://localhost:3000
```

**Option C — VS Code "Live Server" extension** — right-click `index.html` →
"Open with Live Server."

---

## 5. Domain & hosting walkthrough

### 5.1 About your existing domain

Your Google Business listing points to `currycultureindiankitchenandbar.com`,
but that domain currently 301-redirects to an unrelated business ("The
Mooring Fish Cafe Raro"), which strongly suggests it **lapsed and was
re-registered by someone else**. Before buying a new domain:
1. Check who owns it now via a WHOIS lookup (e.g. whois.net) to see the
   registrar and expiry/registration date.
2. If it's genuinely been re-registered by an unrelated party, you generally
   cannot get the exact name back without buying it from the current owner
   (sometimes possible via the registrar, often expensive/not guaranteed).
3. Given that, the practical path is usually to **register a fresh domain**
   (see below) and update your Google Business Profile's website link once
   the new one is live — don't wait on recovering the old one.

### 5.2 Buying a domain (NZ)

- `.co.nz` / `.nz` domains sit under the **.nz namespace**, overseen by
  **InternetNZ / the Domain Name Commission**, but you buy through an
  accredited **registrar**, not directly from them.
- Common NZ registrars: **1st Domains**, **Freeparking**, **Domainz**,
  **GoDaddy** (also sells `.co.nz`), **Namecheap** (limited NZ TLD support).
- Typical cost: **NZD $15–40/year** for `.co.nz` or `.nz`; a `.com` is often
  similar or cheaper via Namecheap or Cloudflare Registrar (at-cost, no
  markup).
- Steps: search your desired name → check availability → provide contact
  details → pay → the domain is yours, managed via the registrar's dashboard
  (DNS records live here unless you delegate DNS elsewhere, e.g. to
  Cloudflare).
- Suggestions worth checking availability for: `currycultureotago.co.nz`,
  `currycultureindian.co.nz`, `currycultureindiankitchen.co.nz`, or a fresh
  `.com` version of the original name.

### 5.3 Hosting a static site

For a plain HTML/CSS/JS site like this, a free static host is simpler and
faster than traditional web hosting, and includes HTTPS automatically:

| Host | Good for | Notes |
|---|---|---|
| **Netlify** | Easiest drag-and-drop or Git-connected deploys | Free tier is generous; custom domain + free SSL included |
| **Vercel** | Same idea as Netlify | Slight edge for anything that later grows into Next.js |
| **GitHub Pages** | Code already lives in a GitHub repo (it does — this is one) | Free, simple, custom domain supported via a `CNAME` file |
| **Cloudflare Pages** | Fastest global CDN, generous free tier | Pairs well if you also use Cloudflare for DNS |

**General flow (Netlify example):**
1. Push this folder to a GitHub repository.
2. In Netlify: "Add new site" → "Import from Git" → pick the repo → deploy
   (no build command needed for plain HTML).
3. Netlify gives you a free `*.netlify.app` URL immediately — good for
   testing before connecting the real domain.
4. In **Site settings → Domain management → Add custom domain**, enter your
   purchased domain.
5. Netlify shows DNS records to add (usually an `A`/`ALIAS` record for the
   root domain, and a `CNAME` for `www`). Add those at your registrar (or
   delegate nameservers to Netlify entirely, which is simpler if you don't
   need DNS for anything else).
6. Wait for DNS propagation (minutes to ~48 hours) — HTTPS is issued
   automatically once it resolves.

**GitHub Pages alternative (also free):**
1. Repo → Settings → Pages → set source to your `main` branch.
2. Add a `CNAME` file to the repo root containing just your domain
   (e.g. `www.example.co.nz`).
3. At your registrar, point DNS to GitHub Pages' IPs (apex domain) and add a
   `CNAME` record for `www` → `yourusername.github.io`.

### 5.4 Checklist before going live
- [ ] Buy the domain (see 5.2) and replace every `YOUR-DOMAIN-HERE`
      placeholder in this codebase with it (`index.html`, `menu.html`,
      `about.html`, `gallery.html`, `contact.html`, `robots.txt`,
      `sitemap.xml`).
- [x] Real photos added — see `assets/img/` (renamed descriptively and wired
      into the header logo, hero, homepage, about, menu category banners,
      contact page and gallery). `og:image` in `index.html` now points to
      `restaurant-exterior-evening.jpg`.
- [ ] `tandoori-chicken-drumsticks-thumb.webp` is only an 11KB thumbnail (its
      higher-resolution source file was lost during renaming) — swap in a
      full-size version if you have one, or take a fresh photo.
- [x] Opening hours confirmed and updated everywhere (JSON-LD in
      `index.html`, footer, and the per-day table on `contact.html`):
      closed Mondays, 6–9:30pm Tue–Thu, 5–9:30pm Fri–Sun.
- [ ] Deploy (5.3), then update the "Website" link on your Google Business
      Profile to point to it.
- [ ] Set up Google Search Console + submit `sitemap.xml`.
- [ ] Wire the contact form to a real backend/service (e.g. Formspree,
      Netlify Forms) — it's currently a front-end-only demo that shows an
      alert instead of sending anything.
- [ ] Add 2–3 real customer review excerpts to the homepage once you have
      permission to quote them (currently just links out to Google Reviews —
      don't invent or paraphrase quotes).

---

## 6. Suggested next steps

- Run Lighthouse (Chrome DevTools → Lighthouse tab) against the local
  preview to catch any performance/SEO/accessibility issues before launch.
- Consider adding an online ordering / reservation integration (e.g.
  OpenTable, Resy, or a simple "Order via Uber Eats/Menulog" button) if you
  want more than click-to-call.
