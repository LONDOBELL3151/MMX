# MaxFoot Dawn — Shopify Theme

A complete Shopify OS 2.0 theme converted from the static MaxFoot preview into modular `sections/*.liquid`, `snippets/*.liquid`, and `templates/*.json`. Every page is built from drag-and-drop sections in the theme editor.

## File structure

```
maxfoot-theme/
├── assets/
│   ├── maxfoot-base.css         reset, tokens, typography, layout primitives
│   ├── maxfoot-components.css   all component styles (~700 rules)
│   ├── maxfoot-responsive.css   mobile / tablet / print / a11y
│   ├── maxfoot.js               vanilla JS (drawers, qty, marquee, gallery)
│   └── maxfoot-logo.png         default header logo (replaceable in theme settings)
├── config/
│   ├── settings_schema.json     theme-wide settings schema
│   └── settings_data.json       default values
├── layout/
│   ├── theme.liquid             main layout (head, fonts, body, scripts)
│   └── password.liquid          storefront password page
├── locales/
│   └── en.default.json          translation strings
├── sections/
│   ├── header-group.liquid      wrapper for header + announcement + mobile menu
│   ├── footer-group.liquid      wrapper for footer
│   ├── announcement-bar.liquid  announcement bar with marquee
│   ├── header.liquid            main nav (logo, links, search, account, cart)
│   ├── mobile-menu.liquid       drawer nav for mobile
│   ├── footer.liquid            footer with logo, menus, newsletter, social, payment
│   ├── hero.liquid              home page hero
│   ├── proof-bar.liquid         social proof / press logos
│   ├── trust-badges.liquid      "Why shop with us" strip
│   ├── featured-collection.liquid  product grid for any collection
│   ├── why-maxfoot.liquid      3-pillar values block
│   ├── press-quote.liquid       single big pull-quote
│   ├── rider-testimonials.liquid  3-up rider reviews
│   ├── faq.liquid               accordion FAQ
│   ├── cta-strip.liquid         "Ready to ride?" call to action
│   ├── newsletter.liquid       newsletter signup form
│   ├── brand-strip.liquid       "As seen in" logo strip
│   ├── image-text.liquid        image + text split
│   ├── rich-text.liquid         centered rich text
│   ├── comparison-table.liquid  spec vs competitor table
│   ├── breadcrumbs.liquid       breadcrumbs strip
│   ├── main-product.liquid      PDP gallery + form + extras
│   ├── pdp-features.liquid     PDP "At a Glance" + story
│   ├── pdp-accordions.liquid   PDP content accordions
│   ├── pdp-pair.liquid          "Complete the ride" upsell
│   ├── pdp-recent.liquid        recently viewed placeholder
│   ├── pdp-reviews.liquid       PDP reviews summary + grid
│   ├── collection-banner.liquid  collection page banner
│   ├── facets.liquid            filter sidebar (desktop + mobile drawer)
│   ├── main-collection.liquid   collection grid + toolbar + pagination
│   ├── main-cart.liquid         cart line items + summary + recommendations
│   ├── page-hero.liquid         generic page hero (yellow/black/soft)
│   ├── story-split.liquid       about-us story (image + text)
│   ├── values-grid.liquid       3 values with big numbers
│   ├── timeline.liquid          vertical milestone timeline
│   ├── stats.liquid             4-up stat counters
│   ├── contact-channels.liquid  4 contact methods
│   ├── contact-form.liquid      contact form + hours + map
│   ├── blog-hero.liquid         blog page hero
│   ├── main-blog.liquid         blog featured + grid
│   ├── post-header.liquid       article hero with author + share
│   ├── post-content.liquid      article body with tags
│   ├── author-card.liquid       post author EEAT card
│   ├── related-posts.liquid     related articles
│   └── main-404.liquid          404 with search + popular pages
├── snippets/
│   ├── icon.liquid              SVG icon library (cart, search, truck, etc.)
│   ├── meta-tags.liquid         Open Graph + Twitter card
│   ├── breadcrumbs.liquid       breadcrumb nav
│   ├── product-card.liquid      reusable product card
│   ├── product-media.liquid     product gallery + thumbnails
│   ├── price.liquid             price block (current + compare + save)
│   ├── stars.liquid             5-star rating
│   ├── free-shipping-bar.liquid shipping progress bar
│   ├── cart-drawer.liquid       slide-out cart drawer
│   ├── post-card.liquid         blog post card
│   └── share-buttons.liquid     social share row
└── templates/
    ├── index.json               home page
    ├── product.json             PDP (galleries, accordions, reviews, etc.)
    ├── collection.json          PLP (banner + facets + grid + pagination)
    ├── cart.json                /cart
    ├── blog.json                /blogs/news
    ├── article.json             /blogs/news/<article>
    ├── search.json              /search
    ├── list-collections.json    /collections
    ├── 404.json                 404 page
    ├── password.json            storefront password
    ├── page.json                generic CMS page
    ├── page.about-us.json       about page
    ├── page.contact.json        contact page
    └── customers/blog.json      alternate blog template
```

## Installation

1. Zip the `maxfoot-theme/` folder.
2. In Shopify admin: **Online Store → Themes → Add theme → Upload zip file**.
3. Click **Customize** to open the theme editor.
4. Replace placeholder content (logo, hero image, products, blog posts) — every section exposes its own editable settings.

## Theme settings

Accessible via **Customize → Theme settings** (top of left sidebar):

- **Logo**: image picker, height (desktop/mobile), invert
- **Colors**: 11 color tokens (primary, accent, bg, text, etc.)
- **Typography**: 3 Google Fonts + base size
- **Layout**: page width, section padding, border radius
- **Social media**: Facebook/Instagram/Twitter/YouTube/TikTok URLs
- **Favicon**: image picker
- **Currency format**: show currency codes
- **Cart**: drawer vs page, free shipping threshold + message
- **Animations**: enable scroll animations, marquee

## Per-section editable settings

Each section is **schema-tagged** so it appears in the theme editor with its own settings panel. Examples:

- **Header** → menu links, search toggle, account toggle, sticky, color scheme
- **Hero** → eyebrow, title (with `<em>` highlight), subtitle, 2 buttons, image, badge, height, image position, bg color
- **Featured collection** → heading, subheading, collection picker, products count, columns, view-all toggle
- **FAQ** → heading, CTA, blocks of question/answer (defaults to 5 questions)
- **Main product** → stock toggle, finance line, extras (block of icon + title + subtitle)
- **Contact channels** → blocks of channel with type/icon/title/CTA/featured
- **Comparison table** → 3 column labels + disclaimer + blocks of row spec

You can add/remove/reorder blocks freely — for example, adding a third button to the hero, removing a FAQ question, or changing how many products show in a featured grid.

## Color system

All colors are theme settings, set via CSS custom properties on `:root`:

```css
:root {
  --color-primary: #121212;       /* black */
  --color-accent: #FFC000;        /* yellow */
  --color-accent-dark: #E6AC00;
  --color-bg: #FFFFFF;
  --color-bg-soft: #F7F7F5;
  --color-text: #1A1A1A;
  --color-text-soft: #6A6A6A;
  --color-border: #E5E5E5;
  --color-success: #1F7A4D;
  --color-danger: #C83A3A;
  --font-display: 'Big Shoulders Display';
  --font-body: 'Inter Tight';
  --font-mono: 'JetBrains Mono';
}
```

Change any color in **Theme settings → Colors** and every section updates instantly.

## Notes

- **Liquid logic** assumes standard Shopify object shapes: `product`, `collection`, `cart`, `blog`, `article`, `page`, `customer`. For `current_tags` and `paginate`, the section only renders on collection pages.
- **Image lazy-loading**: every product image uses Shopify's responsive `image_url` filter with `width:` and `srcset` for retina.
- **Section settings store** as JSON inside `templates/*.json`; theme settings live in `config/settings_data.json`.
- **All icons are inline SVG** via the `icon` snippet — no font icons, no emoji.
- **Accessibility**: keyboard-friendly drawers (ESC closes), aria-labels on all icons, focus-visible outlines, prefers-reduced-motion respected.

## Before launch — content to replace

- [ ] Replace `assets/maxfoot-logo.png` with the real MaxFoot logo (already the real one, but you may want to upload a higher-res version)
- [ ] Add real product images and descriptions in Shopify admin → Products
- [ ] Create navigation menus in Shopify admin → Navigation
- [ ] Add blog posts in Shopify admin → Blog posts
- [ ] Fill in social URLs in Theme settings → Social media
- [ ] Set free-shipping threshold in Theme settings → Cart
- [ ] Configure payment providers (Shopify Payments, PayPal, etc.)
- [ ] Set up shipping zones and rates
- [ ] Test checkout end-to-end
- [ ] Submit sitemap to Google Search Console
- [ ] Run Lighthouse audit on staging