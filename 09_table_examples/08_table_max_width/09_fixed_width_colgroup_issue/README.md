# Table — `table-layout: fixed` + `<colgroup>` with an Unbreakable Token

**What this demo is**

A 2‑column table with **authoritative tracks** defined via `<colgroup>` (150px / 350px) and enforced by `table-layout: fixed; width: 500px`. The second row’s description contains an **unbreakable token** (a very long string without spaces or hyphens) to show how fixed tracks behave under stress.

**What you will see**

* The table is **exactly 500px** wide; columns are **locked** at **150px** and **350px**.
* Normal long prose **wraps** within the 350px column (no layout shift).
* The **unbreakable token does not wrap** by default. Because the tracks are fixed, the token will **overflow** the 350px cell (visually spill/clip or cause horizontal scroll depending on overflow context).

**Why it behaves like this**

* With `table-layout: fixed`, the browser **does not re‑measure content** to resize columns; it uses the `<colgroup>` tracks as given.
* An unbreakable token has a large **min‑content width**. Since the 350px track **cannot expand**, the token either **overflows** or is **clipped** if overflow is hidden.

**How to make it robust**

Add a breaker so hostile strings wrap *inside* the fixed track:

```css
/* Recommended: modern, standards-based */
th, td { overflow-wrap: anywhere; }

/* Optional hyphenation (needs language + soft hyphen support) */
/* th, td { hyphens: auto; } */

/* Aggressive fallback; breaks words arbitrarily (use sparingly) */
/* th, td { word-break: break-all; } */
```

**When to use this pattern**

* You need **hard, predictable column tracks** (reports, invoices, dashboards) and want **performance** on large tables.
* Your content is mostly wrappable, and you can opt‑in to break long tokens with `overflow-wrap:anywhere`.

**Limitations & gotchas**

* **Replaced elements** (images/iframes) may exceed the track unless constrained (e.g., `max-width:100%`).
* Very complex `rowspan`/`colspan` grids still require careful design.

**Key CSS in this demo**

```css
table {
  border-collapse: collapse;
  width: 500px;           /* sum of tracks */
  table-layout: fixed;    /* use <colgroup> tracks as-is */
}
th, td { border: 1px solid #444; }
.col-1 { width: 150px; }
.col-2 { width: 350px; }
```

**Takeaway**

`table-layout: fixed` + `<colgroup>` gives you **exact 150/350 tracks** and a stable 500px table. To survive **unbreakable tokens**, pair it with `overflow-wrap:anywhere` (or hyphenation) so long strings **wrap inside the cell** instead of breaking your layout.
