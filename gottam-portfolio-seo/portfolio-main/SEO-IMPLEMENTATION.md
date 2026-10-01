# SEO Implementation Report: https://gottam.netlify.app/

Hosting: Netlify (config in `netlify.toml`). Preferred URL: `https://gottam.netlify.app/` (HTTPS, no trailing-slash variants, `/index.html` 301 to `/`).

## Site structure
Single-page portfolio, so there is one indexable page (`/`). `intro.html` is the animated intro loaded in an iframe: it is `noindex,nofollow`, canonical to `/`, and excluded from the sitemap. Breadcrumbs and multi-page internal linking were intentionally not added (no sub-pages exist; adding thin pages would hurt SEO).

## Work completed
- **On-page:** unique title (60 chars) and meta description (153 chars), one H1, H2/H3 hierarchy kept, canonical, robots `index,follow` plus max-snippet/max-image-preview.
- **Social:** full Open Graph (profile type) and Twitter `summary_large_image`, with a new 1200x630 `og-image.jpg`.
- **Schema (JSON-LD, linked by @id):** `Person`, `WebSite`, `ProfilePage`. Only facts already on the site are used (name, job title, employer, Jaipur, email, phone, GitHub, education). No reviews, ratings, prices, awards or invented addresses.
- **Images:** descriptive filenames, descriptive alt text, width/height (no layout shift), 500w/640w `srcset` variants, hero image has `fetchpriority=high` plus preload and is not lazy-loaded; below-the-fold images are lazy and async-decoded.
- **Performance:** Google Fonts loaded non-render-blocking (with `<noscript>` fallback), cache headers for `/assets/*`, security headers.
- **Accessibility:** skip link, `<main>`, labelled navs, `aria-expanded` on the menu button, form labels, autocomplete attributes, visible focus states, 44px menu button, decorative marquee/chips hidden from screen readers, descriptive link labels.
- **Internal links:** footer navigation (About, Expertise, Experience, Contact, Back to top).

## Files created
`robots.txt`, `sitemap.xml`, `llms.txt`, `manifest.webmanifest`, `netlify.toml`, `404.html` (custom, noindex, absolute asset paths), `assets/og-image.jpg`, `assets/icon-192.png`, `assets/icon-512.png`, `assets/apple-touch-icon.png`, resized `*-500.webp` / `*-640.webp` images.
Not created (not useful here): `.htaccess` (Netlify, not Apache), `humans.txt`, `security.txt`.

## Files modified
`index.html` (head, body semantics, images, accessibility), `intro.html` (noindex, neutral title, canonical). Images renamed to descriptive names; the resume PDF name is unchanged.

## Redirects / status codes
`/index.html` to `/` (301, no chains). Netlify serves `404.html` with a real 404 status for unknown URLs.

## Tested
Validated locally (1 H1, no duplicate IDs, JSON-LD parses, sitemap/manifest parse, all local files and anchors resolve, all images have alt and dimensions, no horizontal overflow at 390/768/1280 px, no broken images, no localhost/placeholder strings).
Not testable offline: live Lighthouse/PageSpeed scores, the Netlify headers and redirect behaviour, and Google Fonts loading.

## Manual actions still needed
1. Deploy to Netlify and confirm `https://gottam.netlify.app/robots.txt`, `/sitemap.xml` and a random bad URL (404 page) work.
2. Add the property in Google Search Console, submit `sitemap.xml`, and request indexing for `/`. Bing Webmaster Tools is optional.
3. A `*.netlify.app` subdomain ranks weakly for brand trust. A custom domain is recommended; if you add one, replace `gottam.netlify.app` in `index.html`, `robots.txt`, `sitemap.xml`, `llms.txt`, `intro.html` and `404.html`, then set it as the primary domain in Netlify.
4. Google Business Profile does not apply (no storefront or service-area business is stated).
5. The contact form is `mailto:`-based. A hosted form (e.g. Netlify Forms) would be more reliable, but it changes behaviour, so it was left as is.
6. No rankings can be guaranteed. Adding real project case studies and a sub-page per service later would give more indexable content.
