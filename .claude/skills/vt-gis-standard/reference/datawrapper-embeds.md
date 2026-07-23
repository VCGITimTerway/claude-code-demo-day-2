# Tables: plain HTML vs. Datawrapper

VCGI standards pages use three different table treatments. Pick per-table, not per-document — a single standard can mix all three.

## When to use each

- **Plain HTML `<table>`** — short, stable tables that rarely change (e.g. a 5-row field schema, a 10-row RPC code list). No Datawrapper account access needed; anyone can edit the HTML directly.
- **Datawrapper responsive `<div>` embed** — tables that are edited more often than the page itself, or that benefit from client-side sort/search (large lookup tables, submittal-status trackers). Height auto-adjusts to content via `embed.js`.
- **Datawrapper `<iframe>` embed** — functionally equivalent to the div embed; used interchangeably in existing standards (act250, flu). Requires a fixed `height` attribute plus the resize-listener script to avoid clipping — prefer the div form for new tables since it doesn't need a hardcoded height.

Either Datawrapper form requires the chart to already exist in VCGI's Datawrapper account. **This skill cannot create or edit Datawrapper charts** — it can only tell you which snippet to paste once you (or the requester) have built the chart and have its ID. If no chart exists yet, default to a plain HTML table and note that it could be converted to Datawrapper later.

Always wrap wide tables (and Datawrapper embeds) in a `content-wrapper-wide` div, not `content-wrapper` — `content-wrapper` caps at 800px and will squeeze a wide table awkwardly. See `template.html` for the wrapper pattern (close `content-wrapper`, open `content-wrapper-wide`, then reopen `content-wrapper` afterward to return to normal prose width).

## Snippet 1 — responsive div + embed.js (preferred for new tables)

```html
<div style="min-height:400px" id="datawrapper-vis-CHARTID"><script type="text/javascript" defer src="https://datawrapper.dwcdn.net/CHARTID/embed.js" charset="utf-8" data-target="#datawrapper-vis-CHARTID"></script><noscript><img src="https://datawrapper.dwcdn.net/CHARTID/full.png" alt="" /></noscript></div>
```

Replace `CHARTID` (both places, and in the `id` attribute) with the actual Datawrapper chart ID, e.g. `sRGz5`. Set `min-height` to roughly the expected rendered height in pixels (400 is a reasonable default for a small lookup table; use ~578 or more for long tables) — it's just a placeholder to avoid layout jump before the script loads, not a hard cap.

## Snippet 2 — iframe + resize-listener (used in existing act250/flu docs)

```html
<iframe title="CHART TITLE" aria-label="Table" id="datawrapper-chart-CHARTID" src="https://datawrapper.dwcdn.net/CHARTID/VERSION/" scrolling="no" frameborder="0" style="width: 0; min-width: 100% !important; border: none;" height="HEIGHT" data-external="1"></iframe><script type="text/javascript">window.addEventListener("message",function(a){if(void 0!==a.data["datawrapper-height"]){var e=document.querySelectorAll("iframe");for(var t in a.data["datawrapper-height"])for(var r,i=0;r=e[i];i++)if(r.contentWindow===a.source){var d=a.data["datawrapper-height"][t]+"px";r.style.height=d}}});</script>
```

- `title` should describe the table for screen readers (matches the preceding heading text).
- `VERSION` is the Datawrapper publish version number (usually `1`; increments each time the chart is republished — check the embed code Datawrapper gives you).
- `HEIGHT` is a starting pixel height; the resize script corrects it after load, but pick something close to avoid visible layout shift.
- If multiple iframe embeds appear on one page, only include the `window.addEventListener(...)` script **once** — it's a single global listener that handles all Datawrapper iframes on the page (existing docs mistakenly repeat it per-embed; don't copy that duplication into new pages).
