# Claude Code Demo Day 2

This repo is a working example of developing a [Claude Code skill](https://docs.claude.com/en/docs/claude-code) for a real, ongoing job: authoring Vermont GIS data Standards and Guidelines documents for [VCGI](https://vcgi.vermont.gov/) (Vermont Center for Geographic Information).

## What's here

- **`.claude/skills/vt-gis-standard/`** — a skill that scaffolds new VT GIS Standard/Guideline HTML documents matching VCGI's shared publishing template (common header/footer/CSS, table of contents, standard section skeleton, Datawrapper table conventions). See [`SKILL.md`](.claude/skills/vt-gis-standard/SKILL.md) for the full authoring workflow and [`reference/`](.claude/skills/vt-gis-standard/reference/) for the boilerplate template and Datawrapper embed patterns it's built from.

## Background

VCGI publishes GIS data standards (e.g. the [Vermont Protected Lands Data Standard](https://files.vcgi.vermont.gov/other/standards-guidelines/vpld/vpldstandard.html), [Act 250 Tier Map Data Standard](https://files.vcgi.vermont.gov/other/standards-guidelines/act250/act250-standard.html), [Future Land Use Data Standard](https://files.vcgi.vermont.gov/other/standards-guidelines/flu/flu-standard.html), and [Geographic Names and Codes Standard](https://files.vcgi.vermont.gov/other/standards-guidelines/geonames-codes/geonames-codes-standard.html)) as static HTML pages that all share one CSS template ([`vcgi-sov-stylesheet-v.1.1.css`](https://files.vcgi.vermont.gov/other/css/vcgi-sov-stylesheet-v.1.1.css)) and use [Datawrapper](https://www.datawrapper.de/) embeds for many of their data tables.

The actual standards documents are developed in a separate, private GitHub repo, [`VCGI/standards-and-guidelines-dev`](https://github.com/VCGI/standards-and-guidelines-dev), and published to Azure Blob Storage (aliased publicly at `files.vcgi.vermont.gov`). This repo doesn't hold any of those documents — it holds the Claude Code skill that helps author them consistently.

## Status

Skill scaffolds new standards from scratch (head/header/footer boilerplate, ToC, standard section skeleton, Datawrapper vs. plain-HTML table guidance). Refined against real examples in the private dev repo to capture the actual range of section names and folder conventions in use.

This README is kept up to date as the skill evolves.
