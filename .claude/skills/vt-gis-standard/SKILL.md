---
name: vt-gis-standard
description: Scaffold a new Vermont GIS data Standard or Guideline HTML document using VCGI's shared vcgi-sov-stylesheet template — the pattern used at files.vcgi.vermont.gov/other/standards-guidelines/*. Use when asked to draft, create, author, or publish a new VT/Vermont GIS data standard or guideline document, or to convert existing schema/domain documentation into that format.
---

# Vermont GIS Standard/Guideline authoring

VCGI (Vermont Center for Geographic Information) publishes data standards and guidelines as static HTML pages that all share one CSS file (`vcgi-sov-stylesheet-v.1.1.css`) and a common header/footer/layout. Examples: the VPLD, Act 250 Tier Map, Future Land Use, and Geographic Names & Codes standards. This skill scaffolds a new document that matches that shared template exactly, so it drops into the existing family without visual or structural drift.

Reference files (read these before writing):
- `reference/template.html` — full boilerplate: head includes, header, footer, scripts, and a placeholder section skeleton, all copied verbatim from live VCGI standards pages except for `[[PLACEHOLDER]]` tokens.
- `reference/datawrapper-embeds.md` — how to choose between a plain HTML table and the two Datawrapper embed forms, with exact snippets.

## Source repo and publishing target

- **Source/development**: the HTML for these standards is developed and version-controlled in the private GitHub repo [VCGI/standards-and-guidelines-dev](https://github.com/VCGI/standards-and-guidelines-dev). If you're working inside that repo, follow its existing folder layout for where a new standard's files live.
- **Publishing target**: published pages live in Azure Blob Storage, one subfolder per standard, under `https://vcgiblobapps.blob.core.windows.net/other/standards-guidelines/<short-name>/`.
- **Public alias**: `https://files.vcgi.vermont.gov/other/standards-guidelines/<short-name>/` is a friendlier custom-domain alias for the same blob storage — same content, either URL works, prefer the `files.vcgi.vermont.gov` form when writing links for humans.
- **Filename**: standards are **not** named `index.html` — each uses its own filename tied to the standard's short name (e.g. `vpldstandard.html`, `act250-standard.html`, `flu-standard.html`, `geonames-codes-standard.html`). There's no single fixed suffix pattern across existing docs; when authoring a new one, pick something short and consistent with the short-name slug (`<short-name>-standard.html` is a reasonable default), and when updating an existing standard, keep its established filename as-is.
- **Dev repo layout**: the dev repo organizes standards into topic folders at its root — `boundaries/` (e.g. `vpld/`), `planning/` (e.g. `act250-standard.html`, `flu-standard.html`, `zoning-standard.html`), `geonames-codes/`, `parcels/`, `housing/`, `basemaps/`, `metadata/`. Place a new standard's HTML file in the topic folder that matches its subject, creating a new topic folder only if nothing existing fits. Each topic folder's `readme.md` documents data/ETL/process details for that dataset — it's internal reference material, not a style guide, and isn't something a new standard's HTML needs to match structurally.
- **Caution — not everything in a topic folder is the live standard.** Topic folders can contain superseded drafts, `.docx`/`.htm` Word exports, dated backup copies (e.g. `vpldstandard - bu20250812-finaldev.html`), or abandoned `.md` drafts alongside the current file. Before treating any existing file as a structural reference, confirm it's actually the one published at `files.vcgi.vermont.gov` (or ask) — don't assume the newest-looking or only-HTML file in a folder is authoritative.

## Ground rules

1. **Never modify the `<head>` CDN links, `<header>`, `<footer>`, or `<script>` blocks in `template.html`.** They're byte-for-byte identical across every published standard. If the user wants to bump the shared CSS version or change footer contacts, flag that this affects every VCGI standard, not just the one being authored, and confirm before touching it.
2. **Every `h2`/`h3`/`h4` inside `main-article-content` needs an `id` and an inline heading-permalink link**, e.g.:
   ```html
   <h2 id="scope">Scope
       <a href="#scope" class="heading-permalink" aria-label="Permalink to this section">
       <i class="fas fa-link"></i></a>
   </h2>
   ```
3. **The floating Table of Contents must exactly mirror the heading ids** — every ToC `<a href="#id">` needs a matching heading `id`, and every heading needs a ToC entry (nest `h3`/`h4` under their parent as nested `<ul>`, matching `template.html`).
4. **Don't invent new CSS classes or ad-hoc inline styles.** The stylesheet already defines `alert-info/tip/important/warning/danger`, `notice`, `card-grid`/`card`, `table-of-contents`, `color-palette-grid`/`color-swatch`/`bg-*`, `task-list`, etc. — reuse them. For example, a cartographic color-code table (mapping a domain value to a display color, as in the zoning standard's `DIST_TYPE` symbolization table) should use the `color-palette-grid`/`color-swatch` classes rather than one-off `<div style="background-color:...">` swatches — the draft zoning standard does the latter; treat that as a gap to fix, not a pattern to copy.
5. **Pick the right content wrapper per block**: `content-wrapper` (max 800px, default prose column), `content-wrapper-wide` (full width — use for wide schema/domain tables and Datawrapper embeds so they aren't squeezed), `content-wrapper-medium` (90% — for large images/diagrams). A single page can open/close multiple wrapper divs as it moves between prose and wide tables — see `template.html` for the pattern of closing one wrapper, opening another, then reopening the first.
6. **Accessibility**: every `<img>` needs real `alt` text (not empty, unless purely decorative); figures get a `<figcaption>`; don't skip heading levels (h2 → h3 → h4, never h2 → h4).

## Workflow

1. **Gather the essentials** before writing anything. At minimum you need:
   - Full title and a short-name slug (used for the Azure blob subfolder and filename — see "Source repo and publishing target" above)
   - Version string and date (format: `Version X.Y | Month Day, Year` — existing docs use inconsistent version schemes: plain year like `2025`, or semantic like `1.2`/`2.0` — ask which convention this standard's owner already uses, or default to semantic versioning for a brand-new one)
   - Purpose (why the standard exists), Scope (what it covers), Applicability (who must/should comply — check for statutory language like "per 10 V.S.A. § 123" if this is a mandatory-adoption standard, vs. "recommended" for a guideline)
   - Definitions of key terms
   - Referenced standards (federal/ANSI/other VCGI standards this one builds on)
   - The data schema itself: field names, aliases, data types, lengths, descriptions, and any coded-value domains
   - Whether any tables already exist in Datawrapper (get chart IDs) or need to be authored as plain HTML
   - At least one history entry (even a brand-new standard gets an initial "Version X.Y approved/drafted by..." entry)
   - Statutory authority: confirm whether this standard falls under VCGI's general standards-and-guidelines authority (use the canonical paragraph in `template.html`, which cites 10 V.S.A. chapter 8 and the EGC adoption procedure) or has its own separate authorizing statute to cite instead/in addition
2. **Copy `template.html`** as the starting point rather than writing HTML from scratch — this guarantees the shared boilerplate stays exact.
3. **Fill in each section** per the ground rules above. The core skeleton (Purpose, Scope, Applicability, Specifications, Updates and History, Statutory Authority) is universal; everything else is chosen per standard from an established menu — don't force a section that doesn't apply, but don't omit one the schema actually needs. Observed in real standards across the dev repo:
   - **Specifications subsections** vary by standard type: `Data Format`/`Schema`/`Domains`/`Spatial Reference` (feature-class standards like act250, flu, zoning); `Standard Codes`/`Concatenated Fields`/`Domains`/`Listing of Codes` (code/lookup standards like geonames-codes); `Requirements`/`Schema` (database standards like vpld).
   - **Other common top-level sections**: `Definitions`, `Referenced Standards`, `Data Contributors` (multi-steward datasets like vpld), `Submittals` (submission process/who submits to whom), `Naming` (file/layer naming convention, often a `<code>` pattern like `[RPCCODE]_LAYERNAME_poly_SP_[YYYY]`), `Metadata` (points to the Vermont GIS Metadata Standard and any required abstract content), `Cartographic Presentation` (symbology, e.g. a domain-value-to-color table), `Data Template` (link/pointer to a downloadable template gdb/schema), `Crosswalks and Lookup Tables`, `Acknowledgements`.
   - Don't omit a Domains subsection if any field has coded values.
4. **Build the schema/domain tables** using `reference/datawrapper-embeds.md` to decide plain-HTML vs. Datawrapper for each one independently.
5. **Write the History entry** newest-first. Use a nested `<ul>` or a two-column Date/Description `<table>` — either is an established pattern; pick a table if frequent short entries are expected, a list if entries tend to be longer narrative bullets.
6. **Sanity-check before handing back**: every ToC link resolves to a real id; every heading has a permalink icon; no orphaned `content-wrapper-wide` divs left unclosed; all external links (statutes, EGC procedure, referenced standards) are real URLs, not placeholders.
