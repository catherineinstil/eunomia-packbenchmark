# Screen 2 — Benchmarking View: Figma Annotation Spec
**Project:** Best in Class Packaging Tool | **Screen:** 2 of 4 | **Priority:** Critical ("money shot")

---

## Purpose of this screen

For a selected product type (e.g. "1L Floor Cleaner Bottle"), show how packaging across the market compares on key attributes — highlighting best in class, median, and worst in class. This is the core value proposition of the tool. It should feel like a credible, data-rich dashboard — not a chart in a spreadsheet.

**Primary user:** CAA (regulatory body) — uses this to understand market performance and set eco-modulation fee thresholds.

---

## Screen Layout — Zones

### Zone A: Page Header
**Height:** ~64px
**Contents:**
- Back arrow + breadcrumb: `Categories / Floor Cleaners / 1L Floor Cleaner Bottle`
- Page title: `1L Floor Cleaner Bottle` (H1, bold, ~24px)
- Subtitle: `234 products benchmarked · Last updated 18 Apr 2026` (muted, ~13px)
- Top-right: `[Export ↓]` button (ghost/outline style) + `[Set fee thresholds]` button (primary, only visible to PRO/CAA users)

---

### Zone B: Attribute Benchmark Chart (primary content)
**This is the centrepiece. Give it the most vertical space.**

Each row represents one packaging attribute. Lay them out as a stacked list of horizontal range charts.

#### Row anatomy (repeat per attribute):

```
┌──────────────────────────────────────────────────────────────────┐
│ Attribute label     [i tooltip]                                  │
│                                                                  │
│  ●━━━━━━━━━━━━━━━━━━━━━━━━━━━━━●━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━● │
│  28g (Best)                  42g (Median)               67g (Worst) │
└──────────────────────────────────────────────────────────────────┘
```

**Anatomy details:**
- **Attribute label** (left-aligned, ~13px semibold, dark grey `#1A1A2E`)
- **[i] icon** — on hover shows tooltip explaining the attribute (e.g. "Lower weight = less material used")
- **Range bar** — full-width horizontal line, colour-coded:
  - Left zone (best): `#2D7D46` (muted green)
  - Middle zone (median): `#B8860B` (amber)
  - Right zone (worst): `#C0392B` (muted red)
- **Dot markers** — filled circles at best / median / worst positions
- **Value labels** below each dot — value + label (e.g. `28g` + `Best in class`)

#### Attributes to show (in this order):
1. **Weight** — numeric, unit: grams (lower = better)
2. **Recycled content %** — numeric, unit: % (higher = better)
3. **Recyclability rating** — categorical: A / B / C / D / E (A = best)
4. **Plastic type** — compositional: products have a % mix of material types (e.g. 60% HDPE, 30% PET, 10% PVC). Display as a stacked distribution bar showing the spread across all submitted products.
5. **Neck type** — categorical: Standard / Non-standard
6. **Dimensions (volume efficiency)** — numeric, unit: cm³/ml (lower = better)

> **Design note — three types of attribute display:**
> - **Numeric** (weight, recycled content %, dimensions): horizontal range bar with best / median / worst dots + dashed threshold line set by CAA
> - **Simple categorical** (neck type, recyclability rating): tag distribution — e.g. `[Standard 78%]` `[Non-standard 22%]` with a tag-based rule editor for CAA thresholds (each value gets a fee modifier dropdown)
> - **Compositional** (plastic type): stacked horizontal bar showing material mix across all products — e.g. `[HDPE 68%][PET 24%][PVC 8%]`. Threshold is set using a **conditional rule builder**: `IF [PVC %] is greater than [50%] THEN [+15% surcharge]`. Multiple rules can be stacked.

> **Data model note (important for Screen 3):** Touch must record % composition per material when uploading — not just a single plastic type. The upload form needs fields for HDPE %, PET %, PVC %, PP % that must sum to 100%. This is a key data capture requirement that makes compositional thresholds possible.

---

### Zone C: Fee Threshold Indicator (PRO/CAA only)
**Positioned:** Inline within each attribute row

Three threshold patterns depending on attribute type:

**1. Numeric attributes** (weight, recycled content %, dimensions)
A dashed vertical line on the range bar showing where CAA has set the fee threshold.
- Line style: dashed, `#6B7280` (mid grey)
- Label: small pill/badge, `#EFF6FF` background, `#1D4ED8` text — e.g. `Current threshold: 45g`

**2. Simple categorical attributes** (recyclability rating, neck type)
A tag-based rule editor — each category value gets a fee modifier:
```
  [A] → No surcharge ✅     [B] → No surcharge ✅
  [C] → +5% surcharge ⚠️   [D] → +10% ⚠️   [E] → +20% 🔴
```

**3. Compositional attributes** (plastic type)
A conditional rule builder — rules are stacked IF/THEN statements:
```
  IF [PVC %] is greater than [50%] THEN [+15% surcharge]
  IF [PVC %] is greater than [25%] THEN [+5% surcharge]
  [+ Add rule]
```
This pattern mirrors tools like Airtable automations or Excel conditional formatting — familiar to a data-literate regulatory audience.

> **Annotation note:** Label this zone in Figma as *"Conditional threshold rules — CAA Pro tier only"* to make the user permission model clear to pitch reviewers.

---

### Zone D: Top Performers Panel
**Positioned:** Below Zone B
**Layout:** Horizontal row of 3 product cards

Each card shows:
- Product photo (thumbnail, ~80×80px, rounded corners)
- Product name (e.g. "Method All-Purpose Cleaner")
- Brand / supplier
- Overall score badge (e.g. `A` in green circle)
- 2–3 key attribute values as small tags

**Header:** `Top Performers` (H3) + `View all 12 →` link (right-aligned)

---

### Zone E: Navigation / Context Panel (left sidebar or top tabs)
**Option 1 — Tabs (simpler for concept):**
`Overview` | `By Attribute` | `Trend Over Time` | `Fee Thresholds`
(Show "Overview" as active tab — other tabs can be greyed out/coming soon)

**Option 2 — Left sidebar (more Airtable-like):**
Collapsible left nav listing all product types — user can jump between categories without going back.

> **Recommendation for concept screens:** Use tabs (simpler, cleaner for a static pitch screen)

---

## Typography

| Element | Font | Size | Weight | Colour |
|---------|------|------|--------|--------|
| Page title | Inter or system sans | 24px | Bold (700) | `#0F172A` |
| Section heading | Inter | 16px | Semibold (600) | `#0F172A` |
| Attribute label | Inter | 13px | Semibold (600) | `#374151` |
| Value label | Inter | 12px | Regular (400) | `#6B7280` |
| Body / metadata | Inter | 13px | Regular (400) | `#6B7280` |

---

## Colour Palette

| Purpose | Hex | Usage |
|---------|-----|-------|
| Best in class | `#2D7D46` | Green dot, left zone |
| Median | `#B8860B` | Amber dot, middle zone |
| Worst in class | `#C0392B` | Red dot, right zone |
| Range bar track | `#E5E7EB` | Background of bar |
| Page background | `#F8F9FA` | Screen bg |
| Card background | `#FFFFFF` | Content cards |
| Border | `#E5E7EB` | Card borders, dividers |
| Primary action | `#1D4ED8` | Buttons (CAA tier) |
| Text primary | `#0F172A` | Headings |
| Text secondary | `#6B7280` | Labels, metadata |

---

## Spacing & Grid

- **Page max-width:** 1280px, centred
- **Content padding:** 32px horizontal, 24px vertical
- **Card padding:** 20px
- **Row gap between attribute rows:** 24px
- **Border radius:** 8px on cards, 4px on tags/badges

---

## States to show in the concept (annotate in Figma)

1. **Default** — benchmarks loaded, no threshold set
2. **With threshold** — fee threshold line visible on 1–2 rows (to show CAA capability)
3. **Hover state** (annotate, don't need to fully design) — tooltip visible on attribute [i]

---

## What NOT to design (out of scope for concept)

- Clickable filter/sort interactions
- Trend over time tab
- Mobile layout
- Loading/empty states
- Error states

---

## Figma File Structure Suggestion

```
Screen 2 — Benchmarking View
├── Zone A: Header
├── Zone B: Attribute Charts
│   ├── Row — Weight
│   ├── Row — Recycled Content %
│   ├── Row — Recyclability Rating
│   ├── Row — Plastic Type (categorical variant)
│   └── Row — Neck Type (categorical variant)
├── Zone C: Fee Threshold (overlaid on Zone B)
└── Zone D: Top Performers
```

---

## Annotation notes for pitch deck

Add the following callout annotations to the Figma frame for CAA's benefit:
- 💬 *"Best in class / median / worst in class shown per attribute across all submitted products"*
- 💬 *"CAA can set fee modulation thresholds directly in the tool (Pro tier)"*
- 💬 *"Numeric attributes use a threshold line; categorical attributes use rule-based fee modifiers"*
- 💬 *"Compositional attributes (e.g. plastic type) support conditional rules — e.g. IF PVC > 50% THEN +15% surcharge"*
- 💬 *"Data maintained by Touch — updated as new products are submitted"*
- 💬 *"Exportable as PDF for regulatory reporting"*
