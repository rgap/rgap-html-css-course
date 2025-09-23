# Fixed Row Height — hard clip (inner wrapper, 2×2)

**What this demo is**

A 2×2 table that keeps real table cells, but **wraps each cell’s content inside an inner `<div>`**. That inner wrapper has a fixed height (40px) and `overflow: hidden`. This creates a **strict visual row height** while allowing text to wrap inside the wrapper.

**What you will see**

- Every row looks about **41px** tall (≈ 40px content + \~1px from collapsed borders).
- Long text **wraps** inside the inner `<div>`, but anything beyond 40px is **clipped** (no scrollbars, no ellipsis).
- Table semantics are preserved: columns align; `<colgroup>` works; borders collapse.

**Why it behaves like this**

- The `<th>/<td>` themselves don’t control overflow. Instead, the **inner wrapper** enforces the height and clipping.
- Because we keep `display: table-cell` on `<th>/<td>`, the browser maintains proper table layout.

**When to use this pattern**

- You need **strict, uniform row heights** but want to allow **multi-line wrapping up to a limit**.
- You want to **keep real table behavior** (alignment, intrinsic sizing) intact.

**Limitations**

- **Hidden content** beyond the fixed height: users may not realize text is clipped.
- **No multi‑line ellipsis**—extra lines are simply cut off.
- **Accessibility**: hidden text isn’t read by screen readers unless you add an accessible alternative (e.g., `aria-label`, `aria-describedby`, or a details view).
- **Copy/select**: selecting the cell won’t include clipped text.
- **Printing/export**: some print engines may ignore clipping; test if you need hard copies.

**Key CSS used**

```css
th,
td {
  border: 1px solid #444;
  padding: 0; /* move padding to inner div */
}

th > div,
td > div {
  height: 40px; /* strict content height */
  overflow: hidden; /* hard clip beyond 40px */
  white-space: normal; /* allow wrapping */
  padding: 0 8px; /* visual padding lives here */
  box-sizing: border-box;
}
```

**Takeaway**

Use an **inner wrapper** when you want **fixed-looking rows with wrapping** but don’t need multi-line ellipsis or in-cell scrolling.
