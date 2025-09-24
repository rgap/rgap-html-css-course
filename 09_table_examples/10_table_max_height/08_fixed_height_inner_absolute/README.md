# Fixed Row Height — inner absolute (same multi‑line span everywhere)

**What this demo is**

A table that keeps real table cells, but places a **single, shared pattern** inside every header and body cell: an **absolute‑positioned `<span>`** that fills the cell (`position: absolute; inset: 0`). The span uses `line-height: 20px` and `height: 40px` so exactly **two lines** can show; anything beyond is **hard‑clipped**.

**What you will see**

- Rows look about **41px** tall (≈ 40px content + \~1px collapsed border).
- Text **wraps up to two lines**, then is **cut off** (no multi‑line ellipsis, no scrollbars).
- The **same markup** (`<span>`) is used for **both** headers and body cells for consistency.

**Why it behaves like this**

- The `<th>/<td>` remain **table‑cells** (good: alignment, collapsed borders, `<colgroup>`).
- The **absolute span** fills the cell and controls the inner layout: fixed height + wrapping + clipping.
- `line-height × lines` sets exact content height; the row cannot grow.

**When to use this pattern**

- You want **uniform rows** and a **strict multi‑line cap** using a single, reusable element.
- You need to **preserve table semantics** while avoiding per‑cell class soup.

**Limitations**

- **Hidden overflow** (no multi‑line ellipsis). Consider tooltips or a details panel for full text.
- **Copy/select** won’t include clipped content.
- Font changes/zoom/i18n can change where wraps occur; test with your fonts.

**Key CSS used**

```css
th,
td {
  border: 1px solid #444;
  padding: 0;
  height: 40px; /* content-box height target */
  position: relative; /* positioning context for inner span */
}

th > span,
td > span {
  position: absolute;
  inset: 0; /* fill cell */
  padding: 4px 10px; /* inner padding */
  box-sizing: border-box;
  line-height: 20px; /* 2 × 20px = 40px */
  height: 40px; /* hard cap */
  white-space: normal; /* allow wrapping */
  overflow: hidden; /* hard clip */
}
```

**Takeaway**

Use an **absolute inner span** when you want a **uniform two‑line cap** across **all cells** without losing table layout.
