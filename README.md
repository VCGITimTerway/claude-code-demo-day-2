# Claude Code Demo Day 2

This repo is a working example of developing a [Claude Code skill](https://docs.claude.com/en/docs/claude-code) for a real, ongoing job: authoring Vermont GIS data Standards and Guidelines documents for [VCGI](https://vcgi.vermont.gov/) (Vermont Center for Geographic Information).

## What's here

- **`.claude/skills/vt-gis-standard/`** — a skill that scaffolds new VT GIS Standard/Guideline HTML documents matching VCGI's shared publishing template (common header/footer/CSS, table of contents, standard section skeleton, Datawrapper table conventions). See [`SKILL.md`](.claude/skills/vt-gis-standard/SKILL.md) for the full authoring workflow and [`reference/`](.claude/skills/vt-gis-standard/reference/) for the boilerplate template and Datawrapper embed patterns it's built from.
- **`examples/parcel/`** — a worked example: the currently-operational [Vermont GIS Parcel Data Standard v2.3](https://vcgi.vermont.gov/sites/vcgiupdate/files/doc_library/02-k-VT_GIS_Parcel_Data_Standard.pdf) (source PDF and Word doc included alongside) ported into the skill's HTML template, as a real-world test of the skill against an existing, non-web-native standard. Live preview via GitHub Pages: **[vcgitimterway.github.io/claude-code-demo-day-2/examples/parcel/parcel-standard.html](https://vcgitimterway.github.io/claude-code-demo-day-2/examples/parcel/parcel-standard.html)**
- **`examples/metadata/`** — a second worked example: the live, Drupal-hosted [Metadata Standard and Guidelines](https://vcgi.vermont.gov/resources/vermont-gis-standards-and-guidelines/metadata-standard-and-guidelines) (v5.0) ported into the skill's HTML template, testing a web-native source with its own two-part Standard/Guidelines structure and two migrated SVG diagrams. Live preview via GitHub Pages: **[vcgitimterway.github.io/claude-code-demo-day-2/examples/metadata/metadata-standard.html](https://vcgitimterway.github.io/claude-code-demo-day-2/examples/metadata/metadata-standard.html)**

## Background

VCGI publishes GIS data standards (e.g. the [Vermont Protected Lands Data Standard](https://files.vcgi.vermont.gov/other/standards-guidelines/vpld/vpldstandard.html), [Act 250 Tier Map Data Standard](https://files.vcgi.vermont.gov/other/standards-guidelines/act250/act250-standard.html), [Future Land Use Data Standard](https://files.vcgi.vermont.gov/other/standards-guidelines/flu/flu-standard.html), and [Geographic Names and Codes Standard](https://files.vcgi.vermont.gov/other/standards-guidelines/geonames-codes/geonames-codes-standard.html)) as static HTML pages that all share one CSS template ([`vcgi-sov-stylesheet-v.1.1.css`](https://files.vcgi.vermont.gov/other/css/vcgi-sov-stylesheet-v.1.1.css)) and use [Datawrapper](https://www.datawrapper.de/) embeds for many of their data tables.

The actual standards documents are developed and published from a separate, private GitHub repo, [`VCGI/standards-and-guidelines-dev`](https://github.com/VCGI/standards-and-guidelines-dev), out to Azure Blob Storage (aliased publicly at `files.vcgi.vermont.gov`). This repo isn't where VCGI's live standards are authored day-to-day — it holds the Claude Code skill itself, plus worked examples (like `examples/parcel/`) used to test and refine it.

## Status

Skill scaffolds new standards from scratch (head/header/footer boilerplate, ToC, standard section skeleton, Datawrapper vs. plain-HTML table guidance). Refined against real examples in the private dev repo to capture the actual range of section names and folder conventions in use, and validated end-to-end by porting two real, live standards into the template — the currently-operational Parcel Data Standard (v2.3, previously PDF-only) and the Drupal-hosted Metadata Standard and Guidelines (v5.0, including image-asset migration) — rendering each headlessly to confirm layout before committing.

This README is kept up to date as the skill evolves.
