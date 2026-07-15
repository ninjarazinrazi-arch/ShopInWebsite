# Handoff: ShopinEcom Marketing Website

## Overview
ShopinEcom is a done-for-you eCommerce **marketplace-growth agency**. This package is the complete marketing website: a homepage plus a full Services experience (mega menu + a dedicated page per service), an About page, a Case Studies library with detail pages, a Contact / free-audit page, and Resources/Privacy stubs. The site's job is to build trust fast with real proof (Seller Central screenshots, verified results, testimonials) and drive visitors to **book a call / request a free growth audit**.

Primary conversion actions, in priority order:
1. Request a free growth audit (Contact page form).
2. Book a discovery call (CTA buttons throughout).
3. Explore a specific marketplace service page.

## About the Design Files
The files in this bundle are **design references authored in HTML** — a working prototype that shows the intended look, copy, layout, and interaction behavior. **They are not production code to ship as-is.**

The prototype is built as a single "Design Component" (`Shopinecom.dc.html`) that runs on a small in-house runtime (`support.js`). **Do not port the runtime.** The task is to **recreate these designs in the target codebase's real environment** using its established patterns and libraries. If no codebase exists yet, the recommended stack is **Next.js (App Router) + React + TypeScript + Tailwind CSS**, which maps cleanly onto the structure below.

Two representations are included so you can work from whichever is easier:
- `Shopinecom.dc.html` — the authoritative source (all copy, data arrays, and styles live here).
- `reference-build/index.html` — the same site compiled to one self-contained file. Open it in any browser to click through every page/route exactly as intended. **Read-only reference — do not edit.**

## Fidelity
**High-fidelity (hifi).** Final colors, typography, spacing, copy, and interactions are all decided. Recreate the UI pixel-faithfully using the target codebase's component library. Exact tokens, type scale, and per-component specs are documented below.

---

## Global Copywriting Rule (hard requirement)
The client **forbids em dashes (—) and en dashes (–)** anywhere in visible copy. Use commas, periods, or restructured sentences instead. The current build contains **zero** of either. Preserve this rule in all new copy.

Other voice notes: confident but credible, specific over vague, benefit-led. Marketplace names always appear with their brand logo/mark; country references use flags. Core markets are **US, UK, and Europe** (an earlier "GCC / MENA" positioning was removed, do not reintroduce it).

---

## Design Tokens

### Color (CSS custom properties as used in the build)
| Token | Hex | Role |
|---|---|---|
| `--ink` | `#16112A` | Brand core / darkest surfaces, primary text on light |
| `--ink-2` | `#1F1838` | Secondary dark (gradient partner for `--ink`) |
| `--ink-soft` | `#2A2440` | Softer dark text/surfaces |
| `--purple` | `#5A56A5` | Primary action (buttons, links, active states) |
| `--purple-d` | `#4A4690` | Purple pressed/hover-deep |
| `--lav` | `#8B88C9` | Lavender accent |
| `--lav-2` | `#E9E8F4` | Lavender tint (soft chips/backgrounds) |
| `--mist` | `#F2F3F7` | Section background (alt to white) |
| `--paper` | `#FFFFFF` | Default page background |
| `--line` | `#E7E6F0` | Hairline borders / dividers |
| `--muted` | `#6B6880` | Muted body text, captions |

**Marketplace accent colors** (used per service page + logo chips):
- Amazon `#FF9900` (→ `#FF7A00`)
- Walmart `#0071CE` / `#0071DC` + gold `#FFC220` (→ `#004B97`)
- TikTok `#FE2C55` (mark on `#111`)
- eBay `#0064D2` + `#E53238`
- International (US & EU) `#1A9455` (→ `#0B5B35`)

**Signature "Instagram" gradient** (used on the logo chip ring, accent lines, and hero flourishes — a repeated brand device the client explicitly likes):
`linear-gradient(135deg,#feda75,#fa7e1e,#d62976,#962fbf,#4f5bd5)`

### Typography
- **Display / headings:** `Cabinet Grotesk` (weights 400,500,700,800,900). Loaded from Fontshare: `https://api.fontshare.com/v2/css?f[]=cabinet-grotesk@400,500,700,800,900&display=swap`. Used at weight 700–800, letter-spacing about `-0.02em` on large headings.
- **Body / UI:** `Outfit` (300–700), Google Fonts. Default body copy.
- Self-host both fonts in production for performance and reliability.
- Base body: antialiased, `text-rendering:optimizeLegibility`. Selection color `#5A56A5` on white text.

### Spacing & rhythm
- Content column max-width: **1280px** for headers/hero rails, **1100px** for service-detail body sections (kept consistent per page). Homepage sections use up to 1280px.
- Section vertical padding: `clamp(60px, 8vw, 104px)`.
- Horizontal page padding: `clamp(20px, 4-5vw, 48-60px)`.
- Cards commonly `border-radius: 14–22px`; pills `100px`; icon tiles `11–13px`.
- Shadows are soft, low-opacity, ink-tinted, e.g. `0 20px 40px -22px rgba(22,17,42,.5)`; purple-tinted on hover, e.g. `0 24px 48px -22px rgba(90,86,165,.45)`.

### Motion
- Reveal-on-scroll: elements marked `data-reveal` fade+rise (`opacity 0 → 1`, `translateY(18px) → 0`) via `IntersectionObserver`. Keyframe `seFadeUp .6s`.
- Preferred easings: `cubic-bezier(.16,1,.3,1)` (smooth), `cubic-bezier(.34,1.56,.64,1)` (spring/overshoot for chips & lifts).
- Named effects present: marquee logo rail (`seMarquee`), gentle float (`seFloat`/`seFloatY`), shine sweep on buttons (`seShine`), live-status ping dot (`sePing`), gradient shift (`seGradShift`), number count-up flash (`seNumFlash`).
- Respect `prefers-reduced-motion` in production (reduce/disable transforms).

---

## Information Architecture / Routes
The prototype is a hash-router SPA. Recreate as real routes:

| Route (prototype) | Production path | Page |
|---|---|---|
| `#/` | `/` | Home |
| `#/services` | `/services` | Services overview (all services) |
| `#/services/:slug` | `/services/[slug]` | Service detail (see slugs below) |
| `#/about` | `/about` | About |
| `#/case-studies` | `/case-studies` | Case studies library |
| `#/case/:slug` | `/case-studies/[slug]` | Case study detail |
| `#/resources` | `/resources` | Resources |
| `#/contact` | `/contact` | Contact / free audit form |
| `#/privacy` | `/privacy` | Privacy policy |

**Service slugs:** `amazon-account-management`, `walmart-seller-management`, `tiktok-shop-management`, `ebay-store-management`, `global-expansion`.

**Case slugs:** `womens-lifestyle`, `mens-grooming`, `smart-gadgets`, `uk-flagship`, `us-scale`, `health-wellness`.

There are **two service-page templates** (a deliberate design decision — do not collapse them into one):
1. **Standard service detail** — Amazon, TikTok, International Expansion. Hero → overview/problems → what-we-manage (interactive capability tabs) → process → results/proof → related cases → testimonials → FAQ → CTA.
2. **Automation / wholesale** — Walmart and eBay. Adds a "done-for-you" narrative: 3-step ownership ribbon (You hand over → We run it 24/7 → You collect profit), a deliverables grid (10 steps Walmart / 6 eBay) with per-step icons, an investment/ROI block, and real proof videos + screenshots.

---

## Screens / Views

### Header + Services Mega Menu (global)
- **Layout:** sticky top bar, height ~74px, max-width 1280px. Left: logo (gradient-ring chip `assets/logo-mark-purple.png` + wordmark "Shopin" in `--purple` / "ecom" in ink). Center/right: nav links (Services with mega trigger, plus Case Studies, About, Resources). Far right: primary CTA button "Book a call" (`--purple` fill, white text, arrow icon, `border-radius` ~11px, `white-space:nowrap`).
- **Header theming:** on the **home** route the hero is dark, so the header sits transparent-to-translucent over it and text is light; after scroll (`scrolled` state) it becomes solid white with ink text. On all other routes it is solid/light from the top.
- **Mega menu (desktop):** absolutely-positioned panel below the bar, white, `box-shadow:0 40px 80px -36px rgba(22,17,42,.35)`, enters with `seFadeUp .24s`. Grid `repeat(auto-fit, minmax(560px,1fr))`. Left column = "Marketplaces we manage" service cards; each card: 40×40 logo chip (brand-gradient background), title (Cabinet Grotesk 700, 14.5px), one-line description (`--muted`, 12.5px), and a slide-in arrow (`.se-mega-arrow`, opacity 0 → 1 + translateX on hover). A dashed "View all services" card closes the list. Card hover: background `--mist`, `translateX(4px)`, logo chip `scale(1.1) rotate(-4deg)`.
- **Mobile nav:** the mega menu must collapse into an accordion/drawer — full-screen or slide-in panel, each marketplace a large tappable row (≥44px), same icon + title + description, expandable sub-links. CTA pinned.

Mega-menu service cards & copy:
- **Amazon Account Management** — "PPC, listings, A+ content and account health, run as one profit engine."
- **TikTok Shop Management** — "Creator-led commerce that turns attention into orders."
- **Walmart Seller Management** — "Approval to advertising, managed end to end."
- **eBay Store Management** — "Listings, promotions and feedback, compounding quietly."
- **International Expansion** — "US, UK and Europe. Launch and scale across premium Western markets."

### Home
Section order (all present in `reference-build/index.html`, ~21 sections):
1. **Hero** (dark, `--ink`): H1 "Marketplace growth, managed end to end." + subcopy + dual CTA (Book a call / See results). Trust badge pill ("Amazon Ads Verified Partner", uses `badges/amazon-verified-partner.webp`) and a live Seller Central proof screenshot (`proof/seller-central-3-38m.webp`) with a floating "£3.38M" stat label. A row of marketplace logos (Amazon, Walmart, eBay, TikTok Shop, Shopify) aligned on one/two lines. Add a small bottom padding under the logo row.
2. **Stat / counter band** — animated count-up numbers (managed sales, growth, ACoS improvement).
3. **Six channels, one obsession** — marketplace capability cards, each with the real platform logo (no duplicate Shopify).
4. **"Pick a marketplace, see exactly how we grow it"** — interactive marketplace selector; per-platform challenges → services → outcome. Data in `marketplaceData()`.
5. **Proof: real numbers, real screenshots** — grid of Seller Central account screenshots (`proof/account-screenshots/account-ss-*.webp`) each with a styled value label (e.g. "$1.78M", "+416%") and caption.
6. **Featured case study** + secondary case cards (metric chips like "3x", "~20%", tag chips like "Amazon", "PPC & Listings", "Read story" button).
7. **The difference a managed account makes** — comparison (managed vs. unmanaged / typical agency).
8. **Testimonials** — "Brand owners, unscripted." carousel.
9. **What we manage, all under one roof** — Amazon/Walmart/eBay/TikTok blocks with relevant logos.
10. **The full picture, not just the ads** — full-funnel capability visual.
11. **Your embedded team** — role cards (expandable on tap/click; must clearly signal expandability on mobile).
12. **International expansion (US, UK, Europe)** — country flags as icons.
13. **Process: from first call to compounding growth** — numbered step circles filled with the Instagram-style multi-color gradient; tap a step to preview it.
14. **Cross-platform launches / expansion** — for brands already on one marketplace expanding to another (Amazon → TikTok Shop / Shopify / Walmart / eBay). Clear, visually rich, single message.
15. **Final CTA + footer** — footer includes verified-partner badge and a multi-color gradient hairline the client specifically likes (reuse the signature gradient).

### Services overview (`/services`)
Card grid of all five services (data in `servicesData()`), each with icon, name, tagline, and a short capability menu. Links to each detail page.

Service taglines:
- Amazon: "Full account ownership built for profitable, defensible growth."
- Walmart: "From account approval to advertising, run end to end on Walmart Marketplace."
- TikTok Shop: "Turn attention into orders with creator-led commerce and paid amplification."
- eBay: "Storefront, listings and promotions managed for steady, compounding sales."
- International Expansion: "Launch and scale across the US, UK and European marketplaces."

### Service detail — standard (Amazon / TikTok / International)
Per-service content lives in `details()` and `servicesData()`. Structure:
- **Hero:** eyebrow (e.g. "Flagship · Amazon"), service accent color, H1 (e.g. Amazon: "Run your entire Amazon brand as one profit engine."), supporting copy, CTA, service-specific visual, and a sub-nav that scroll-jumps to sections (Overview, What we manage, Process, Results, FAQ).
- **Problems → solutions:** `ps[]` array of `{p: pain, s: solution}` pairs.
- **Who it's for:** `who[]` checklist paired with a live growth-dashboard mockup on the right (built from the service accent). Convert to a stacked layout on mobile.
- **What we manage:** interactive capability tabs (`manageList`), one panel visible at a time (`capIdx` state). Each capability must clearly look clickable; the active panel opens below. On mobile use an accordion so a first-time user sees content without guessing.
- **Process, outcomes (`outcomes[]`), FAQ (`faqs[]`), related case studies (3), and a final CTA.**

### Service detail — automation (Walmart / eBay)
Data in `autoData()`. Adds:
- **3-step ownership ribbon:** Step 1 "You — Hand over the store" (brand gradient), Step 2 "Us — We run it all, 24/7" (purple), Step 3 "You — Collect the profit" (green). Each: 44px gradient icon tile + eyebrow + bold label.
- **Deliverables grid:** `included[]` (Walmart 10, eBay 6). `repeat(auto-fit, minmax(230px,1fr))`. Each card: white, `border-radius:16px`, a filled brand-gradient 46px icon tile with a **distinct icon per step** (from the item's `ic` key: search, supplier, inventory, ship, wfs, fbm, listing, orders, support, scale), a faint step number top-right, bold title. Hover: `translateY(-4px)` + deeper shadow.
- **Gradient CTA bar** to close the section ("Ready to hand it over? → Start automation").
- **Investment / ROI block:** two figures rendered on single lines each (e.g. Walmart "$5,000" setup and "15 to 55%" ROI) with labels beneath; keep numbers non-wrapping.
- **Proof:** real videos + screenshots. Walmart: `assets/walmart-proof-1..3.jpeg` + `assets/walmart-proof-video.mp4`. eBay: `assets/ebay-proof-1..3.jpeg` + `assets/ebay-proof-video-1..3.mp4`. Keep each screenshot presented on one "page"/card, not split.

Automation copy — badges: Walmart "Done-for-you Walmart wholesale", eBay "Done-for-you eBay wholesale". Hero titles: Walmart "Walmart Marketplace, run end to end.", eBay "A managed eBay store that sells while you sleep."

### Case Studies library + detail
`caseData()` holds six studies, each: `slug, market, cat, brand, title, metric, metricLabel, sub, challenge, audit, [work], result, quote, quoteName`. Library = filterable card grid (metric chip, market/category tags, "Read story"). Detail page = challenge → audit → work → result narrative with the pull quote and metric callouts. Representative results (all framed as verified brand-owner outcomes; keep the "results vary" disclaimer, and give that disclaimer adequate contrast):
- Women's Lifestyle (Amazon, Full account): ACoS 60%+ → stable ~20%.
- Men's Grooming (Amazon, PPC & Listings): 3x revenue, no added ad spend.
- Smart Gadget (Amazon, Content & CRO): conversions doubled (2x).
- Amazon UK (Full account): £3.38M ordered product sales across 104,863 orders (May 2024–May 2026).
- Amazon US (PPC & Scale): $1.78M sales at +416% growth.
- Health & Wellness (Amazon US, Full funnel): +224% sales, full-funnel not just PPC.

### Contact / free audit (`/contact`)
Lead form ("The growth leak scanner" / free audit). Fields captured via `setField` / `submitForm` (name, email, brand/URL, marketplace, monthly revenue, message). **Currently client-side only — no backend.** In production, wire to a real endpoint/CRM (e.g. HubSpot, or an API route emailing the team) with validation, success/error states, and spam protection. Include the primary CTA and a reassuring, benefit-led intro.

### About / Resources / Privacy
About tells the agency story + embedded-team model. Resources is a content stub. Privacy is a policy stub. Keep consistent with the system.

---

## Interactions & Behavior (summary)
- **Scroll progress bar** at the very top (fills as the page scrolls).
- **Reveal-on-scroll** via IntersectionObserver on `data-reveal` elements.
- **Mega menu:** open on hover/focus (desktop) and tap (mobile); arrow rotates 180°; closes on outside click / route change.
- **Capability tabs** (service pages): click to switch active panel (`capIdx`); active state uses the service accent.
- **FAQ accordions:** `toggleFaq` open/close one item.
- **Marketplace selector** (home): switching updates challenges/services/outcome.
- **Process steps:** tap a numbered (gradient-filled) circle to preview that step.
- **Testimonials carousel:** advance/prev.
- **Count-up stats:** animate when scrolled into view.
- **Live-status dots:** blinking green ping (`sePing`) to signal "live/verified".
- **Video proof:** click-to-play with a scale-up play button on hover.
- All hover lifts, shine sweeps, and float loops listed under Motion.

## State Management
Prototype state (recreate with your framework's router + local component state / a light store):
- `route` = `{ name, slug }` from the URL (use the real router).
- `scrolled` (bool) — header theming.
- `megaOpen`, `waOpen` (menu/drawer open flags).
- `capIdx` (active capability tab per service page).
- `faqOpen` (open FAQ index).
- Marketplace-selector index, testimonial index, count-up "in view" flags.
- Contact form field values + submit status.
All page content is **static data** (the `servicesData()`, `details()`, `caseData()`, `marketplaceData()`, `autoData()`, `renderTestimonials()` arrays). In production, move these into typed data modules or a CMS.

## Assets
Bundled locally (in `assets/` and `brand/`):
- `assets/logo-mark-purple.png`, `assets/logo-mark-dark.png` — logo marks.
- `assets/walmart-proof-1..3.jpeg`, `assets/walmart-proof-video.mp4` — Walmart proof.
- `assets/ebay-proof-1..3.jpeg`, `assets/ebay-proof-video-1..3.mp4` (+ `ebay-proof-video.mp4`) — eBay proof.
- `brand/img-1..7.jpg` — brand guideline boards (logo system, color palette, type system) for reference; `brand/_icons_preview.png`, `brand/_pick.png`.

Loaded from ShopinEcom's own CDN `https://growth.shopinecom.com/` (confirmed reachable; **download and self-host before launch**):
- `badges/amazon-verified-partner.webp` — verified partner badge.
- `proof/seller-central-3-38m.webp`, `proof/seller-central-1-14m.webp` — hero/positioning screenshots.
- `proof/account-screenshots/account-ss-{04,06,13,15,22,31}.webp` — proof grid.
- `logos/{ecom-hot-sauce,benz-hawk,byld-commerce,afm,extreme-commerce,orrys-vital,my-protect-kit,canarie-shirts,dot,bd}.webp` — client logos.

Marketplace brand logos (Amazon, Walmart, eBay, TikTok Shop, Shopify) should be the **official brand assets** at production — source them from each platform's brand/press kit and respect usage guidelines. Fonts: Cabinet Grotesk (Fontshare), Outfit (Google Fonts).

## Files in this bundle
- `Shopinecom.dc.html` — authoritative design source (all markup, copy, data, styles).
- `support.js` — the prototype's runtime. **Reference only; do not port.**
- `reference-build/index.html` — self-contained compiled site; open in a browser to click through everything.
- `assets/`, `brand/` — local images/video and brand boards.

## Implementation notes / gotchas
- **No em/en dashes** in any copy (hard client rule).
- Keep the **two distinct service templates**; don't flatten to one.
- Reuse the **signature multi-color gradient** as an intentional brand device (logo ring, accent lines, process-step circles, footer hairline) — the client explicitly likes it.
- **Mobile-first:** ~99% of traffic is mobile. Every diagram/table must have a clean vertical/stacked mobile form; tap targets ≥44px; expandable elements must visibly signal they expand.
- Watch **contrast**: several sections pair light text on light backgrounds in earlier drafts — verify WCAG AA on all body copy, especially disclaimers and captions.
- Prevent horizontal overflow (a few sections historically ran wide); constrain to the content column and test at 360px, 768px, 1280px.
- Marketplaces and countries should always render **with their logo/flag**, never as bare text.
