# State of Vermont Design Guide — Reference Extract

Condensed from "2026 Design Guide for State of Vermont (SOV).docx." This is the binding
spec for every platform, page, app, or form this skill produces. Nothing here is optional
and nothing here is user-configurable — see SKILL.md's "Non-Negotiables."

---

## Color Palette

### Primary Palette (core UI — use these first)

| Color | Hex | Use |
|---|---|---|
| Dark Green | `#003300` | Header/footer backgrounds, deep contrast, official communications, trust |
| Light Green (Platform) | `#EDF0EC` | Section backgrounds, button backgrounds, branding elements |
| Blue | `#174A7C` | **Primary buttons and hyperlinks** — the interaction color |
| Red | `#8B2929` | Brand-aligned alerts, secondary section blocks |
| Off-Black | `#303030` | Standard body text |

### Secondary Palette (vibrant accents — supplementary only)

| Color | Hex | Use |
|---|---|---|
| Light Green (Alerts) | `#56A054` | "Success" / positive feedback |
| Bright Red (Alerts) | `#E74C39` | "Error" / "Critical" / "Destructive" actions |
| Yellow | `#F5B324` | "Warning" / "Attention Required" |
| Gray | `#D7D2CB` | Background fills, disabled buttons, subtle separators |

### Dark Mode & High Contrast

| Mode | Background | Text | Trigger |
|---|---|---|---|
| Light (Default) | `#FFFFFF` | `#303030` | Standard Vermont brand experience |
| Dark (System) | `#1B1B1B` | `#F1F1F1` | `@media (prefers-color-scheme: dark)` |
| High Contrast | `#000000` | `#FFFF00` | Prioritize yellow-on-black for max visibility |

**Text-overlay rule:** white text on Primary Palette colors; black text on Secondary
Palette colors.

**Button color rule:** Blue (`#174A7C`) is the primary CTA color. **Never use Vermont
Green for buttons** — green is reserved for branding (header/footer/section backgrounds),
not interaction.

---

## Typography

- **Sans-serif only.** Libre Franklin is the official state standard. Public Sans (USWDS
  standard) is the approved alternative for React-based apps.
- **Minimum 16px (1rem)** for all body copy — never smaller.
- **Logical heading hierarchy**: H1 → H2 → H3, no skipped levels. H1 is reserved for the
  single, unique page title.
- **Title case or sentence case only.** Never all-caps (legibility).

---

## Header

- Dark green (`#003300`) background, white text throughout — WCAG 2.1 AAA contrast.
- Official Vermont "moon over mountain" logo, transparent background, **white reverse
  variant**. Position far left.
- **Never generate the logo.** Use the provided image asset (`assets/vermont-logo-white.png`)
  only. If a different/updated logo is needed, ask the developer or the Communications and
  Marketing Office for the correct asset — do not draw or approximate it.
- Include only the official logo and the word "Vermont."
- A vertical white divider line sits immediately right of the logo.
- To the right of the divider: **Agency or Department name** (top line) and **Application
  or website title** (second line), constrained to the same vertical height as the logo,
  with clear typographic hierarchy distinguishing agency from product name.

## Footer

- Same dark green background, white text.
- Support/contact info on the **left side** of the footer.
- At least one accessible contact method (email, phone, or support link), with
  descriptive, screen-reader-friendly link text (never bare "click here").

---

## Orientation — Required Intro Content

**Every application must include a brief introduction before any input fields or
interactive elements.** This is not optional and is not a nice-to-have — it's required
for every build this skill produces.

- **Placement:** top of the page, before any form fields or interactive elements.
- **Length:** 2–3 concise sentences. Plain language, no jargon or acronyms.
- **Must communicate:** what the service is; which Vermont agency/department owns it;
  what users can do on the platform; any critical info the user needs before proceeding.
- **Reading level:** 6th–8th grade.
- **Example pattern:** "This application is managed by the [Agency Name] and allows
  Vermont residents to [primary task]. You can use this service to [key actions]. Before
  you begin, please make sure you have [important requirement or note]."

This is why the mandatory interview (see `references/interview-script.md`) asks the user
to describe the platform's introduction before any building starts — that description
becomes this required intro block.

---

## Spacing — 8px System

- **8px linear scale.** All margins and padding must be multiples of 8 (8, 16, 24, 32,
  48, 64px).
- **Micro-spacing** (8px, 16px): between related elements (label ↔ input).
- **Macro-spacing** (32px, 48px, 64px): between major sections (header ↔ body).
- **Recognition over recall:** don't hide important features inside complex menus —
  minimize the user's memory load by keeping actions/options visible.
- **Touch targets:** minimum 44×44px hit area on mobile for all buttons/interactive links.

---

## User Control & Freedom

- **"Emergency exit"**: every modal, multi-step form, or complex process needs a clearly
  visible Cancel or Go Back option.
- **Input protection**: a confirmation dialog is required before any destructive action
  (e.g. deleting a record).
- **Data transparency**: tell users how their data will be used at the point of
  collection.

## Feedback Loops

- **System status**: a progress indicator is required if an action takes longer than
  1.0 second. A percentage-based or relative progress bar is required past 10 seconds.
- **Predictable navigation**: the USWDS "Official Government Banner" must be the first
  element in the DOM — this establishes immediate trust.

## Stacking & Menu Logic

- Multi-column layouts must stack vertically at the "Medium" breakpoint (`< 640px`).
- Mobile touch targets: minimum 44×44px.
- Mobile navigation: USWDS "Overlay" or "Drawer" pattern.
- **Menu placement**: prioritize a top horizontal menu for predictability. Exception — if
  the Agency's primary website already uses a left-hand sidebar, the new
  app/page can use a sidebar too, for consistency with that existing site.

---

## Accessibility (WCAG 2.1 AA required; prefer AAA)

All State of Vermont platforms are legally required to meet **WCAG 2.1 Level AA**, with
a preference for AAA where achievable.

- **Double-Indicator Rule**: never use color alone to convey meaning. An error field
  needs both a red border *and* an error icon/text label.
- **Semantic structure**: use correct HTML landmarks (`<main>`, `<nav>`, `<header>`) so
  screen readers can navigate.
- **Links**: two visual cues distinguishing links from body text (not color alone); link
  text must describe the destination/action, never "click here."
- **Phone numbers**: always hyperlinked as `tel:000-000-0000`.
- **Alt text**: meaningful, describes what the image shows or means. Never put
  important text only inside an image — repeat it in page content. Mark purely
  decorative images as decorative (`role="presentation"` / empty `alt=""`), don't
  caption them with "image of X."
- **Heading styles**: logical order, no skipped levels (never h2 → h4), never used
  purely for visual styling, each heading descriptive of what follows.
- **Tables**: only for genuinely complex/tabular data, never for layout. Simple data
  (like contact info) should be a list instead.
- **Keyboard access**: every interactive element (links, buttons, menus, forms, modals)
  must be operable and closeable via keyboard alone, with a visible focus indicator and
  a logical tab order (generally top-to-bottom, left-to-right).
- **No flashing/auto-moving content** — or provide a pause/stop control if motion is
  necessary.
- **Consistency**: identical menu item names across the whole site; short, descriptive,
  unique page titles.

---

## Good vs. Bad Patterns

### ✅ Do

- Official Identifier Banner — the USWDS government banner establishes trust as an
  official `.gov` platform.
- Plain-language labels — "Renew My Driver's License," not "Submit Form 22-A."
- Progressive disclosure — accordions instead of overwhelming walls of content.
- Inline validation — e.g. an immediate checkmark on a correctly filled field.
- Fluid widths (`width: 100%`) for containers — never fixed-pixel widths. Use
  percentages or `rem`.
- "Skip Navigation" link at the top of the DOM for screen-reader/keyboard users.
- The USWDS `usa-banner` component to identify the site as official government.
- Alt text on every image, or `role="presentation"` if purely decorative.

### ❌ Don't

- Poor contrast, or information overload (too many competing CTAs/images/fonts).
- Icon-only navigation with no text label (e.g. an unlabeled hamburger icon).
- Infinite scroll on government sites — it prevents users from reaching the footer
  (contact info, legal, accessibility links).
- A "wall of text" — a single `<p>` for an entire page of instructions.
- Low-contrast links (e.g. blue on dark blue — violates the 4.5:1 contrast minimum).
- Fixed-pixel (`px`) layout widths.
- Forcing light mode when the user has a system-level dark preference.
- Bitmap images of text (e.g. a photo of a document) — use real, searchable HTML text.
- Disabling zoom — users must be able to scale to 200% without losing content/function.

---

## Final Implementation Checklist

| Feature | ✅ Do | ❌ Don't |
|---|---|---|
| Forms | Group related fields with clear labels; single-column layout | Use placeholders as the only label; use two-column layouts (breaks eye path) |
| Mobile | Stack columns vertically | Force horizontal scrolling |
| Language | Write at 8th-grade reading level; test for complexity | Use technical or legal jargon |
| Buttons | Blue (`#174A7C`) for the primary CTA | Use Vermont Green for buttons — it's for branding only |
| Imagery | Alt text describes the image's *function* | Caption decorative images ("image of a mountain") instead of marking them decorative |
| Errors | Summary box at the top of long forms; immediate in-field feedback | Make users scroll or progress further to discover why a form failed |
