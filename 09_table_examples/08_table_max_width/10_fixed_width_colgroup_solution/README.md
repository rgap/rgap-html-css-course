# Table — `table-layout: fixed` + `<colgroup>` + `overflow-wrap:anywhere`

**What this demo is**

A 2‑column table with **authoritative column tracks** via `<colgroup>` (**150px / 350px**) and `table-layout: fixed` to enforce them. It also applies **`overflow-wrap:anywhere`** to **all cells**, so even long, unbroken strings wrap inside the 350px column instead of overflowing.

**What you will see**

* The table box is **exactly 500px** wide (150 + 350).
* Columns are **locked** to **150px / 350px** because of fixed layout + `<colgroup>`.
* Regular long text wraps normally.
* **Unbreakable tokens** (e.g., `Veryverylongproduct…`) **wrap mid‑word** rather than bursting the layout.

**Why it behaves like this**

* `table-layout: fixed` makes the browser size columns from the **table/col tracks** without re‑measuring cell content, so tracks stay stable.
* `overflow-wrap:anywhere` allows breaks **between any characters** when needed, preventing overflow inside a fixed track.

**When to use this pattern**

* You need **predictable, hard column widths** (reports, invoices, dashboards) and want resilience against **hostile strings**.
* You want **fast layout** on large tables (fixed layout skips expensive content measurement).

**Limitations & notes**

* Mid‑word breaking can look **visually abrupt**. If you prefer hyphenation, also try `hyphens:auto;` (with proper language and/or soft hyphens) alongside `overflow-wrap:anywhere`.
* **Replaced elements** (images/iframes) can still overflow unless constrained (e.g., `max-width:100%`).
* Complex `rowspan`/`colspan` patterns still need thoughtful design with fixed tracks.

**Key CSS in this demo**

```css
table {
  border-collapse: collapse;
  width: 500px;              /* sum of tracks */
  table-layout: fixed;       /* use <colgroup> tracks as-is */
}
th, td {
  border: 1px solid #444;
  overflow-wrap: anywhere;   /* wrap long tokens inside the cell */
}
.col-1 { width: 150px; }
.col-2 { width: 350px; }
```

**Variants**

```css
/* Shrink-wrap the table to ~500px without setting width */
/* table { display: inline-table; table-layout: fixed; } */

/* Prefer hyphenation (where supported) */
/* th, td { hyphens: auto; } */
```

**Takeaway**

This combo—**fixed layout + `<colgroup>` + `overflow-wrap:anywhere`**—delivers **exact column tracks** and **robust wrapping**. It’s the most reliable pattern here for predictable tables that won’t break when faced with long, unspaced tokens.
