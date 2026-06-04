# GamsGo Marketplace Landing Page Design

## Objective

This page is a mobile-first advertising landing page for GamsGo marketplace deals. It should feel credible, compact, and conversion-oriented: users land, understand the discount/subscription value quickly, scan deals, then click a product card to continue to GamsGo.

## Brand Direction

The visual language is a refined deal-board style rather than a marketing-heavy landing page. The page should feel like a premium subscription marketplace:

- Dense enough for fast comparison.
- Clean enough to build trust.
- Red-led, but not aggressively red.
- Lightweight and readable on mobile.

## Color System

Core tokens are defined in `index.html` under `:root`.

- Brand red: `#ef534f`
  Used for the top bar, key hero emphasis, prices, and primary accents.
- Coral hover: `#FF5A4D`
  Used for warm hover/action states.
- Success green: `#10B981`
  Used for savings badges and positive trust signals.
- Heading text: `#111827`
  Used for main titles and high-emphasis content.
- Muted text: `#6B7280`
  Used for subtitles, seller metadata, original price, and secondary copy.
- Soft red background: `#FFF5F5`
  Used in the hero gradient.
- Light borders: `#E5E7EB` / low-opacity variants
  Used on cards, trust badges, and subtle separators.

## Typography

Primary font:

- `Plus Jakarta Sans`
- Fallbacks: `Inter`, system UI, sans-serif

Hero title:

- Text: `Premium Subscriptions, Fraction of the Cost.`
- Mobile: around `28px`
- Desktop: scales up to around `42px`
- Weight: `800`
- Letter spacing: `-0.03em`
- Line-height: tight but readable

Product cards:

- Title: compact, bold, max two display lines.
- Subtitle/spec: muted gray, semibold.
- Price: red, bold, clear but not oversized.
- Original price: muted gray, strikethrough.
- Metadata: small muted text.

## Layout

### Header

- Sticky top bar.
- Mobile height: `48px`.
- Desktop height: `56px`.
- Background: brand red.
- Content width aligns with the main page container: `max-w-4xl`.
- Logo uses the original remote image without filter or distortion.
- Right-side actions use inline SVG icons, not emoji.

### Hero

Hero background:

```css
linear-gradient(180deg, #FFF5F5 0%, #FFFFFF 100%)
```

Mobile:

- Single-column layout.
- Hero image hidden.
- Compact heading and short full subtitle.
- Platform chip strip visible: Netflix, YouTube, Spotify, Disney+.

Tablet/Desktop:

- Two-column layout.
- Left: heading, subtitle, trust bar, update text.
- Right: hero image in a rounded, lightly elevated frame.
- Image remains visually integrated through soft border/shadow and subtle warm background.

Hero subtitle:

`Shared premium plans with instant setup, clear pricing, and DealShield protection.`

### Trust Bar

The trust bar should read as one cohesive badge:

`鉁?DealShield Protection | 鈽?4.8/5 | 12k+ users`

Style:

- White background.
- Rounded-full pill.
- Light red-tinted border.
- Soft shadow.
- Consistent icon/text spacing.
- Single-line display where possible.

### Updated Signal

The urgency line is intentionally weaker than the price and headline:

`鈼?Updated just now 路 Limited deals available`

Only the dot uses brand red. Text uses dark gray.

## Product Grid

Grid behavior:

- Mobile: two columns.
- Desktop: four columns.
- Gap: `12px` on mobile.
- Container: `max-w-4xl`.

Cards should scan quickly and remain compact. The entire card is a clickable outbound product link.

## Product Cards

Card style:

- Rounded: `rounded-2xl`.
- Border: very light gray.
- Shadow: subtle default shadow.
- Hover: slight upward movement and slightly stronger shadow.
- Active tap: small scale-down feedback.

Image area:

- Container ratio: `16 / 9`.
- Image uses original square artwork.
- Image is centered and height-fit:

```css
mx-auto h-full w-auto max-w-full object-contain
```

This avoids horizontal stretching or cropping.

Badges:

- Service badge: top-left, white/transparent pill.
- Save badge: top-right, green `#10B981` pill.

Text hierarchy:

- Display title: first line, bold.
- Display subtitle/spec: second line, muted.
- Price: brand red, bold.
- Original price: muted gray, strikethrough.
- Seller and viewing count: small muted metadata with a divider line above.

## Product Configuration

Product content is not hardcoded in the card HTML. It is loaded from:

```text
assets/products.json
```

Each product supports:

- `sku`
- `offerId`
- `title`
- `displayTitle`
- `displaySubtitle`
- `seller`
- `service`
- `image`
- `price`
- `official`
- `period`
- `link`
- `typePlanId`

Current image assets:

- Netflix: `assets/22b7fdc1-88cd-4818-bd2c-17209b23ead6.webp`
- YouTube: `assets/fe3c7e6f-8a1c-436c-9a1e-a0696d533334.webp`
- Hero: `assets/hero-banner.webp`

## Tracking And Data Flow

The page keeps existing business behavior:

- Products load from `assets/products.json`.
- Live prices are fetched from the GamsGo plan detail API.
- Fallback prices are used if live price fetch fails.
- Product links receive Google Ads UTM parameters.
- Product card clicks fire `cta_click` with `sku` and `offer_id`.

## Compliance

Footer copy must clearly state that GamsGo is an independent third-party intermediary service and is not officially affiliated with, endorsed by, or sponsored by Netflix, YouTube, or listed brands.

Avoid using official product UI patterns. Plain service names and GamsGo-hosted product imagery are acceptable for this prototype.

## File Structure

```text
index.html
DESIGN.md
AGENTS.md
assets/
  hero-banner.webp
  products.json
  22b7fdc1-88cd-4818-bd2c-17209b23ead6.webp
  fe3c7e6f-8a1c-436c-9a1e-a0696d533334.webp
```

## Design Principles

- Keep mobile first.
- Keep red meaningful, not overwhelming.
- Keep cards compact and comparable.
- Preserve fast loading and simple static deployment.
- Do not introduce heavy animation or complex frameworks.
- Do not change business logic when making UI-only refinements.
