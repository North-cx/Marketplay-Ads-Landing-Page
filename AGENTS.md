# Project: GamsGo Marketplace Ads Landing Page

## Goal

Build and maintain a mobile-first single-page landing page for Google Ads traffic. The page should feel credible, refined, and conversion-oriented while helping users quickly scan GamsGo marketplace subscription deals and click through to product pages.

## Tech Stack

- Static site only.
- Primary file: `index.html`.
- Styling: Tailwind CDN plus small custom CSS in `index.html`.
- No build step.
- Local preview: use a static server such as `python -m http.server`; direct file preview may not load `assets/products.json` because products are fetched.
- Mobile-first responsive behavior using Tailwind `sm`, `md`, and `lg` breakpoints.

## Current File Structure

```text
index.html
DESIGN.md
AGENTS.md
assets/
  products.json
  hero-banner.webp
  22b7fdc1-88cd-4818-bd2c-17209b23ead6.webp
  fe3c7e6f-8a1c-436c-9a1e-a0696d533334.webp
```

## Brand And Visual System

- Brand red: `#ef534f` via `--brand`.
- Heading text: `#111827`.
- Muted text: `#6B7280`.
- Success/save green: `#10B981`.
- Hero background: subtle red-to-white gradient.
- Font: `Plus Jakarta Sans`, with Inter/system fallbacks.
- Logo: `https://static.gamsgocdn.com/image/6c0c5709ee54b72f9d153f6013a152dd.webp`.
- Do not distort, invert, recolor, or force-resize the logo beyond its natural width/height attributes unless explicitly requested.

## Page Structure

1. Sticky top header:
   - Red background.
   - Original GamsGo logo.
   - White outlined rounded language pill with globe icon and current language label.
   - Do not add search or hamburger/menu buttons unless explicitly requested.

2. Hero:
   - Main title: `Premium Subscriptions, Fraction of the Cost.`
   - Short subtitle: `Shared premium plans with instant setup, clear pricing, and DealShield protection.`
   - Trust bar: `DealShield Protection`, `4.8/5`, `12k+ users`.
   - Weak urgency line: red dot + `Updated just now &middot; Limited deals available`.
   - Desktop only: right-side hero image.

3. Product grid:
   - Compact service filter pills sit directly above the product grid on mobile and desktop.
   - Filters include: All, Netflix, YouTube, Prime Video, Disney+, Gemini, DAZN, Runway, Xbox.
   - The All view is shuffled on every refresh, while preserving tier order:
     - Tier 1: Netflix, YouTube, Prime Video.
     - Tier 2: Disney+, Gemini, DAZN.
     - Tier 3: all other services.
   - Mobile: 2 columns.
   - Desktop: 4 columns.
   - Product cards are entire clickable outbound links.
   - No card-level internal CTA buttons.
   - No mobile bottom fixed Buy Now bar.
   - Product card metadata shows seller, merchant star rating, and compact sold count when available.
   - Each non-All filter changes the bottom `View all deals` link into that service's GamsGo account entry.

4. Benefits strip:
   - Four items: Low Price, Genuine, Instant, Guaranteed.
   - Mobile stays a four-column grid.

5. Trust/FAQ:
   - DealShield support messaging.
   - User reviews.
   - Native `details/summary` FAQ accordion.

6. Footer:
   - Compliance disclaimer.
   - Terms and refund links.

## Product Data

Product card content is loaded from:

```text
assets/products.json
```

Do not hardcode product cards in HTML. To add or update products, edit the JSON config.

Each product object should include:

- `sku`
- `offerId`
- `title`
- `displayTitle`
- `displaySubtitle`
- `i18n`
- `seller`
- `service`
- `image`
- `price`
- `official`
- `period`
- `link`
- `typePlanId`

Current product imagery:

- Netflix: `assets/22b7fdc1-88cd-4818-bd2c-17209b23ead6.webp`
- YouTube: `assets/fe3c7e6f-8a1c-436c-9a1e-a0696d533334.webp`

Product image containers use a `16 / 9` ratio. The square source images should be centered and height-fit with no horizontal stretching.

## CTA And Tracking

- Product links and GamsGo entry links append the shared Google Ads parameters:
  `utm_source=google&utm_medium=cpc&utm_campaign=GG_Suppliers_260604&promote=Z3UNq`.
- Do not add `utm_content` or `utm_term` back to outbound URLs.
- Product card clicks fire:
  `gtag("event", "cta_click", { sku, offer_id, event_category: "outbound", event_label })`.
- Product cards navigate in the current tab.
- Only the bottom `View all deals on GamsGo ->` link opens in a new tab.
- Keep `page_view` tracking.
- Do not remove or bypass UTM and GA4 tracking logic when making UI changes.

## Pricing

- Live price fetch:
  `POST https://mapi.gamsgo2.com/index/planDetail`
- Request body includes:
  `language`, `show_currency`, and `type_plan_id`.
- Use `data.total_price` when available.
- Use `data.merchant_comment_rate` when available and convert percent to a one-decimal star score by mapping `80%` -> `1.0` and `100%` -> `5.0`.
- Use `data.merchant_comment_num` when available and display it as a compact sold count, e.g. `1731` -> `1.7k`.
- Keep fallback prices from `assets/products.json` on API failure.

## i18n

- Default locale is English.
- Copy is stored in the `COPY` object in `index.html`.
- Supported locales: `en`, `fr`, `de`, `es`, `pt`, `it`, `ko`, `ar`.
- Product title/subtitle translations live under each product's `i18n` object in `assets/products.json`.
- Arabic uses RTL direction.
- Locale is persisted in `localStorage` under `gamsgo-locale`.
- GamsGo URL locale rules:
  - English uses no language path.
  - French, German, Spanish, Portuguese, Korean, and Arabic use `/fr/`, `/de/`, `/es/`, `/pt/`, `/ko/`, and `/ar/`.
  - Italian uses the `www.gamsgo.it` domain and does not use an `/it/` path.

## SEO

- Keep `<meta name="robots" content="noindex, nofollow">` unless the campaign is explicitly approved for indexing.

## Performance

- Keep the site static and lightweight.
- Use explicit image dimensions where practical.
- Product images are lazy-loaded.
- Hero image may load eagerly.
- Avoid adding heavy libraries or complex animation.

## Compliance

- Clearly state that GamsGo is an independent third-party intermediary service.
- Do not imply official affiliation with Netflix, YouTube, or any listed brand.
- Avoid official brand UI patterns.
- Plain service labels and locally provided marketplace imagery are acceptable.

## Editing Guidance

- Preserve business logic unless the user explicitly asks to change it.
- Prefer updating CSS classes, small helper functions, or `assets/products.json` for visual/product changes.
- Keep mobile readability as the first priority.
- Do not reintroduce:
  - Bottom fixed Buy Now bar.
  - Internal card CTA buttons.
  - Emoji header icons.
  - Header search or hamburger/menu buttons.
  - Hardcoded product card HTML.
  - Separate service entry cards inside the grid.
  - Unrelated variant/stitch files.
