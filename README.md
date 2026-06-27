# Expert Visa Point — Website

A redesigned, multi-page recreation of expertvisapoint.com — a B2B visa
consultancy based in Mumbai. Built as a static site (plain HTML/CSS/JS,
no build step) so it deploys directly to GitHub Pages, Netlify, or Vercel.

## Design concept

**Theme: "The Stamped Page."** The site borrows its visual language from
passports and customs ink stamps — a recurring dashed-circle "stamp" seal
(`js/main.js` → `buildStampSVG`) is the signature element used in the hero,
about page, country pages, and the 404. Cards get a perforated bottom edge
like a ticket stub. The palette pairs a deep "ink navy" with passport gold
and a visa-stamp red; headings use Fraunces (a serif with character), body
copy uses Inter, and data/labels use Space Mono for a document-like feel.

## Pages

| File              | Purpose                                                   |
|-------------------|------------------------------------------------------------|
| `index.html`      | Home — hero, services, "what we do", certifications, destinations, CTA |
| `about.html`      | About — who we are, values, services recap                |
| `contact.html`    | Contact — form (mailto-based) + embedded Google map        |
| `visa-info.html`  | Searchable/filterable directory of 70+ destinations         |
| `country.html`    | Dynamic country detail page, driven by `?country=slug`      |
| `404.html`        | Not-found page                                             |

## How the country pages work

`js/data.js` holds a `COUNTRIES` array (slug, name, ISO-2 code, region,
visa type, typical processing time/validity) plus generic document
checklists per visa type. `country.html` reads the `country` query
parameter (e.g. `country.html?country=usa`), looks up the matching entry,
and renders the page client-side — so there's one template file instead
of 70+ duplicated HTML pages. Flags are pulled from the free
[flagcdn.com](https://flagcdn.com) CDN by ISO-2 code.

**Important:** the visa type / processing time / validity figures in
`data.js` are general, commonly-seen ranges for planning purposes —
**not** a live feed from any embassy. Update them with your team's
verified figures before relying on them, and keep the on-page disclaimer.

## Editing content

- **Services, copy, stats:** edit directly in the relevant `.html` file.
- **Countries:** add/edit entries in the `COUNTRIES` array in `js/data.js`.
  Each entry needs `slug`, `name`, `iso2`, `region`, `type`
  (`evisa` / `voa` / `sticker` / `free`), `processing`, and `validity`.
- **Logo:** currently linked directly from the Shopify CDN URL provided.
  To self-host, download it into `assets/img/logo.png` and update every
  `<img src="https://cdn.shopify.com/...">` reference to `assets/img/logo.png`.
- **Contact form:** currently opens the visitor's email client via
  `mailto:`. To collect submissions silently, point the form at a service
  like [Formspree](https://formspree.io) or your own backend endpoint and
  remove the `mailto` script in `contact.html`.
- **Map:** the embedded iframe in `contact.html` uses a Google Maps
  query URL — replace the address in the `q=` parameter if the office
  moves.

## Local preview

No build tools needed — just open `index.html` in a browser, or serve the
folder locally:

```bash
npx serve .
# or
python3 -m http.server 8080
```

## Deploying

**GitHub Pages**
1. Push this folder to a GitHub repo.
2. Repo → Settings → Pages → Source: `main` branch, `/ (root)`.
3. Your site will be live at `https://<username>.github.io/<repo>/`.

**Netlify / Vercel**
Drag-and-drop the folder, or connect the repo — no build command needed
(static site, publish directory = root).

## Structure

```
.
├── index.html
├── about.html
├── contact.html
├── visa-info.html
├── country.html
├── 404.html
├── css/
│   └── style.css
├── js/
│   ├── data.js
│   └── main.js
└── README.md
```

## Credits

Logo supplied by Expert Visa Point. Flags via flagcdn.com. Fonts via
Google Fonts (Fraunces, Inter, Space Mono).
