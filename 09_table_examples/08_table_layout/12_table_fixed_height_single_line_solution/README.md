# Fixed Row Height — single-line solution (2×2)

**What this demo is**

A normal 2×2 table that keeps real table cells. Each cell shows **one line** only: we use `white-space: nowrap`, `overflow: hidden`, and `text-overflow: ellipsis`.

**What you will see**

- Rows look about **41px** tall (≈ 40px content + \~1px collapsed border).
- Long text is **truncated with …** instead of making the row taller.
- Columns align and borders collapse normally because cells remain table‑cells.

**Why it behaves like this**

- `height: 40px` targets the **content box** of the cell.
- `white-space: nowrap` keeps content on a single line; `overflow: hidden` stops it from spilling; `text-overflow: ellipsis` renders the “…”.
- With `border-collapse: collapse`, the visible row is the content height plus the shared border (\~+1px).

**When to use this pattern**

- You want a **clean, fixed-looking row** and it’s OK to show **only one line** per cell.
- You need to **preserve real table behavior** (column alignment, `<colgroup>`, etc.).

**Limitations**

- Only one visible line; extra text is hidden.
- No multi-line ellipsis. Some special content (emoji/replaced elements) can still nudge heights across browsers.

**Key CSS used**

```css
th,
td {
  border: 1px solid #444;
  padding: 0;
  height: 40px; /* content-box target */
  overflow: hidden; /* stop spill */
  white-space: nowrap; /* single line */
  text-overflow: ellipsis; /* show … */
}
```

**Takeaway**

This file is the **simplest practical fix** for tidy, uniform-looking rows: keep true table cells and use a **single-line ellipsis** to prevent growth.
