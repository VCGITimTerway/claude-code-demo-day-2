---
name: vt-platform-builder
description: >
  Assists with standardized building of State of Vermont websites, web pages, apps, and
  forms, following the 2026 Design Guide for State of Vermont. Use this skill any time a
  user wants to build, design, or scaffold a new State platform, page, app, or form, or
  wants to modify an existing one to bring it in line with Vermont brand and
  accessibility standards. Triggers include: "build a new page," "design a State
  website," "create a form for my agency," "make this app match the Vermont design
  guide," "scaffold a new platform," or any request to produce a web asset that should
  look and behave like an official Vermont government product. Always runs the mandatory
  pre-build interview first — never generate code before it's complete.
---

# Vermont Platform Development Skill

Helps build brand-compliant, accessible State of Vermont websites, pages, apps, and
forms — designed by a UX designer for standardized, predictable output across agencies.
Every build follows the 2026 Design Guide for State of Vermont, uses USWDS-aligned
patterns (see the reference screenshots in `assets/reference-photos/`), and is delivered
as code the user applies themselves.

---

## Non-Negotiables

These hold regardless of what the user asks for mid-conversation. If a request
conflicts with one of these, say so plainly and explain why, rather than complying.

1. **The interview in `references/interview-script.md` is mandatory and comes first.**
   All 13 questions, one at a time, no skipping. "I don't know" is an acceptable answer;
   silence or moving on without an answer is not. See that file for the full rules.
2. **Plain language always** — in the interview, and in everything the built product
   says to its end users. No jargon, no acronyms without expansion, no legalese.
3. **No color or typography deviation.** Every build uses the exact palette and font
   stack in `references/design-guide.md` — Libre Franklin/Public Sans, the Primary/
   Secondary palette hex values, Blue (`#174A7C`) for primary CTAs, Vermont Green
   reserved for branding only. The user cannot request a different scheme; if asked,
   explain that the Design Guide fixes this and isn't a per-project choice.
4. **This skill never acts on or changes a live system by itself.** It has no scripts
   that deploy, push, or write into a running Drupal site, database, or repository on
   the user's behalf. Every deliverable is code (HTML/CSS/JS, or a chainable patch — see
   `references/chainable-edits.md`) that the user reviews and applies at their own
   discretion, in their own environment, on their own timeline.
5. **HTML + JavaScript, Drupal-presumed, unless told otherwise.** Default to
   framework-free HTML/CSS/JS that drops cleanly into a Drupal template or block. Don't
   introduce a build step, a JS framework, or a package dependency unless the user's
   answers make clear their environment already has one.
6. **Simple, modern, spacious by default.** Large accessible type (16px+ body,
   Libre Franklin/Public Sans), generous white space, the 8px spacing scale — this is
   the aesthetic baseline for every build, not a style option.

---

## Workflow

### Step 1 — Run the mandatory interview

Work through `references/interview-script.md` in full, one question at a time, before
producing any code, wireframe, or design description. Summarize the answers back to the
user and confirm accuracy before moving on.

### Step 2 — Classify the build

From question 1's answer, confirm which shape this is:

| Build type | What that implies |
|---|---|
| New State website | Full header/footer, banner, nav, likely multiple pages/templates |
| New page in an existing site | Match the existing site's nav/menu placement (see Design Guide's menu exception); only the page body is new |
| App | May be more interactive/stateful; same brand and a11y rules still apply in full |
| Form | Prioritize the single-column, progressive, error-summary patterns in `references/html-patterns.md` |

If question 10 revealed this replaces or modifies something that already exists, or
question 11/12 revealed live-system interaction or legacy dependencies, treat this as an
**existing-system build** — follow `references/chainable-edits.md` for how output is
structured, not a fresh scaffold.

### Step 3 — Build content and structure

- Use the interview's Question 7 answer to write the required intro block (see Design
  Guide's "Orientation" section) — tighten it to 2–3 plain-language sentences at a
  6th–8th grade reading level if the user's draft was rougher than that, but preserve
  their meaning and facts.
- Use Question 8/9's answers (Agency, owner, support email) to fill the header/footer
  agency name and footer contact block.
- Use Question 13's answer (Agency logo) in the header alongside the Vermont logo — if
  the user doesn't have one yet, build with the Vermont logo alone and flag the missing
  Agency logo as an open item in your delivery, not something to silently omit or fake.
- Pull structure and components from `references/html-patterns.md`. Don't invent new
  visual patterns when an equivalent one already exists there.

### Step 4 — Apply brand and accessibility rules

Check every piece of output against `references/design-guide.md` before delivering:
palette, typography, spacing (8px multiples), header/footer spec, WCAG 2.1 AA/AAA rules,
the Double-Indicator Rule, keyboard operability, and the Good/Bad and Final Checklist
tables. Treat that file as the acceptance criteria, not just inspiration.

### Step 5 — Deliver

- **New build**: deliver complete, ready-to-use HTML/CSS/JS the user can drop into a
  Drupal page or template.
- **Existing-system build**: deliver per `references/chainable-edits.md` — small, named,
  independently-reviewable patches, never a full-file rewrite, never framed as already
  applied.
- Always state plainly what you're handing back and what the user needs to do with it
  (where it goes, anything it depends on, anything still missing like an Agency logo or
  a support email). Never imply the change is already live — it isn't, and this skill
  doesn't make it live.

---

## Reference Files

| File | Purpose |
|---|---|
| `references/interview-script.md` | The mandatory 13-question pre-build interview, asked one at a time |
| `references/design-guide.md` | Condensed, binding extract of the 2026 Design Guide — palette, type, spacing, header/footer, a11y, do/don't |
| `references/html-patterns.md` | Copy-paste HTML/CSS/JS patterns (banner, header/footer, forms, errors, accordion, cards, sidebar), styled per the Design Guide |
| `references/chainable-edits.md` | How to structure output when modifying an existing/live system instead of building fresh |
| `assets/vermont-logo-white.png` | Official Vermont logo, white reverse variant — use as-is, never regenerate |
| `assets/reference-photos/` | Screenshots (Vermont.gov, USA.gov, Mass.gov) showing the USWDS-aligned patterns this skill implements |
