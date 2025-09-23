# Fixed Row Height — N‑line clamp via inner divs (preserve table semantics)

**What this demo is**

A 2×2 table that keeps real table cells, but places an **inner `<div>`** inside each cell. That inner wrapper:

- uses **multi‑line clamping** (`display: -webkit-box`, `-webkit-line-clamp: N`)
- has a computed height of **N × line-height**
- **hides** anything beyond those N lines

This preserves **true table layout** (column alignment, collapsed borders, `<colgroup>`) because clamping happens **inside** the cell, not on the `<th>/<td>` itself.

**What you will see**

- Rows look about **(N × line-height) + \~1px** tall (the extra \~1px comes from collapsed borders).
- Text can wrap **up to N lines**; after that it’s **clipped** (no scrollbars, no visible “…”, unless the platform renders one).
- You can change **N** and **line-height** per cell via small utility classes.

**Why it behaves like this**

- The wrapper’s height is fixed to `N × line-height` → the row can’t grow beyond that.
- `display: -webkit-box` + `-webkit-line-clamp` limits rendering to N lines.
- Because the `<th>/<td>` remain **table-cells**, table semantics are kept.

**When to use this pattern**

- You want **uniform row heights** while allowing **a few lines of text** (e.g., 2–3 lines) before clipping.
- You need to **preserve** real table behavior.

**Limitations**

- **Clamped text is hidden** (no built-in “show more”). Consider a tooltip or details view.
- **Browser support**: `-webkit-line-clamp` works best on WebKit/Blink engines. Other engines are improving but may differ; test across browsers.
- **No selectable overflow**: copying the cell won’t include hidden text.
- **Printing/export**: some engines ignore clamping; verify if you need hard copies.

**Key CSS used**

```css
:root {
  --lines: 2; /* default visible lines */
  --lh: 20px; /* default line-height */
}

th,
td {
  border: 1px solid #444;
  padding: 0; /* move padding to inner div */
  box-sizing: border-box;
}

/* The ONLY element that clamps is the inner wrapper */
.cellClamp {
  padding: 0 8px; /* visual padding */
  display: -webkit-box; /* required for -webkit-line-clamp */
  -webkit-box-orient: vertical;
  -webkit-line-clamp: var(--lines);
  overflow: hidden; /* hide beyond N lines */
  white-space: normal; /* allow wrapping */
  line-height: var(--lh);
  height: calc(var(--lines) * var(--lh)); /* fixed content height */
}

/* Utilities to tweak per cell */
.l-1 {
  --lines: 1;
}
.l-2 {
  --lines: 2;
}
.l-3 {
  --lines: 3;
}
.lh-16 {
  --lh: 16px;
}
.lh-18 {
  --lh: 18px;
}
.lh-20 {
  --lh: 20px;
}
.lh-24 {
  --lh: 24px;
}
```

**Takeaway**

Use **N‑line clamping** on an **inner wrapper** to keep tables aligned while letting content show **a controlled number of lines** before being clipped.
