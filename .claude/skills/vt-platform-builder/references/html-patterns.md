# HTML/JS Pattern Library

Copy-paste-ready patterns, styled per `design-guide.md`. All patterns assume plain
HTML + vanilla JavaScript, deployed inside a **Drupal** page/template — no framework
dependency, no build step required. Every pattern below was checked against the four
reference screenshots in `assets/reference-photos/` (Vermont.gov, USA.gov, Mass.gov) —
they show the same underlying USWDS-derived shapes this library implements: an official
banner first in the DOM, single-column forms, card grids for topic browsing, and a
sidebar contact block.

Every snippet uses the Primary Palette hex values directly — never a user-suppliable
color variable. See SKILL.md's "Non-Negotiables."

---

## Skip Navigation Link (must be first focusable element)

```html
<a class="skip-nav" href="#main-content">Skip to main content</a>
<style>
  .skip-nav {
    position: absolute; left: -9999px; top: 0;
    background: #174A7C; color: #FFFFFF;
    padding: 8px 16px; z-index: 1000;
  }
  .skip-nav:focus { left: 8px; top: 8px; }
</style>
```

---

## Official Government Banner (first element in DOM, per Feedback Loops rule)

```html
<div class="usa-banner" role="banner">
  <div class="usa-banner-inner">
    <span>An official website of the State of Vermont</span>
    <button type="button" class="usa-banner-toggle" aria-expanded="false" aria-controls="banner-details">
      Here's how you know
    </button>
  </div>
  <div id="banner-details" class="usa-banner-details" hidden>
    <p>Official websites use .gov. A .gov website belongs to an official government
    organization in the United States.</p>
  </div>
</div>
<style>
  .usa-banner { background: #EDF0EC; color: #303030; font-size: 14px; }
  .usa-banner-inner { display: flex; align-items: center; justify-content: space-between; padding: 8px 16px; }
  .usa-banner-toggle {
    background: none; border: none; color: #174A7C; text-decoration: underline;
    cursor: pointer; font-size: 14px; min-height: 44px; padding: 0 8px;
  }
</style>
<script>
  document.querySelector('.usa-banner-toggle').addEventListener('click', function () {
    var details = document.getElementById('banner-details');
    var expanded = this.getAttribute('aria-expanded') === 'true';
    this.setAttribute('aria-expanded', String(!expanded));
    details.hidden = expanded;
  });
</script>
```

---

## Header (Vermont brand header — logo, agency name, app title)

```html
<header class="vt-header">
  <div class="vt-header-inner">
    <div class="vt-header-logo">
      <img src="assets/vermont-logo-white.png" alt="State of Vermont" height="40">
      <span class="vt-header-divider" aria-hidden="true"></span>
    </div>
    <div class="vt-header-titles">
      <span class="vt-header-agency">{{AGENCY_NAME}}</span>
      <span class="vt-header-app">{{APP_TITLE}}</span>
    </div>
  </div>
</header>
<style>
  .vt-header { background: #003300; color: #FFFFFF; }
  .vt-header-inner { display: flex; align-items: center; gap: 16px; padding: 16px 24px; max-width: 1200px; margin: 0 auto; }
  .vt-header-logo { display: flex; align-items: center; gap: 16px; }
  .vt-header-divider { width: 1px; height: 32px; background: #FFFFFF; display: inline-block; }
  .vt-header-titles { display: flex; flex-direction: column; }
  .vt-header-agency { font-size: 14px; opacity: 0.85; }
  .vt-header-app { font-size: 20px; font-weight: 700; }
</style>
```

**`{{AGENCY_NAME}}`** and **`{{APP_TITLE}}`** are placeholders — fill them from the
interview answers (Agency/Department, and what's being built), never leave the literal
token in delivered code.

---

## Footer (Vermont brand footer — support/contact on the left)

```html
<footer class="vt-footer">
  <div class="vt-footer-inner">
    <div class="vt-footer-support">
      <h2>Need help?</h2>
      <p>Contact {{AGENCY_NAME}} at
        <a href="mailto:{{SUPPORT_EMAIL}}">{{SUPPORT_EMAIL}}</a>.
      </p>
    </div>
  </div>
</footer>
<style>
  .vt-footer { background: #003300; color: #FFFFFF; padding: 32px 24px; }
  .vt-footer-inner { max-width: 1200px; margin: 0 auto; }
  .vt-footer a { color: #FFFFFF; text-decoration: underline; }
</style>
```

---

## Required Intro Block (before any form/interactive content)

```html
<section class="vt-intro" aria-label="About this service">
  <p>
    This application is managed by {{AGENCY_NAME}} and allows Vermont residents to
    {{PRIMARY_TASK}}. You can use this service to {{KEY_ACTIONS}}. Before you begin,
    please make sure you have {{REQUIREMENT_OR_NOTE}}.
  </p>
</section>
<style>
  .vt-intro { max-width: 700px; margin: 0 auto; padding: 32px 24px 0; font-size: 18px; line-height: 1.5; color: #303030; }
</style>
```

Fill every `{{...}}` token from the interview's introduction answer (Question 7). Never
ship the literal placeholder text — if the user's answer was rough, tighten it to 2–3
plain-language sentences at a 6th–8th grade reading level, but keep their meaning intact.

---

## Single-Column Form with Progress + Emergency Exit

Mirrors the USA.gov multi-step form pattern (progress indicator, single column,
Back/Next, no two-column layouts).

```html
<form class="vt-form" novalidate>
  <div class="vt-form-progress" role="progressbar" aria-valuenow="1" aria-valuemin="1" aria-valuemax="2">
    <span class="vt-form-progress-fill" style="width: 50%;"></span>
  </div>

  <h1>{{STEP_TITLE}}</h1>

  <div class="vt-form-field">
    <label for="field-1">{{FIELD_LABEL}} <span class="vt-required">(required)</span></label>
    <input type="text" id="field-1" name="field-1" required aria-describedby="field-1-hint">
    <p id="field-1-hint" class="vt-form-hint">{{HELP_TEXT}}</p>
  </div>

  <div class="vt-form-actions">
    <button type="button" class="vt-btn vt-btn-secondary">Back</button>
    <button type="submit" class="vt-btn vt-btn-primary">Next</button>
    <a href="{{CANCEL_URL}}" class="vt-btn-cancel">Cancel and exit</a>
  </div>
</form>
<style>
  .vt-form { max-width: 600px; margin: 0 auto; padding: 24px; }
  .vt-form-progress { background: #D7D2CB; height: 8px; border-radius: 4px; margin-bottom: 24px; }
  .vt-form-progress-fill { display: block; height: 8px; background: #174A7C; border-radius: 4px; }
  .vt-form-field { margin-bottom: 24px; display: flex; flex-direction: column; gap: 8px; }
  .vt-form-field label { font-size: 16px; font-weight: 600; color: #303030; }
  .vt-required { font-weight: 400; color: #52514E; }
  .vt-form-field input {
    font-size: 16px; padding: 12px; min-height: 44px;
    border: 1px solid #303030; border-radius: 4px; width: 100%;
  }
  .vt-form-hint { font-size: 14px; color: #52514E; margin: 0; }
  .vt-form-actions { display: flex; align-items: center; gap: 16px; margin-top: 32px; }
  .vt-btn { min-height: 44px; padding: 12px 24px; border-radius: 4px; font-size: 16px; cursor: pointer; border: none; }
  .vt-btn-primary { background: #174A7C; color: #FFFFFF; }
  .vt-btn-secondary { background: #EDF0EC; color: #174A7C; border: 1px solid #174A7C; }
  .vt-btn-cancel { color: #8B2929; text-decoration: underline; margin-left: auto; }
</style>
```

The "Cancel and exit" link is the required "emergency exit" per the Design Guide's User
Control & Freedom rule — never remove it from a multi-step form.

---

## Error Summary (top of form) + Inline Field Error

Implements the Double-Indicator Rule — never color alone.

```html
<div class="vt-error-summary" role="alert" tabindex="-1">
  <h2>There's a problem</h2>
  <ul>
    <li><a href="#field-1">{{FIELD_LABEL}}: {{ERROR_MESSAGE}}</a></li>
  </ul>
</div>

<div class="vt-form-field vt-form-field-error">
  <label for="field-1">{{FIELD_LABEL}}</label>
  <input type="text" id="field-1" aria-invalid="true" aria-describedby="field-1-error">
  <p id="field-1-error" class="vt-field-error">
    <span aria-hidden="true">⚠</span> {{ERROR_MESSAGE}}
  </p>
</div>
<style>
  .vt-error-summary {
    border: 2px solid #8B2929; background: #FBEEEE; color: #303030;
    padding: 16px 24px; margin-bottom: 24px; border-radius: 4px;
  }
  .vt-error-summary h2 { color: #8B2929; margin-top: 0; font-size: 18px; }
  .vt-form-field-error input { border: 2px solid #E74C39; }
  .vt-field-error { color: #8B2929; font-size: 14px; display: flex; gap: 6px; align-items: center; }
</style>
```

---

## Accordion (progressive disclosure)

```html
<div class="vt-accordion">
  <h3>
    <button type="button" class="vt-accordion-trigger" aria-expanded="false" aria-controls="panel-1">
      {{QUESTION_OR_TOPIC}}
    </button>
  </h3>
  <div id="panel-1" class="vt-accordion-panel" hidden>
    <p>{{ANSWER_OR_DETAIL}}</p>
  </div>
</div>
<style>
  .vt-accordion-trigger {
    width: 100%; text-align: left; background: #EDF0EC; border: none;
    padding: 16px; font-size: 16px; font-weight: 600; color: #174A7C;
    cursor: pointer; min-height: 44px; border-radius: 4px;
  }
  .vt-accordion-panel { padding: 16px; }
</style>
<script>
  document.querySelectorAll('.vt-accordion-trigger').forEach(function (btn) {
    btn.addEventListener('click', function () {
      var panel = document.getElementById(this.getAttribute('aria-controls'));
      var expanded = this.getAttribute('aria-expanded') === 'true';
      this.setAttribute('aria-expanded', String(!expanded));
      panel.hidden = expanded;
    });
  });
</script>
```

---

## Card Grid (topic/service browsing — mirrors USA.gov's "All topics and services")

```html
<div class="vt-card-grid">
  <a class="vt-card" href="{{LINK_URL}}">
    <h3>{{CARD_TITLE}}</h3>
    <p>{{CARD_DESCRIPTION}}</p>
  </a>
  <!-- repeat .vt-card for each topic/service -->
</div>
<style>
  .vt-card-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 16px; }
  .vt-card {
    display: block; padding: 24px; border: 1px solid #D7D2CB; border-radius: 8px;
    text-decoration: none; color: #303030; min-height: 44px;
  }
  .vt-card h3 { color: #174A7C; margin-top: 0; }
  @media (max-width: 640px) {
    .vt-card-grid { grid-template-columns: 1fr; }
  }
</style>
```

---

## Sidebar Contact Block (mirrors Mass.gov's pattern)

Use only when the Agency's primary site already uses a sidebar layout (per the Design
Guide's menu-placement exception) — otherwise prefer the plain footer contact block.

```html
<aside class="vt-contact-sidebar" aria-label="Contact information">
  <h2>{{AGENCY_NAME}}</h2>
  <p><a href="mailto:{{SUPPORT_EMAIL}}">{{SUPPORT_EMAIL}}</a></p>
</aside>
<style>
  .vt-contact-sidebar {
    background: #EDF0EC; padding: 24px; border-radius: 8px; max-width: 320px;
  }
  .vt-contact-sidebar a { color: #174A7C; }
</style>
```

---

## Dark Mode / High Contrast (system-driven, never forced)

```css
@media (prefers-color-scheme: dark) {
  body { background: #1B1B1B; color: #F1F1F1; }
}
@media (prefers-contrast: more) {
  body { background: #000000; color: #FFFF00; }
}
```

Never force light mode over a system-level dark preference — this media-query approach
is the only acceptable implementation.
