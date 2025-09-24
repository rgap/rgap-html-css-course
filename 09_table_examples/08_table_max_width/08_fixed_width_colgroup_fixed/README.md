# Table — `table-layout: fixed` + `<colgroup>` (Exact 150px / 350px Tracks)

**What this demo is**

A 2‑column table that sets **authoritative column tracks** using `<colgroup>` and enforces them with `table-layout: fixed`:

```css
table {
  border-collapse: collapse;
  width: 500px;        /* sum of tracks */
  table-layout: fixed; /* use <colgroup> tracks as-is */
}
.col-1 { width: 150px; }
.col-2 { width: 350px; }
```

This yields a predictable layout: a **150px** `Code` column and a **350px** `Description` column, totaling **500px**.

**What you will see**

* The table box is **exactly 500px** wide.
* Columns are **locked** to **150px / 350px** regardless of text length.
* Normal prose **wraps** inside each column and never stretches the tracks.
* Layout is stable across rows because the browser **does not re-measure content** to change column widths.

**Why it behaves like this**

* `table-layout: fixed` tells the engine to size columns from **table/col widths** rather than scanning cell content. This makes `<colgroup>` widths **authoritative**.
* `width: 500px` pins the table’s outer box to the **sum of the tracks**, avoiding container-driven stretching.
* With collapsed borders, you get tight, consistent grid lines.

**When to use this pattern**

* You need **hard, predictable tracks** (dashboards, data grids, invoice layouts).
* You want **performance** on large tables (skips expensive content measurement).
* Your content is mostly **wrappable** text, or you handle edge cases with wrapping rules.

**Limitations & edge cases**

* **Unbreakable tokens** (long IDs/URLs, `SuperLongWordWithoutBreaks`) can **overflow the cell** since tracks won’t expand. Add a breaker:

  ```css
  th, td { overflow-wrap: anywhere; /* or word-break: break-word (legacy alias) */ }
  /* optional: hyphens: auto;  (needs language + soft hyphens) */
  ```
* **Replaced elements** (large images, iframes) obey their own intrinsic sizes; they may overflow unless constrained (`max-width:100%`, fixed dimensions, or object-fit).
* Very complex `rowspan`/`colspan` layouts still require care—fixed tracks don’t eliminate spanning constraints.

**Key CSS in this demo**

```css
table {
  border-collapse: collapse;
  width: 500px;
  table-layout: fixed; /* authoritative tracks */
}
th, td { border: 1px solid #444; }
.col-1 { width: 150px; }
.col-2 { width: 350px; }
```

**Alternatives & tweaks**

* Use `display: inline-table;` instead of `width:500px` to **shrink‑wrap** to the track sum (\~500px) while still using fixed layout.
* Keep a global rule for resilience:

  ```css
  table.fixed th, table.fixed td { overflow-wrap: anywhere; }
  ```
* If you need **responsive** tracks, pair this with container queries or swap to percentage widths in `<col>`.

**Takeaway**

`table-layout: fixed` + `<colgroup>` is the **authoritative, predictable** way to size table columns. It locks in **150/350** tracks, improves performance, and avoids content-driven width drift. Just remember to handle unbreakable tokens and oversized media so cells don’t overflow.
