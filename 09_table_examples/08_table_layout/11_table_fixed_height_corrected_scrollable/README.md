# Fixed Row Height — Scrollable Cell Variant

This lesson demonstrates how to keep a table row visually fixed at ~41 px tall (40 px content box + collapsed border), while allowing cell content to scroll vertically if it exceeds the fixed height.

## What you'll learn

- Why a declared `height: 40px` on `<td>` shows up as ~41 px visible with collapsed borders.
- How to turn a table cell into a block (`display: block`) so overflow rules apply strictly.
- How to enable vertical scrolling inside a fixed-height table cell.
- Trade-offs between scrollable cells and normal table-cell alignment.

## Explanation

- **Height vs. visible size**

  - `td { height: 40px; }` defines the content box.
  - With `border-collapse: collapse` and 1 px borders, the visible row measures ~41 px.

- **Normal behavior**

  - A `<td>` will auto-grow to fit content. Long text causes rows to expand.

- **Scrollable cell approach**

  - Add `td.clip { display: block; }` so the cell behaves like a block box.
  - Combine with `overflow-y: auto;` → vertical scrollbar appears if content exceeds 40 px.
  - `overflow-x: hidden;` avoids a horizontal scrollbar when text wraps.
  - `-webkit-overflow-scrolling: touch;` enables smooth scroll on mobile.

- **Trade-offs**
  - The cell is no longer a true table-cell, which may break vertical alignment in multi-column layouts.
  - Works best for single-column demos, data tables with independent rows, or when clipping/scrolling is more important than strict table semantics.

## How to run

Open `index.html` in your browser. You’ll see three rows:

1. Short text — visible height **≈ 41 px** (40 px content + border).
2. Long text (normal cell) — row **expands beyond ≈ 41 px** because the table-cell auto-grows.
3. Long text with `td.clip` — the cell is a block box with fixed 40 px content height; a vertical scrollbar appears inside the row. The visible row stays **≈ 41 px**.

## Notes

- Table rows won’t shrink below content unless overflow is enforced.
- Use the scrollable-cell approach only when user interaction with long content is acceptable.
- For strict fixed heights across many columns, prefer inner wrappers instead of `display:block` on `<td>`.
- ±1 px differences are expected due to border collapse rounding and device-pixel ratios.
