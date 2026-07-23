# Chainable Edits — Modifying an Existing System

Triggered when the interview reveals this build is **not** a from-scratch platform —
Question 10 ("Is this replacing an existing platform or page?") or Question 11/12
(interacts with other live systems / depends on legacy tech) came back with an existing
system in the picture.

## The rule

**Never hand back a full-file rewrite of something that already exists.** A full
rewrite forces the user to diff your entire output against their live file by hand to
figure out what actually changed, and it silently drops anything in the original file
this skill didn't know to preserve (custom Drupal hooks, inline comments, a stray
override someone added last year). Both are how a "helpful" full-file replacement
quietly breaks a production system.

Instead, output **small, self-contained, addable units** — each one:

1. **Named and scoped** — say exactly what it is and exactly where it goes ("add this
   `<section>` immediately after the existing `.vt-intro` block," "insert this rule into
   the site's existing stylesheet, don't create a new one").
2. **Complete on its own** — a full block (a whole HTML section, a whole CSS rule, a
   whole JS function), never a half-edited fragment the user has to mentally complete.
3. **Reviewable before it's applied** — written so the user can read it, understand
   exactly what it does, and decide to use it or not. Never phrase output as already
   applied ("I've updated your header") — it hasn't been; the user hasn't acted yet.
4. **Ordered, if there's more than one** — when a change requires several pieces (e.g. a
   new form section plus a new validation script), number them and note any dependency
   between them ("Step 2 assumes Step 1's `<form id="vt-form">` id is present").

Think of the output as a small, well-labeled patch set the user chains onto their
existing code themselves — not a replacement for it.

## What this looks like in practice

**Don't:**
> Here's your updated `page.html`: [500 lines, most of them unchanged from what the
> user already has]

**Do:**
> Add this block right after your existing `<header>` and before `<main>` — it's the
> required intro content per the Design Guide's Orientation rule:
>
> ```html
> <section class="vt-intro" aria-label="About this service">
>   ...
> </section>
> ```
>
> Nothing else on the page needs to change.

## Drupal-specific note

Most existing-system requests in this skill's context are Drupal pages/templates. When
patching Drupal output specifically:

- Prefer additions inside a **single Twig template block** or a **new, clearly-named
  custom block/region** over touching a core or contrib template directly.
- If a change must touch a `.twig`, `.theme`, or `.module` file, quote only the
  surrounding lines needed for the user to locate the insertion point — not the whole
  file.
- Flag explicitly if a change would require a Drupal cache rebuild or a config export,
  since the user (not this skill) is the one who will run it.
