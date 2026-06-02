# NEXPHORIA RELAUNCH — MASTER BRAND BRIEF (Wave 2 rebrand)

**Read this entire file before writing a single line of code.** Every fleet agent must conform to this brief. If a UI choice isn't covered here, default to "less = more, lab-grade, premium, pharmaceutical."

---

## 1. The brand

Nexphoria is a premium **research-use-only (RUO) peptide** company. Pharmaceutical-grade, third-party HPLC verified, cold-chain shipped. Positioning: 20% above market MSRP. Aesthetic target: **what a peptide company designed by the people behind Aesop, Future, and Apple's pharmacy section would look like.**

---

## 2. Logo + identity

- Wordmark: `NEXPHORIA™` (tall, condensed, slightly squared sans)
- Mark: 4-node molecule glyph — a cross of 4 connected circles
- Tag-lockup: under wordmark, "ADVANCED PEPTIDE SCIENCE" in spaced caps (letterspacing ~0.25em)
- Available in 3 variants:
  - **Silver foil on black** (hero, master) → `/public/brand/label-black-foil.jpg`
  - **Black on pearl** (sections, cards)
  - **Olive on cream** (inline thumbnails)

Master vial render: `/public/products/vial-bpc157-hero.jpg`
3-vial box render: `/public/brand/box-3vial-set.jpg`

---

## 3. Color tokens (FINAL)

Use exactly these CSS variable names. Replace every existing color token.

```css
:root {
  --nx-ink:        #0A0A0A;   /* deep black — primary background */
  --nx-ink-2:      #141414;   /* panel, elevation */
  --nx-ink-3:      #1C1C1C;   /* card on dark */
  --nx-pearl:      #F4F2EB;   /* label cream — section bg, cards */
  --nx-pearl-2:    #ECEAE0;   /* pearl elevation */
  --nx-silver-1:   #E8E6DF;   /* foil highlight, text on dark */
  --nx-silver-2:   #B8B4A8;   /* foil mid, secondary text on dark */
  --nx-silver-3:   #8A867A;   /* tertiary text on dark */
  --nx-olive:      #7B8B4F;   /* accent / CTA / SKU chip */
  --nx-olive-2:    #5C6B3A;   /* accent hover/dark */
  --nx-olive-3:    #95A565;   /* accent light, used rarely */
  --nx-line:       rgba(232,230,223,0.12);  /* hairline on dark */
  --nx-line-dark:  rgba(10,10,10,0.10);     /* hairline on pearl */
  --nx-success:    #7B8B4F;   /* same as olive */
  --nx-warn:       #C8A24A;   /* amber, used very rarely */
  --nx-danger:     #B8463A;   /* clay red, errors only */
}
```

**KILLED — do not use anywhere:**
- `--accent #B8E04F` (acid green)
- `--accent-glow #D4F08A`
- Any green that isn't `--nx-olive` family
- Any "neon", "lime", "electric" colors

---

## 4. Typography

- **Display**: `Inter Tight` weight 600/700, letter-spacing -0.02em (load via next/font/google). Use for H1-H3, hero, big numbers.
- **Body**: `Inter` 400/500 (already loaded). Use for paragraphs, buttons, UI.
- **Mono / spec values**: `JetBrains Mono` 400 (already loaded). Use for SKU codes, dosages, LOT numbers, prices in spec tables, REF/LOT/MFG/EXP.

Sizes (tailwind):
- Hero H1: `text-6xl md:text-8xl` `tracking-tighter` `font-display` `font-bold`
- Section H2: `text-4xl md:text-5xl` `tracking-tight` `font-display` `font-semibold`
- Card title: `text-xl font-display font-semibold`
- Body: `text-base leading-relaxed`
- Eyebrow: `text-xs tracking-[0.25em] uppercase font-medium`
- Spec value: `font-mono text-sm`

---

## 5. Voice + copy rules

**Vibe:** pharmaceutical lab × premium fashion brand. Short. Declarative. Lowercase periods at end of headlines. Never excited. Never hype.

**Approved headlines/phrases:**
- "Beyond Baseline. For Research."
- "Pharmaceutical-grade peptides. Independently verified."
- "Pure compound. Verified purity. Cold chain to your bench."
- "Precision is the protocol."
- "Dare to verify. Trust the data. Repeat the result."
- "Every lot. Every vial. Third-party HPLC > 99% purity."
- "Built for serious research."

**RUO trust marks (4):**
SCIENCE-BACKED · PURE & POTENT · QUALITY ASSURED · COLD CHAIN

**Strict vocabulary bans (NEVER appear anywhere on site):**
nootropic, cognitive (as benefit), mental clarity, focus (as benefit), wellness, ritual, supplement, vitamin, biohack, miracle, breakthrough, transform (as benefit), elevate (as benefit), unlock, journey, potential, dream, defy, transcend, peak, pinnacle

**RUO compliance — must appear:**
- Top thin ribbon: "FOR RESEARCH USE ONLY · NOT FOR HUMAN OR VETERINARY USE"
- Repeated in footer
- Repeated in checkout before submit button
- Repeated on every PDP near pack selector

---

## 6. Information architecture (FINAL — 7 routes + legal)

```
/             Home
/shop         PLP — all 14 SKUs, filter by category
/quiz         60-second protocol quiz → personalized stack
/p/[slug]     PDP — vial render, pack selector, spec, COA, FAQ
/cart         Cart
/checkout     Checkout (single page, guest by default)
/about        Story + science + RUO statement
/contact      Form + wholesale CTA
/legal        Terms + Privacy + RUO (single page, footer)
```

**DELETE THESE ROUTES + all their links:**
- `/protocols`, `/protocols/[slug]` and any protocols hub pages
- `/journal`, `/journal/[slug]` blog
- `/compare`
- `/coa` (hub) — keep COA PDFs inline on PDP only
- `/account`, `/account/*`
- `/admin`, `/admin/*`
- `/affiliate`, `/affiliates`, `/affiliate/*`
- `/stack-builder` standalone
- `/faq` (move content to Home accordion)
- `/shipping`, `/returns` (move to checkout copy + footer)
- `/wholesale` (move to /contact)
- `/style-guide` if any

Update every reference in nav, footer, sitemap, and internal links.

---

## 7. Pack size language (FINAL — use exactly this)

Replace every "1x / 3x / 6x" reference with:

```
1-MONTH PROTOCOL     1 vial · 10mg          $89
3-MONTH STACK        3 vials · 10mg ea     SAVE 10%   $240
6-MONTH RESERVE      6 vials · 10mg ea     SAVE 20%   $427
```

- Duration is the headline
- Vial count + content is sublabel
- Savings on the right
- Use `font-mono` for prices

Pack selector component: `<PprPackSelector>` — segmented control style, 3 radio options, click changes selected pack + price + Add-to-Cart updates.

---

## 8. Conversion mechanics (build into every page where relevant)

- **Top RUO ribbon** (40px tall): pearl text on ink, dismissible cookie one-time
- **Trust strip 2** below nav on home: 4 trust marks, mono caps, silver-2
- **Sticky mobile buy bar** on PDP (fixed bottom): price + pack + Add
- **Cart drawer** opens on add-to-cart (right-side slide-in, never full nav)
- **Free shipping > $150** — show progress bar in cart drawer
- **Exit-intent overlay** on home (desktop): "First protocol? Take the 60-sec quiz." dismissible cookie
- **Pre-checkout trust strip** above submit button
- **Apple Pay / Shop Pay buttons FIRST**, card form second
- **Guest checkout default**, no account creation gate
- **10% off first order** email capture in footer + after first add-to-cart

---

## 9. Motion direction

- Hero vial: 0.5° tilt on mouse parallax (desktop), kenburns on mobile
- Section reveals: 200ms fade + 8px up on scroll, respect `prefers-reduced-motion`
- Pack selector: morph pill highlight + price counter animate
- Buy button: silver-foil shimmer on hover (CSS gradient sweep 0.6s)
- Cart drawer: spring slide-in via framer-motion
- Quiz cards: 300ms slide between questions

**NEVER:**
- Autoplay video
- Parallax scrolljacking
- Bouncing pills, glowing rings, pulsing badges
- "In stock" green badges
- Emoji
- Confetti

---

## 10. Mock product data — DO NOT BREAK SHAPE

Files locked, edit additively only:
- `src/lib/mock-products.ts` (14 SKUs, packPrices {one,three,six})
- `src/lib/cart-store.ts` (Zustand)
- `src/lib/mock-protocols.ts`, `mock-citations.ts`, `mock-journal-articles.ts`
- `src/lib/mock-account.ts`, `mock-admin.ts`, `mock-affiliate.ts`

If you need a field that doesn't exist, add it additively, document in commit message.

---

## 11. Commerce adapter — migration-ready (NEW for Wave 2)

Create `src/lib/commerce/index.ts` exporting a single interface:

```ts
export interface CommerceAdapter {
  getProduct(handle: string): Promise<Product | null>;
  listProducts(filter?: ProductFilter): Promise<Product[]>;
  // cart ops go via cart-store; checkout creates an Order
  createOrder(input: OrderInput): Promise<OrderResult>;
  getQuizStack(answers: QuizAnswers): Promise<Stack>;
}
```

v1 implementation: `src/lib/commerce/local.ts` reads from `mock-products.ts`.
Future v2: `src/lib/commerce/shopify.ts` calls Shopify Storefront API.

All pages import from `src/lib/commerce`, never from `mock-products` directly.

Product shape MUST align with Shopify: `handle`, `title`, `vendor`, `productType`, `tags[]`, `variants[].price`, `variants[].compareAtPrice`, `images[].url`, `descriptionHtml`.

---

## 12. Payments (v1)

- Use a hosted checkout-redirect placeholder: after "Place Order" click, redirect to `/checkout/pending` with order summary + a "we'll email a secure payment link" copy block. Real gateway wires in once user's high-risk MID approval lands.
- Show payment method icons in checkout: Visa, MC, Amex, **Apple Pay**, **Shop Pay**, **Crypto** (Coinbase Commerce logo), and **ACH** (auto-shown when cart > $250).
- All payment buttons are placeholder/disabled with copy "Available at checkout."

---

## 13. Other 13 SKU images

Until AI-generated black-foil renders exist for the other 13 SKUs, use this fallback component: `<PprVialPlaceholder compound="TB-500" mg="5MG" />` that renders a black card with silver-foil-styled compound name. Same dimensions as the real BPC-157 hero render.

**This component must be created in Wave 1.** Don't use any of the old `/public/products/*.png` or `*.webp` placeholder files. Those are AI-template look and will be deleted.

---

## 14. Component prefix

Keep `Ppr` prefix (legacy namespace). New components: `PprPackSelector`, `PprVialPlaceholder`, `PprTrustStrip`, `PprRUORibbon`, `PprCartDrawer`, `PprQuizCard`, etc.

---

## 15. Routing cleanup — exact files to delete

```
src/app/protocols/                    DELETE entire folder
src/app/journal/                      DELETE entire folder
src/app/compare/                      DELETE entire folder
src/app/coa/                          DELETE entire folder (PDF assets stay in /public/coa)
src/app/account/                      DELETE entire folder
src/app/admin/                        DELETE entire folder
src/app/affiliate/                    DELETE entire folder
src/app/affiliates/                   DELETE entire folder (if exists)
src/app/stack-builder/                DELETE entire folder
src/app/faq/                          DELETE entire folder
src/app/shipping/                     DELETE entire folder
src/app/returns/                      DELETE entire folder
src/app/wholesale/                    DELETE entire folder (merge into /contact)
src/app/style-guide/                  DELETE if exists
```

Then run `rg -l "from '@/app/protocols\|/protocols\|/journal\|/compare\|/coa\|/account\|/admin\|/affiliate\|/stack-builder\|/faq\|/shipping\|/returns\|/wholesale'"` and clean every import + nav link.

---

## 16. Build verification

Every agent before pushing must:
1. `npm run build` succeeds (Next.js static export, no errors)
2. No console errors in `npx next dev` for the pages they touched
3. No references to killed routes anywhere in their changes
4. No "acid green" (`#B8E04F`) or banned vocab in their changes
5. Commit + push to their own branch, open PR to `main`

---

## 17. Pinned reference images

- `/public/products/vial-bpc157-hero.jpg` — PDP hero photo (use for BPC-157 specifically)
- `/public/brand/label-black-foil.jpg` — label design spec (do not embed on site, use for reference only)
- `/public/brand/box-3vial-set.jpg` — 3-vial box, use as "what ships" visual in checkout + about

---

End of brief. Build accordingly.
